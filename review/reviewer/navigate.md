# 代码审核的步骤



## 概要

Now that you know [what to look for](looking-for.md), what's the most efficient
way to manage a review that's spread across multiple files?
现在，你已经知道[在代码审核过程中要看些什么？](looking-for.md)，那么对于CL包含多个文件的CL，怎样做会让代码审核变得高效呢？

1.  Does the change make sense? Does it have a good
    [description](../developer/cl-descriptions.md)? 这个CL是否有意义？它是否包含好的[描述](../developer/cl-descriptions.md)？
2.  Look at the most important part of the change first. Is it well-designed
    overall先综观整个CL中最重要的部分。整体上，是否设计合理？
3.  Look at the rest of the CL in an appropriate sequence.以合适的顺序检查CL的其他部分。

## 第一步：全面了解CL {#step_one}

Look at the [CL description](../developer/cl-descriptions.md) and what the CL
does in general. Does this change even make sense? If this change shouldn't have
happened in the first place, please respond immediately with an explanation of
why the change should not be happening. When you reject a change like this, it's
also a good idea to suggest to the developer what they should have done instead.
阅读[CL 描述](../developer/cl-descriptions.md)，了解CL是实现的功能。判断这个修改是否有意义？如果答案是“否”，请立即回复，并解释为什么要取消这个修改。当拒绝的同时，你最好向开发者给出建议，这种情况应该怎么做。

For example, you might say "Looks like you put some good work into this, thanks!
However, we're actually going in the direction of removing the FooWidget system
that you're modifying here, and so we don't want to make any new modifications
to it right now. How about instead you refactor our new BarWidget class?"
例如，你可能会这么说，“这个CL的工作看起来挺不错的，谢谢你！不过，目前我们正在删除 FooWidget 系统，目前最好不要修改它，不过这个CL正在修改它。换种方式吧，你看重构一下 BarWdidget 的类，怎么样？”

Note that not only did the reviewer reject the current CL and provide an
alternative suggestion, but they did it *courteously*. This kind of courtesy is
important because we want to show that we respect each other as developers even
when we disagree.
从上面的例子来看，你拒绝了这个 CL ，并提供了一种可选方案。整个过程，你都*很有礼貌*。这种礼貌非常重要，这向大家展示了：尽管不同意你的观点，但我们彼此都很尊重。

If you get more than a few CLs that represent changes you don't want to make,
you should consider re-working your team's development process or the posted
process for external contributors so that there is more communication before CLs
are written. It's better to tell people "no" before they've done a ton of work
that now has to be thrown away or drastically re-written.
如果这种情况（开发者提交了你认为不应该这么做的 CL）经常出现，那么你应该考虑一下，是不是应该优化团队的开发流程或外部贡献者（针对某些与外部开发人员共同协作的场景）的发布流程，以便先与开发者进行充分的沟通，然后再开发 CL。最好在他开发一大堆工作之前就说“不”，以避免大量不必要的返工。

## 第二步：检查CL的主要部分 {#step_two}

Find the file or files that are the "main" part of this CL. Often, there is one
file that has the largest number of logical changes, and it's the major piece of
the CL. Look at these major parts first. This helps give context to all of the
smaller parts of the CL, and generally accelerates doing the code review. If the
CL is too large for you to figure out which parts are the major parts, ask the
developer what you should look at first, or ask them to
[split up the CL into multiple CLs](../developer/small-cls.md).

If you see some major design problems with this part of the CL, you should send
those comments immediately, even if you don't have time to review the rest of
the CL right now. In fact, reviewing the rest of the CL might be a waste of
time, because if the design problems are significant enough, a lot of the other
code under review is going to disappear and not matter anyway.

There are two major reasons it's so important to send these major design
comments out immediately:

-   Developers often mail a CL and then immediately start new work based on that
    CL while they wait for review. If there are major design problems in the CL
    you're reviewing, they're also going to have to re-work their later CL. You
    want to catch them before they've done too much extra work on top of the
    problematic design.
-   Major design changes take longer to do than small changes. Developers nearly
    all have deadlines; in order to make those deadlines and still have quality
    code in the codebase, the developer needs to start on any major re-work of
    the CL as soon as possible.

## Step Three: Look through the rest of the CL in an appropriate sequence {#step_three}

Once you've confirmed there are no major design problems with the CL as a whole,
try to figure out a logical sequence to look through the files while also making
sure you don't miss reviewing any file. Usually after you've looked through the
major files, it's simplest to just go through each file in the order that
the code review tool presents them to you. Sometimes it's also helpful to read the tests
first before you read the main code, because then you have an idea of what the
change is supposed to be doing.

Next: [Speed of Code Reviews](speed.md)
