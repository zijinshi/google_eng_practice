# 代码评论被拒绝时，应如何处理？


Sometimes a developer will push back on a code review. Either they will disagree
with your suggestion or they will complain that you are being too strict in
general.
有时候，面对审核者的评论，开发者可能会拒绝。有可能他们不同意你的建议，或者他们认为你太过于苛刻了。

## 谁是对的? {#who_is_right}

When a developer disagrees with your suggestion, first take a moment to consider
if they are correct. Often, they are closer to the code than you are, and so
they might really have a better insight about certain aspects of it. Does their
argument make sense? Does it make sense from a code health perspective? If so,
let them know that they are right and let the issue drop.当开发者不同意的建议时，先花点时间考虑一下他们是否正确。开发者往往更接近代码，在某些方面他们对代码有更好的见解。他们的论点是否理由充分？站在代码健康的角度，是否应该如此？如果回答“是”，告诉他们，他们是对的，可以忽略这条评论。

However, developers are not always right. In this case the reviewer should
further explain why they believe that their suggestion is correct. A good
explanation demonstrates both an understanding of the developer's reply, and
additional information about why the change is being requested.
但开发者并非总是对的。这种情况，代码审核者应该进一步解释为何他相信自己的建议是正确的。一个很好地解释通常包含两部分：对开发人员的回复的解释和进一步说明这么改的必要性。

In particular, when the reviewer believes their suggestion will improve code
health, they should continue to advocate for the change, if they believe the
resulting code quality improvement justifies the additional work requested.
**Improving code health tends to happen in small steps.**
尤其是当审核者相信他们的建议能够有效提升代码质量时，他们应该继续拥护这种改变。即使有证据显示这种代码提升需要一些额外的工作，也值得做。 **提升代码质量往往是聚沙成塔的过程。**


Sometimes it takes a few rounds of explaining a suggestion before it really
sinks in. Just make sure to always stay [polite](comments.md#courtesy) and let
the developer know that you *hear* what they're saying, you just don't *agree*.
有时候，需要经过好几轮的解释与澄清，你的建议才会被接受。确保自始至终都保持[礼貌](comments.md#courtesy) ，让开发者知道你在 *听* 他说的话，只是不 *同意* 他的观点而已。

## 烦躁的开发者 {#upsetting_developers}

Reviewers sometimes believe that the developer will be upset if the reviewer
insists on an improvement. Sometimes developers do become upset, but it is
usually brief and they become very thankful later that you helped them improve
the quality of their code. Usually, if you are [polite](comments.md#courtesy) in
your comments, developers actually don't become upset at all, and the worry is
just in the reviewer's mind. Upsets are usually more about
[the way comments are written](comments.md#courtesy) than about the reviewer's
insistence on code quality.
审核者相信，有时候如果自己坚持应该改进，那么开发者可能会心烦。这种事的确偶有发生，但通常持续时间很短，稍后他们会感谢审核者，正是他的坚持让代码质量得以提升。通常，如果在评论中保持[礼貌](comments.md#courtesy)，开发者根本就不会烦躁，审核者不必担忧。烦躁大多是因为[写评论的方式](comments.md#courtesy)没有把焦点放在代码质量上。

## 稍后再清理 {#later}

A common source of push back is that developers (understandably) want to get
things done. They don't want to go through another round of review just to get
this CL in. So they say they will clean something up in a later CL, and thus you
should LGTM *this* CL now. Some developers are very good about this, and will
immediately write a follow-up CL that fixes the issue. However, experience shows
that as more time passes after a developer writes the original CL, the less
likely this clean up is to happen. In fact, usually unless the developer does
the clean up *immediately* after the present CL, it never happens. This isn't
because developers are irresponsible, but because they have a lot of work to do
and the cleanup gets lost or forgotten in the press of other work. Thus, it is
usually best to insist that the developer clean up their CL *now*, before the
code is in the codebase and "done." Letting people "clean things up later" is a
common way for codebases to degenerate.
一种常见的拒绝原因是：开发者（可以理解得）想尽快完成它。他们不想再进行一轮审核，只想快点把 CL 提交到代码库。所以，他们说他们会在稍后的 CL 中再清理代码，这样你应该对 *当前* CL 评论 LGTM了。有些开发者的确是这么做的，他们随后的确创建了一个新的 CL，用于修复当问题。然而，经验告诉我们，从开发者提交了原始 CL 之后，时间过得越久，他们清理代码的可能性越小。事实上，除非开发者在当前 CL 之后 *立即* 清理代码，否则以后也不会清理。这并不是说开发者不靠谱，而是因为他们有太多的开发工作要做，迫于其他工作的压力已经忘了清理之前提交的代码这件事。因此，我们建议，最好坚持让开发者 *现在* 就开始清理代码，而不是提交到代码库 *之后* 。 我们应该有种理念， 代码退化的常见原因有几个，“稍后再清理” 就是其中之一。

If a CL introduces new complexity, it must be cleaned up before submission
unless it is an [emergency](../emergencies.md). If the CL exposes surrounding
problems and they can't be addressed right now, the developer should file a bug
for the cleanup and assign it to themselves so that it doesn't get lost. They
can optionally also write a TODO comment in the code that references the filed
bug.
如果 CL 让代码变得复杂，那么它必须在提交之前清理完毕，除非是[紧急情况](../emergencies.md)。如果 CL 满是问题却不立即解决，开发者应该给自己发一个清理代码相关的bug，把它分配给自己，以避免遗忘。除此之外，在代码中加上 TODO 注释和相关的 bug 编码。

## 与严格相关的常见抱怨 {#strictness}

If you previously had fairly lax code reviews and you switch to having strict
reviews, some developers will complain very loudly. Improving the
[speed](speed.md) of your code reviews usually causes these complaints to fade
away.
如果以前你在做代码评审时比较宽松，现在突然变得严格起来，有些开发者可能会抱怨。没关系，通过提升审核代码的[速度](speed.md)通常会让抱怨消失。

Sometimes it can take months for these complaints to fade away, but eventually
developers tend to see the value of strict code reviews as they see what great
code they help generate. Sometimes the loudest protesters even become your
strongest supporters once something happens that causes them to really see the
value you're adding by being strict.
有时候，让抱怨消失的过程比较漫长，长达数月，但最后，开发者会往往趋于赞同严格审核代码的价值，因为在严格审核的帮助下，他们写出了伟大的代码。一旦大家看到了这种严格带来的价值，甚至最强烈的抗议者可能会变成最强大的拥护者。

## 冲突解决 {#conflicts}

If you are following all of the above but you still encounter a conflict between
yourself and a developer that can't be resolved, see
[The Standard of Code Review](standard.md) for guidelines and principles that
can help resolve the conflict.
作为审核者，如果你已经遵循本文中提到的所有规则，但仍旧与开发者之前产生了难以解决的冲突，可以参考[代码审核的标准](standard.md) ，以其中提到的规则与理论来指导解决冲突。
