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