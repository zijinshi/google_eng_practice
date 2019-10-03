# 如何处理审核评论

When you've sent a CL out for review, it's likely that your reviewer will
respond with several comments on your CL. Here are some useful things to know
about handling reviewer comments.
在发出 CL 之后，一般会收到审核者的评论。下面我们就来详细描述如何处理这些评论。

## 不要情绪化 {#personal}

The goal of review is to maintain the quality of our codebase and our products.
When a reviewer provides a critique of your code, think of it as their attempt
to help you, the codebase, and Google, rather than as a personal attack on you
or your abilities.
代码审核的目标是保证提交到的代码库中代码的质量，进而保证产品的质量。当审核者提出一些批判性的评论时，开发者应该告诉自己，他在尝试帮助你，保证代码库的质量，帮助 Google，而不是针对你的人身攻击或个人能力的怀疑。

Sometimes reviewers feel frustrated and they express that frustration in their
comments. This isn't a good practice for reviewers, but as a developer you
should be prepared for this. Ask yourself, "What is the constructive thing that
the reviewer is trying to communicate to me?" and then operate as though that's
what they actually said.
有时候，审核者感到很沮丧，并在评论中表达了这种心情。其实，这不是一种正确的方式，但作为开发者，你应该有足够的心理状态来面对这种情况。问一下自己，“我能从审核者的评论中读出那些建设性的意见？”假想他们就是以这种建设性的语气对你说的，然后按照这种建议去做。


**Never respond in anger to code review comments.** That is a serious breach of
professional etiquette that will live forever in the code review tool. If you
are too angry or annoyed to respond kindly, then walk away from your computer
for a while, or work on something else until you feel calm enough to reply
politely.
**不要在代码审核中带着情绪回复评论。** 在审核代码过程中，违反专业礼仪是件很严重的事情，但我们永远没法确保别人是否违反专业礼仪。但我们可以保证自己不要违反它。如果你很生气或恼火，以致于无法友好地回复，那就离开电脑一会儿，或者先换一件事情做直到心态平静下来，再礼貌地回复。

In general, if a reviewer isn't providing feedback in a way that's constructive
and polite, explain this to them in person. If you can't talk to them in person
or on a video call, then send them a private email. Explain to them in a kind
way what you don't like and what you'd like them to do differently. If they also
respond in a non-constructive way to this private discussion, or it doesn't have
the intended effect, then
escalate to your manager as
appropriate.
一般情况下，如果审核者没有以建设性地口吻提供反馈，反馈的方式不够礼貌，可以私下里向他解释。如果不能私下与他沟通，也不能通过是视频电话远程沟通，可以给他单独发一封邮件。在邮件中，以友好的态度向他解释，你很难接受这种反馈方式，期待他能换一种沟通方式。如果他仍旧以一种非建设性的方式回复你，或没有达到预期效果，那就升级到他的主管吧。

## 修复代码 {#code}

If a reviewer says that they don't understand something in your code, your first
response should be to clarify the code itself. If the code can't be clarified,
add a code comment that explains why the code is there. If a comment seems
pointless, only then should your response be an explanation in the code review
tool.
如果审核者说，他对你的代码中有些内容不理解，你的第一反应是澄清代码本身。如果代码无法澄清，加一段注释用以解释为什么这段代码这样写。如果这段注释放到代码里毫无意义，那就应该放到代码评审工作的评论中作为反馈的解释。

If a reviewer didn't understand some piece of your code, it's likely other
future readers of the code won't understand either. Writing a response in the
code review tool doesn't help future code readers, but clarifying your code or
adding code comments does help them.
如果审核者无法理解某段代码，很有可能其他的代码阅读者也不懂。在代码审核工具中回复它对未来的代码阅读者没有任何好处。这种情况应该尝试清理代码，或增加一些必要的注释，以帮助他们阅读。

## 先思考自己是否有改进的空间 {#think}

Writing a CL can take a lot of work. It's often really satisfying to finally
send one out for review, feel like it's done, and be pretty sure that no further
work is needed. So when a reviewer comes back with comments on things that could
be improved, it's easy to reflexively think the comments are wrong, the reviewer
is blocking you unnecessarily, or they should just let you submit the CL.
However, **no matter how certain you are** at this point, take a moment to step
back and consider if the reviewer is providing valuable feedback that will help
the codebase and Google. Your first question to yourself should always be, "Is
the reviewer correct?"
写一个 CL 会耗费大量精力。在提交一个 CL 审核时，开发者的心态会往往会产生几乎快要完成的幻想，确定无需进一步修改。当审核者回复需要修改某些代码时，开发者容易条件反射地认为反馈不正确，审核者没必要阻碍自己的开发，他应该让这个 CL 审核通过 。
然而，**无论你有多确定** 这点，最好还是先退一步，仔细考虑审核者是否在反馈中提供了有价值的内容，可以帮助提高代码库的质量。你的第一个问题应该永远都是，“审核者说得对吗？”

If you can't answer that question, it's likely the reviewer needs to clarify
their comments.
如果你无法回答这个问题，很有可能审核者需要进一步澄清评论。

If you *have* considered it and you still think you're right, feel free to
respond with an explanation of why your method of doing things is better for the
codebase, users, and/or Google. Often, reviewers are actually providing
*suggestions* and they want you to think for yourself about what's best. You
might actually know something about the users, codebase, or CL that the reviewer
doesn't know. So fill them in; give them more context. Usually you can come to
some consensus between yourself and the reviewer based on technical facts.
如果你 *已经* 思考过，并确认你是对的，那就在回复中解释为什么你的方法比较好（相对已有的代码、用户）。通常，审核者也会提供*建议* ，他们希望你比较一下哪个更好。你可能知道一些关于用户、代码库或 CL的内容，而这些正是审核者不了解的，那么就把这些写出来，提供更多的上下文。通常，你在技术上可以与审核者达成一致。

## 解决冲突 {#conflicts}

Your first step in resolving conflicts should always be to try to come to
consensus with your reviewer. If you can't achieve consensus, see
[The Standard of Code Review](../reviewer/standard.md), which gives principles
to follow in such a situation.
在解决冲突的第一步，永远都是应该先尝试与审核者达成共识。如果无法达成共识，可以参考[审核代码标准](../reviewer/standard.md)，当面临这种情形时，它为我们提供了一些准则。
