# 代码审核开发者指南

## 目录
*   [介绍](#intro)
*   [代码审核者应该看什么?](#look_for)
    *   [挑选最好的代码审核者](#best_reviewers)
    *   [面对面审核](#in_person)
*   [参考](#seealso)


## 介绍 {#intro}

A code review is a process where someone other than the author(s) of a piece of
code examines that code.代码作者写完了一段代码，让其他人来检查这些代码，这个过程称为代码审核。

At Google we use code review to maintain the quality of our code and products.
在Google，我们通过代码审核来保证代码的质量，进而保证产品的质量。

This documentation is the canonical description of Google's code review
processes and policies.此文档是Google代码审核的规范说明流程和政策。



This page is an overview of our code review process. There are two other large
documents that are a part of this guide:当前页面是对我们的代码审核过程作简要介绍，更多详情可阅读如下两篇文档：

-   **[怎样进行代码审核](reviewer/)** ：针对代码审核者的指南。
-   **[作者指南](developer/)** ：针对CL提交者的指南。

## 代码审核者应该看什么？ {#look_for}

代码审核者应该关注以下几项：

-   **Design**: Is the code well-designed and appropriate for your system?**设计**：代码是否设计良好？设计是否适合当前系统？
-   **Functionality**: Does the code behave as the author likely intended? Is
    the way the code behaves good for its users?**功能**：代码实现的行为是否与作者的期望相符？代码实现的行为是否对用户友好。
-   **Complexity**: Could the code be made simpler? Would another developer be
    able to easily understand and use this code when they come across it in the
    future?**复杂性**：代码可以更简单吗？如果将来有其他开发者使用这段代码，他能很快读懂吗？
-   **Tests**: Does the code have correct and well-designed automated tests?**测试**：这段代码是否有正确的、设计良好的自动化测试？
-   **Naming**: Did the developer choose clear names for variables, classes,
    methods, etc.?**Naming**：在为变量、类名、方法等命名时，开发者应该选择清晰的名称。
-   **Comments**: Are the comments clear and useful? **注释**：是否所有的注释都清晰、有用。
-   **Style**: Does the code follow our
    [style guides](http://google.github.io/styleguide/)? 是否所有的代码都遵循代码[样式指南](http://google.github.io/styleguide/)？
-   **Documentation**: Did the developer also update relevant documentation?**文档**：开发者是否更新了相关文档？

See **[How To Do A Code Review](reviewer/)** for more information.详情请参见文档：[怎样进行代码审核](reviewer/)。

### 挑选最好的代码审核者 {#best_reviewers}

In general, you want to find the *best* reviewers you can who are capable of
responding to your review within a reasonable period of time.一般来讲，你一定会找*最好*的代码审核者来帮你审核代码，这个人应该在你期望的时间内有能力对审核负责。

The best reviewer is the person who will be able to give you the most thorough
and correct review for the piece of code you are writing. This usually means the
owner(s) of the code, who may or may not be the people in the OWNERS file.
Sometimes this means asking different people to review different parts of the
CL.
最好的审核者是对你的代码能给出最彻底、最正确的反馈的人。这通常意味着，代码的责任人既可能在OWNES文件中，也可能不在。有时候，你不得不让不同的人来审核代码的不同部分。

If you find an ideal reviewer but they are not available, you should at least CC
them on your change.
如果你发现最理想的代码审核人无法帮你审核，至少应该抄送给他（或者把他加到可选的审核者里去）。

### 面对面审核 {#in_person}

If you pair-programmed a piece of code with somebody who was qualified to do a
good code review on it, then that code is considered reviewed.
如果你正在与一个人结对编程，他已经对你的代码做过细致地审核，那么这段代码可以认为是审核过的。

You can also do in-person code reviews where the reviewer asks questions and the
developer of the change speaks only when spoken to.
你还可以与代码审核者进行面对面的审核。当审核者对代码有疑问时，向你提出问题，你进行回答。

## See Also {#seealso}

-   [怎样进行代码审核](reviewer/)：针对代码审核者的指南。
-   [作者指南](developer/)：针对CL提交者的指南。
