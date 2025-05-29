---
id: Build - The first pillar

tags:
  - feature toggle
category: Tech
date: "2024-10-20"
published: 2024-10-20
title: Build - The first pillar
---

## What is Build?

The Build pillar addresses the use of feature flags for building and delivering new features, bug fixes, and code changes of any kind. While much of this category deals with release management, we've named it "Build" because of the critical role feature flags also play in pre-release activities. Such activities might include trunk-based development, testing in production, and rollout planning.

Traditional software development is reactive: teams push code and pray things go well. Build offers a proactive approach, wherein developers test features in production and collect user feedback before a release. This implies making feature flags an essential part of your release strategy. 

Build thus spans release management and pre-release activities.  

## What is the goal of Build?

The main goal of Build is to enable teams to ship continuously, enjoy risk-free (and thus stress-free) releases, and deliver amazing digital experiences.

### Deploy != release

The core benefit of feature flags is they allow you to separate code deployments from feature releases. As a result, developers can deploy to production whenever they want, and the business can release when it’s ready.

The simple yet powerful ability to decouple _deploy_ from _release_ unlocks a host of other practices—trunk-based development, testing in production, targeted rollouts, etc.—that speed up development cycles, boost productivity across multiple teams (especially in Engineering), and improve customer satisfaction.

### **Deploy** when you want, **release** when you’re ready.

When the business units (e.g., Product Management) are able to control who sees which features when, it creates a topflight customer experience. Among other things, it lets customers adapt to change at a pace that is ideal for them. 

### Trunk-based development

Rather than wait for PRs to get approved and endure the painful merge conflicts that follow, developers can use feature flags to commit unfinished code to the master branch whenever they want. In this scenario, the code is in a deployable state. If the code were deployed, users would be unable to see the incomplete feature. Nor could they activate the code paths for that feature. 

Enabling developers to keep their code in a deployable state at all times is, of course, a prerequisite for Continuous Integration and Continuous Delivery (CI/CD). Thus, by enabling trunk-based development, feature flags also enable teams to do CI/CD safely. 

### “Safe” CI/CD with feature flags

Feature management, and the feature flags underpinning it, enable safe CI/CD. Feature flags act as a safety net when continuously delivering software. If a feature throws a bug in production, you can disable it instantly without having to redeploy your entire application. What’s more, feature flags let you control who can see new features. You can choose to expose features to a subset of users, all users, or no users. This control empowers teams to continuously ship features—even incomplete ones—without the fear of disaster.

For those who have struggled to adopt Continuous Delivery due to the risks, feature management offers a solution. Feature management allows you to move fast but with control. If you ship code to production, and a failure occurs, you can use a “kill switch” (a topic we’ll cover in Operate) to resolve the incident quickly. And if, in this case, you’ve performed a canary launch, then you will have confined the impact of that failure to a small group.

“Feature management enables safe CI/CD” is another way of saying that feature management enables Progressive Delivery. For Progressive Delivery embodies an approach to CI/CD that is designed for failure and virtually eliminates risk when deploying software. Thus, if you leverage feature management to engage in Progressive Delivery, it’s implied that you are engaging in CI/CD.

### Continuous Delivery without feature flags is the continuous delivery of risk.

Doing CI/CD with feature management is a win-win for software organizations and customers. Software teams remove feature backlogs, validate new features from a technical and user engagement perspective earlier in the process, and end up releasing better features. And customers are shielded from performance issues as they enjoy the higher-quality software that’s been delivered to them.  

To learn more about the interplay of feature management, CI/CD, and Progressive Delivery, read [“What Is Progressive Delivery All About?”](https://launchdarkly.com/blog/what-is-progressive-delivery-all-about/).

#### Testing in production

Try as you might, you can never predict what will happen in a production environment. That is not to say you should, therefore, do away with staging environments—though some feature management adopters certainly have done that. But the fact is, staging environments slow you down. And they still often fail to prevent issues when deploying a feature into a real-world context.  

Thus, at LaunchDarkly, we contend that the safest, fastest way to deliver software is by first testing small changes in production. To do this safely, you need feature flags.

Testing in production frees you from the pain and inefficiency of Waterfall. Instead of waiting several weeks or months to ship simple code changes, you can get them out immediately. 

![](https://images.prismic.io/launchdarkly/d5baecd6-f812-4717-be86-8820fb24d25f_atlassian.svg?auto=compress,format)

"We use LaunchDarkly to control risky changes. Sometimes there’s changes in the product that we can’t test effectively in development or in staging. And the only way we can really effectively test this is when we really get to production."

Aaron Gentleman

Senior Engineering Manager

For many organizations, the first time they test a feature in production is the same day as the marketing launch for the release containing that feature. Feature flags allow engineers to test features in production far in advance of a marketing launch. So when Product or Marketing or whoever decides to release those features to customers, Engineering feels confident that those features won't break anything. Ben Nadel, founder at InVision and an avid LaunchDarkly customer, describes such confidence as ["intoxicating."](https://www.bennadel.com/blog/3766-my-personal-best-practices-for-using-launchdarkly-feature-flags.htm)

![](https://images.prismic.io/launchdarkly/e51df588-1264-4d4c-8055-cbad569242f5_icims.svg?auto=compress,format)

"Our engineers can deploy features as soon as they're done building them. And we [on the release team] can gradually release those features at a pace that matches our enterprise customers' tolerance for change."

Dave Cacciatore

Director of Release Management

In the absence of feature flags, software releases can be nerve-wracking and stressful, even scary. But with feature flags, they are safe and forgettable. A big part of this can be attributed to the ability to test in production. Using feature flags as kill switches also plays a big part in making releases safe and boring. 

![](https://images.prismic.io/launchdarkly/9a5acab5-840e-45c2-8127-806e758de9a6_honeycomb.png?auto=compress,format)

"Everyone tests in production. Some of us do it on purpose."

Charity Majors

Co-Founder and CTO

#### Targeted rollouts

A targeted rollout involves releasing new functionality to a defined cohort of users rather than dumping it on all users at once. Ring deployments, a term coined by Microsoft, are an example of such a rollout. You can also have a targeted rollout in which you only expose features to a specific user group without ever making them available to your entire user base. For instance, you may need to display a specific message in your application that is only relevant to customers in Singapore. As such, using feature management, you reveal the message to Singapore users while concealing it from everyone else. This, too, is a targeted rollout.

Targeted rollouts are examples of “release progressions”, a core tenet of Progressive Delivery. They give you total control over who sees what, when. And feature management makes it easy to create user segments, run targeted rollouts, and clean up the feature flags associated with those rollouts afterward.

#### Canary launches

You've likely heard the grim anecdote about the "canary in the coal mine", so we’ll spare you the details. But essentially, a canary launch entails releasing a new feature to a small group of real users before rolling it out to a broader audience. Canary launches can be done in either a randomized or targeted fashion.

Teams use this technique to see if anything breaks in production and to spot potential hazards. Should a system failure occur at this stage, its blast radius will have been limited to the canary group—a far preferable outcome compared to a failure affecting your entire user base.  

Beyond measuring a feature’s impact on application performance, teams also use canary launches to look for early signs of whether a feature is likely to succeed or fail in terms of user engagement. 

Canary launches are a quintessential example of testing in production. They differ from internal betas (dog fooding), user testing, and QA and performance testing in that they are done on real users in a production environment. All the testing approaches just mentioned happen in a controlled staging environment. Most developers can attest, you simply cannot forecast all the weirdness that will happen in production. 

Ultimately, canary launches dramatically reduce the cost and impact of a system failure. They are the release equivalent of playing the penny slots at a casino—it’s hard to lose ten grand when you’re only gambling with pocket change.

A feature management platform makes it easy to perform canary launches and resolve incidents quickly when bugs arise.

#### Ring deployments 

A ring deployment entails gradually releasing a feature to defined user cohorts (“rings”), with each successive ring representing a higher degree of risk and uncertainty. 

As a simple example, you might first roll out a feature to internal developers. Certain system performance criteria must be met before you can release the feature to the next ring. Assuming such criteria have been met, you might then roll the feature out to a canary group of happy customers eager to try the latest and greatest functionality. If your application remains stable, and you see high user engagement among the canary group, then you might release the feature to a larger group of users segmented by geography (e.g., users in the United States). Perhaps in this case, you feel more confident in your infrastructure for U.S. customers than you do for, say, customers in Europe. Once everything checks out with the U.S. ring, you release the feature to the Europe ring, and so on and so forth, until eventually making the feature generally available to all users.   

At each stage of the ring deployment, you are “limiting the blast radius” of any small system failures that occur. What’s more, you are continuously iterating on the new feature throughout the process. As a result, by the time the feature has been made generally available, it performs significantly better than it would have in a traditional big-bang deployment. You might also think of a ring deployment as a gated deployment.

As a core technique of Progressive Delivery, ring deployments give software teams the control they need to deliver unmatched digital experiences. They vastly reduce the cost and impact of failure. And they give teams the confidence to do CI/CD safely.

As with canary launches, a feature management platform also simplifies the process of performing ring deployments. 

##### Percentage deployments

Like targeted rollouts, percentage-based deployments are gradual. But where in the former case, the user cohorts for each stage of the rollout are well defined, in percentage-based deployments, the cohorts are chosen at random. Such deployments are useful when you cannot run a beta program or when there is little variation among the intended users. 

You may initially release a feature to a random 10% of users, then bump that up to 25%, then 50%, and so on until releasing to all users. Some companies automate this process. If at any stage in the rollout, the number of errors or response times exceed a set threshold, then the release stops. But in cases where all goes smoothly, every customer eventually gets access to new functionality with little involvement from you.

Many also use ring and percentage deployments in tandem. You first deploy to a hand-picked canary group, and once the feature has passed through this first ring, you can roll it out to the rest of your user base in a random percentage format.

##### Summary: The benefits of Build

In Build, teams use feature management to decouple deployments and releases, do trunk-based development, engage in safe CI/CD, and test in production. They also perform targeted rollouts, canary launches, ring deployments, and percentage rollouts.

Teams that engage in these practices vastly improve their software delivery performance. They deploy faster, avoid disasters, and greatly reduce the impact of application failures. What’s more, they control who sees which code changes when, thus creating a masterful user experience.

The net result of all this is happier, more productive software teams, happier customers, and more revenue.


## 什么是构建（Build）？

构建支柱涉及使用特性标志来构建和交付新功能、修复漏洞以及任何类型的代码更改。虽然这个类别的大部分内容涉及发布管理，我们将其命名为“构建”，是因为特性标志在发布前的活动中也扮演着关键角色。这些活动可能包括基于主干的开发、在生产环境中测试和发布计划。

传统的软件开发是被动的：团队推送代码并祈祷一切顺利。构建提供了一种主动的方法，开发者可以在发布前在生产环境中测试功能并收集用户反馈。这意味着将特性标志作为你发布策略的一个重要部分。

因此，构建涵盖了发布管理和发布前的活动中。

## 构建的目标是什么？

构建的主要目标是使团队能够持续交付，享受无风险（因此也无压力）的发布，并提供令人惊叹的数字体验。

### 部署（Deploy）≠发布（Release）

特性标志的核心好处是它们允许你将代码部署与功能发布分开。因此，开发者可以随时部署到生产环境，而业务可以在准备好时发布。

将部署与发布解耦的简单但强大的能力，解锁了一系列其他实践——基于主干的开发、在生产环境中测试、针对性的发布等——这些实践加快了开发周期，提高了多个团队（特别是在工程领域）的生产力，并提高了客户满意度。

### 随时部署（Deploy），准备好时发布（Release）

当业务部门（例如，产品管理）能够控制谁在何时看到哪些功能时，它创造了一流的客户体验。除其他外，它允许客户以对他们来说理想的速度适应变化。

### 基于主干的开发

开发者不必等待PR（Pull Request）被批准并忍受随之而来的痛苦合并冲突，他们可以随时使用特性标志将未完成的代码提交到主分支。在这种情况下，代码处于可部署状态。如果代码被部署，用户将无法看到不完整的功能。他们也无法激活该功能代码路径。

使开发者能够始终保持代码处于可部署状态，当然是持续集成和持续交付（CI/CD）的先决条件。因此，通过实现基于主干的开发，特性标志也使团队能够安全地进行CI/CD。

### 使用特性标志进行“安全”的CI/CD

特性管理和支撑它的特征标志，使CI/CD变得安全。特性标志在持续交付软件时充当安全网。如果一个功能在生产环境中抛出错误，你可以立即禁用它，而不必重新部署整个应用程序。更重要的是，特性标志让你可以控制谁可以看到新功能。你可以选择向一部分用户、所有用户或不向任何用户展示功能。这种控制能力使团队能够持续交付功能——即使是不完整的——而不必担心灾难。

对于那些因风险而努力采用持续交付的团队来说，特性管理提供了解决方案。特性管理允许你快速行动，但有控制。如果你将代码部署到生产环境，并且发生故障，你可以使用“杀伤开关”（我们将在运营中讨论的主题）来快速解决问题。而如果，在这种情况下，你执行了金丝雀发布，那么你就将故障的影响限制在了一个小群体中。

“特性管理使CI/CD变得安全”是另一种说法，即特性管理使渐进式交付成为可能。渐进式交付是一种为失败而设计的CI/CD方法，几乎消除了部署软件时的风险。因此，如果你利用特性管理进行渐进式交付，这意味着你也在进行CI/CD。

### 没有特性标志的持续交付就是持续交付风险。

使用特性管理进行CI/CD对软件组织和客户来说是双赢的。软件团队消除了功能积压，从技术和用户参与的角度更早地验证新功能，并最终发布更好的功能。客户免受性能问题的影响，因为他们享受到了交付给他们的更高质量的软件。

要了解更多关于特性管理、CI/CD和渐进式交付的相互作用，请阅读[“渐进式交付是怎么回事？”](https://launchdarkly.com/blog/what-is-progressive-delivery-all-about/)。

#### 在生产环境中测试

无论你如何尝试，你都无法预测生产环境中会发生什么。这并不是说你因此应该放弃暂存环境——尽管一些特性管理的采用者确实这样做了。但事实是，暂存环境会拖慢你的速度。而且它们仍然经常无法防止在将功能部署到现实环境中时出现的问题。

因此，在LaunchDarkly，我们认为通过首先在生产环境中测试小的更改来交付软件是最安全、最快的方法。要做到这一点，你需要特性标志。

在生产环境中测试使你摆脱了瀑布模型的痛苦和低效。你不必等待几周或几个月来发布简单的代码更改，你可以立即发布它们。

[https://images.prismic.io/launchdarkly/d5baecd6-f812-4717-be86-8820fb24d25f_atlassian.svg?auto=compress,format](https://images.prismic.io/launchdarkly/d5baecd6-f812-4717-be86-8820fb24d25f_atlassian.svg?auto=compress,format)

“我们使用LaunchDarkly来控制风险变化。有时产品中的变化我们无法在开发或暂存环境中有效测试。而我们真正有效地测试这些变化的唯一方式就是当我们真正进入生产环境。”

Aaron Gentleman

高级工程经理

对于许多组织来说，他们在生产环境中测试功能的时间与包含该功能的营销发布日是同一天。特性标志允许工程师在营销发布之前很早就在生产环境中测试功能。因此，当产品或营销或任何人决定将这些功能发布给客户时，工程团队对这些功能不会破坏任何东西感到有信心。InVision的创始人兼热衷于LaunchDarkly的客户Ben Nadel将这种信心描述为[“令人陶醉的。”](https://www.bennadel.com/blog/3766-my-personal-best-practices-for-using-launchdarkly-feature-flags.htm)

[https://images.prismic.io/launchdarkly/e51df588-1264-4d4c-8055-cbad569242f5_icims.svg?auto=compress,format](https://images.prismic.io/launchdarkly/e51df588-1264-4d4c-8055-cbad569242f5_icims.svg?auto=compress,format)

“我们的工程师可以在完成构建后立即部署功能。而我们[在发布团队]可以逐渐以符合我们企业客户对变化的容忍度的速度发布这些功能。”

Dave Cacciatore

发布管理总监

如果没有特性标志，软件发布可能会令人紧张、压力大，甚至可怕。但有了特性标志，它们就是安全和容易忘记的。这在很大程度上可以归因于在生产环境中测试的能力。使用特性标志作为杀伤开关在使发布安全和乏味方面也发挥了重要作用。

[https://images.prismic.io/launchdarkly/9a5acab5-840e-45c2-8127-806e758de9a6_honeycomb.png?auto=compress,format](https://images.prismic.io/launchdarkly/9a5acab5-840e-45c2-8127-806e758de9a6_honeycomb.png?auto=compress,format)

“每个人都在生产环境中测试。我们中的一些人是故意这样做的。”

Charity Majors

联合创始人兼首席技术官

#### 针对性发布

针对性发布涉及将新功能发布给一个定义好的用户群体，而不是一次性地发布给所有用户。微软创造的“环部署”一词就是这种发布的例子。你也可以进行针对性发布，只向特定用户群体展示功能，而从未向整个用户群体提供。例如，你可能需要在应用程序中显示一个只与新加坡客户相关的特定消息。因此，使用特性管理，你向新加坡用户展示该消息，而对其他人则隐藏它。这也是一个针对性发布。

针对性发布是“发布进度”的例子，这是渐进式交付的核心原则。它们让你完全控制谁在何时看到什么。而特性管理使创建用户细分、运行针对性发布以及在这些发布之后清理与之相关的功能标志变得容易。

#### 金丝雀发布

你可能听说过“煤矿中的金丝雀”的可怕轶事，所以我们将省略细节。但基本上，金丝雀发布涉及在向更广泛的受众发布之前，先向一小群真实用户发布一个新功能。金丝雀发布可以以随机或针对性的方式进行。

团队使用这种技术来查看生产环境中是否有任何问题，并发现潜在的危险。如果在这个阶段发生系统故障，其影响范围将被限制在金丝雀群体——这比故障影响你整个用户群体要可取得多。

除了衡量功能对应用程序性能的影响外，团队还使用金丝雀发布来寻找功能在用户参与方面可能成功或失败的早期迹象。

金丝雀发布是生产环境中测试的典型例子。它们与内部测试（狗食）、用户测试以及QA和性能测试的区别在于，它们是在真实用户的真实环境中进行的。上述所有测试方法都发生在受控的暂存环境中。大多数开发人员都可以证明，你根本无法预测生产环境中会发生的所有奇怪事情。

最终，金丝雀发布极大地减少了系统故障的成本和影响。它们是发布等价于在赌场玩一分钱老虎机——当你只拿零钱赌博时，很难输掉十美元。

特性管理平台使执行金丝雀发布和在出现错误时快速解决问题变得容易。

#### 环部署

环部署涉及逐步向定义好的用户群体（“环”）发布功能，每个后续环代表更高程度的风险和不确定性。

作为一个简单的例子，你可能会首先向内部开发人员发布一个功能。在将功能发布到下一个环之前，必须满足某些系统性能标准。假设这些标准已经满足，你可能会然后将功能发布给一群乐于尝试最新功能的快乐的客户的金丝雀群体。如果你的应用程序保持稳定，并且在金丝雀群体中看到高用户参与度，那么你可能将功能发布给一个按地理位置划分的更大的用户群体（例如，美国的用户）。或许在这种情况下，你对美国客户的基础设施比对欧洲客户更有信心。一旦美国环的一切都检查完毕，你将功能发布给欧洲环，以此类推，直到最终使功能对所有用户普遍可用。

在环部署的每个阶段，你都在“限制”任何小系统故障的影响范围。更重要的是，在整个过程中，你都在不断地迭代新功能。因此，当功能最终普遍可用时，它的性能比传统的一次性大规模部署要好得多。你也可以将环部署视为门控部署。

作为渐进式交付的核心技术，环部署为软件团队提供了他们需要的控制，以提供无与伦比的数字体验。它们极大地减少了失败的成本和影响。它们还给予了团队安全进行CI/CD的信心。

像金丝雀发布一样，特性管理平台也简化了执行环部署的过程。

##### 百分比部署

与针对性发布类似，基于百分比的部署是逐步进行的。但在前一种情况下，每个阶段的用户群体是明确定义的，而在基于百分比的部署中，群体是随机选择的。当你无法运行beta程序或预期用户之间变化很小的时候，这种部署是有用的。

你可能会最初向随机的10%的用户发布一个功能，然后将其提高到25%，然后是50%，依此类推，直到向所有用户发布。一些公司自动化了这个过程。如果在发布过程中的任何阶段，错误数量或响应时间超过了设定的阈值，那么发布就会停止。但在一切顺利的情况下，每个客户最终都会在你需要很少参与的情况下获得新功能。

许多人还同时使用环部署和百分比部署。你首先部署到一个精心挑选的金丝雀群体，一旦功能通过了这个第一环，你就可以以随机百分比的形式将其发布给你的其余用户群体。

#### 总结：构建的好处

在构建中，团队使用特性管理来解耦部署和发布，进行基于主干的开发，参与安全的CI/CD，并在生产环境中测试。他们还执行针对性发布、金丝雀发布、环部署和百分比部署。

参与这些实践的团队极大地提高了他们的软件交付性能。他们部署得更快，避免了灾难，并大大减少了应用程序故障的影响。更重要的是，他们控制了谁在何时看到哪些代码更改，从而创造了卓越的用户体验。

所有这些的最终结果是更快乐的、更有生产力的软件团队，更快乐的客户，以及更多的收入。