---
id: The definitive guide to feature management.
title: The definitive guide to feature management.
tags:
  - feature toggle
category: Tech
date: "2024-10-20"
published: 2024-10-20

---

#### What is feature management?

Feature management is a new class of software development tools and techniques powered by feature flags. A **feature flag** is a lever of control within your code (an _if-else_ statement) that decouples code deployments from feature releases. Developers have used some variation of feature flags for years. But when it comes to enjoying the full benefits of feature flags, many have only scratched the surface.

At most organizations, the art of feature flagging is confined to just a few teams across a few use cases. Such limits stem, in part, from the fact that managing feature flags at scale is quite challenging. For one thing, technical debt can rapidly accrue if you start using flags in large volumes. As a result, only a handful of developers end up using them, thus limiting the value an organization can capture from those flags (see what we did there?). Another drawback of conventional flags is they only support basic true-false, or Boolean, use cases. This, too, prevents organizations from realizing the full benefits of feature flags.

A [feature management platform](https://launchdarkly.com/product/) like LaunchDarkly fills the gaps of conventional feature toggles. It provides a simple user interface, robust infrastructure, and a suite of functionality that enable you to use feature flags on a large scale. What’s more, LaunchDarkly supports a wide range of complex use cases—multivariate feature flags, user segmentation, feature delegation, A/B testing and experimentation, etc.—all in one platform. You get all the benefits of feature flags without the risk and overhead of maintaining your own homegrown feature flag management system. 

In the following pages, we will explain what feature management is, who it's for, and why you should care. 

Let’s begin by unpacking the relationship between feature management and Progressive Delivery, a new and important software development lifecycle.

#### Feature management and Progressive Delivery

[Progressive Delivery](https://launchdarkly.com/blog/what-is-progressive-delivery-all-about/) is a new software development methodology that builds upon the core tenets of Continuous Delivery. You can think of it as the next iteration of CI/CD but with more emphasis on risk reduction, business outcomes, and control. Feature management is a key enabler of Progressive Delivery. The two are entwined. For this reason, the goals of feature management and Progressive Delivery look nearly identical.

As with its predecessor CI/CD, we expect Progressive Delivery to shape how software is built and delivered; and to decide who wins and loses in modern software development. 

Feature management, and its four pillars, are essential to Progressive Delivery. To learn more about the origins of Progressive Delivery, [click here](https://launchdarkly.com/blog/all-the-canaries-lived-its-time-to-adopt-progressive-delivery/). For a more in-depth understanding of the methodology, get our free [Progressive Delivery eBook.](https://learn.launchdarkly.com/progressive-delivery/)

On a related note, feature management has been shown to drive performance improvements across the Four Key Metrics of software development and delivery laid out in the annual _State of DevOps_ _Report_. 

#### Feature management and the Four Key DORA Metrics

Feature management enables teams to improve their performance across the Four Key Metrics of software development and delivery set by the esteemed DevOps Research and Assessment Group (DORA):

1. **Deployment and release frequency:** IBM went from deploying to production twice a week to 100+ times a day with LaunchDarkly. Read the full [IBM case study](https://launchdarkly.com/case-studies/ibm/).  
    
2. **Lead time for changes:** A 2020 survey shows that, after using LaunchDarkly, customers saw a 76% decrease in their lead time for changes. See the full survey results at [“The ROI of Feature Management.”](https://launchdarkly.com/roi-feature-management/)  
    
3. **[Mean time to restore service (MTTR):](https://launchdarkly.com/blog/mean-time-to-restore-mttr/)** Atlassian, maker of popular software products such as Trello, Confluence, and Jira, reduced its MTTR hours by 97% with LaunchDarkly. Read the full [Atlassian case study](https://launchdarkly.com/case-studies/atlassian/).  
    
4. **Change fail rate:** LaunchDarkly enables Honeycomb to maintain a 0.1% change fail rate—a feat that puts Honeycomb among the elite of the elite, according to DORA’s _2019 State of DevOps_ _Report_. Watch [Honeycomb’s testimonial video](https://youtu.be/qin6mszJ6rI).

![null](https://images.prismic.io/launchdarkly/c5083c0d-8f3a-473b-9dcf-1cd6f6b12a3f_Screen+Shot+2020-06-27+at+2.51.26+PM.png?auto=compress,format)

 _Source: “Accelerate: State of DevOps 2019.” DevOps Research & Assessment, p. 18_

![](https://images.prismic.io/launchdarkly/9a5acab5-840e-45c2-8127-806e758de9a6_honeycomb.png?auto=compress,format)

"Less than 0.1% of Honeycomb’s changes catastrophically fail. That is compared to an industry average, where roughly less than 5% is considered good performance, and many companies struggle to achieve anywhere between a 10-30% change fail rate. Only 1 out of 1000 of our deployments fail—in large part because LaunchDarkly allows us to toggle things on and off to make things safe."

Liz Fong-Jones

Principal Developer Advocate

#### Four Pillars of Feature Management: Build, Operate, Learn, Empower

Feature management consists of four pillars: Build, Operate, Learn, and Empower. Many software teams begin their feature management journey in Build. They might use feature flags for [trunk-based development](https://launchdarkly.com/blog/git-branching-strategies-vs-trunk-based-development/) and managing releases. Other teams first use feature flags for back-end operational purposes like disabling non-essential web services during unusual spikes in site traffic. Others might even start down the feature management road in the Learn pillar, [running experiments](https://launchdarkly.com/blog/nine-experimentation-best-practices/) and A/B tests to uncover insights into both user and system behavior. In general, we encourage organizations to start using feature flags in the Build pillar and work their way into the other pillars over time.

But regardless of the pillar you start with, your long-term goal should be to engage in all four pillars of feature management. Leveraging feature flags for use cases across all four pillars equates to practicing feature management at an elite level.

The more advanced your use of feature management, the more benefits you will reap. It's similar to a smartphone. If you were to solely use a smartphone to take photos, browse the internet, and get driving directions, no doubt, you would enjoy vastly more benefits than you would with an old flip phone. Even so, you're really only tapping into a fraction of the smartphone's full capabilities. It's not until you start managing your emails on the go, listening to every song ever made, updating your bank account from an airplane, virtually paying a friend for lunch while you're still eating, etc., that you realize just how powerful the computer in your pocket is.

As with your smartphone, the ROI of feature management grows as you leverage more of its capabilities. 

Feature management is not meant to be a perennial pilot project. It is meant to span multiple teams and use cases, all of which are contained in the four pillars. This is key to maximizing the return on the time, money, and resources you invest in feature management.

In the following pages of this guide, we will unpack each of the four pillars of feature management and explain how you stand to benefit.



#### 什么是特性管理？

特性管理是由特性标志（feature flags）驱动的一类新的软件开发工具和技术。一个**特性标志**是代码中的一个控制杠杆（一个_if-else_语句），它将代码部署与特性发布解耦。开发者多年来一直在使用特性标志的一些变体。但是，当涉及到享受特性标志的全部好处时，许多人只是触及了表面。

在大多数组织中，特性标志的艺术仅限于少数几个团队的几个用例。这种限制部分源于大规模管理特性标志的挑战性。首先，如果你开始大量使用标志，技术债务可能会迅速累积。因此，最终只有少数开发者使用它们，从而限制了组织可以从这些标志中捕获的价值（看我们做了什么？）。传统标志的另一个缺点是它们只支持基本的真-假，或布尔值，用例。这也阻碍了组织实现特性标志的全部好处。

像LaunchDarkly这样的[特性管理平台](https://launchdarkly.com/product/)填补了传统特性切换的空白。它提供了一个简单的用户界面、强大的基础设施和一套功能，使你能够在大规模上使用特性标志。更重要的是，LaunchDarkly支持广泛的复杂用例——多变量特性标志、用户细分、特性委托、A/B测试和实验等——全部集成在一个平台中。你得到了所有特性标志的好处，而没有维护自己的特性标志管理系统的风险和开销。

在接下来的页面中，我们将解释什么是特性管理，它适用于谁，以及为什么你应该关心。

让我们首先探讨特性管理与渐进式交付（Progressive Delivery）之间的关系，这是一种新的和重要的软件开发生命周期。

#### 特性管理与渐进式交付

[渐进式交付](https://launchdarkly.com/blog/what-is-progressive-delivery-all-about/)是一种新的软件开发方法论，它建立在持续交付的核心原则之上。你可以将其视为CI/CD的下一个迭代，但更加强调风险降低、业务成果和控制。特性管理是渐进式交付的关键推动者。两者是交织在一起的。因此，特性管理和渐进式交付的目标几乎相同。

和它的前身CI/CD一样，我们预计渐进式交付将塑造软件的构建和交付方式；并决定现代软件开发中的胜者和败者。

特性管理及其四大支柱对渐进式交付至关重要。要了解更多关于渐进式交付的起源，请[点击这里](https://launchdarkly.com/blog/all-the-canaries-lived-its-time-to-adopt-progressive-delivery/)。要更深入地了解这种方法论，请获取我们的免费[渐进式交付电子书](https://learn.launchdarkly.com/progressive-delivery/)。

顺便说一下，特性管理已经被证明可以在DevOps研究和评估小组（DORA）在年度《DevOps现状》报告中列出的软件开发和交付的四大关键指标上推动性能改进。

#### 特性管理与四大DORA指标

特性管理使团队能够在DevOps研究和评估小组（DORA）设定的软件开发和交付的四大关键指标上提高性能：

1. **部署和发布频率：**IBM使用LaunchDarkly从每周部署到生产两次增加到每天100多次。阅读完整的[IBM案例研究](https://launchdarkly.com/case-studies/ibm/)。
    
2. **变更的前置时间：**2020年的一项调查显示，在使用LaunchDarkly后，客户的变更前置时间减少了76%。查看完整的调查结果在[“特性管理的ROI。”](https://launchdarkly.com/roi-feature-management/)
    
3. **[平均恢复服务时间（MTTR](https://xn--(mttr-k86ht1z1tdltqqve4qsv7c2t6t/)）：**Atlassian，Trello、Confluence和Jira等流行软件产品的制造商，使用LaunchDarkly将其MTTR小时数减少了97%。阅读完整的[Atlassian案例研究](https://launchdarkly.com/case-studies/atlassian/)。
    
4. **变更失败率：**LaunchDarkly使Honeycomb能够保持0.1%的变更失败率——这一壮举使Honeycomb成为DORA的《2019年DevOps现状》报告中的精英中的精英。观看[Honeycomb的证词视频](https://youtu.be/qin6mszJ6rI)。
    

[https://images.prismic.io/launchdarkly/c5083c0d-8f3a-473b-9dcf-1cd6f6b12a3f_Screen+Shot+2020-06-27+at+2.51.26+PM.png?auto=compress,format](https://images.prismic.io/launchdarkly/c5083c0d-8f3a-473b-9dcf-1cd6f6b12a3f_Screen+Shot+2020-06-27+at+2.51.26+PM.png?auto=compress,format)

 _来源：“加速：2019年DevOps现状。”DevOps研究与评估，第18页_

[https://images.prismic.io/launchdarkly/9a5acab5-840e-45c2-8127-806e758de9a6_honeycomb.png?auto=compress,format](https://images.prismic.io/launchdarkly/9a5acab5-840e-45c2-8127-806e758de9a6_honeycomb.png?auto=compress,format)

“Honeycomb的变更中不到0.1%会灾难性失败。相比之下，行业平均水平，大约不到5%被认为是良好的表现，许多公司努力实现在10-30%的变更失败率之间。我们的部署中只有1/1000会失败——这在很大程度上是因为LaunchDarkly允许我们开启和关闭事物以确保安全。”

Liz Fong-Jones

首席开发者倡导者

#### 特性管理的四大支柱：构建、运营、学习、授权

特性管理由四大支柱组成：构建、运营、学习、授权。许多软件团队从构建开始他们的功能管理之旅。他们可能会使用特性标志进行[基于主干的开发](https://launchdarkly.com/blog/git-branching-strategies-vs-trunk-based-development/)和管理发布。其他团队可能首先使用特性标志进行后端运营目的，例如在网站流量异常激增时禁用非必要的网络服务。其他团队甚至可能从学习支柱开始功能管理之路，[进行实验](https://launchdarkly.com/blog/nine-experimentation-best-practices/)和A/B测试，以发现用户和系统行为的洞察。总的来说，我们鼓励组织从构建支柱开始使用特性标志，并随着时间的推移逐步进入其他支柱。

但不管你从哪个支柱开始，你的长期目标应该是参与特性管理的所有四大支柱。利用特性标志进行所有四大支柱的用例等同于在精英级别上实践特性管理。

你对特性管理的使用越先进，你将获得的好处就越多。这就像一部智能手机。如果你只使用智能手机拍照、浏览互联网和获取驾驶方向，毫无疑问，你会比使用旧翻盖手机获得更多的好处。即便如此，你实际上只触及了智能手机全部功能的一小部分。直到你开始在移动中管理你的电子邮件，听每一首歌，从飞机上更新你的银行账户，在你还在吃午餐的时候虚拟支付给朋友午餐费用等，你才意识到你口袋里的计算机有多强大。

就像你的智能手机一样，随着你利用更多特性管理的功能，其ROI也会增加。

特性管理不应该是永久性的试点项目。它应该跨越多个团队和用例，所有这些都包含在四大支柱中。这是最大化你在特性管理上投入的时间、金钱和资源的回报的关键。

在本指南的后续页面中，我们将详细解释特性管理的四大支柱，并解释你将如何受益。

