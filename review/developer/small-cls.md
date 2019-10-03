# 小 CL



## 为什么应该写小CL{#why}

小 CL 有如下优点：

-   **Reviewed more quickly.** It's easier for a reviewer to find five minutes
    several times to review small CLs than to set aside a 30 minute block to
    review one large CL. **审核更快。**  相对让审核者单独拿出30分钟审核大 CL，不如让他花费几个5分钟审核代码。对审核者而言，后者更容易。
-   **Reviewed more thoroughly.** With large changes, reviewers and authors tend
    to get frustrated by large volumes of detailed commentary shifting back and
    forth—sometimes to the point where important points get missed or dropped.
    **审核更彻底。** 发生较大修改时，往往会反复审核、修改，审核者与开发者经常会因为过多的反复而在情绪上受到影响，以致于把精力放在修改上了，却忽略了 CL 中更重要的部分。    
-   **Less likely to introduce bugs.** Since you're making fewer changes, it's
    easier for you and your reviewer to reason effectively about the impact of
    the CL and see if a bug has been introduced.
    **引入新缺陷的可能性更小。** 如果修改的内容比较少，自然审核人的效率会更高，开发者与审核者都更容易判断是否引入了新的缺陷。
    
-   **Less wasted work if they are rejected.** If you write a huge CL and then
    your reviewer says that the overall direction is wrong, you've wasted a lot
    of work.
    **如果被拒绝，浪费的时间更少。** 如果开发者花费了很大的精力开发了一个大 CL，直到审核的时候才知道整个开发的方向错了，那么整个时间就全浪费了。
    
-   **Easier to merge.** Working on a large CL takes a long time, so you will
    have lots of conflicts when you merge, and you will have to merge
    frequently.
    **更容易合并代码。** 大 CL 在合并代码时会花费很长的时间，在合并时需要花费大量时间，而且在写 CL 期间可能不得不频繁地合并。
    
-   **Easier to design well.** It's a lot easier to polish the design and code
    health of a small change than it is to refine all the details of a large
    change.
    **更易于设计。** 完善设计和代码要容易得多，多次微小的代码质量提高比一次大的设计改变更容易。
    
-   **Less blocking on reviews.** Sending self-contained portions of your
    overall change allows you to continue coding while you wait for your current
    CL in review.
    **减少阻塞审核的可能性。** 小 CL 通常是功能独立的部分，你可能正在修改很多代码（多个小 CL），在发送一个 CL 审核时，同时可以继续修改其他的代码，并不会因为当前 CL 的审核没有完成而阻塞。
    
-   **Simpler to roll back.** A large CL will more likely touch files that get
    updated between the initial CL submission and a rollback CL, complicating
    the rollback (the intermediate CLs will probably need to be rolled back
    too).
    **更容易回退。** 一个大 CL 开发的时间比较长，这意味从开发到代码提交这段期间，代码文件的变更会比较多。当回退代码时，情况会变得很复杂，因为所有中间的 CL 很有可能也需要回退。

Note that **reviewers have discretion to reject your change outright for the
sole reason of it being too large.** Usually they will thank you for your
contribution but request that you somehow make it into a series of smaller
changes. It can be a lot of work to split up a change after you've already
written it, or require lots of time arguing about why the reviewer should accept
your large change. It's easier to just write small CLs in the first place.
请注意：**审核者有权因为你的 CL 太大而拒绝它。** 通常，他们会感谢你为代码做出的贡献，但是会要求你把它拆分多个小 CL。一旦写好了代码之后，要把它拆分成小 CL 通常需要花很多时间，当然，你也可能会花费大量时间与审核者争论为什么他应该接受这个大 CL 。与其如此，不如设计之初就保证 CL 尽量小。

## 如何定义“小”？ {#what_is_small}

In general, the right size for a CL is **one self-contained change**. This means
that:
一般而言，一个 CL 的大小就应该是 **独立功能的修改**。这意味着：

-   The CL makes a minimal change that addresses **just one thing**. This is
    usually just one part of a feature, rather than a whole feature at once. In
    general it's better to err on the side of writing CLs that are too small vs.
    CLs that are too large. Work with your reviewer to find out what an
    acceptable size is.
    
    一个 CL 尽量最小化，它只 **做一件事**。通常它只是一个功能的一部分，而不是整个功能。总体而言，CL 太小或太大都不好，二者取其轻的话，太小稍微好点。可以与审核者一起讨论，找出大多比较合适。
    
-   Everything the reviewer needs to understand about the CL (except future
    development) is in the CL, the CL's description, the existing codebase, or a
    CL they've already reviewed.
    审核者需要理解 CL 中包含的一切（除了以后可能要开发的功能之外），包括 CL 代码、描述、已存在的代码（或之前已经审核过的相关 CL ）。
    
-   The system will continue to work well for its users and for the developers
    after the CL is checked in.
    在 CL 代码提交之后，无论是针对用户，还是针对开发人员，系统应该仍旧运行良好。
    
-   The CL is not so small that its implications are difficult to understand. If
    you add a new API, you should include a usage of the API in the same CL so
    that reviewers can better understand how the API will be used. This also
    prevents checking in unused APIs.
    如果代码难以理解，通常是以为 CL 还不够小。如果新增一个 API，同时应该同一个 CL 中附上这个 API 的使用方法，便于审核者理解如何使用，也方便以后的开发者理解。同时也可能有效防止提交的 API 无人使用。

There are no hard and fast rules about how large is "too large." 100 lines is
usually a reasonable size for a CL, and 1000 lines is usually too large, but
it's up to the judgment of your reviewer. The number of files that a change is
spread across also affects its "size." A 200-line change in one file might be
okay, but spread across 50 files it would usually be too large.
没有直观的标准判断怎样的 CL 是“太大”。 100行代码通常是一个合理的大小。1000行代码通常太大了，但也不能一概而论，这取决于审核者的判断。修改文件的个数也影响它的“大小”。在一个文件中修改200行可能没问题，如果这200行代码横跨50个文件，通常而言太大了。

Keep in mind that although you have been intimately involved with your code from
the moment you started to write it, the reviewer often has no context. What
seems like an acceptably-sized CL to you might be overwhelming to your reviewer.
When in doubt, write CLs that are smaller than you think you need to write.
Reviewers rarely complain about getting CLs that are too small.
记住，当你开始编写代码时，只有你最了解代码，而审核者通常不了解上下文。在你看起来很是一个合适大小的 CL，审核者可能会很困惑。毫无疑问，在写 CL 时，CL 的大小最好比认为的还要小。审核者通常不会抱怨你的 CL 太小了。

## 什么时候可以有大 CL ？ {#large_okay}

There are a few situations in which large changes aren't as bad:
当然，也有一些例外情形，允许 CL 比较大：
-   You can usually count deletion of an entire file as being just one line of
    change, because it doesn't take the reviewer very long to review.
    删除一个文件与修改一行没有太大区别， 因为它不会花费审核者太多时间。
    
-   Sometimes a large CL has been generated by an automatic refactoring tool
    that you trust completely, and the reviewer's job is just to sanity check
    and say that they really do want the change. These CLs can be larger,
    although some of the caveats from above (such as merging and testing) still
    apply.
    有时候，一个大 CL 可能是由可靠的自动代码重构工具生成的，审核者的工作主要是检查它是否做了它应该做的工作。虽然符合以上提到的注意事项（例如合并和测试），这类 CL 也可能比较大。

### 以文件来拆分 {#splitting-files}

Another way to split up a CL is by groupings of files that will require
different reviewers but are otherwise self-contained changes.
另外一种拆分大 CL 的方法是：对 CL 中涉及的文件进行分组，这就要求不同独立功能的修改需要相应的审核者。

For example: you send off one CL for modifications to a protocol buffer and
another CL for changes to the code that uses that proto. You have to submit the
proto CL before the code CL, but they can both be reviewed simultaneously. If
you do this, you might want to inform both sets of reviewers about the other CL
that you wrote, so that they have context for your changes.
例如：你提交了一个 CL，这个 CL 修改了协议缓冲区，而且另外一个 CL 用到它。因此我们先提交第一个 CL，再提交第二个 CL，并让两个 CL 同时审核。如果这么做的话，你就得分别向两个 CL 的审核者告知另外一个 CL 的内容，以便他们知道上下文。

Another example: you send one CL for a code change and another for the
configuration or experiment that uses that code; this is easier to roll back
too, if necessary, as configuration/experiment files are sometimes pushed to
production faster than code changes.
以代码和配置文件进行拆分。例如，你提交了2个 CL：其中一个 CL 修改了一段代码，另外一个 CL 调用了这段代码或代码的相关配置；当需要代码回滚时，这也比较容易，因为配置或调用文件有时候推送到产品比代码修改相对容易。

## 单独重构 {#refactoring}

It's usually best to do refactorings in a separate CL from feature changes or
bug fixes. For example, moving and renaming a class should be in a different CL
from fixing a bug in that class. It is much easier for reviewers to understand
the changes introduced by each CL when they are separate.
在修改功能或修复缺陷的 CL 中，不建议把重构也加进来，而是建议把它放到单独的 CL 中。例如，修改类名或把某个类移到其他包内是一个 CL，修复这个类中的某个缺陷是一个 CL，不要把它们合并到一个 CL 中。把它们拆分出来更有利于审核者理解代码的变化。

Small cleanups such as fixing a local variable name can be included inside of a
feature change or bug fix CL, though. It's up to the judgment of developers and
reviewers to decide when a refactoring is so large that it will make the review
more difficult if included in your current CL.
有些代码清理工作，如修改某个类中的一个变量的名称，可以把它包含在一个功能修改或缺陷修复的 CL 中。那标准是什么呢？这取决开发者与审核者的判断，这种重构是否大到让审核工作变得很困难。

## 把测试代码包含到对应功能的 CL 中 {#test_code}

Avoid splitting test code into a separate CL. Tests validating your code
modifications should go into the same CL, even if it increases the code line
count.
避免单独提交测试代码。测试代码用以验证代码功能，应该把它与代码提交到相同的 CL 中，虽然它会增大 CL 的代码行数。

However, <i>independent</i> test modifications can go into separate CLs first,
similar to the [refactorings guidelines](#refactoring). That includes:
然而，<i>独立的</i>测试修改可以放到单独的 CL 中，这与[重构指南]中的观点比较类似。它包含如下：

*   validating pre-existing, submitted code with new tests.为过去提交的已存在代码创建新的测试代码。
*   refactoring the test code (e.g. introduce helper functions). 重构测试代码（例如，引入 helper 函数）。
*   introducing larger test framework code (e.g. an integration test). 引入测试框架代码（如，集成测试）。

## 不要破坏编译 {#break}

If you have several CLs that depend on each other, you need to find a way to
make sure the whole system keeps working after each CL is submitted. Otherwise
you might break the build for all your fellow developers for a few minutes
between your CL submissions (or even longer if something goes wrong unexpectedly
with your later CL submissions).
如果同时在审核的有多个 CL，并且这些 CL 之间存在依赖关系，你需要找到一种方式，确保在依次提交 CL 时，保证整个系统仍旧运行良好。否则，可能在提交某个 CL 之后，让系统编译错误。此时，你的同事在更新代码后，不得不花时间查看你的 CL 历史并回退代码以确保本地编译没有问题（如果是你之后的 CL 提交出了问题，可能会花费更多时间）。

## 无法将其变小 {#cant}

Sometimes you will encounter situations where it seems like your CL *has* to be
large. This is very rarely true. Authors who practice writing small CLs can
almost always find a way to decompose functionality into a series of small
changes.
在某些情形下，好像你没法然 CL 变得更小，这种情况很少发生。如果开发者经常写小 CL，那么他往往都能找到一种把 CL 拆得更小的方法。

Before writing a large CL, consider whether preceding it with a refactoring-only
CL could pave the way for a cleaner implementation. Talk to your teammates and
see if anybody has thoughts on how to implement the functionality in small CLs
instead.
如果在写代码之前就估计这个 CL 比较大，此时应该考虑是否先提交一个代码重构的 CL，让已有的代码实现更清晰。或者，与团队其他成员讨论下，看是否有人能帮你指出，怎样在提交小 CL 的前提下实现当前功能。

If all of these options fail (which should be extremely rare) then get consent
from your reviewers in advance to review a large CL, so they are warned about
what is coming. In this situation, expect to be going through the review process
for a long time, be vigilant about not introducing bugs, and be extra diligent
about writing tests.
如果以上所有方法都试过，还是不可行（当然，这种情况比较罕见），那就先与所有的审核者沟通一下，告知他们你将会提交一个大 CL，让他们先有心理准备。出现这种情况时，审核过程往往会比较长，同事需要写大量的测试用例。需要警惕，不要引入新的 bug。

Next: [How to Handle Reviewer Comments](handling-comments.md)
下一章: [如何处理审核评论](handling-comments.md)
