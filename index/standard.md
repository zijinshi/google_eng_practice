# 代码审核的标准

## 标准 <a id="standard"></a>

代码审核的目的是为了保证代码库中的代码质量持续改进，代码审核的工具和流程都是为了实现这个目的而设计。

为了达到目标，我们需要权衡得失。

首先，开发人员必须能在任务上 _取得进展_ 。如果从没向代码库提交代码，那么代码库就不会改善。同时，如果审核者让开发者在提交代码时变得很困难，那么开发者不得不花费大量的精力解决审核评论，没有动力在未来的提交中改进代码质量。

另一方面，审核者有责任确保提交者的代码质量。随着时间的推移，代码库的质量不会降低。这有点棘手，冰冻三尺非一日之寒，代码库质量的降低是随着每次代码提交的微小降低累积而成的，尤其当团队面临很大的时间压力时，为了完成任务，他们不得不采取一些临时方案。

另外，代码审核者对他们审核的代码有所有权和责任，他们有义务确保代码库是一致的、可维护的，所有这些内容可参见[代码审核过程中要看些什么？ （What to Look For In a Code Review）](looking-for.md)这篇文章。

因此，我们希望在代码审核中能遵循这条原则：

**一般情况下，如果代码提交者的代码能显著提高代码库的质量，那么审核者就应该批准它，尽管它并不完美。**

这是代码审核中所有规则的 _最高原则_。

当然，也有例外。例如，一次提交包含了系统中不应加入的功能，那么审核者就不应批准它，即使它设计得非常完美。

还有一个关键点，那就是世上根本就没有“完美”的代码——只有 _更好_ 的代码。审核者不应该要求代码提交者在每个细节都写得很完美。审核者应该做好修改时间与修改重要性之间的平衡。无需追求完美，而应寻求 _持续的改进_ 。 倘若一个 CL 能够改进系统的可维护性、可读性，那么它不应该仅仅因为不够完美而延迟数天（甚至数周）才批准提交。

我们应该营造这种氛围：当审核者发现某些事情有更好的方案时，他可以无拘束地提出来。如果这个更好的方案并不是非改不可，可以在注释前加上：“Nit:”，让提交者明白，这段评论只是锦上添花，你可以选择忽略。

注意：在提交代码时不应显著地 _恶化_ 代码质量，唯一的例外是 [紧急情况](../emergencies.md)。

## 指导 <a id="mentoring"></a>

代码审核还有一项重要的功能：能让开发者学到新知识，可能是编程语言方面的，也可能是框架方面的，或一些常规的软件设计原则。作为审核者，如果你认为某些评论有助于开发者学到新知识，那就毫不犹豫地写下来吧。分享知识是提高代码质量的一种方式。记住，如果你的评论是纯学习相关的，与文档中提及的标准关系不大，那就最好在前面加上“Nit”，否则就意味着开发者必须在 CL 中修正这个问题。

## 原则 <a id="principles"></a>

* 以技术因素与数据为准，而非个人喜好。
* 在代码样式上，遵从[代码样式指南](http://google.github.io/styleguide/)的权威。任何与样式指南不一致的观点（如空格）都是个人偏好。所有代码都应与其保持一致。如果某项代码样式在文档中并未提及，那就接受作者的样式。
* **任何涉及软件设计的问题，都不应由个人喜好来决定。** 它应取决于基本设计原则，以这些原则为基础进行权衡，而不是简单的个人看法。当有多种可行方案时，如果作者能证明（以数据或公认的软件工程原理为依据）这些方案基本差不多，那就接受作者的选项；否则，应由标准的软件设计原则为准。
* 如果没有可用的规则，那么审核者应该让作者与当前代码库保持一致，至少不会恶化代码系统的质量。

## 冲突解决 <a id="conflicts"></a>

在代码审核中碰到冲突时，首先要做的永远是先尝试让双方（开发者和审核者）在两份文档（[开发者指南](./) 和 [审核者指南](../developer/)）的基础上达成共识。

当很难达成共识时，审核者与开发者最好开一个面对面的会议（或视频会议），而不要继续通过代码审核评论进行解决。（在开会讨论之后，一定要在评论中记录讨论的结果，以便让以后阅读的人知道前因后果。）

如果仍旧无法解决问题，最好的方式是升级。常见的升级方式比较多，如让更多的人（如团队的其他人）参与讨论，把团队领导卷进来，征询代码维护人员的意见，让工程经理来决定。 **千万不要因为开发者与审核者无法达成一致而让CL停留在阻塞状态。**

下一章：[在代码审核过程中要看些什么？](looking-for.md)
