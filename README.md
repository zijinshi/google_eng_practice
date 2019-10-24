# Google的工程实践文档

Google有很多优秀的工程实践，这些实践遍布公司内的所有项目，覆盖了几乎所有编程语言。 随着开发项目的增多，我们不断总结经验，把这些最佳实践以文档的形式整理出来。这份文档是我们集体经验的结晶。除了我们之外，相信其他公司、组织或开源项目也能从中受益，现在时机成熟了，我们决定将其公开发布。

这份工程实践文档包含如下内容：
*   [Google的代码审核指南 (Google's Code Review Guidelines)](review/index.md)，它包含两部分：
    *   [代码审核者指南 (The Code Reviewer's Guide)](review/reviewer/index.md)
    *   [代码提交者指南 (The Change Author's Guide)](review/developer/index.md)

## 术语

在文档中，我们用到了一些 Google 内部术语，为避免误解，我们稍作解释：

*   **CL**： 即“changelist”， 中文可以翻译成修改列表，它是提交到版本控制工具中的一次代码修改（即将审核的代码）。有的公司或组织称它为 “改变”(change)或“补丁”(patch)。
*   **LGTM**： “Looks Good to Me.” 的缩写，“看起来不错”。 当一个审核者这么说的时候，意味着他会批准这个CL。
*   **g3doc**： Google内部的工程文档平台。


## 版本
英文原文来自 [Google's Engineering Practices documentation](https://github.com/google/eng-practices)，中文版由 [ zijinshi ](https://github.com/zijinshi) 翻译整理。根据中文表达习惯，在原文基础上有少量删改。


| 版本 | 日期 | 说明 |
| :--- | :--- | :--- |
| 1.0 | 2019.10.07 | 初版完成 |
| 1.1 | 2019.10.18 | 修复某些翻译不准确的地方 |

中文版同时发布于网站：
*   [Google的工程实践文档(Github)](https://zijinshi.github.io/google_eng_practice/index)
*   [Google的工程实践文档(Gitbook)](https://zijinshi.gitbook.io/google)

PDF版本下载：
*   [Google的工程实践文档](https://github.com/zijinshi/google_eng_practice/raw/gitbook/Google%E7%9A%84%E5%B7%A5%E7%A8%8B%E5%AE%9E%E8%B7%B5%E6%96%87%E6%A1%A3.pdf)

[Google代码实践的一些感悟](preface.md)

## License
本文遵守 CC-By 3.0 License（[中文版](https://creativecommons.org/licenses/by/3.0/deed.zh)、[英文版](https://creativecommons.org/licenses/by/3.0/)）。

The documents in this project are licensed under the CC-By 3.0 License, which
encourages you to share these documents. See
https://creativecommons.org/licenses/by/3.0/ for more details.

<a rel="license" href="https://creativecommons.org/licenses/by/3.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/3.0/88x31.png" /></a>
