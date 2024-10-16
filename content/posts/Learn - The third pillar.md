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