---
id: Operate - The second pillar
aliases: []
tags:
  - feature toggle
category: Tech
date: 2024-10-20
published: 2024-10-20
title: Operate - The second pillar
---

## What is Operate?

Operate, the second of the Four Pillars of Feature Management, encompasses feature flag use cases that improve the operational health of your application. It entails making feature flags a mission-critical piece of your operations. As deployment speeds and infrastructural complexity go up, so does the need for operational safeguards. Feature management is that safeguard.

Teams that use feature flags via a feature management platform reduce risk and ensure customers remain satisfied with their service. They dramatically cut down on serious incidents. For example, as previously cited, Honeycomb has a “change fail rate” of just [0.1%](https://www.youtube.com/watch?v=qin6mszJ6rI&t=6s), a feat shared only by the world’s most elite software teams. And the company cites its use of LaunchDarkly as a big reason for its exceedingly low failure rate.

But even when teams that rely on feature management do face incidents, they recover much faster than they would otherwise. For example, you may recall that Atlassian improved its [mean time to restore](https://launchdarkly.com/blog/mean-time-to-restore-mttr/) service (MTTR) hours by [97%](https://launchdarkly.com/case-studies/atlassian/) after using LaunchDarkly.

In Operate, teams are better equipped to meet their service level objectives (SLOs) and deliver the 100% uptime customers expect. The primary use cases of the Operate pillar include:

- Kill switches and circuit breakers
- Dynamic configurations
- Service metrics (reactive monitoring)
- Safe migrations

For all you DevOps engineers, site reliability engineers (SREs), software architects, and other ops professionals who feel left out of the feature flag discussion, this pillar is for you.

## What is the goal of Operate?

The main goal of Operate is to improve the operational health of your application and infrastructure through feature flags. Operate helps software teams maintain high system stability, reliability, and availability, thus giving developers the confidence to ship code faster.

### Kill switches and circuit breakers

Feature flags can be used as kill switches and circuit breakers. Both allow you to disable broken parts of your application instantly. Where they differ is in the duration they stay in your code. A kill switch is generally considered a temporary or short-term feature flag. It’s something you use in, say, a product launch. A circuit breaker, on the other hand, is a more permanent, long-term flag.

#### Example of a kill switch

Let’s say you release a compute-heavy feature, and it causes latency issues. If you’ve attached a kill switch to this feature, then you can shut it off as soon as you detect the problem. One person toggles a feature flag—that’s it. Compare that to the pain of several people across multiple teams scrambling to change config files, restart the app for all users, perform hotfixes, do cumbersome rollbacks, and so on and so forth.

Kill switches give teams the confidence to release more frequently. For they know that if something goes wrong, they can click a button, and the problem is solved.

Once you’ve released a feature to all the intended users and are confident in its performance, we suggest removing the kill switch for that feature. Otherwise, technical debt will start accruing.

Kill switches give teams the confidence to release more frequently. If something goes wrong, they can click a button, and the problem is solved.

#### Example of a circuit breaker

You insert feature flags as circuit breakers, or control points, in areas of your code where you suspect an error might occur. The incident you’re predicting might not happen today, it might not happen tomorrow, it might not happen ever. But if it does, it could set off a series of bad outcomes.

For example, microservices architectures often rely on various third-party services. If one of these services goes down, it can wreak havoc on your system and, consequently, your user experience. But if you attach circuit breakers (feature flags) to each third-party service, you can quickly disable a service that has suffered an outage. As such, you take what could have been a catastrophe and reduce it to a modest bump in the road.

Kill switches and circuit breakers give you more control over your application. They play a big part in enabling teams to move fast safely. What’s more, they span all of the Four Pillars of Feature Management and are present in all the other use cases of Operate.

For example, when we talk about using kill switches and circuit breakers, we’re describing _dynamic configurations_.

### Dynamic configurations

Feature flags allow you to change configurations on the fly. This means you can change the behavior of your application without having to deploy new code, thus avoiding an application restart. If you’ve placed feature flags strategically throughout your code, then you can control your features in real-time. Dynamic configurations come in handy for things like API rate limiting, load shedding, and adjusting log levels.

Feature flags allow you to change the behavior of your application in real-time without having to deploy new code.

#### API rate limiting when your APIs are getting slammed

Typically, when your API is getting throttled, say, from a DDoS attack, to block the offending domain, you have to change a configuration and then redeploy your application. Meanwhile, the bad actor continues slamming your API and disrupting your service.

But if you assign a [multivariate feature flag](https://docs.launchdarkly.com/home/managing-flags/flag-variations) to your rate limiting rules, you can adjust your rate limit during an attack instantly and automatically. Once a domain hits your API enough times, it will trigger your circuit breakers to deny access to the bad actor. Again, in this way, feature management enables you to maintain system availability for all customers.

You can also use dynamic configurations for more pleasant rate-limiting purposes.

#### API rate limiting based on customer tier

You can also use multivariate flags and [targeting rules](https://docs.launchdarkly.com/home/managing-flags/targeting-users) to serve up different rate limits to different customer tiers. For example, you may offer 600 requests/minute to premium customers, 60 to standard ones, and five to free-version users. Any time someone signs up for, say, a premium subscription, the relevant feature flag will automatically set the appropriate rate limit. In this case, feature flags significantly improve your operational efficiency. We know this to be true because this is precisely how we manage our API rate limits in LaunchDarkly.

Also worthy of note, this particular rate limiting example fits into the Empower Pillar, in that it employs feature flags for [entitlements](https://launchdarkly.com/blog/how-to-manage-entitlements-with-feature-flags/). 

#### Adjust logging levels on the fly

You can also use long-term operational flags to dynamically configure the mode of your server logs. For example, if your observability tool shows a spike in errors, the multivariate flag you’ve created will change the logging level from WARNING to DEBUG automatically and in real-time. This helps you find and resolve the source of the problem faster. And it also enables you to better regulate your server logs. After all, you don’t want your app generating verbose logs any longer than it has to.

Everything we’re describing in the Operate Pillar is much easier to do with a centralized [feature management platform](https://launchdarkly.com/product/) like LaunchDarkly. For example, LaunchDarkly integrates with several [observability and application performance monitoring (APM) solutions](https://launchdarkly.com/integrations/) such as AppDynamics, Datadog, Dynatrace, Honeycomb, New Relic, and SignalFX. These integrations help you measure how each feature affects key service metrics such as response times and error rates.

### Service metrics (reactive monitoring)

When you pair a feature management platform with your observability and APM tools, it allows you to detect incidents faster and react to them in real-time.

#### Find the cause of an incident with feature flags

Imagine you’re seeing a surge in error rates. This metric event will trigger LaunchDarkly to send feature flag event data to your observability and monitoring tools. Depending on the tool you’re using, you’ll see those events displayed alongside performance graphs. This, in turn, helps you quickly pinpoint which recent feature rollout, if any, impaired your service. In this way, feature management helps you rapidly determine the root cause of an incident.

This is half of the reason why LaunchDarkly customers are able to consistently lower their MTTR. The other reason is, once they find the source of the problem, they can fix it immediately with a kill switch.

Pairing a feature management platform with your observability and APM tools allows you to detect incidents faster and react to them in real-time.

Consider another example.

#### Load shedding

You can also use feature flags for things like “load shedding”. Imagine the response times on your website have exceeded a certain threshold. Perhaps an unusual number of users have visited your site. Let’s further assume that you’ve integrated your observability and monitoring tools with LaunchDarkly. Finally, let’s say you’ve created a long-term feature flag that instantly disables non-essential services when toggled off.

The moment the metric event occurs, LaunchDarkly will be alerted to the issue and automatically put your website in a degraded or reduced service mode. While this is not ideal, it does allow you to avert the disaster of your website crashing. You keep the service running while you debug and troubleshoot. You can enable these automatic feature flag changes via [Flag Triggers](https://launchdarkly.com/blog/launched-automatic-kill-switches-using-flag-triggers/) in LaunchDarkly.

Ultimately, tracking key service metrics alongside feature flag events improves the overall stability, reliability, and availability of your service.

#### Safe migrations

Feature management—and the feature flags that fuel it—also enables ops teams to perform safer infrastructure migrations.

#### Microservices migration

When adopting a microservices architecture, many unforeseen issues can arise. But if you employ kill switches at each stage of the migration, you can turn off a defective service the moment it starts acting up. This alone removes a good deal of risk in a systems migration. And it reduces the odds of you defaulting on your SLOs.

#### Database migration

When moving to a new database, you can use feature flags to perform a gradual rollout of the new system. For example, at the start of the migration, you can route 100% of ‘read’ and ‘write’ events to the old database, while duplicating 10% of the write events and then pushing them to the new database. As you monitor performance and see that your system has remained stable, you can then move to the next phase of the rollout, until 100% of events are funneled to the new system.

In this case, you would have performed a targeted percentage deployment. But instead of gradually rolling out new functionality to customers, you’re routing data to a database. And if your application performance suffers during any part of the migration, you can halt the rollout with a kill switch.

Such an approach is safe and controlled. In fact, we followed this very process when [switching databases at LaunchDarkly](https://launchdarkly.com/blog/feature-flagging-to-mitigate-risk-in-database-migration/).

#### Cloud migration

Migrating your infrastructure from an on-premises data center to a cloud infrastructure as a service (IaaS) platform is a stressful undertaking. But feature flags bring ease, safety, and predictability to the project. For example, TrueCar migrated 500 websites to Amazon Web Services (AWS) Cloud with the help of LaunchDarkly.

As with the database example, TrueCar used feature flags and targeting rules to control the flow of web traffic between its legacy and cloud systems. The team would gradually increase the flow of traffic to the cloud when it became clear that it was safe to do so. They also used LaunchDarkly to route web traffic by request type. For example, web searches for “new cars” might have been associated with a cloud database, while searches for “used cars” were tied to the legacy system.

Feature flags simplified these complex routing rules. Moreover, LaunchDarkly’s simple and clean user interface made it easy to manage the vast sprawl of web traffic flows. In the end, TrueCar completed its cloud migration with zero downtime due to infrastructure problems.

![](https://images.prismic.io/launchdarkly/a5e885d2-0641-4457-bfe1-8b9f9d879faf_truecar.svg?auto=compress,format)

"Business users and application software engineers used LaunchDarkly’s A/B testing framework to manage traffic flows across the whole infrastructure. For that and many other reasons, TrueCar’s AWS migration was the smoothest, most uneventful of any I’ve ever managed."

Regis Wilson

SRE

Regis Wilson details his experience using LaunchDarkly for the cloud migration in a [blog post he wrote](https://launchdarkly.com/blog/dynamic-routing-with-aws-lambdaedge/). You can also read the [full TrueCar case study](https://launchdarkly.com/case-studies/truecar/). Lastly, you can learn best practices for [infrastructure migrations in our LaunchDarkly Guides](https://docs.launchdarkly.com/guides/best-practices/infrastructure-migration).

Feature management equips you with far more control over infrastructure changes than you would have otherwise. And it virtually wipes out risk in the process.

#### Summary: The benefits of Operate

When software teams engage in the core practices of the Operate pillar of feature management, they purge their operations of risk. This is especially true of those who use LaunchDarkly in conjunction with their monitoring and observability stack. Such teams achieve greater system stability, even as developers ship more frequently. In fact, the safeguards of feature management enable this increase in speed.

In Operate, teams experience fewer system failures; and when failures do occur, they recover faster—often in minutes, if not seconds. Lastly, adherents of Operate preserve customer loyalty and trust. It’s hard to put a price tag on that.


## 什么是运营（Operate）？

运营，作为特性管理四大支柱中的第二大支柱，涵盖了使用特性标志来改善你的应用程序的运营健康状况的用例。它涉及将特性标志作为你运营的关键部分。随着部署速度和基础设施复杂性的提高，对运营保障的需求也在增加。特性管理就是这种保障。

通过特性管理平台使用特性标志的团队降低了风险，并确保客户对他们的服务保持满意。他们大大减少了严重事件的发生。例如，正如之前引用的，Honeycomb的“变更失败率”仅为[0.1%](https://www.youtube.com/watch?v=qin6mszJ6rI&t=6s)，这一成就只有世界上最精英的软件团队才能共享。该公司将其极低的失败率归功于使用LaunchDarkly。

但即使依赖特性管理的团队确实面临事件，他们的恢复速度也比以往快得多。例如，你可能还记得，Atlassian在使用LaunchDarkly后将其[平均恢复服务时间](https://launchdarkly.com/blog/mean-time-to-restore-mttr/)（MTTR）提高了[97%](https://launchdarkly.com/case-studies/atlassian/)。

在运营中，团队更有能力满足他们的服务水平目标（SLOs），并提供客户期望的100%正常运行时间。运营支柱的主要用例包括：

- 杀伤开关和断路器
- 动态配置
- 服务指标（反应性监控）
- 安全迁移

对于所有DevOps工程师、网站可靠性工程师（SREs）、软件架构师和其他运维专业人员，如果你们觉得自己被排除在特性标志讨论之外，这一支柱就是为你们准备的。

## 运营的目标是什么？

运营的主要目标是通过特性标志改善你的应用程序和基础设施的运营健康状况。运营帮助软件团队保持高系统稳定性、可靠性和可用性，从而使开发者有信心更快地发布代码。

### 杀伤开关和断路器

特性标志可以用作杀伤开关和断路器。两者都允许你立即禁用应用程序中损坏的部分。它们的区别在于它们在代码中的持续时间。杀伤开关通常被认为是临时或短期的特性标志。这是你在产品发布时使用的东西。另一方面，断路器是一个更永久、长期的标志。

#### 杀伤开关的例子

假设你发布了一个计算密集型功能，它导致了延迟问题。如果你为这个功能附加了一个杀伤开关，那么一旦你检测到问题，就可以立即关闭它。一个人切换一个特性标志——就这样。与多个人跨多个团队争先恐后地更改配置文件、为所有用户重新启动应用程序、执行热修复、执行繁琐的回滚等痛苦相比。

杀伤开关给团队带来了更频繁发布的信心。因为他们知道如果出了问题，他们可以点击一个按钮，问题就解决了。

一旦你向所有预期的用户发布了一个功能，并且对其性能有信心，我们建议移除该功能的杀伤开关。否则，技术债务将开始累积。

杀伤开关给团队带来了更频繁发布的信心。如果出了问题，他们可以点击一个按钮，问题就解决了。

#### 断路器的例子

你将特性标志作为断路器或控制点插入到你的代码中，你怀疑错误可能发生的地方。你预测的事件可能今天不会发生，明天可能不会发生，可能永远不会发生。但如果它确实发生了，它可能会引发一系列不良结果。

例如，微服务架构通常依赖各种第三方服务。如果这些服务之一宕机，它可能会对你的系统造成严重破坏，因此影响你的用户体验。但如果你对每个第三方服务附加断路器（特性标志），你可以在服务出现故障时迅速禁用该服务。这样，你可以将可能的灾难减少到道路上的一个适度的颠簸。

杀伤开关和断路器为你的应用程序提供了更多的控制权。它们在使团队能够安全快速地移动中发挥了重要作用。更重要的是，它们跨越了特性管理的所有四大支柱，并出现在运营的其他所有用例中。

例如，当我们谈论使用杀伤开关和断路器时，我们正在描述**动态配置**。

### 动态配置

特性标志允许你实时更改配置。这意味着你可以在不部署新代码的情况下更改应用程序的行为，从而避免应用程序重新启动。如果你在代码中策略性地放置了特性标志，那么你可以实时控制你的功能。动态配置对于API速率限制、负载卸载和调整日志级别等事情非常有用。

特性标志允许你在不部署新代码的情况下实时更改应用程序的行为。

#### 当你的API受到攻击时的API速率限制

通常，当你的API受到节流时，比如说，受到DDoS攻击，为了阻止违规域名，你必须更改配置，然后重新部署你的应用程序。与此同时，不良行为者继续猛烈攻击你的API，扰乱你的服务。

但如果你对速率限制规则分配了一个[多变量特性标志](https://docs.launchdarkly.com/home/managing-flags/flag-variations)，你可以在攻击期间立即并自动调整你的速率限制。一旦域名足够多次击中你的API，它将触发你的断路器以拒绝不良行为者的访问。同样，在这种情况下，特性管理使你能够为所有客户维护系统的可用性。

你还可以使用动态配置进行更愉快的速率限制目的。

#### 基于客户层级的API速率限制

你还可以使用多变量标志和[目标规则](https://docs.launchdarkly.com/home/managing-flags/targeting-users)为不同的客户层级提供不同的速率限制。例如，你可能为高级客户提供每分钟600个请求，为标准客户提供60个，为免费版本用户提供5个。任何时候有人注册，比如说，高级订阅，相关的功能标志将自动设置适当的速率限制。在这种情况下，特性标志显著提高了你的运营效率。我们知道这是真的，因为这就是我们在LaunchDarkly中管理API速率限制的方式。

同样值得注意的是，这个特定的速率限制示例符合授权支柱，因为它使用特性标志进行[权限](https://launchdarkly.com/blog/how-to-manage-entitlements-with-feature-flags/)。

#### 实时调整日志级别

你还可以使用长期运营标志动态配置服务器日志的模式。例如，如果你的可观察性工具显示错误数量激增，你创建的多变量标志将自动并实时地将日志级别从WARNING更改为DEBUG。这有助于你更快地找到并解决问题。它还使你能够更好地管理你的服务器日志。毕竟，你不希望你的应用程序生成冗长的日志超过必要的时间。

我们在运营支柱中描述的所有内容都可以通过像LaunchDarkly这样的集中式[特性管理平台](https://launchdarkly.com/product/)更容易地完成。例如，LaunchDarkly与几个[可观察性和应用程序性能监控（APM](https://xn--(apm-kg1go6a888akhfjby22ada668hkl1dc4e62n431ag86a/)）解决方案集成，如AppDynamics、Datadog、Dynatrace、Honeycomb、New Relic和SignalFX。这些集成帮助你测量每个功能对关键服务指标如响应时间和错误率的影响。

### 服务指标（反应性监控）

当你将特性管理平台与你的可观察性和APM工具配对时，它允许你更快地检测事件并实时做出反应。

#### 使用特性标志找到事件的原因

想象你看到错误率激增。这个指标事件将触发LaunchDarkly将特性标志事件数据发送到你的可观察性和监控工具。根据你使用的工具，你将看到这些事件与性能图表一起显示。这反过来帮助你快速确定最近的哪个功能发布（如果有的话）损害了你的服务。通过这种方式，特性管理帮助你迅速确定事件的根本原因。

这就是为什么LaunchDarkly客户能够持续降低他们的MTTR的一半原因。另一个原因是，一旦他们找到问题的根源，他们可以立即用杀伤开关修复它。

将特性管理平台与你的可观察性和APM工具配对，可以让你更快地检测事件并实时做出反应。

考虑另一个例子。

#### 负载卸载

你还可以使用特性标志进行“负载卸载”。想象你的网站响应时间超过了某个阈值。也许不寻常数量的用户访问了你的网站。让我们进一步假设你已经将你的可观察性和监控工具与LaunchDarkly集成。最后，假设你创建了一个长期特性标志，当切换关闭时立即禁用非必要的服务。

当指标事件发生时，LaunchDarkly将被提醒到问题，并自动将你的网站置于降级或减少服务模式。虽然这不是理想的，但它确实允许你避免网站崩溃的灾难。你在调试和故障排除时保持服务运行。你可以通过LaunchDarkly中的[Flag Triggers](https://launchdarkly.com/blog/launched-automatic-kill-switches-using-flag-triggers/)启用这些自动特性标志更改。

最终，跟踪关键服务指标与特性标志事件一起提高了你的服务的整体稳定性、可靠性和可用性。

#### 安全迁移

特性管理——以及推动它的功能标志——还使运维团队能够执行更安全的基础设施迁移。

#### 微服务迁移

在采用微服务架构时，可能会出现许多不可预见的问题。但如果在迁移的每个阶段都使用杀伤开关，你可以在有缺陷的服务开始出现问题时立即关闭它。这本身就消除了系统迁移中的大部分风险。它还减少了你违约SLOs的可能性。

当迁移到一个新的数据库时，你可以使用特性标志来逐步推出新系统。例如，在迁移开始时，你可以将100%的“读取”和“写入”事件路由到旧数据库，同时复制10%的写入事件，然后将它们推送到新数据库。当你监控性能并发现你的系统保持稳定后，你可以进入推出计划的下一阶段，直到100%的事件都被引导到新系统。

在这种情况下，你将执行一个有针对性的百分比部署。但你不是逐步向客户推出新功能，而是将数据路由到数据库。如果在迁移的任何部分你的应用程序性能受到影响，你可以使用杀伤开关停止推出。

这种方法是安全和可控的。实际上，我们在LaunchDarkly[切换数据库时](https://launchdarkly.com/blog/feature-flagging-to-mitigate-risk-in-database-migration/)正是遵循了这一过程。

#### 云迁移

将基础设施从本地数据中心迁移到云基础设施即服务（IaaS）平台是一项压力重重的任务。但特性标志为项目带来了便利、安全性和可预测性。例如，TrueCar在LaunchDarkly的帮助下将500个网站迁移到了亚马逊网络服务（AWS）云。

与数据库示例一样，TrueCar使用特性标志和目标规则来控制其传统系统和云系统之间的网络流量流动。当明确安全时，团队会逐渐增加流向云的流量。他们还使用LaunchDarkly按请求类型路由网络流量。例如，对“新车”的网络搜索可能与云数据库相关联，而对“二手车”的搜索则与遗留系统绑定。

特性标志简化了这些复杂的路由规则。此外，LaunchDarkly简单清晰的用户界面使得管理庞大的网络流量流动变得容易。最终，TrueCar完成了其云迁移，由于基础设施问题导致的停机时间为零。

[https://images.prismic.io/launchdarkly/a5e885d2-0641-4457-bfe1-8b9f9d879faf_truecar.svg?auto=compress,format](https://images.prismic.io/launchdarkly/a5e885d2-0641-4457-bfe1-8b9f9d879faf_truecar.svg?auto=compress,format)

"商业用户和应用软件工程师使用LaunchDarkly的A/B测试框架来管理整个基础设施的流量流动。出于这个和许多其他原因，TrueCar的AWS迁移是我管理过的最顺利、最不引人注目的迁移之一。"

Regis Wilson

SRE

Regis Wilson在他的一篇[博客文章](https://launchdarkly.com/blog/dynamic-routing-with-aws-lambdaedge/)中详细介绍了他使用LaunchDarkly进行云迁移的经历。你还可以阅读[完整的TrueCar案例研究](https://launchdarkly.com/case-studies/truecar/)。最后，你可以在我们的[LaunchDarkly指南](https://docs.launchdarkly.com/guides/best-practices/infrastructure-migration)中学习基础设施迁移的最佳实践。

特性管理为你提供了比以往更多的对基础设施变化的控制权。它几乎消除了过程中的风险。

#### 总结：运营的好处

当软件团队参与特性管理的运营支柱的核心实践时，他们消除了运营中的风险。特别是那些将LaunchDarkly与其监控和可观察性栈结合使用的团队。这样的团队实现了更大的系统稳定性，即使开发者更频繁地交付。事实上，特性管理的保障措施使这种速度的提高成为可能。

在运营中，团队经历的系统故障更少；当故障确实发生时，它们的恢复速度更快——通常在几分钟内，如果不是几秒钟的话。最后，运营的拥护者保持了客户忠诚度和信任。这很难用价格来衡量。
