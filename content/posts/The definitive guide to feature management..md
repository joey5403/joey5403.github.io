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