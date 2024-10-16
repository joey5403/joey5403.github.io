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