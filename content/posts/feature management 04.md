---
id: Learn - The third pillar
title: Learn - The third pillar
date: 2024-10-20
tags: feature toggle
category: Tech

published: 2024-10-20

---

## What is Learn?

The Learn pillar of feature management focuses on enabling all teams to better understand how software changes affect users and systems. It is designed for the entire product delivery team: [developers](https://launchdarkly.com/solutions/development-teams/), [DevOps and site reliability engineers (SREs)](https://launchdarkly.com/solutions/devops-site-reliability-engineer-teams/), and product managers (PMs).

Of all the pillars, Learn is especially concerned with helping software orgs become more data-driven. As a part of this, it provides mechanisms for engaging in hypothesis-driven development, an approach that embeds the scientific method and experimentation into the process of building software. In this way, Learn also supports the “relentless pursuit of continuous improvement,” a key principle of [Continuous Delivery](https://continuousdelivery.com/principles/).

Learn springs naturally from the [Build pillar of feature management](https://launchdarkly.com/blog/build-the-first-pillar-of-feature-management/). In Build, you attach feature flags to every change to control the deployment and release processes. In Learn, you assign metrics to those flags and give the right people control over toggling them. The idea is—_you’re already using feature management for releases; why not collect some data and improve your product along the way?_.

Learn, or experimentation in a feature management context, can also be thought of as “holistic experimentation.”

## What is the goal of Learn?

The goal of Learn is to enable the entire product delivery team, including developers and DevOps engineers, to continuously improve their software in terms of both operational performance and user engagement. Learn accomplishes this by making it easier for teams to collect, analyze, and act upon qualitative and quantitative data.

#### Holistic experimentation vs. traditional experimentation

Holistic experimentation delivers maximum value to customers while maintaining peak system performance and unifying engineers and non-engineers. This strain of experimentation, which embodies the Learn pillar, is defined in contrast to traditional notions of experimentation.

### Traditional: One-track learning

By and large, traditional experimentation connotes running A/B tests on front-end features: design elements, site navigation, content recommendations, etc. To be sure, A/B tests yield insights that often lead to richer user experiences (and more profit). But when it comes to delivering value to all customers, front-end features are only half of the story.

For example, imagine you’ve released a winning feature variation after running a series of A/B tests on it. And let’s assume customers are thrilled with the idea of this feature. But then you make a vexing discovery. When hurled into production, the feature seriously impairs your application response times.

In this case, can you claim to have delivered value to your customers? No, not really. This is just one example highlighting the limits of thinking of experimentation solely in terms of front-end A/B tests.

### Holistic: Full-stack learning

Holistic experimentation defines value according to both front-end and back-end performance. It entails running not only A/B tests on public-facing features but also multivariate tests for back-end changes.

In this context, product managers can easily run experiments tied to the user interface (UI) and user experience (UX). Meanwhile, their friends in Engineering can measure the impact of those front-end features on system performance and reliability. What’s more, engineers can also run their own experiments on infrastructural changes.

Another component of Learn (i.e., holistic experimentation) is that teams collect both quantitative and qualitative data. And the gathering of such data is not restricted to a single event before a release. On the contrary, it can be done gradually as a part of a [“release progression”](https://launchdarkly.com/blog/what-is-progressive-delivery-all-about/): ring deployment, percentage rollout, targeted release, etc. As such, you have more opportunities to iterate and improve upon a feature before moving it to general availability (GA).

### Traditional: Experimentation in a silo

Another drawback of traditional experimentation is it can conflict with an organization’s normal software development workflows. The tools and processes that business stakeholders use to run experiments are often distinct from—and, at times, incompatible with—those used by developers to take action on an experiment. This disconnect poses quite a dilemma. For one thing, after a winning feature has been determined, engineers must then rebuild it in real code.

Product Management and Marketing rely on engineers to deploy the triumphant features of an experiment. Thus, it would seem beneficial to unite the workflows of these teams. But instead, in a traditional setting, you get friction, inefficiency, and poor customer outcomes.

### Holistic: Experimentation as a part of the deployment process

Holistic experimentation integrates with your organization’s software development and delivery workflows. Experiments and beta tests align with the deployment process for the features you’re testing. In this way, holistic experimentation supports the objectives of everyone on the product delivery team: developers, DevOps engineers, SREs, software architects, product marketing managers (PMMs), product managers, and so on. This is in stark contrast to traditional notions of experimentation, which tend to treat developers as an afterthought.

Such cohesion among the product delivery team yields a host of benefits. For starters, virtually anyone can run tests without needing much developer intervention. Also, the overhead of experimenting and deploying in a holistic setting is much lower than the alternative.

Unlike traditional experimentation, holistic experimentation (powered by feature management) aligns with your organization's normal software development and delivery workflows.

The path to reaping these benefits is much clearer when you consider holistic experimentation in the context of the [LaunchDarkly Feature Management Platform](https://launchdarkly.com/product/).

#### LaunchDarkly feature management enables holistic experimentation

LaunchDarkly allows teams to manage releases and run experiments in one place. When developers wrap software changes in feature flags, those changes can then be easily experimented upon using [LaunchDarkly’s Experimentation Add-on](https://launchdarkly.com/features/experimentation/). And when the experiment is done, anyone can roll out the winning feature variant in real-time from within LaunchDarkly. PMs, for example, can initiate the rollout without placing an additional burden on developers.

Those on the engineering, data science, and growth teams can use feature flags to both manage releases and apply metrics to what they ship, thereby measuring the output of their work.

LaunchDarkly allows teams to manage releases and run experiments in one place. 

We should reiterate that LaunchDarkly supports experimentation in a real-world production environment. By testing features in production, you increase the odds of them working properly when unveiled to the full user base.

Ultimately, holistic experimentation, particularly with LaunchDarkly, is more efficient, affordable, and empowering. Let’s consider the following areas of the Learn pillar, in which teams put holistic experimentation into practice.

1. Beta groups (qualitative data)
2. Experimentation – A/B/n tests (quantitative data)
3. Baseline metrics
4. Performance tests

#### Beta testing (qualitative data)

Beta testing with feature management is far less painful than without. In a feature management setting, developers build the new incomplete feature—while attaching a feature flag to it, of course—and then empower product managers to release it to select beta users. In addition to controlling the beta test itself, PMs can also control who to include in the beta group. With PMs thus empowered, developers can spend less time administering beta tests and more time building high-value functionality. And both parties can manage all of this in the LaunchDarkly dashboard.

Owing to the ease of running beta tests with LaunchDarkly, teams end up conducting more tests than they would otherwise. Consequently, they gather more customer feedback earlier in the development process. Product updates are more thoroughly vetted by customers as a result. In heeding customer feedback, developers avoid wasting months building things that flop when brought to market. Instead, they devote their time to creating features and services that customers love.

Atlassian has used LaunchDarkly to perform beta tests in the manner we’ve described. As a result, the company saw net promoter scores (NPS), a key indicator of customer satisfaction, go up within the first year. Read the full case study: [https://launchdarkly.com/case-studies/atlassian](https://launchdarkly.com/case-studies/atlassian/)

After running beta tests in LaunchDarkly, Atlassian saw net promoter scores (NPS) go up within the first year.

[Animoto](https://launchdarkly.com/case-studies/animoto/), [Reciprocity](https://launchdarkly.com/case-studies/reciprocity/), and other customers also empower PMs with the ability to run their own beta tests with LaunchDarkly and have seen similar results. We, too, at LaunchDarkly run our early access program (EAP) in this exact way.

All in all, beta testing in Learn enables teams to continuously improve their product, so as to maximize user engagement and satisfaction.

#### Experimentation – A/B/n tests (quantitative data)

In Learn, both engineers and business stakeholders can seamlessly create and run experiments, including multivariate ones. Beyond running binary A/B tests, teams can use multivariate feature flags to test several variations of a feature at once. And as soon as the winning feature has been identified, it can be rolled out to the intended users and systems. Lastly, in Learn, teams can collect and analyze data generated from experiments within [LaunchDarkly’s Experimentation Add-on](https://launchdarkly.com/features/experimentation/). Or they can use LaunchDarkly’s [Data Export Add-on](https://launchdarkly.com/features/data-export/) to move raw experimentation data to their analytics stack.

Up to this point, we’ve made much ado about how holistic experimentation measures the impact of both front-end and back-end changes. Let’s examine this in practice.

#### Use case: Search algorithm

Many organizations, particularly in e-commerce, have search algorithms on their app or website that display products, services, and information based on a user’s search query. These models often fail to grasp the intent behind user searches and, as a consequence, miss the mark in the results they generate. Given this, an online retailer might want to build a new algorithm that more reliably captures users’ search intentions. But before rolling it out, they’ll want to experiment with it.

In this case, product managers can run beta tests and experiments to assess the performance of the new algorithm. For instance, they might measure the number of conversions across each model, the old and the new. At the same time, DevOps engineers can measure the effects of the algorithm on system performance: response times, error rates, latency, etc.

In the process, they may discover that, while the beta version of the algorithm is driving conversions, it is also putting undue strain on their infrastructure. After uncovering such insights, the team can tweak the algorithm and shore up infrastructural gaps. When the algorithm is eventually released, it will be optimized for its intended purpose—generating better search results—as well as system stability.

##### Baseline metrics

Baseline metrics are a function of holistic experimentation. They refer to the act of assigning test metrics to a software change (feature, bug fix, architectural change, etc.) and then tracking those metrics against a baseline. Again, you can conduct these experiments as you’re rolling the change out to either users or systems. As mentioned earlier, using LaunchDarkly feature flags and experimentation in tandem allows you to seamlessly perform these hypothesis-driven rollouts.

Infrastructure costs are a common baseline metric upon which DevOps/SRE teams can experiment. Generally, these teams have a good sense of what they normally pay their cloud providers (Amazon Web Services (AWS), Microsoft Azure, IBM Cloud, Google Cloud Platform, etc.). And when it comes time to release new functionality or modify their architecture, the operations team can measure how those changes affect their infrastructure costs compared to the baseline. This can lead to significant cost-savings over time.

##### Performance tests

As alluded to throughout, back-end performance tests are an essential part of holistic experimentation. With feature management, development and operations teams can test hypotheses tied to key service metrics such as response times, error rates, and infrastructure costs. Moreover, they can measure the impact of new functionality on those metrics.

#### Use case: Website toolbar

For example, software engineers may devise a hypothesis around the effect of a new website toolbar on page load times. Let’s imagine multiple toolbar variations with slight architectural differences. In this scenario, engineers can run an experiment as a part of a canary launch, wherein the toolbars are rolled out to a select group of real users. The engineers can thus gauge how the toolbars affect load times across different browsers, network types, and other environmental conditions, all in production.

Once the experiment has run its course, and the ideal toolbar has been identified, engineers can then hand the reins over to product managers. And the latter can finish the rollout at a pace that works best for the business.

#### Financial services company runs experiments on back-end infrastructure

In another example, [Stash](https://launchdarkly.com/case-studies/stash/), a New York-based financial services company, uses LaunchDarkly to run advanced experiments on back-end infrastructure. Before, the company lacked a way to run such tests. But now, engineers can measure things like the operational impact of their content personalization services. Further, they use LaunchDarkly’s Data Export Add-on to pump experimentation data to their internal analytics platform, where they aggregate all their testing data. This has given Stash a more comprehensive, granular view into customer engagement. As a result, the company has become more data-driven and elevated the quality of its product.

![](https://images.prismic.io/launchdarkly/4ef8b46d-7e96-4bee-be0b-1bb49899e70f_stash.svg?auto=compress,format)

"LaunchDarkly has played a big part in helping us build a culture at Stash, where we experiment with everything. Not only that, it has enabled us to release new features way faster than before. The fact that we can manage software releases and support experimentation in the same platform is remarkable."

Kahne Raja

Engineering Manager

The ability to run back-end experiments with feature management adds a powerful layer to your broader analytics efforts.

##### Summary: The benefits of Learn

Feature management brings harmony to experimentation and software delivery—and to the teams involved in each pursuit. It allows developers, DevOps engineers/SREs, and product managers to collect and analyze greater quantities of data on user behavior and system performance. This enables them to make data-driven enhancements to new features at each stage of a rollout. The Learn pillar thus fuels a virtuous cycle of continuous improvement among product delivery teams.

Those who employ holistic experimentation deliver higher-quality software that performs exceedingly well across key metrics. They see better system reliability, operational efficiency, and user engagement. Moreover, they spot bad ideas early, scrapping them before they waste too much time, money, and resources. And they invest in the good ideas, reaping the benefits that follow.

Practitioners of the Learn pillar of feature management, who treat experimentation holistically, provide value to customers in increasing measure. And they enjoy greater team unity.


## 什么是学习（Learn）？

学习支柱是特性管理的核心，它专注于使所有团队更好地理解软件变更如何影响用户和系统。它旨在服务于整个产品交付团队，包括[开发人员](https://launchdarkly.com/solutions/development-teams/)、[DevOps和网站可靠性工程师（SRE](https://xn--devops(sre-915q12d471d9nav6x865i73cl22asp8h/)）以及产品经理（PM）。

在所有支柱中，学习特别关注帮助软件组织变得更加数据驱动。作为其中的一部分，它提供了进行假设驱动开发（hypothesis-driven development）的机制，这种方法将科学方法和实验嵌入到构建软件的过程中。通过这种方式，学习也支持了[持续交付](https://continuousdelivery.com/principles/)的一个关键原则——“持续改进的无情追求”。

学习自然而然地源于[特性管理的构建支柱](https://launchdarkly.com/blog/build-the-first-pillar-of-feature-management/)。在构建中，你将特性标志附加到每个更改上，以控制部署和发布过程。在学习中，你为这些标志分配指标，并将控制权交给合适的人来切换它们。理念是——你已经在使用特性管理进行发布了；为什么不在过程中收集一些数据并改进你的产品呢？

学习，或者在特性管理背景下的实验，也可以被认为是“全面实验”。

## 学习的目标是什么？

学习的目标是使整个产品交付团队，包括开发人员和DevOps工程师，能够持续改进他们的软件，无论是在运营性能还是用户参与度方面。学习通过使团队更容易收集、分析和对定性和定量数据采取行动来实现这一点。

#### 全面实验与传统实验

全面实验在保持系统性能峰值的同时，为客户提供最大价值，并统一工程师和非工程师。这种实验，体现了学习支柱，与传统的实验观念形成对比。

### 传统：单轨学习

大体上，传统实验意味着对前端特性进行A/B测试：设计元素、网站导航、内容推荐等。可以肯定的是，A/B测试提供了洞察，这些洞察通常会导致更丰富的用户体验（和更多利润）。但当涉及到为所有客户交付价值时，前端特性只是故事的一半。

例如，想象你在对它进行了一系列A/B测试后发布了一个成功的功能变体。我们假设客户对这一功能的想法感到兴奋。但然后你发现了一个令人困扰的问题。当投入到生产中时，该功能严重损害了你的应用程序响应时间。

在这种情况下，你能声称为客户交付了价值吗？不，实际上没有。这只是其中一个例子，突出了将实验仅以前端A/B测试为思考范围的局限性。

### 全面：全栈学习

全面实验根据前端和后端性能定义价值。它不仅涉及对面向公众的特性进行A/B测试，还涉及对后端更改进行多变量测试。

在这种情况下，产品经理可以轻松地运行与用户界面（UI）和用户体验（UX）相关的实验。与此同时，他们在工程领域的朋友们可以衡量这些前端特性对系统性能和可靠性的影响。更重要的是，工程师也可以对基础设施变更进行自己的实验。

学习（即全面实验）的另一个组成部分是，团队收集定量和定性数据。而且，这种数据的收集并不局限于发布前的单一事件。相反，它可以作为[“发布进度”](https://launchdarkly.com/blog/what-is-progressive-delivery-all-about/)的一部分逐步进行：环部署、百分比发布、针对性发布等。因此，你在将功能移动到普遍可用性（GA）之前有更多的机会进行迭代和改进。

### 传统：孤立的实验

传统实验的另一个缺点是，它可能与组织的正常软件开发工作流程发生冲突。业务利益相关者用于运行实验的工具和流程通常与开发人员用于采取实验行动的工具不同——有时甚至不兼容。这种脱节造成了相当大的困境。首先，确定获胜功能后，工程师必须在真实代码中重建它。

产品管理和市场营销依赖于工程师部署实验的成功功能。因此，将这些团队的工作流程统一起来似乎是有益的。但在传统环境中，你却得到了摩擦、低效率和糟糕的客户结果。

### 全面：作为部署过程一部分的实验

全面实验与你的组织的软件开发和交付工作流程集成。实验和beta测试与你所测试的功能的部署过程一致。通过这种方式，全面实验支持产品交付团队的每个人的目标：开发人员、DevOps工程师、SRE、软件架构师、产品营销经理（PMM）、产品经理等。这与将开发人员视为事后考虑的传统实验观念形成了鲜明对比。

产品交付团队之间的这种凝聚力带来了许多好处。首先，几乎任何人都可以运行测试，而不需要太多的开发人员干预。此外，在全面环境中进行实验和部署的开销远低于另一种选择。

与需要大量开发人员干预的传统实验不同，全面实验（由特性管理提供支持）与你的组织的正常软件开发和交付工作流程一致。

当你在[LaunchDarkly特性管理平台](https://launchdarkly.com/product/)的背景下考虑全面实验时，收获这些好处的道路变得更加清晰。

#### LaunchDarkly特性管理使全面实验成为可能

LaunchDarkly允许团队在一个地方管理发布和运行实验。当开发人员将软件更改包装在特性标志中时，然后可以使用[LaunchDarkly的实验附加组件](https://launchdarkly.com/features/experimentation/)轻松地对这些更改进行实验。当实验完成后，任何人都可以从LaunchDarkly内部实时推出获胜的功能变体。例如，产品经理可以在不增加开发人员负担的情况下启动发布。

工程、数据科学和增长团队可以使用特性标志来管理发布，并对它们发布的内容应用指标，从而衡量他们工作的结果。

LaunchDarkly允许团队在一个地方管理发布和运行实验。

我们应该再次强调，LaunchDarkly支持在现实生产环境中进行实验。通过在生产中测试功能，你增加了它们在向完整用户基础展示时正常工作的可能性。

最终，全面实验，特别是与LaunchDarkly一起，更有效、更实惠、更有力量。让我们考虑以下学习支柱的领域，在这些领域中，团队将全面实验付诸实践。

1. Beta组（定性数据）
2. 实验——A/B/n测试（定量数据）
3. 基线指标
4. 性能测试

#### Beta测试（定性数据）

使用特性管理进行Beta测试比没有特性管理要少痛苦得多。在特性管理设置中，开发人员构建新的不完整的功能——当然要附加特性标志——然后授权产品经理将其发布给选定的Beta用户。除了控制Beta测试本身，产品经理还可以控制谁被包括在Beta组中。有了这样的授权，开发人员可以花更少的时间管理Beta测试，更多时间构建高价值功能。双方都可以像这样在LaunchDarkly仪表板中管理所有这些。

由于使用LaunchDarkly运行Beta测试的便捷性，团队最终会进行比他们否则会进行的更多的测试。因此，他们在开发过程的早期收集了更多的客户反馈。产品更新因此得到了客户的更彻底的审查。在听取客户反馈时，开发人员避免了浪费数月时间构建在市场推出时失败的功能。相反，他们将时间投入到创建客户喜爱的功能和服务上。

Atlassian已经使用LaunchDarkly以我们描述的方式进行Beta测试。结果，公司在第一年内就看到了净推荐值（NPS）——客户满意度的关键指标——上升。阅读完整的案例研究：[https://launchdarkly.com/case-studies/atlassian](https://launchdarkly.com/case-studies/atlassian/)

Animoto、Reciprocity和其他客户也通过使用LaunchDarkly让产品经理有能力运行自己的Beta测试，并看到了类似的结果。我们，在LaunchDarkly也以完全相同的方式运行我们的早期访问计划（EAP）。

总的来说，学习中的Beta测试使团队能够持续改进他们的产品，以最大化用户参与度和满意度。

#### 实验——A/B/n测试（定量数据）

在学习中，工程师和业务利益相关者可以无缝地创建和运行实验，包括多变量实验。除了运行二元A/B测试外，团队可以使用多变量特性标志同时测试一个功能的几种变体。一旦确定了获胜的功能，就可以将其发布给预期的用户和系统。最后，在学习中，团队可以在[LaunchDarkly的实验附加组件](https://launchdarkly.com/features/experimentation/)中收集和分析实验生成的数据。或者，他们可以使用LaunchDarkly的[数据导出附加组件](https://launchdarkly.com/features/data-export/)将原始实验数据移动到他们的分析堆栈中。

到目前为止，我们已经讨论了很多全面实验如何衡量前端和后端更改的影响。让我们在实践中检查这一点。

#### 使用案例：搜索算法

许多组织，特别是在电子商务领域，他们的应用程序或网站上都有搜索算法，这些算法根据用户的搜索查询显示产品、服务和信息。这些模型经常无法把握用户搜索背后的意图，因此，在它们生成的结果中错过了标记。鉴于此，在线零售商可能想要构建一个更可靠地捕获用户搜索意图的新算法。但在推出之前，他们想要对其进行实验。

在这种情况下，产品经理可以运行Beta测试和实验来评估新算法的性能。例如，他们可能会测量每个模型的转化次数，旧的和新的。同时，DevOps工程师可以衡量算法对系统性能的影响：响应时间、错误率、延迟等。

在这个过程中，他们可能会发现，虽然算法的Beta版本推动了转化，但它也对基础设施造成了不必要的压力。在发现这些洞见后，团队可以调整算法并弥补基础设施的不足。当算法最终发布时，它将针对其预期目的——生成更好的搜索结果——以及系统稳定性进行优化。

##### 基线指标

基线指标是全面实验的一个功能。它们指的是将测试指标分配给软件更改（功能、错误修复、架构更改等），然后与基线对比跟踪这些指标。再次强调，你可以在向用户或系统推出更改时进行这些实验。如前所述，结合使用LaunchDarkly特性标志和实验可以让您无缝地执行这些假设驱动的推出。

基础设施成本是DevOps/SRE团队可以实验的常见基线指标。通常，这些团队对他们通常支付给云提供商（Amazon Web Services（AWS）、Microsoft Azure、IBM Cloud、Google Cloud Platform等）的费用有很好的了解。当发布新功能或修改架构时，运维团队可以衡量这些更改与基线相比如何影响他们的基础设施成本。这可以随着时间的推移带来显著的成本节省。

##### 性能测试

如前所述，后端性能测试是全面实验的重要组成部分。通过特性管理，开发和运维团队可以测试与关键服务指标相关的假设，如响应时间、错误率和基础设施成本。此外，他们可以衡量新功能对这些指标的影响。

#### 使用案例：网站工具栏

例如，软件工程师可能会围绕新网站工具栏对页面加载时间的影响提出假设。让我们想象有多个工具栏变体，它们之间有轻微的架构差异。在这种情况下，工程师可以作为金丝雀发布的部分运行实验，其中工具栏被推广到一群精选的真实用户。工程师因此可以衡量工具栏在生产环境中对不同浏览器、网络类型和其他环境条件下的加载时间的影响。

一旦实验完成，并且确定了理想的工具栏，工程师就可以将控制权交给产品经理。然后，后者可以以最适合业务的速度完成发布。

#### 金融服务公司在后端基础设施上运行实验

在另一个例子中，[Stash](https://launchdarkly.com/case-studies/stash/)，一家总部位于纽约的金融服务公司，使用LaunchDarkly在后端基础设施上运行高级实验。以前，公司缺乏运行此类测试的方法。但现在，工程师可以衡量像他们的内容个性化服务这样的操作影响。此外，他们使用LaunchDarkly的数据导出附加组件将实验数据传输到他们的内部分析平台，在那里他们汇总了所有的测试数据。这给了Stash一个更全面、更细粒度的视图来了解客户参与度。结果，公司变得更加数据驱动，并提高了其产品的质量。

[https://images.prismic.io/launchdarkly/4ef8b46d-7e96-4bee-be0b-1bb49899e70f_stash.svg?auto=compress,format](https://images.prismic.io/launchdarkly/4ef8b46d-7e96-4bee-be0b-1bb49899e70f_stash.svg?auto=compress,format)

"LaunchDarkly在帮助我们在Stash建立一种文化方面发挥了重要作用，我们尝试一切。不仅如此，它还使我们能够比以前更快地发布新功能。我们可以在同一个平台上管理软件发布并支持实验，这是非常了不起的。"

Kahne Raja

工程经理

使用特性管理运行后端实验的能力为您更广泛的分析工作增加了一个强大的层次。

##### 总结：学习的好处

特性管理为实验和软件开发交付——以及参与每项追求的团队——带来了和谐。它允许开发人员、DevOps工程师/SRE和产品经理收集和分析更多关于用户行为和系统性能的数据。这使他们能够在推出新功能的每个阶段进行数据驱动的增强。因此，学习支柱推动了产品交付团队持续改进的良性循环。

那些采用全面实验的人提供了在关键指标上表现出色的更高质量的软件。他们看到了更好的系统可靠性、运营效率和用户参与度。此外，他们早早地发现了糟糕的想法，在它们浪费太多时间、金钱和资源之前放弃它们。他们投资于好的想法，收获随之而来的好处。

学习支柱的特性管理实践者，将实验视为一个整体，为客户不断提供价值。他们享受着更大的团队团结。