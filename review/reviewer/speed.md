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
如果你现在没有进行一项需要集中集中精力的任务，**你应该在收到审核邀请时，短时间内就开始代码审核。** 

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

Instead, wait for a break point in your work before you respond to a request for
review. This could be when your current coding task is completed, after lunch,
returning from a meeting, coming back from the microkitchen, etc.

## 快速响应 {#responses}

When we talk about the speed of code reviews, it is the _response_ time that we
are concerned with, as opposed to how long it takes a CL to get through the
whole review and be submitted. The whole process should also be fast, ideally,
but **it's even more important for the _individual responses_ to come quickly
than it is for the whole process to happen rapidly.**

Even if it sometimes takes a long time to get through the entire review
_process_, having quick responses from the reviewer throughout the process
significantly eases the frustration developers can feel with "slow" code
reviews.

If you are too busy to do a full review on a CL when it comes in, you can still
send a quick response that lets the developer know when you will get to it,
suggest other reviewers who might be able to respond more quickly, or
[provide some initial broad comments](navigate.md). (Note: none of this means
you should interrupt coding even to send a response like this&mdash;send the
response at a reasonable break point in your work.)

**It is important that reviewers spend enough time on review that they are
certain their "LGTM" means "this code meets [our standards](standard.md)."**
However, individual responses should still ideally be [fast](#fast).

## 跨时区的审核 {#tz}

When dealing with time zone differences, try to get back to the author when they
are still in the office. If they have already gone home, then try to make sure
your review is done before they get back to the office the next day.

## LGTM的反馈 {#lgtm-with-comments}

In order to speed up code reviews, there are certain situations in which a
reviewer should give LGTM/Approval even though they are also leaving unresolved
comments on the CL. This is done when either:

*   The reviewer is confident that the developer will appropriately address all
    the reviewer's remaining comments.
*   The remaining changes are minor and don't _have_ to be done by the
    developer.

The reviewer should specify which of these options they intend, if it is not
otherwise clear.

LGTM With Comments is especially worth considering when the developer and
reviewer are in different time zones and otherwise the developer would be
waiting for a whole day just to get "LGTM, Approval."

## 大 CL {#large}

If somebody sends you a code review that is so large you're not sure when you
will be able to have time to review it, your typical response should be to ask
the developer to
[split the CL into several smaller CLs](../developer/small-cls.md) that build on
each other, instead of one huge CL that has to be reviewed all at once. This is
usually possible and very helpful to reviewers, even if it takes additional work
from the developer.

If a CL *can't* be broken up into smaller CLs, and you don't have time to review
the entire thing quickly, then at least write some comments on the overall
design of the CL and send it back to the developer for improvement. One of your
goals as a reviewer should be to always unblock the developer or enable them to
take some sort of further action quickly, without sacrificing code health to do
so.

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
