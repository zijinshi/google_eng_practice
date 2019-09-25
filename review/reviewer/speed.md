# 审核的速度

## 为什么应该尽快审核代码 {#why}

**At Google, we optimize for the speed at which a team of developers can produce
a product together**, as opposed to optimizing for the speed at which an
individual developer can write code. The speed of individual development is
important, it's just not _as_ important as the velocity of the entire team.
**在Google，我们优化了开发团队开发产品的的速度**，而不是优化单个开发人员写代码的速度。单个开发人员的开发速度固然重要，但远没有整个团队的开发速度 _重要_ 。

When code reviews are slow, several things happen:
当代码审核者很慢的时候，以下几件事情发生：

*   **The velocity of the team as a whole is decreased.** Yes, the individual,
    who doesn't respond quickly to the review, gets other work done. However,
    new features and bug fixes for the rest of the team are delayed by days,
    weeks, or months as each CL waits for review and re-review. **作为一个整体，团队的进度降低了。** 是的，单个人没有对代码审核及时响应，而是在完成其他的工作。如果每个人都这样的话，团队的新功能或缺陷修复就会延期，累积下来，可能会是几天、几周，甚至几个月，团队每个人都在等待别人审核或再次审核自己的代码。
    
*   **Developers start to protest the code review process.** If a reviewer only
    responds every few days, but requests major changes to the CL each time,
    that can be frustrating and difficult for developers. Often, this is
    expressed as complaints about how "strict" the reviewer is being. If the
    reviewer requests the _same_ substantial changes (changes which really do
    improve code health) but responds _quickly_ every time the developer makes
    an update, the complaints tend to disappear. **Most complaints about the
    code review process are actually resolved by making the process faster.**
    **开发者开始抗议代码审核流程。** 如果审核者几天反馈一次，但是每次都要求 CL 重大改变，这样开发者就会变得很沮丧，很困难。经常，这会编程对审核者太过“严格”的抱怨。如果审核者 _同样_ 要求大量的改变（的确有利于改善代码质量的改变），并且每当开发者更新后，审核者响应 _迅速_ ，抱怨就会消失。 **大多数关于代码审核流程的抱怨实际上可以通过让流程变得更快来解决。**
    
*   **Code health can be impacted.** When reviews are slow, there is increased
    pressure to allow developers to submit CLs that are not as good as they
    could be. Slow reviews also discourage code cleanups, refactorings, and
    further improvements to existing CLs. **影响代码质量。** 当审核很慢时，会增加开发者的压力，他会感觉自己的代码不尽人意。迟缓的审核也会阻碍代码清理、重构，和对已有 CL 的进一步改善。

## 代码审核应该多迅速？ {#fast}

If you are not in the middle of a focused task, **you should do a code review
shortly after it comes in.**
如果你现在没有进行一项需要集中精力的任务，**你应该在收到审核邀请时，短时间内就开始代码审核。** 

**One business day is the maximum time it should take to respond** to a code
review request (i.e. first thing the next morning).
在收到审核请求时，**一个工作日是审核响应的最长时间允许** ，即第二天早上低的第一件事情。 

Following these guidelines means that a typical CL should get multiple rounds of
review (if needed) within a single day. 遵循这些规则意味着一个典型的 CL 的几轮（如果有必要的话）审核会在一天内完成。

## 速度 vs. 中断 {#interruption}

There is one time where the consideration of personal velocity trumps team
velocity. **If you are in the middle of a focused task, such as writing code,
don't interrupt yourself to do a code review.** Research has shown that it can
take a long time for a developer to get back into a smooth flow of development
after being interrupted. So interrupting yourself while coding is actually
_more_ expensive to the team than making another developer wait a bit for a code
review.
当然，有一个列外。**如果你正在做一项需要集中精力的任务时，例如写代码，不要打断自己。** 研究显示，在被打断之后，开发者需要耗费很长的时间才能进入打断前的状态。所以，相比让另外一位开发者稍微，在写代码的时候打断自己，实际上 _成本更高_ 。

Instead, wait for a break point in your work before you respond to a request for
review. This could be when your current coding task is completed, after lunch,
returning from a meeting, coming back from the microkitchen, etc.
相反，在下一个工作断点之后，可以再对这个审核进行相应。这个断点可能是你当前的代码已经完成的时候、午饭后、某个会议结束、从公司的餐厅回来，等等。


## 快速响应 {#responses}

When we talk about the speed of code reviews, it is the _response_ time that we
are concerned with, as opposed to how long it takes a CL to get through the
whole review and be submitted. The whole process should also be fast, ideally,
but **it's even more important for the _individual responses_ to come quickly
than it is for the whole process to happen rapidly.**
当我们谈及代码审核的速度时，我们指的是 _响应时间_ ，而不是审核 CL 整个流程走下来直到提交代码所花费的时间。整个流程也应该快，但 **更重要的是 _个人的快速响应_ ，而不是整个流程快点完成。**

Even if it sometimes takes a long time to get through the entire review
_process_, having quick responses from the reviewer throughout the process
significantly eases the frustration developers can feel with "slow" code
reviews.
即使有时候，整个 _审核_ 流程走下来会花费很多时间，但在整个过程中，审核者都在快速响应，这也会很大程度减轻开发者对 “慢” 代码审核的挫败感。

If you are too busy to do a full review on a CL when it comes in, you can still
send a quick response that lets the developer know when you will get to it,
suggest other reviewers who might be able to respond more quickly, or
[provide some initial broad comments](navigate.md). (Note: none of this means
you should interrupt coding even to send a response like this&mdash;send the
response at a reasonable break point in your work.)
当收到一个 CL 的审核的时候，如果你当时太忙没有时间做完整的审核，你仍然可以快速响应，告诉开发者你会做审核（但是当时没时间），建议他先让他其他能快速响应的开发者先审核，或者先[提供一些初步的反馈](navigate.md)。（注意：者并不意味着你可以打断当前的编码工作，还是应该在工作的断点对审核进行响应。）

**It is important that reviewers spend enough time on review that they are
certain their "LGTM" means "this code meets [our standards](standard.md)."**
However, individual responses should still ideally be [fast](#fast).
**有一点很重要，当审核者反馈“LGTM”时，意味着他花了足够的时间审核代码，并且认为代码满足[代码标准](standard.md)。** 然而，每个人还是应该[迅速](#fast)响应

## 跨时区的审核 {#tz}

When dealing with time zone differences, try to get back to the author when they
are still in the office. If they have already gone home, then try to make sure
your review is done before they get back to the office the next day.
当有时差时，尽量在开发者离开办公室之前给他反馈。如果已经回家了，尽量确保他在第二天早上来公司之前给出反馈。

## LGTM的反馈 {#lgtm-with-comments}

In order to speed up code reviews, there are certain situations in which a
reviewer should give LGTM/Approval even though they are also leaving unresolved
comments on the CL. This is done when either:
为了加快代码审核，有一些确定的场景，你应该给出 LGTM/赞同 的反馈，即使开发者仍有一些未处理的反馈（unresolved comments）。这些场景满足如下任一种情况即可：

*   The reviewer is confident that the developer will appropriately address all
    the reviewer's remaining comments.
    审核者相信开发者会对所有未处理的反馈做出合适的响应。
*   The remaining changes are minor and don't _have_ to be done by the
    developer.
    未处理的反馈无关紧要，开发者 _没必要_ 处理。

The reviewer should specify which of these options they intend, if it is not
otherwise clear.
审核者应该阐明他做出 LGTM 是哪种场景。

LGTM With Comments is especially worth considering when the developer and
reviewer are in different time zones and otherwise the developer would be
waiting for a whole day just to get "LGTM, Approval."
LGTM 特别值得考虑，尤其是当开发者与审核者跨时区时，否则开发者又得等一天时间才能得到“LGTM，赞成”。

## 大 CL {#large}

If somebody sends you a code review that is so large you're not sure when you
will be able to have time to review it, your typical response should be to ask
the developer to
[split the CL into several smaller CLs](../developer/small-cls.md) that build on
each other, instead of one huge CL that has to be reviewed all at once. This is
usually possible and very helpful to reviewers, even if it takes additional work
from the developer.
如果某位开发者提交一份很大的代码审核，你不打确认自己是否有时间审核它，一种典型的响应是让开发者[把一个CL拆分成多个](../developer/small-cls.md)，而不是让审核者一次审核大 CL 。这样对审核者比较有用，虽然对开发者而言有些额外的工作，这是值得的。

If a CL *can't* be broken up into smaller CLs, and you don't have time to review
the entire thing quickly, then at least write some comments on the overall
design of the CL and send it back to the developer for improvement. One of your
goals as a reviewer should be to always unblock the developer or enable them to
take some sort of further action quickly, without sacrificing code health to do
so.
如果一个 CL *不能* 拆分成多个，并且你很难在短时间内审核代码，至少在CL的整体设计上向开发者提出反馈，以便让开发者改进。作为一个审核者，你的目标之一是：尽量不要阻塞开发者，让他能迅速采取下一步行动。当然，前提是不会降低代码质量。

## Code Review Improvements Over Time {#time}

If you follow these guidelines and you are strict with your code reviews, you
should find that the entire code review process tends to go faster and faster
over time. Developers learn what is required for healthy code, and send you CLs
that are great from the start, requiring less and less review time. Reviewers
learn to respond quickly and not add unnecessary latency into the review
process.
But **don't compromise on
the [code review standards](standard.md) or quality for an imagined improvement
in velocity**&mdash;it's not actually going to make anything happen more
quickly, in the long run.

## 紧急情况

There are also [emergencies](../emergencies.md) where CLs must pass through the
_whole_ review process very quickly, and where the quality guidelines would be
relaxed. However, please see [What Is An Emergency?](../emergencies.md#what) for
a description of which situations actually qualify as emergencies and which
don't.

Next: [How to Write Code Review Comments](comments.md)
下一章: [怎样写代码审核反馈](comments.md)
