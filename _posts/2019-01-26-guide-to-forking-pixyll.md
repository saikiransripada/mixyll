---
layout: post
title: Guide to Forking Mixyll
date: 2019-01-26 19:22
summary: Mixyll is available to you under the MIT license.
categories: jekyll mixyll
---

The following is an overview to copying and sharing Mixyll.[^1]

Most people have an understanding of what the copyright and licensing obligations are for source code, but not everyone has practical experience.  There is a lot of information about how to use free and open source source code generally, but not necessarily how it works specifically.

## Basics

Mixyll is free and open source software under the MIT license, a _permissive license_.  You can use Mixyll without charge and it is provided to you, "as is", without warranty of any kind.

These are some of the rights for Mixyll since it is under the MIT license:[^2]

1. You can **copy** Mixyll by forking it on GitHub or by any other means of copying.
2. You can **use** Mixyll to publish your site without restriction or limitation.
3. You can **change** Mixyll as you wish, and you can publish your site with a modified version of Mixyll.
4. You can also **distribute** copies of Mixyll to other people.
5. You can also **distribute modified** copies of Mixyll.

Other rights you have of Mixyll under the MIT license:

- You can **sell** copies of Mixyll, including copies you have modified.
- You can **combine** Mixyll with other works that are under the MIT license, or other permissive licenses, a copyleft license or a proprietary license.  Mixyll already does this itself by using Jekyll, Ruby and other dependencies.
- You can distribute copies of Mixyll to others under either the MIT license or you can **relicense** Mixyll under another license.  This includes a different permissive license, a copyleft license or a proprietary license.

Your only responsibility is to preserve both the copyright notices of Mixyll and the MIT license in your copy or modified work.

## How to

If you've modified Mixyll significantly and want to share your version, especially public copies of the code, then there are a few items you should do.

1. You should probably **rename** your fork of Mixyll with a different name.
2. A new name isn't required by the MIT license, but it is good etiquette.[^3]
3. You should add your name to the **copyright** of your version, and you should preserve the existing copyrights of Mixyll.
4. Maintaining the copyright notices isn't required of the MIT license, but it is suggested by the license and is a good practice for documenting the copyrights of your derived work.

The items above do not apply when you just copied and modified Mixyll in small ways to just publish your site and you have no plans to fork Mixyll under a different name.

If you want to publish a fork of Mixyll under a different name but keeping it under the MIT license, then you should add your name to the copyright notices:

    Copyright (c) 2019 Your Name
    Copyright (c) 2014-2019 John Otander for Mixyll

However, if you want to publish a fork of Mixyll under a different name *and* a different license, then you should should still add your name to the copyright notices but have a section titled "Mixyll" at the bottom of your LICENSE file that preserves the copyright and license notices for Mixyll:

    Mixyll
    
    Copyright (c) 2014-2019 John Otander
    
    MIT License
    
    Permission is hereby granted, [...]

If you are just modifying Mixyll in small ways to customize your site, you are not obligated to maintain the copyright notices of Mixyll on your site.  However, if you want to credit the Mixyll theme that would be appreciated, see section on "Mixyll Plug" in the README file that came with Mixyll.

Thanks for using Mixyll, and happy hacking!

---
[^1]: **Disclaimer**: This material is for informational purposes only, and should not be construed as legal advice or opinion.  For actual legal advice, you should consult with professional legal services.
[^2]: This list of privileges are derived from the four freedoms of "The Free Software Definition" published by the GNU project <https://www.gnu.org/philosophy/free-sw.en.html>.
[^3]: Using a different name from "Mixyll" for your derivate work helps avoid misdirected questions from people who are using your version.  It's similar to using version numbers to discrimate the revisions of software when troubleshooting issues.
