# 代码审核的标准 （The Standard of Code Review）



The primary purpose of code review is to make sure that the overall
code health of Google's code
base is improving over time. All of the tools and processes of code review are
designed to this end.
代码审核的目的是为了确保Google代码库中所有的代码保持在不断地改善过程中，代码审核的所有工具和过程都是为了这个目的而设计。

In order to accomplish this, a series of trade-offs have to be balanced.
为了达到目标，我们需要权衡得失。

First, developers must be able to _make progress_ on their tasks. If you never
submit an improvement to the codebase, then the codebase never improves. Also,
if a reviewer makes it very difficult for _any_ change to go in, then developers
are disincentivized to make improvements in the future.
首先，开发人员必须能在任务上 _取得进展_ 。如果从没向代码库提交代码，那么代码库就不会改善。同时，如果审核者让代码提交者在提交代码时变得很困难的话，那么开发者会认为这种 _改进_ 没有益处，也就没有动力在未来的提交中做出改进。

On the other hand, it is the duty of the reviewer to make sure that each CL is
of such a quality that the overall code health of their codebase is not
decreasing as time goes on. This can be tricky, because often, codebases degrade
through small decreases in code health over time, especially when a team is
under significant time constraints and they feel that they have to take
shortcuts in order to accomplish their goals.
另一方面，审核者有责任确保提交者的代码质量，随着时间的推移，代码库的质量不会降低。这有点棘手，冰手三尺非一日之寒，代码库质量的降低是随着每次代码提交的微小降低累积而成的，尤其是当团队处于时间压力下时，为了完成任务，他们不得不采取一些临时方案。

Also, a reviewer has ownership and responsibility over the code they are
reviewing. They want to ensure that the codebase stays consistent, maintainable,
and all of the other things mentioned in
["What to look for in a code review."](looking-for.md)
另外，代码审核者对他们审核的代码有所有权和责任，他们应该确保代码库保持一致、可维护的，所有这些内容可参见[代码审核过程中要看些什么？ （What to Look For In a Code Review）](looking-for.md)这篇文章。

Thus, we get the following rule as the standard we expect in code reviews:
这样，我们希望在代码审核中能遵循如下原则：

**In general, reviewers should favor approving a CL once it is in a state where
it definitely improves the overall
code health of the system
being worked on, even if the CL isn't perfect.**
**一般情况下，如果代码提交者的代码能显著提高代码库的质量，那么审核者就应该批准它，尽管它并不完美。**

That is _the_ senior principle among all of the code review guidelines.
这是所有代码评审指南的 _最高原则_。

There are limitations to this, of course. For example, if a CL adds a feature
that the reviewer doesn't want in their system, then the reviewer can certainly
deny approval even if the code is well-designed.
当然，也有例外。例如，如果一次提交包含了一些系统中不应加入的功能，那么审核者就不应批准它，即使它设计得非常完美。


A key point here is that there is no such thing as "perfect" code&mdash;there is
only _better_ code. Reviewers should not require the author to polish every tiny
piece of a CL before granting approval. Rather, the reviewer should balance out
the need to make forward progress compared to the importance of the changes they
are suggesting. Instead of seeking perfection, what a reviewer should seek is
_continuous improvement_. A CL that, as a whole, improves the maintainability,
readability, and understandability of the system shouldn't be delayed for days
or weeks because it isn't "perfect."
还有一个关键点，那就是世上根本就没有“完美”的代码－－只有 _更好_ 的代码。审核者不应该要求代码提交者

Reviewers should _always_ feel free to leave comments expressing that something
could be better, but if it's not very important, prefix it with something like
"Nit: " to let the author know that it's just a point of polish that they could
choose to ignore.

Note: Nothing in this document justifies checking in CLs that definitely
_worsen_ the overall code health of the system. The only time you would do that
would be in an [emergency](../emergencies.md).

## Mentoring

Code review can have an important function of teaching developers something new
about a language, a framework, or general software design principles. It's
always fine to leave comments that help a developer learn something new. Sharing
knowledge is part of improving the code health of a system over time. Just keep
in mind that if your comment is purely educational, but not critical to meeting
the standards described in this document, prefix it with "Nit: " or otherwise
indicate that it's not mandatory for the author to resolve it in this CL.

## Principles {#principles}

*   Technical facts and data overrule opinions and personal preferences.

*   On matters of style, the [style guide](http://google.github.io/styleguide/)
    is the absolute authority. Any purely style point (whitespace, etc.) that is
    not in the style guide is a matter of personal preference. The style should
    be consistent with what is there. If there is no previous style, accept the
    author's.

*   **Aspects of software design are almost never a pure style issue or just a
    personal preference.** They are based on underlying principles and should be
    weighed on those principles, not simply by personal opinion. Sometimes there
    are a few valid options. If the author can demonstrate (either through data
    or based on solid engineering principles) that several approaches are
    equally valid, then the reviewer should accept the preference of the author.
    Otherwise the choice is dictated by standard principles of software design.

*   If no other rule applies, then the reviewer may ask the author to be
    consistent with what is in the current codebase, as long as that doesn't
    worsen the overall code health of the system.

## Resolving Conflicts {#conflicts}

In any conflict on a code review, the first step should always be for the
developer and reviewer to try to come to consensus, based on the contents of
this document and the other documents in [The CL Author's Guide](../developer/)
and this [Reviewer Guide](index.md).

When coming to consensus becomes especially difficult, it can help to have a
face-to-face meeting or a VC between the reviewer and the author, instead of
just trying to resolve the conflict through code review comments. (If you do
this, though, make sure to record the results of the discussion in a comment on
the CL, for future readers.)

If that doesn't resolve the situation, the most common way to resolve it would
be to escalate. Often the
escalation path is to a broader team discussion, having a TL weigh in, asking
for a decision from a maintainer of the code, or asking an Eng Manager to help
out. **Don't let a CL sit around because the author and the reviewer can't come
to an agreement.**

Next: [What to look for in a code review](looking-for.md)
