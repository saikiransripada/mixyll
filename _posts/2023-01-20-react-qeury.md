---
layout: post
title: React query 프로젝트 도입기
date: 2023-01-20 11:12:00
summary: React Query는 리액트에서 서버 상태를 가져오고 패칭, 캐싱하고, 동기화, 업데이트하는 것을 쉽게 해준다
categories:
---

# React Query

| 💡 React Query is often described as the missing data-fetching library for React, but in more technical terms, it makes **fetching, caching, synchronizing andupdating server state** in your React applications a breeze - [Overview](https://react-query.tanstack.com/overview) -

- React Query는 리액트에서 서버 상태를 가져오고 패칭, 캐싱하고, 동기화, 업데이트하는 것을 쉽게 해준다 - [공식문서](https://tanstack.com/query/latest/docs/react/overview?from=reactQueryV3&original=https%3A%2F%2Freact-query-v3.tanstack.com%2Foverview)

회사 프로젝트에서 진행했던 API 관련 코드 들은 Redux 와 Redux-saga, Context API를 사용하여 전역 상태에 client, server state의 모든 상태들을 관리 하고 있었다.

store라는 것은 내가 생각하기에 전역 상태가 저장되고 관리되는 공간인데, 상태 관리 보단 API 통신 코드들이 많아지는 이슈 아닌 이슈를 만들고 있었다. 만약 프로젝트가 커지고 팁원들과 협업을 계속해서 진행할 경우 코드가 더 비대해 질 수 있고, 나중에는 리펙토링을 진행하기에 코드를 만지기에도 거부감일 들 수가 있다.

리덕스를 사용하면서 API 요청에 관련한 상태를 관리 하려면

- 시작 Loading
- 성공 Success
- 실패 Fail

```ts
const patchChangePAssword = (payload) => ({
  type: PATCH_CHANGE_PASSWORD,
  payload,
});

const patchChangePasswordSuccess = (payload) => ({
  type: PATCH_CHANGE_PASSWORD_SUCCESS,
  payload,
});

const patchChangePasswordFail = (payload) => ({
  type: PATCH_CHANGE_PASSWORD_FAIL,
  payload,
});
```

```ts
const initialState: IAppointmentState = {
    isLoading: false,
    changePasswordSuccess: false,
    changePasswordFail: false,
    ...

```

에 대한 3가지 액션들을 만들고 해당 액션들을 처리하는 함수를 따로 만들어야 한다. 이부분은 개발자 입장에서 조금 번거럽고 효율적이지 않은 작업이라고 할 수 있다. 만약 큰 프로젝트를 한다면 많은 요청의 API들이 있을텐데 이런 부분에서 너무 많은 state들과 함수들이 늘어나게 되고
하나의 state로 관리할 수 도 있겠지만 많은 API들을 컨트롤 하기에는 조금 벅찬 경우가 있다.

기존 데이터 패칭에는 로딩 상태 관리, 패칭한 데이터 들을 위해 여러 훅을 사용해야 했으나,
**리액트 쿼리**를 사용하게 된다면 훨씬 간결하고 관리하기 쉽도록 패칭 로직을 작성할 수 있고, 서버의 상태를 다른 곳에 저장하여 관리할 필요가 없다.

이렇게 된다면 위에서 쓴 이슈에서 전역 상태 관리 store에서 **_client state_** 와 **_server state_**를 나눌수 있는 굉장한 이 점이 있다.

간단한 React Query 예제를 살펴보면서 많이 쓰이는 3가지만 정리해보자

```ts
import {
   useQuery,
   useMutation,
   useQueryClient,
   QueryClient,
   QueryClientProvider,
 } from 'react-query'
 import { getTodos, postTodo } from '../my-api'

 // Create a client
 const queryClient = new QueryClient()

 function App() {
   return (
     // Provide the client to your App
		// queryClient 는 Context 기반으로 Provider가 사용된다
     <QueryClientProvider client={queryClient}>
       <Todos />
     </QueryClientProvider>
   )
 }

 function Todos() {
   // Access the client
   const queryClient = useQueryClient()

   // Queries
   const { data: todos, isLoading, isError } = useQuery('todos', getTodos);

	 if(isLoading) return <div> 로딩중... </div>

	 if(isError) return < <div> Error </div>

   // Mutations
   const { mutate } = useMutation(postTodo, {
     onSuccess: () => {
       queryClient.invalidateQueries('todos')
     },
   })

   return (
     <div>
       <ul>
         {todos.map(todo => (
           <li key={todo.id}>{todo.title}</li>
         ))}
       </ul>

       <button
         onClick={() => {
           mutate({
             id: Date.now(),
             title: 'Do Laundry',
           })
         }}
       >
         Add Todo
       </button>
     </div>
   )
 }



```

<br/>
<br/>
<br/>

---

<br/>
<br/>

## 1. **_Queries_**

- CRUD중 Reading을 사용할때 사용하게 된다. 자동으로 실행된다 / Get
- useQuery 의 파라미터는 3개의 인자가 들어가는데
  - 첫번째 인자: QueryKey (key 에 따라 caching을 관리)
    - Unique 하여 보통 관리할때 도메인 끼리 묶어서 관리를 한다. 키가 겹치지 않도록
    - String, Array, Object를 넣을 수 있는데 보통 Array를 많이 사용한다.
  - 두번째 인자: Query Function ( Promise를 반환하는 함수 ) / fetch, axios
  - 세번째 인자 : Config ( Option etc. )

```ts
const { data, isLoading, isSuccess, isError, refetch , ... } = useQuery([qeuryKey] , qeuryFn? , {...option});
```

useQuery의 return 값에서 자주 사용하는 부분만 정리한다면

- **data** : 마지막으로 성공한 resoleved 된 데이터 ( Response )
- **isLoading**, **isSuccess**, **isError** 등 : 모두 현재 query의 상태
- **refetch**: 해당 query refetch하는 함수 제공

많은 return 값들이 있지만, 공식문서를 참고하면 더많은 정보들을 알 수 있다.

세번째 인자로 들어가는 config (option) 값에서 커스텀을 진행 할수도 있다.

```ts
 = useQuery([qeuryKey] , qeuryFn? , {
    onSuccess, onError, retry, enabled, select, keepPreviousData ...
 });
```

- **onSuccess**, **onError**, **onSettled**: query fetching 성공/실패/완료 시 실행할 Side Effect를 정의 할 수 있다.
- **enabled**: 자동으로 query를 실행시킬지 말지 여부
- **retry**: query 동작 실패 시 , 자동으로 retry를 할지 말지 여부
- **select**: 성공 시 가져온 data를 가공해서 전달
- **keepPreviousData**: 새롭게 fetching 시 이전 데이터 유지여뷰 / pagination 유용
- **refetchInterval**: 주기적으로 refetch 할지 결정하는 옵션

### **실제 프로젝트에서 적용 예시**

```ts
const getWatingList = async (doctor: number, cyrrentPage: number, today: string) => {
  const { data } = await axiosClient.get(
    `appointment/list/?doctor=${doctor}&status=1&offset=${currentPage - 1}0&startDate=${today}`,
  );
};

const { data } = useQuery(
  ['WaitingList', doctor, currentPage, today],
  () => getWatingList(doctor, currentPage, today),
  { enabled: !doctor },
);
```

<br/>
<br/>
<br/>

---

<br/>
<br/>

Query(리스트?를)가 여러 개일 땐 어떻게 해야하나 / [공식문서](https://tanstack.com/query/latest/docs/react/guides/parallel-queries?from=reactQueryV3&original=https%3A%2F%2Freact-query-v3.tanstack.com%2Fguides%2Fparallel-queries)

```ts
function App () {
    // The following queries will execute in parallel
    // 알아서 parallel(병렬적) 하게 동작한다.
    const waitingList = useQuery('waitingList', fetchWaitingList)
    const completeList = useQuery('completeList', fetchCompleteList)
    const pendingList = useQuery('pendingList', fetchPendingList)
    ...
}

```

<br/>
<br/>
<br/>

---

<br/>
<br/>

## 2. **_Mutation_**

- CRUD 중 Create/Update/Delete 을 사용할때 쓰인다. / POST , DELETE , PATCH ,PUT
  - 데이터 생성, 수정 , 삭제 용 / 자동으로 실행 되지 않는다.
- useQuery 보다 심플하게 Promise 반환 함수만 있어도 된다.
  - 단, Query Key 를 넣어주면 Devtools에서 디버깅이 용이하다

```ts
const { mutate, mutateAsync , reset ,  ... } = useMutation( mutationFn , {...option});
```

- **mutate**: mutation 을 실행하는 함수
- **moutateAsync**: `mutate` 와 비슷 하지만 Promise를 반환
- **reset**: mutation 의 내부 상태를 clean

useQeury와 마찬가기로 config (option) 에서 커스텀을 진행할수 있다.

```ts
 = useMutation( mutationFn , {onMutate , onError, onSuccess, retry , ...});
```

- **onMutate**: 본격적인 Mutation 동작 전에 먼저 동작 하는 함수, Optimistic Update 적용할때 유용
- 나머진 useQuery랑 비슷하다.

### **실제 프로젝트에서 적용 예시**

```ts
const patchChangePassword = async ({ password, changePassword }: IUserInfo) => {
  const { data } = await axiosClient.put('user/change_password', {
    password,
    changePassword,
  });
};

const {
  mutate: changePassword,
  isSuccess,
  isError,
} = useMutation((userInfo) => patchChangePassword(userInfo), {
  onSuccess: (data) => {
    localStorage.setItem('token', data.token);
  },
  onSettled: () => {
    setShowConfirmModal();
  },
});
```

<br/>
<br/>
<br/>

---

<br/>
<br/>

## 3. **_Query Invalidation_**

- 간단하게 queryClient를 통해 `invalidate` 메소드를 호출 하면 끝이다.

```ts
// Invalidate every qeury in the cache
queryClient.invalidateQueries();
// Invalidate every query wuth a ket thay starts with "todos"
queryClient.invalidateQueries('todos');
```

- 해당 key를 가진 query는 stale (신선하지 않은) 취급되고,현재 rendering 되고 있는 query들은 백그라운드에서 refetch 가 이루어진다.

<br/>
<br/>
<br/>

---

<br/>
<br/>

## 4. **_장점 & 고려해야할점_**

<br/>
장점

- 서버상태 관리하기 용이 하다 (Redux, MobX 사용할때보다) 직관적인 API 호출 코드
- 데이터 페칭 시 로딩, 에러 처리를 한곳에서 처리 가능
- API 처리에 관한 각종 인터페이스 및 옵션 제공 ([useInfiniteQuery](https://react-query.tanstack.com/guides/infinite-queries), [pagination](https://react-query.tanstack.com/guides/paginated-queries), refetch ,prefetching, retry,등등)
- Client store 가 정말로 필요한 전역상태만 남아 store 답게 사용할 수 있다
- Devtool 제공으로 원활한 디버깅 - [공식문서](https://react-query.tanstack.com/devtools)
- Cache 전략 필요할때 아주 좋음 ( 현재 프로덕트에 적합한지는 ? / 예약 승인 , 취소, 대기 등 최신화가 우선 )
- [Npm Download Trend](https://www.npmtrends.com/react-query-vs-swr-vs-redux-saga) / 트렌드의 기술을 적용해보는 장점

<br/>

고려해야할점

- Componenet가 상대적으로 비대해지는 문제
- Hooks를 기반으로 사용하는지라 Component 설계 / 분리에 대한 고민이 필요하다
- 좀 더 난이도가 높아지는 프로젝트 설계 ( Component 최소화 및 파악)
- 기존 Rudex , MobX 와 비교하여 커뮤니티 규모가 그리 크지않아 queryKey에 대한 Best Practice 가 정립 되어있지않음.
- React query 의 장점을 더 잘 활용할 방법
- 리덕스 및 사가를 한번에 바꾸는 부담이 있다. 순차적으로 적용
- 트렌드를 따라가기보단 프로덕트에 맞는지 생각해보고 적용
- 프로젝트 규모가 작은 경우 라이브러리에서 제공하는 컨텍스트를 유지하는 효용보다 더 커질수 있다.
