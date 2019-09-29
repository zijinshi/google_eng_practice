# 编写良好的 CL 描述


A CL description is a public record of **what** change is being made and **why**
it was made. It will become a permanent part of our version control history, and
will possibly be read by hundreds of people other than your reviewers over the
years.
CL 描述是一项公开的记录，记录内容包含修改了 **什么** 与 **为什么** 这么修改。 虽然你的 CL 只是在你与审核者之间发生，但它是版本控制历史的一部分，若干年之后，很有可能会有成百上千的人阅读。

Future developers will search for your CL based on its description. Someone in
the future might be looking for your change because of a faint memory of its
relevance but without the specifics handy. If all the important information is
in the code and not the description, it's going to be a lot harder for them to
locate your CL.
以后得开发者可能需要根据描述搜到你以前写的 CL 。他们可能在没有精确数据的情况下，根据自己的模糊记忆搜索CL。如果所有的信息都只包含在代码里面，描述中几乎没有相关内容，那么定位到你的 CL 将会花费太多的时间。

## 第一行 {#firstline}

*   Short summary of what is being done. 简短描述做了什么。
*   Complete sentence, written as though it was an order. 完整的句子，祈使句。
*   Follow by empty line. 后面空一行。

The **first line** of a CL description should be a short summary of
*specifically* **what** *is being done by the CL*, followed by a blank line.
This is what most future code searchers will see when they are browsing the
version control history of a piece of code, so this first line should be
informative enough that they don't have to read your CL or its whole description
just to get a general idea of what your CL actually *did*.
CL 描述的 **第一行** 应该是一句简短的描述，用以说明 *CL做了* **什么** 。在第一行后面再空一行。以后有开发者搜索版本控制历史的代码时，这是他们看到的第一行，所以第一行应该提供足够的信息，他们不必阅读代码，也不必阅读整个描述，只需扫一眼便知道 CL 做什么，为他们节省时间。

By tradition, the first line of a CL description is a complete sentence, written
as though it were an order (an imperative sentence). For example, say
\"**Delete** the FizzBuzz RPC and **replace** it with the new system." instead
of \"**Deleting** the FizzBuzz RPC and **replacing** it with the new system."
You don't have to write the rest of the description as an imperative sentence,
though.
一般而言，CL 描述的第一行是一句以命令口吻（祈使句）写的一句话。举例说明，我们应该写“ **删除** FizzBuzz RPC，并用写的系统 **替换** 它。”，而不是写成 “ **删除了** FizzBuzz RPC，并 **已经** 用写的系统 **替换** 它。”  当然，第一行写成祈使句就可以了，其他内容不必如此。
(译者注：原文中的反面例子是现在进行时。但在中文中现在进行时与祈使句基本一致，不好翻译。此处改成了现在完成时。)

## 描述内容要提供充分的信息 {#informative}

The rest of the description should be informative. It might include a brief
description of the problem that's being solved, and why this is the best
approach. If there are any shortcomings to the approach, they should be
mentioned. If relevant, include background information such as bug numbers,
benchmark results, and links to design documents.
描述内容应该提供足够的信息。它可能包含一段关于问题的简短描述，为什么这是最好的解决方案。如果有更好的解决方案，也应该提及。如果有的话，相关的背景信息，如 bug 编号、基准结果和相关的设计文档也应包含在内。

Even small CLs deserve a little attention to detail. Put the CL in context.
即使是小的 CL，也应该包含这些信息。

## 糟糕的 CL 描述 {#bad}

"Fix bug" is an inadequate CL description. What bug? What did you do to fix it?
Other similarly bad descriptions include:
“修复 bug”是一个很不恰当的描述。哪个 bug ？你做了哪些事情来修复它？通通都没有。类似糟糕的描述还包括：

-   "Fix build." “修复编译。”
-   "Add patch." “增加补丁。”
-   "Moving code from A to B." “把代码从 A 移到 B。”
-   "Phase 1." “第一阶段。”
-   "Add convenience functions."  “增加方便的功能。”
-   "kill weird URLs." “清除死链。”

Some of those are real CL descriptions. Their authors may believe they are
providing useful information, but they are not serving the purpose of a CL
description.
以上这些都是我们见过的 CL 描述。作者可能认为他们提供了足够的信息，实际上它们不符合CL的目的描述。

## 良好的 CL 描述 {#good}

Here are some examples of good descriptions.这是几个良好描述的样例。

### Functionality change 功能修改

> rpc: remove size limit on RPC server message freelist.
>
> Servers like FizzBuzz have very large messages and would benefit from reuse.
> Make the freelist larger, and add a goroutine that frees the freelist entries
> slowly over time, so that idle servers eventually release all freelist
> entries.

> RPC：移除 RPC 服务器的消息空闲列表的大小限制。
> 
> 服务器（如 FizzBuzz）有大量的消息，可以从重用中受益。使空闲列表更大，并添加一个goroutine，以便随着时间的推移缓慢释放空闲列表，以便空闲
> 服务器最终释放所有空闲列表。

The first few words describe what the CL actually does. The rest of the
description talks about the problem being solved, why this is a good solution,
and a bit more information about the specific implementation.
前面几句话描述了 CL 做什么的，接下来描述解决了什么问题，为什么这是一个好的解决方案，最后涉及到了一些实现细节。

### Refactoring 重构

> Construct a Task with a TimeKeeper to use its TimeStr and Now methods.
> 构建一个带 TimeKeeper 的 Task，以便使用它的 TimeStr 和 Now 方法。
>
> Add a Now method to Task, so the borglet() getter method can be removed (which
> was only used by OOMCandidate to call borglet's Now method). This replaces the
> methods on Borglet that delegate to a TimeKeeper.
>
> Allowing Tasks to supply Now is a step toward eliminating the dependency on
> Borglet. Eventually, collaborators that depend on getting Now from the Task
> should be changed to use a TimeKeeper directly, but this has been an
> accommodation to refactoring in small steps.
>
> Continuing the long-range goal of refactoring the Borglet Hierarchy.

The first line describes what the CL does and how this is a change from the
past. The rest of the description talks about the specific implementation, the
context of the CL, that the solution isn't ideal, and possible future direction.
It also explains *why* this change is being made.

### Small CL that needs some context

> Create a Python3 build rule for status.py.
>
> This allows consumers who are already using this as in Python3 to depend on a
> rule that is next to the original status build rule instead of somewhere in
> their own tree. It encourages new consumers to use Python3 if they can,
> instead of Python2, and significantly simplifies some automated build file
> refactoring tools being worked on currently.

The first sentence describes what's actually being done. The rest of the
description explains *why* the change is being made and gives the reviewer a lot
of context.

## Review the description before submitting the CL

CLs can undergo significant change during review. It can be worthwhile to review
a CL description before submitting the CL, to ensure that the description still
reflects what the CL does.

Next: [Small CLs](small-cls.md)
