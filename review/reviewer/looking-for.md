# 在代码审核过程中要看些什么？



Note: Always make sure to take into account
[The Standard of Code Review](standard.md) when considering each of these
points.
注意：在考虑下面这些要素时，时刻记住要遵循[代码审核标准](standard.md)。

## 设计

The most important thing to cover in a review is the overall design of the CL.
Do the interactions of various pieces of code in the CL make sense? Does this
change belong in your codebase, or in a library? Does it integrate well with the
rest of your system? Is now a good time to add this functionality?
审核一个CL最重要的事情就是考虑它的整体设计。CL中的代码交互是否有意义？这段代码应该放到代码库（codebase）里，还是库（library）里？它能很好地与系统其他部分集成吗？现在加入这个功能是时机正好吗？

## 功能

Does this CL do what the developer intended? Is what the developer intended good
for the users of this code? The "users" are usually both end-users (when they
are affected by the change) and developers (who will have to "use" this code in
the future).
这个CL所实现的行为与开发者期望开发的功能是一致的吗？开发者的意图是否对代码的“用户”有好处？这儿提到的“用户”通常包含最终用户（最终使用这些开发出来的功能的用户）和开发者（以后可能会“使用”这些代码的开发者）。

Mostly, we expect developers to test CLs well-enough that they work correctly by
the time they get to code review. However, as the reviewer you should still be
thinking about edge cases, looking for concurrency problems, trying to think
like a user, and making sure that there are no bugs that you see just by reading
the code.
大多数情况下，我们期望开发者在提交CL进行审核之前，已经经过充分的测试。但是，作为审核者，在审核代码时，仍要考虑边界情况、并发问题等等。确保消灭那些通过阅读代码就能发现的bug。

You *can* validate the CL if you want—the time when it's most important for a
reviewer to check a CL's behavior is when it has a user-facing impact, such as a
**UI change**. It's hard to understand how some changes will impact a user when
you're just reading the code. For changes like that, you can have the developer
give you a demo of the functionality if it's too inconvenient to patch in the CL
and try it yourself.
作为审核者，你*可以*根据需要亲自验证CL的功能，尤其是当这个CL的行为包含面向用户的影响时，如**UI改变**。如果仅通过阅读代码，你很难理解有哪些改变，对用户有哪些影响。对于这样的改变，可以让开发者演示这个功能。当然，如果方便把CL的代码集成到你的开发环境的话，你也可以自己亲自尝试。

Another time when it's particularly important to think about functionality
during a code review is if there is some sort of **parallel programming** going
on in the CL that could theoretically cause deadlocks or race conditions. These
sorts of issues are very hard to detect by just running the code and usually
need somebody (both the developer and the reviewer) to think through them
carefully to be sure that problems aren't being introduced. (Note that this is
also a good reason not to use concurrency models where race conditions or
deadlocks are possible—it can make it very complex to do code reviews or
understand the code.)
在代码审核过程中也需要考虑功能的一种重要情形是：CL中包含一些“并行计算”，可能会带来死锁或竞争条件。这种类型的问题一般很难通过运行代码就能发现，通常需要一些人（开发者和审核者）仔细考虑，以确保不会引入新的问题。（这也是不要引入并发模型的一个好理由，因为它可能引入死锁或竞争条件，同时也增加了代码评审和理解代码的难度。）


## 复杂性

Is the CL more complex than it should be? Check this at every level of the
CL—are individual lines too complex? Are functions too complex? Are classes too
complex? "Too complex" usually means **"can't be understood quickly by code
readers."** It can also mean **"developers are likely to introduce bugs when
they try to call or modify this code."**
是不是CL不应该这么复杂？在CL的每个层次上检查--哪一行或那几行是不是太复杂了？是否功能太复杂了？是否类（class）太复杂了？“太复杂”的定义是**代码阅读者不易快速理解。** 同时意味着**以后其他开发者调用或修改它时，很容易引入新的bug。**

A particular type of complexity is **over-engineering**, where developers have
made the code more generic than it needs to be, or added functionality that
isn't presently needed by the system. Reviewers should be especially vigilant
about over-engineering. Encourage developers to solve the problem they know
needs to be solved *now*, not the problem that the developer speculates *might*
need to be solved in the future. The future problem should be solved once it
arrives and you can see its actual shape and requirements in the physical
universe.
另一种类型的复杂是**过度工程化**（也称为过度设计）。开发者在设计代码时太过于在意它的通用性，或在系统中加入了目前不需要的功能。审核者应该特别警惕过度工程化。鼓励开发者解决 *当前* 应该解决的问题，而不是开发者推测将来 *可能* 需要解决的问题。将来的问题，等碰到的时候，你才能看到它的实际需求和具体情况，这个时候再解决也不迟。

## 测试

Ask for unit, integration, or end-to-end
tests as appropriate for the change. In general, tests should be added in the
same CL as the production code unless the CL is handling an
[emergency](../emergencies.md).
同时要求提供CL对应的单元、集成或端到端的测试。一般情况下，测试代码与开发代码放到同一个CL中，除非碰到[紧急情况](../emergencies.md)。

Make sure that the tests in the CL are correct, sensible, and useful. Tests do
not test themselves, and we rarely write tests for our tests—a human must ensure
that tests are valid.
确保CL中的测试时正确的、明智的、有用的。测试代码并不是用来测试其自身，我们很少为测试代码写测试代码--这就要求我们一定要确保测试代码是正确的。

Will the tests actually fail when the code is broken? If the code changes
beneath them, will they start producing false positives? Does each test make
simple and useful assertions? Are the tests separated appropriately between
different test methods?
当代码出问题时，是否测试会运行失败？如果代码改变了，是否会产生误报？是否每个测试都使用了简单有用的断言？不同的测试方式是否做了合适的拆分？

Remember that tests are also code that has to be maintained. Don't accept
complexity in tests just because they aren't part of the main binary.
记住，测试代码也是需要维护的代码。不要接受复杂的测试代码，因为它不会编译打包到最终的产品中。

## 命名

Did the developer pick good names for everything? A good name is long enough to
fully communicate what the item is or does, without being so long that it
becomes hard to read.
开发者是否为所有的元素（如类、变量、方法等）取了一个好名称。一个好的名称应该足够长，足以明确地描述它是什么，他能做什么，但是也不要长到很难阅读。

## 注释

Did the developer write clear comments in understandable English? Are all of the
comments actually necessary? Usually comments are useful when they **explain
why** some code exists, and should not be explaining *what* some code is doing.
If the code isn't clear enough to explain itself, then the code should be made
simpler. There are some exceptions (regular expressions and complex algorithms
often benefit greatly from comments that explain what they're doing, for
example) but mostly comments are for information that the code itself can't
possibly contain, like the reasoning behind a decision.
开发者是否使用英文写了清晰的注释？是否所有的注释都是必须的？通常当注释**解释为什么**这些代码应该存在时，它才是必须的，而不是解释这些代码做**什么**。如果代码逻辑不清晰，让人看不懂，那么应该重写，让它变得更简单。当然，也有例外（例如，正则表达式和复杂的算法通常需要注释来说明），但是大多数注释应该提供代码本身没有提供的信息，如这么做背后的原因是什么。

It can also be helpful to look at comments that were there before this CL. Maybe
there is a TODO that can be removed now, a comment advising against this change
being made, etc.
有时候也应该看一下这个CL之前的注释。例如，以前写的TODO，可能现在能删掉了；建议不要做改动的注释，但是这个CL里面却改了，也应该仔细分析下。


Note that comments are different from *documentation* of classes, modules, or
functions, which should instead express the purpose of a piece of code, how it
should be used, and how it behaves when used.
注意，注释与类、模块、功能的*文档*是不同的，这类文档应该描述这些代码的功能，怎样被调用，以及被调用时它的行为是什么。

## 样式

We have [style guides](http://google.github.io/styleguide/) at Google for all
of our major languages, and even for most of the minor languages. Make sure the
CL follows the appropriate style guides.
在Google，我们所有的主要编程语言都要遵循[样式指南](http://google.github.io/styleguide/)。确保CL遵守样式指南中的建议。

If you want to improve some style point that isn't in the style guide, prefix
your comment with "Nit:" to let the developer know that it's a nitpick that you
think would improve the code but isn't mandatory. Don't block CLs from being
submitted based only on personal style preferences.
如果你发现某些样式在样式指南中并未包含，在注释中加上“Nit”，让开发者知道，这是一个小瑕疵，他可以依照你的建议去做，但这不是必须的。不要因为个人的样式偏好而导致CL延迟提交。

The author of the CL should not include major style changes combined with other
changes. It makes it hard to see what is being changed in the CL, makes merges
and rollbacks more complex, and causes other problems. For example, if the
author wants to reformat the whole file, have them send you just the
reformatting as one CL, and then send another CL with their functional changes
after that.
CL的作者在提交时，代码中不应包含较大的样式改变。因为这样很难比较出CL中有哪些改变，让代码合并、回滚变得更困难，容易产生问题。如果作者想重新格式化文件，应该把格式化作为一个单独CL先提交，之后再提交包含功能的CL。

## 文档

If a CL changes how users build, test, interact with, or release code, check to
see that it also updates associated documentation, including
READMEs, g3doc pages, and any generated
reference docs. If the CL deletes or deprecates code, consider whether the
documentation should also be deleted.
If documentation is missing, ask for it.
如果CL改变了编译、测试、交互、发布的方式，那么应检查下相关的问题是否也更新了，如README文件、g3doc页面，还有任何生成的参考文档。如果CL删除或弃用（deprecate）了一些代码，考虑是否也应该删除相应的文档。如果没有相关的问题，先找到它。

## 每行代码 {#every_line}

Look at *every* line of code that you have been assigned to review. Some things
like data files, generated code, or large data structures you can scan over
sometimes, but don't scan over a human-written class, function, or block of code
and assume that what's inside of it is okay. Obviously some code deserves more
careful scrutiny than other code&mdash;that's a judgment call that you have to
make&mdash;but you should at least be sure that you *understand* what all the
code is doing.
如果让你评审这些代码的话，仔细查看*每行*代码。有些文件，如数据文件、生成的代码或较大的数据结构，可以一扫而过。但是人写的代码，如类、功能或代码块不能一目十行，我们不应假设它就是正确的。显然有些代码应该尤其小心--这需要你自己权衡--至少你应该明白你*理解*这些代码在做什么。

If it's too hard for you to read the code and this is slowing down the review,
then you should let the developer know that
and wait for them to clarify it before you try to review it. At Google, we hire
great software engineers, and you are one of them. If you can't understand the
code, it's very likely that other developers won't either. So you're also
helping future developers understand this code, when you ask the developer to
clarify it.
如果代码很难读懂，那就放慢审核速度，让开发这知道你没读懂，并让他解释与澄清代码，然后再审核。在Google，我们雇佣都是伟大的工程师，你是其中一员。如果你也不懂，很有可能其他工程师也不懂。实际上，这么做也是在帮助以后在这段代码基础上开发的工程师，让他们更容易理解代码。所以，让开发者解释清楚。

If you understand the code but you don't feel qualified to do some part of the
review, make sure there is a reviewer on the CL who is qualified, particularly
for complex issues such as security, concurrency, accessibility,
internationalization, etc.
如果你理解这些代码，但是感觉自己没有资格审核这些代码，确保找到一个够资格的人来审核，尤其是比较复杂的问题，如安全、并发、可访问性、国际化等等。

## 上下文

It is often helpful to look at the CL in a broad context. Usually the code
review tool will only show you a few lines of code around the parts that are
being changed. Sometimes you have to look at the whole file to be sure that the
change actually makes sense. For example, you might see only four new lines
being added, but when you look at the whole file, you see those four lines are
in a 50-line method that now really needs to be broken up into smaller methods.
把这个CL放到一个更广阔的上下文中来看通常很有用。审核工具中，我们往往只能看到开发者修改的那部分代码。有时候从整个文件的角度来读代码才有意义。例如，有时候你只看到添加了几行代码，但从整个文件来看，你发现这4行代码在添加到了一个50行的方法中，因此需要把它拆分成更小的方法。

It's also useful to think about the CL in the context of the system as a whole.
Is this CL improving the code health of the system or is it making the whole
system more complex, less tested, etc.? **Don't accept CLs that degrade the code
health of the system.** Most systems become complex through many small changes
that add up, so it's important to prevent even small complexities in new
changes.
把这个CL放到这个系统的上下文中来考虑这个CL也很有用。这个CL能够提升整个系统的代码健康状况，还是让系统变得更复杂、更难测试？**不要接受恶化系统的健康状况的代码。** 大多数系统系统变得很复杂都是由每个微小的复杂累积而成的，在提交每个CL时都应避免让代码变得复杂。

## 好的东西 {#good_things}

If you see something nice in the CL, tell the developer, especially when they
addressed one of your comments in a great way. Code reviews often just focus on
mistakes, but they should offer encouragement and appreciation for good
practices, as well. It’s sometimes even more valuable, in terms of mentoring, to
tell a developer what they did right than to tell them what they did wrong.
如果在CL中看到一些比较好的方面，告诉开发者，尤其是当他解释你对他的代码的评论的时候。审核者往往只关注代码中的错误，他们也应该对开发者的一些好的实践表示鼓励和感谢。有时候，告诉开发者他们在那些方面做得很好，比告诉他们在哪些方面做得不足更有价值。

## 总结

In doing a code review, you should make sure that:
在进行代码评审时，你应该确保如下几点：
-   The code is well-designed. 代码是否涉及良好。
-   The functionality is good for the users of the code. 功能是否对代码的用户有用。
-   Any UI changes are sensible and look good.所有的UI改变都是明智的，看起来很不错。
-   Any parallel programming is done safely.所有的并行计算都很安全。
-   The code isn't more complex than it needs to be. 代码尽量简单。
-   The developer isn't implementing things they *might* need in the future but
    don't know they need now. 开发这没有实现现在不需要，但是他们认为将来*可能*会用到的功能。
-   Code has appropriate unit tests.代码有合适的单元测试。
-   Tests are well-designed. 单元测试涉及良好。
-   The developer used clear names for everything.
-   Comments are clear and useful, and mostly explain *why* instead of *what*.
-   Code is appropriately documented (generally in g3doc).
-   The code conforms to our style guides.

Make sure to review **every line** of code you've been asked to review, look at
the **context**, make sure you're **improving code health**, and compliment
developers on **good things** that they do.

Next: [Navigating a CL in Review](navigate.md)
下一章：[代码审核的步骤](navigate.md)
