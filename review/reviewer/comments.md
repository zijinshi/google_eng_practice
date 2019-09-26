# 怎样写代码审核的评论？



## 概述

-   保持友善。
-   Explain your reasoning.解释你的原因。
-   Balance giving explicit directions with just pointing out problems and
    letting the developer decide. 给出明确的信息，指出问题所在，让开发者最后做决定。
-   Encourage developers to simplify code or add code comments instead of just
    explaining the complexity to you.鼓励开发者简化代码，给代码添加注释，而不是向你解释为什么这么复杂。

## 礼貌

In general, it is important to be
courteous and respectful while also being
very clear and helpful to the developer whose code you are reviewing. One way to
do this is to be sure that you are always making comments about the *code* and
never making comments about the *developer*. You don't always have to follow
this practice, but you should definitely use it when saying something that might
otherwise be upsetting or contentious. For example:
一般而言，在审核代码时，礼貌和尊重都很重要，与此同时，评论应该描述清晰，有利于开发者改进代码。确保你对代码的评论应该是针对“代码”，而不是针对“开发者”本人。当然，不必总是遵循这个实践，但是当你要说某些可能让人沮丧或引起争议的话时，一定要对事不对人。例如：

Bad: "Why did **you** use threads here when there's obviously no benefit to be
gained from concurrency?"
不好的说法：“为什么**你**在这儿使用线程？明显这儿使用并发没有任何好处。”

Good: "The concurrency model here is adding complexity to the system without any
actual performance benefit that I can see. Because there's no performance
benefit, it's best for this code to be single-threaded instead of using multiple
threads."
好的说法：“这儿的并发模型增加了系统的复杂度，我没有在性能上看到好处。因为没有性能提升，这段代码最好还是由多线程改成单线程。”

## 解释为什么 {#why}

One thing you'll notice about the "good" example from above is that it helps the
developer understand *why* you are making your comment. You don't always need to
include this information in your review comments, but sometimes it's appropriate
to give a bit more explanation around your intent, the best practice you're
following, or how your suggestion improves code health.
从上面“好的说法”中，我们看到，它有助于开发者理解 *为什么* 你要写这条评论。当然，不必每次都解释为什么，但有时很有必要在阐明你的意图、你正在遵循的最佳实践、你在提升代码健康程度的时候，解释原因是有必要的。

## 提供指导 {#guidance}

**In general it is the developer's responsibility to fix a CL, not the
reviewer's.** You are not required to do detailed design of a solution or write
code for the developer.
**一般而言，修复 CL 的责任人是开发者，而不是审核者。** 你不必为开发者写出详细的设计方案，也不必为他写代码。

This doesn't mean the reviewer should be unhelpful, though. In general you
should strike an appropriate balance between pointing out problems and providing
direct guidance. Pointing out problems and letting the developer make a decision
often helps the developer learn, and makes it easier to do code reviews. It also
can result in a better solution, because the developer is closer to the code
than the reviewer is.
但这不代表审核者可以不提供任何帮助。作为审核者，你应该在指出问题所在与提供直接指导之间做好平衡。指出问题，并让开发者自己做决定，这样有助于开发者自我学习，审核者自己也很省时间。这种方式，开发者也更容易找出更好的解决方案，因为相对审核者，开发者对自己的代码更熟悉。

However, sometimes direct instructions, suggestions, or even code are more
helpful. The primary goal of code review is to get the best CL possible. A
secondary goal is improving the skills of developers so that they require less
and less review over time.
当然，有些时候也可以给出直接的指示、建议或代码。毕竟，代码审核的首要目标是尽可能让 CL 变得更好；次要目标才是提升开发者的技能，以便缩短审核时间。


## 接受解释 {#explanations}

If you ask a developer to explain a piece of code that you don't understand,
that should usually result in them **rewriting the code more clearly**.
Occasionally, adding a comment in the code is also an appropriate response, as
long as it's not just explaining overly complex code.
如果某段代码你看不懂，让开发者解释，通常结果是他们会**重写代码让它更清晰**。有时候，添加注释也可以，只要它不是用来解释一段过于复杂的代码。

**Explanations written only in the code review tool are not helpful to future
code readers.** They are acceptable only in a few circumstances, such as when
you are reviewing an area you are not very familiar with and the developer
explains something that normal readers of the code would have already known.
**仅仅把解释卸载代码审核工具里不利于以后得代码阅读者。** 只有几种情况可以这样，如当你正在审核一段你并不是很熟悉的代码时，开发者向你解释的文字，其他开发者都知道，那这种解释就不必写到代码里。

Next: [Handling Pushback in Code Reviews](pushback.md)
下一章：[如何应对被拒绝的代码评论？](pushback.md)
