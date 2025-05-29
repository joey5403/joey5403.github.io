---
id: Empower - The fourth pillar

tags:
  - feature toggle
authors:
  - joey5403
category: Tech
date: "2024-10-20"
published: 2024-10-20
title: Empower - The fourth pillar
---

## What is Empower?

Empower, the fourth and final pillar of feature management, reimagines the process of giving users access to your software. It applies especially, though not exclusively to managing entitlements. In a software context, [“entitlements”](https://launchdarkly.com/blog/how-to-manage-entitlements-with-feature-flags/) refers to the act of enabling or disabling features, services, and products for customers. For example, when you unlock your full application for a customer who had previously been using an abbreviated trial version, you have managed an entitlement.

In the Empower pillar, feature flags empower customer-facing teams—Product Management, Marketing, Sales, Customer Support, etc.—to control the granting and denying of access to certain functionality.

Enabling those outside of Engineering to manage access to features results in:

1. Engineers spending less time on administrative work that falls outside their scope of responsibility and expertise;
2. Customer-facing teams promptly delivering software to customers, rather than waiting for engineers to sort through a backlog of request tickets; and
3. Customers getting a personalized, superior experience.

Empower is the pillar of feature management that deals most closely with “progressive delegation,” another core tenet of [Progressive Delivery](https://launchdarkly.com/blog/what-is-progressive-delivery-all-about/). Progressive delegation refers to gradually delegating the control of a feature to the team most responsible for the outcome of that feature (e.g., a product manager ensuring that customers are satisfied with a given feature). This might look like transferring the ownership of a feature from Engineering to Product Management, then from Product Management to Marketing, and so on. Feature management enables Progressive Delivery, and the core use cases of Empower exemplify progressive delegation.

Empower is all about enabling customer-facing teams to play a bigger role in delivering software.

The procedures of Empower echo those of the [Build pillar](https://launchdarkly.com/blog/build-the-first-pillar-of-feature-management/). Both employ [feature flags](https://launchdarkly.com/blog/what-are-feature-flags/) and [user targeting](https://docs.launchdarkly.com/home/managing-flags/targeting-users) to dictate who sees which features when. Moreover, in each pillar, engineers can delegate control to non-engineers over the delivery of such features—though, engineers do less delegating in Build. 

But the two pillars differ in where they fall in the feature lifecycle. Build focuses on the stages before and during a software release. Whereas, Empower addresses the periods during and after. It entails long-term customer targeting for things like giving an enterprise customer access to a set of features built exclusively for them. That’s just one example.

Software orgs can use [feature management](https://launchdarkly.com/product/) to empower all teams to influence software delivery in the following areas:

1. Feature entitlements
2. Customer targeting
3. Proof of concepts (POCs) and trials
4. Sunsetting features

## What is the goal of Empower?

The goal of Empower is to enable customer-facing teams to play a bigger role in delivering software. This reduces the burden on engineers, helps business stakeholders do their jobs more effectively, and creates a better, more personalized customer experience.

### Feature entitlements

Conventional approaches to managing entitlements require developer intervention. Such approaches are more involved than they need to be. Depending on the scenario, provisioning an entitlement may require an engineer to change a configuration file (forcing a restart of the app), alter a user database, perform a custom-build, and so on. In isolation, these actions are not a big deal. But when aggregated on a large scale, they exhaust considerable time and present needless risks. Any time you modify a user database, for example, you run the risk of losing sensitive data, throwing fields into disorder, and making other costly mistakes.

Typically, managing entitlements requires developer intervention. Feature management reduces the burden on engineers, allowing them to do what they do best: build software.

Besides the risks and overhead, conventional approaches to managing entitlements are marred by yet another flaw. They force engineers to turn features ‘on’ and ‘off’ for customers when, theoretically, their colleagues in the line of business units could just as easily do this work. In fact, it makes more sense for business stakeholders to control customer experiences, given how they routinely engage with those customers. Engineers’ time would be better spent doing that which customer-facing teams cannot: building software!

Feature flags lift the burden on Engineering and empower customer-facing teams. Here are a few examples to illustrate the point.

#### Empowering sales teams to manage entitlements

One tech company, whose software enables customers to detect, manage, and protect sensitive data across their technology stack, uses feature management for entitlements. In the past, when a customer signed up, the sales team would have to submit an engineering request to add the customer’s universally unique identifier (UUID) to a config file. Only then would the new customer get access to the features they paid for. This process strained the engineers, negatively affected the sales team, and hurt the customer experience.

Since using LaunchDarkly, engineers can hand off the responsibility of entitlements to the sales team. As a result, salespeople now provide faster turnaround times for clients. No more Jira tickets, no more waiting—just value delivered instantly.

#### How LaunchDarkly empowers sales teams

[LaunchDarkly](https://launchdarkly.com/product/) empowers sales teams in the following way. Engineers create a feature flag for the bundle of features tied to a given software membership plan (e.g., a Premium plan). Through user targeting, they then create a designated user segment for this tier. If a user is in this segment, they will see the premium features.

Against this backdrop, anytime a customer signs up for a premium subscription, an account executive can simply go into the LaunchDarkly dashboard and add the new customer to the appropriate segment. Taking this a step further, you can also automate the process of adding users to a segment. In this case, if a customer purchases a subscription on your website, they will automatically appear in the correct segment, in turn, granting them immediate access to the right features. LaunchDarkly thus brings ease and fluidity to entitlements.

Let’s explore another example.

#### Automating entitlements at a large consultancy

The health and wellness arm of a large consulting firm uses LaunchDarkly to dynamically control the behavior of its new health application. LaunchDarkly feature flags enable and disable functionality based on complex business logic and in-app triggers. For instance, the company unlocks specific features only after a user has accepted the terms and conditions. The same goes for when users upgrade their accounts. Such automation increases the company’s agility, thus allowing developers to spend time improving the product versus doling out features. All of this drives engineer productivity and enhances the customer experience.

### Customer targeting

Customer targeting is another entitlements use case. The scope of this type of targeting is broader than with discrete user targeting. It entails delivering functionality to specific organizations, industries, countries, and other large entities, each containing scores of individual users.

Here’s an example.

#### White labeling

It has become the norm for banks to provide a mobile banking app as a part of their service. In some cases, particularly among small and mid-size banks, the banks will purchase the core software for their app from a third-party provider and cloak it in their branding (a practice known as “white labeling”).

These third-party providers have several banks in their client portfolio, all of whom want different things. Without feature flags, the providers may create separate feature branches to deliver unique versions of their software, effectively creating custom-builds for each bank. Such an approach is hard to sustain. 

For starters, each general change you make to one branch must be replicated across the other branches to avoid getting out of sync. The more changes you make, the more unwieldy your code becomes. Ultimately, doing customer targeting via feature branching is time-consuming, error-prone, and expensive.

But with feature management, software providers can deliver custom experiences to each banking client using a single master branch (trunk). And they can control who sees what with feature flags. They can build and deliver unique experiences to every customer in one codebase. Such an approach is efficient, safe, and controlled.

With feature management, software providers can deliver custom experiences to each customer.

#### Targeting by geographic location

Many software companies serve international customers. And they must adapt their software to the laws and regulations of each country. Features that are embraced in one country may be outlawed in another. Again, one way to deliver specific functionality by country is to create separate instances of your application via a tangled mess of feature branches. We’ve already discussed the drawbacks of this approach.

But with LaunchDarkly, you can leverage feature flags and customer targeting to dispense the right features to the right customers by country—again, all within a single codebase. Moreover, business stakeholders can do the dispensing. As business stakeholders are more attuned to the needs (and laws) of their customers than engineers, it is wise to let them manage the entitlements for these global customers.

### POCs and trials

For many software companies, giving prospective customers temporary access to your application for trials and proof of concept evaluations (POCs) can be a thorny process. When salespeople are in the throes of a high-stakes deal, and they have to ask Engineering to extend a trial or issue temporary POC licenses, it prolongs the sales cycle. Worse, it can threaten the deal entirely. POCs often arise in sales engagements with enterprises, in which thousands or millions of dollars are on the line. The last thing you want to do is stall the deal, especially if the prospects are already test-driving competitor tools.

Imagine if salespeople could grant software access themselves (with proper guardrails in place, of course)? Engineers wouldn’t have to worry about fielding entitlements requests. And salespeople could more promptly deliver features to prospects, increasing the odds of outflanking competitors on the deal. If nothing else, delegating feature control means one less roadblock in sales evaluations.

With feature management, salespeople _can_ control software access for trials and POCs. That’s precisely what we do at LaunchDarkly.

#### LaunchDarkly’s sales team uses LaunchDarkly for POCs

Our solutions engineers (SEs) on the revenue team use feature flags to issue trials without needing developer involvement. Flags allow us to quickly add LaunchDarkly seats for prospects as well as for additional groups within an existing customer organization. We want as many people to use LaunchDarkly’s product as possible so that they can see the value of it firsthand. Feature flags prevent us from getting in our own way in this regard. Moreover, they keep our engineers from having to do extra work to enable temporary and permanent features.

Feature flags prevent sales evaluations from stalling by granting prospects instant access to your software during a POC.

By opening up more seats for customers, we deliver more value during an evaluation. And we pave the way for a potentially larger business case than what was originally scoped out. More seats equal more revenue.

This simple process for managing entitlements also leads to happier salespeople, engineers, and customers. Through LaunchDarkly feature flags, we empower our sales team to make the best decisions for existing and future customers.

#### Sunsetting features

Feature management is a powerful solution for launching new functionality. But it’s also great for retiring old features.

At some point, old features conflict with new ones, or they fall into disuse and become technical debt. Feature management gives teams fine-grained control over sunsetting these features. Engineers can tee up the sunsetting process with feature flags and user targeting. Then, they can delegate control of the flags to product managers, customer success reps, or someone else who has a relationship with the customers affected by the loss of features. The customer-facing team can remove the old feature at a cadence that matches each customer’s needs. This gives customers more time to wean off the feature, thus easing the pain of the transition.

The [LaunchDarkly Feature Management Platform](https://launchdarkly.com/product/) enables you to manage the entire lifecycle of your features, including end-of-life. This creates a better customer experience when sunsetting features. It also reduces the risks of offloading old functionality by giving you more control over the process with feature flags.

#### Summary: The benefits of Empower

Empower is all about giving customer-facing teams control over sections of software within their domain. Generally, business stakeholders have more insight into customers’ needs than developers. Yet, historically, they’ve lacked a way to control how features are released to these customers. At the same time, developers would gladly forfeit the perennial burden of having to enable functionality for users, assuming they could do so without added risk.

[Feature management](https://launchdarkly.com/feature-management/) empowers business stakeholders with the control they’ve been missing, to the benefit of all teams. When engineers build features, they can hand them off to business stakeholders and say, “Hey, we wrapped these features in a feature flag; you decide when they go live, who sees them, etc.” Everybody wins.

Ultimately, leveraging feature management for entitlements drives operational efficiency, greater productivity across all teams, and better customer outcomes.


## 什么是授权（Empower）？

授权是特性管理的第四大也是最后一个支柱，它重新构想了让用户访问你的软件的过程。它特别（尽管不是唯一）适用于管理权限。在软件背景下，“[权限](https://launchdarkly.com/blog/how-to-manage-entitlements-with-feature-flags/)”指的是为客户启用或禁用功能、服务和产品的行为。例如，当你为之前使用过简化试用版的客户解锁完整应用程序时，你就管理了一个权限。

在授权支柱中，特性标志授权面向客户的团队——产品管理、市场营销、销售、客户支持等——控制授予和拒绝对某些功能的访问。

使那些在工程之外的人能够管理对功能的访问，可以带来以下结果：

1. 工程师花更少的时间在超出他们责任和专业范围的行政工作上；
2. 面向客户的团队迅速向客户交付软件，而不是等待工程师处理请求票证的积压；以及
3. 客户获得个性化、更优越的体验。

授权是与“渐进式委托”这一[渐进式交付](https://launchdarkly.com/blog/what-is-progressive-delivery-all-about/)的核心原则最密切相关的特性管理支柱。渐进式委托指的是逐渐将一个功能的控制权委托给对该功能结果最负责的团队（例如，产品经理确保客户对某个功能满意）。这可能看起来像是将一个功能从工程转移到产品管理，然后从产品管理转移到市场营销，等等。特性管理使渐进式交付成为可能，而授权的核心用例就是渐进式委托的典范。

授权是关于让面向客户的团队在软件交付中发挥更大的作用。

授权的程序与[构建支柱](https://launchdarkly.com/blog/build-the-first-pillar-of-feature-management/)相似。两者都使用[特性标志](https://launchdarkly.com/blog/what-are-feature-flags/)和[用户定向](https://docs.launchdarkly.com/home/managing-flags/targeting-users)来决定谁在何时看到哪些功能。此外，在每个支柱中，工程师可以将这些功能的交付控制权委托给非工程师——尽管，在构建中工程师做的委托较少。

但是这两个支柱在功能生命周期中的位置不同。构建专注于软件发布前和发布期间的阶段。而授权则涉及期间和之后。它包括长期客户定向，例如为特定企业客户群体提供他们独有的功能集。这只是其中一个例子。

软件组织可以使用[特性管理](https://launchdarkly.com/product/)来授权所有团队在以下领域影响软件交付：

1. 功能权限
2. 客户定向
3. 概念验证（POC）和试用
4. 功能淘汰

## 授权的目标是什么？

授权的目标是让面向客户的团队在软件交付中发挥更大的作用。这减轻了工程师的负担，帮助业务利益相关者更有效地完成工作，并创造了更好、更个性化的客户体验。

### 功能权限

传统管理权限的方法需要开发者干预。这些方法比必要的更复杂。根据场景，配置权限可能需要工程师更改配置文件（迫使应用程序重新启动）、修改用户数据库、执行自定义构建等。孤立地看，这些动作不是什么大问题。但是当大规模聚合时，它们消耗了大量时间，并带来了不必要的风险。例如，每次你修改用户数据库时，你都有丢失敏感数据、将字段投入混乱和犯其他昂贵错误的风险。

通常，管理权限需要开发者干预。特性管理减轻了工程师的负担，让他们做他们最擅长的事情：构建软件。

除了风险和开销外，传统管理权限的方法还有另一个缺点。它们迫使工程师为客户“开启”和“关闭”功能，而理论上，他们的业务部门同事也可以同样轻松地完成这项工作。事实上，让业务利益相关者控制客户体验更有意义，因为他们经常与这些客户互动。工程师的时间最好花在面向客户团队无法做到的事情上：构建软件！

特性标志减轻了工程的负担，并授权面向客户的团队。以下是一些说明这一点的例子。

#### 授权销售团队管理权限

一家科技公司，其软件使客户能够在他们的技术栈中检测、管理和保护敏感数据，使用特性管理来管理权限。过去，当客户注册时，销售团队必须提交工程请求，将客户的通用唯一识别码（UUID）添加到配置文件中。只有这样，新客户才能获得他们付费的功能。这个过程使工程师感到压力，对销售团队产生负面影响，并损害了客户体验。

自从使用LaunchDarkly以来，工程师可以将权限的责任交给销售团队。结果，销售人员现在可以为客户提供更快的响应时间。不再有Jira票证，不再等待——只有即时交付的价值。

#### LaunchDarkly如何授权销售团队

[LaunchDarkly](https://launchdarkly.com/product/)以以下方式授权销售团队。工程师为与给定软件会员计划（例如，高级计划）相关的功能集创建一个特性标志。然后通过用户定向，他们为这个层级创建一个指定的用户细分。如果用户在这个细分中，他们将看到高级功能。

在这种背景下，每当客户注册高级订阅时，客户经理可以简单地进入LaunchDarkly仪表板，并将新客户添加到适当的细分中。更进一步，你还可以自动化将用户添加到细分的过程。在这种情况下，如果客户在网站上购买订阅，他们将自动出现在正确的细分中，从而立即获得正确的功能。LaunchDarkly因此为权限带来了便利和流畅性。

让我们探索另一个例子。

#### 在一家大型咨询公司自动化权限

一家大型咨询公司的健康和保健部门使用LaunchDarkly动态控制其新的健康应用程序的行为。LaunchDarkly特性标志根据复杂的业务逻辑和应用内触发器启用和禁用功能。例如，公司只在用户接受条款和条件后才解锁特定功能。当用户升级他们的账户时也是如此。这种自动化提高了公司的反应能力，使开发人员有时间改进产品，而不是分发功能。所有这些都推动了工程师的生产力，并增强了客户体验。

### 客户定向

客户定向是另一种权限用例。这种类型的定向范围比离散用户定向更广。它涉及向特定组织、行业、国家和其他大型实体交付功能，每个实体都包含许多个人用户。

这里有一个例子。

#### 白标

银行提供移动银行应用程序作为他们服务的一部分已经成为常态。在某些情况下，特别是中小银行，银行将从第三方提供商那里购买他们应用程序的核心软件，并将其包装在自己的品牌中（一种被称为“白标”的做法）。

这些第三方提供商在他们的客户组合中有几家银行，他们都想要不同的东西。如果没有特性标志，提供商可能会创建单独的功能分支来交付他们软件的独特版本，有效地为每家银行创建自定义构建。这种方法很难维持。

首先，你对一个分支所做的每一个总体更改都必须在其他分支中复制，以避免失去同步。你做的更改越多，你的代码就越难以驾驭。最终，通过功能分支进行客户定向是耗时的、容易出错的，并且昂贵的。

但是有了特性管理，软件提供商可以使用单个主分支（树干）为每个银行客户交付定制体验。他们可以使用特性标志控制谁看到什么。他们可以在一个代码库中为每个客户构建和交付独特的体验。这种方法是高效的、安全的，并且可控的。

有了特性管理，软件提供商可以为每个客户交付定制体验。

#### 按地理位置定向

许多软件公司为国际客户服务。他们必须使他们的软件适应每个国家的法律和法规。在一个国家被接受的功能可能在另一个国家被禁止。再次，按国家提供特定功能的一种方式是通过功能分支的混乱来创建你的应用程序的单独实例。我们已经讨论了这种方法的缺点。

但是有了LaunchDarkly，你可以利用特性标志和客户定向，通过国家向正确的客户提供正确的功能——再次，所有这些都在一个代码库中。此外，业务利益相关者可以进行分配。由于业务利益相关者比工程师更了解客户的需求（和法律），让他们管理这些全球客户的权限是明智的。

### 概念验证（POC）和试用

对于许多软件公司来说，为潜在客户提供临时访问你的应用程序进行试用和概念验证评估（POC）可能是一个棘手的过程。当销售人员正处于高风险交易的热潮中，他们必须要求工程部门延长试用或发放临时POC许可证，这延长了销售周期。更糟糕的是，它可能完全威胁到交易。POC通常出现在与企业的销售人员的互动中，这些企业的销售涉及数千或数百万美元。你最不想做的事情就是拖延交易，特别是如果潜在客户已经在试用竞争对手的工具。

想象一下，如果销售人员可以自己授权软件访问（当然，有适当的防护措施）？工程师不必担心处理权限请求。销售人员可以更及时地向潜在客户提供功能，增加在交易中超越竞争对手的机会。如果没什么别的，委托功能控制意味着在销售评估中少了一个障碍。

有了特性管理，销售人员确实可以控制试用和POC的软件访问。这正是我们在LaunchDarkly所做的。

#### LaunchDarkly的销售团队使用LaunchDarkly进行POC

我们的收入团队中的解决方案工程师（SE）使用特性标志在不需要开发者参与的情况下发放试用。标志使我们能够快速为潜在客户以及现有客户组织内的其他群体添加LaunchDarkly座位。我们希望尽可能多的人使用LaunchDarkly的产品，以便他们可以亲身看到它的价值。特性标志在这方面阻止了我们自己的方式。此外，它们还使我们的工程师免于做额外的工作来启用临时和永久功能。

特性标志通过在POC期间向潜在客户提供即时访问你的软件，防止销售评估停滞。

通过为客户开放更多的座位，我们在评估期间提供更多的价值。我们为可能比最初规划的更大的业务案例铺平了道路。更多的座位等于更多的收入。

这种简单的权限管理过程也导致销售人员、工程师和客户更满意。通过LaunchDarkly特性标志，我们授权我们的销售团队为现有和未来的客户做出最佳决策。

#### 功能淘汰

特性管理是推出新功能的有力解决方案。但它也非常适合淘汰旧功能。

在某些时候，旧功能与新功能冲突，或者它们被废弃并成为技术债务。特性管理为团队提供了对淘汰这些功能的细粒度控制。工程师可以使用特性标志和用户定向来启动淘汰过程。然后，他们可以将标志的控制权委托给产品经理、客户成功代表或与受功能丧失影响的客户有关系的其他人员。面向客户的团队可以按照每个客户的需求的节奏移除旧功能。这给了客户更多的时间来逐渐放弃该功能，从而减轻了过渡的痛苦。

[LaunchDarkly特性管理平台](https://launchdarkly.com/product/)使您能够管理您的功能的整个生命周期，包括生命周期结束。这在淘汰功能时创造了更好的客户体验。它还通过特性标志为您提供了更多对过程的控制，从而降低了卸载旧功能的风险。

#### 总结：授权的好处

授权是关于让面向客户的团队控制他们领域内的软件部分。通常，业务利益相关者比开发者更了解客户的需求。然而，从历史上看，他们缺乏控制这些功能如何发布给这些客户的方式。同时，开发者很高兴放弃必须为用户启用功能的永久负担，假设他们可以这样做而没有额外的风险。

[特性管理](https://launchdarkly.com/feature-management/)赋予了业务利益相关者他们一直缺失的控制权，这对所有团队都有好处。当工程师构建功能时，他们可以将其移交给业务利益相关者，并说：“嘿，我们将这些功能包装在特性标志中；你们决定它们何时上线，谁可以看到它们等。”每个人都是赢家。

最终，利用特性管理进行权限管理推动了运营效率、提高所有团队的生产力和更好的客户结果。