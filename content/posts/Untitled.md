# Reducing technical debt from feature flags

##### Read time: 16 minutes

##### Last edited: Oct 15, 2024

## [](https://docs.launchdarkly.com/guides/flags/technical-debt#overview)Overview

This guide provides ways to reduce and eliminate technical debt related to feature flags using LaunchDarkly. Like all debt, technical debt accumulates over time, but you can mitigate that debt over time if you put effective processes in place before you need them.

In this guide, we'll explore:

- The challenge of technical debt
- The lifecycle of a flag
- Naming conventions
- Using tags
- Code references
- Deprecating, archiving, and deleting flags

Just like feature flags should be a core engineering practice, so should a strategy to address technical debt. LaunchDarkly can help you by automatically identifying flags that need code removal or are ready to archive.

## [](https://docs.launchdarkly.com/guides/flags/technical-debt#prerequisites)Prerequisites

To complete this guide, you must have the following prerequisites:

- Proficiency and understanding of creating a feature flag in LaunchDarkly
- Knowledge of your organization’s release process

## [](https://docs.launchdarkly.com/guides/flags/technical-debt#concepts)Concepts

You should understand these concepts before you read this guide:

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#technical-debt)Technical debt

Technical debt is a concept in software development that describes the implied cost of rework required in the future because of short-term, limited solutions. It is often caused by choosing a fast, limited solution now instead of using a better approach that would take longer. A common reason for this is that necessary work must be delayed to meet a deliverable or a deadline.

As this debt accumulates, it is harder to maintain the system and code, which can impact the speed of development and efficiency of your codebase in the future.

One way technical debt can accumulate is when you fail to maintain your feature flags.

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#software-delivery-lifecycle)Software delivery lifecycle

The software delivery lifecycle (SDLC) is a process followed for a software project. The process describes how to develop, maintain, and modify software. The stages of the software delivery cycle are:

- Planning
- Analysis
- Design
- Implementation
- Testing and integration
- Maintenance

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#temporary-and-permanent-flags)Temporary and permanent flags

Flags are either temporary or permanent. A temporary flag has a limited lifespan. Once the flag has fulfilled its business purpose, remove it from the codebase. Temporary flags include flags for release management, experiments, and interoperability testing.

Permanent flags provide control for an extended time after the release of a feature. They will potentially exist for the life of a feature. Permanent flags include flags for entitlements, load shedding, custom-branding, or accessibility.

## [](https://docs.launchdarkly.com/guides/flags/technical-debt#challenges-of-technical-debt)Challenges of technical debt

Every feature should have a flag, but if you don't regularly archive flags, you can accumulate a lot of debt.

Cluttered code is harder to maintain and test. Unnecessary code remains because nobody remembers why it existed, and there is a fear that things will break if it is removed. Failure to remove flags leads to cluttered code.

Not only do you want to remove the references to the flag in your code, but you also don’t want to send evaluation settings for flags you don’t need. When you use features like Data Export to track the impact of your rollouts, your database may be overwhelmed with unnecessary event data. You don't want to transfer and store data on flags that should have been archived three months ago.

Failure to remove flags clutters your **Flags** list, as well as your code. You can’t quickly find the flag you need to toggle. This may seem like a minor inconvenience, but if you need to quickly toggle a flag's targeting off, having to scroll through hundreds of flags adds time. But cluttered code and extensive **Flags** lists aren’t the only challenges.

You also run the risk of an old flag evaluating to a state that is invalid or undesirable. When you’re rolling out a new change such as an updated user interface (UI), it is common to keep the current UI as the default version until you have confidence in the new one. Once the flag is serving 100% of contexts the new UI, the flag has reached the end of its lifecycle and should be archived. Failure to do this runs the risk of falling back to the undesired old UI if a flag gets turned off or an SDK failure results in using the fallback value.

Test the fallback values of permanent flags periodically to ensure they are up to date and delivering valid states. To learn more about fallback values, read [Change default flag values](https://docs.launchdarkly.com/home/flags/variations#change-default-flag-values).

## [](https://docs.launchdarkly.com/guides/flags/technical-debt#the-flag-lifecycle)The flag lifecycle

A flag may go through several stages over the course of its lifecycle, including:

- Live
- Ready for code removal
- Ready to archive
- Archived
- Deprecated
- Deleted

The lifecycle stage is based on what is happening across all environments. Not all flags will go through all lifecycle stages.

Flags are ready for code removal if they are temporary flags that are either not being evaluated any more ("Inactive" status), or are serving the same variation to all contexts ("Launched" status). An "Inactive" status may mean that you're no longer running the code which evaluates the flag. A "Launched" status likely means that any gradual rollout of a new feature has ended, and the feature is now live for all contexts. The flag is still evaluated every time the code is run, but because it returns the same variation for everyone, it's no longer needed. You should now either remove the flag from your code and then archive the flag, or turn the flag into a permanent flag that you can use as a circuit breaker to disable the feature entirely.

For example, consider this flag:

[![A flag with status of "Inactive" and a lifecycle stage of "Ready to archive."](https://docs.launchdarkly.com/static/1729099785499.1948812414/6af66/tech-debt-inactive.auto.png)](https://docs.launchdarkly.com/static/1729099785499.1948812414/8da59/tech-debt-inactive.auto.png)

A flag with status of "Inactive" and a lifecycle stage of "Ready to archive."

This flag’s status is "Inactive," and it is marked as "Ready to archive." No one is using the flag. You can remove it from your code and archive it.

LaunchDarkly automatically determines if a flag is ready to archive by checking the flag in all of your [critical environments](https://docs.launchdarkly.com/home/account/environment#critical-environments) for code references, age, status, and whether it is a prerequisite. You can view flags that are ready to archive from the **Flags** list. Each flag that is ready to archive has a "Ready to archive" indicator in the **Flags** list. Click the indicator to begin the archival process.

To find all flags that need code removal or are ready to archive, navigate to the **Flags** list and open the **Filters** menu. Under "Lifecycle," select **Needs code removal** or **Ready to archive**. To learn more, read [Archiving flags](https://docs.launchdarkly.com/home/flags/archive).

If you don't remove and archive flags that no one is using, they can become a form of technical debt. However, do not archive flags solely because of their status. Be sure the flag is no longer in use. To learn more, read [Flag statuses and lifecycle stages](https://docs.launchdarkly.com/home/observability/flag-status).

You may sometimes see flags on the **Flags** list that you have removed from your code, but appear to still be active. To troubleshoot this, read the LaunchDarkly Knowledge Base articles [How to investigate removed flags that appear active](https://support.launchdarkly.com/hc/en-us/articles/26504511566363-How-to-investigate-removed-flags-that-appear-active) and [Flag removed from code is still showing evaluations](https://support.launchdarkly.com/hc/en-us/articles/14030042957083-Flag-removed-from-code-is-still-showing-evaluations).

## [](https://docs.launchdarkly.com/guides/flags/technical-debt#organizational-methods-for-reducing-flag-debt)Organizational methods for reducing flag debt

This section discusses processes you can follow within your organization to reduce or eliminate flag debt.

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#create-organization-wide-naming-conventions)Create organization-wide naming conventions

A shared naming convention for your organization's flags is an effective way to eliminate debt. Flags should have understandable, intuitive names.

For example, imagine a flag named `FF123_do_not_delete_this_72`. When the developer that created the flag leaves the company, the person who takes over their work cannot necessarily tell what that flag is supposed to do. The name of that flag is too obscure to easily determine if the flag is important or not, and taking time to find the flag references in the codebase, determine the results of its variations, and calculate the impact of archiving the flag all seem less urgent than other work.

If flags do not have human-readable names, they can become technical debt.

To learn more, read [Flag conventions](https://docs.launchdarkly.com/guides/flags/flag-conventions).

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#write-useful-descriptions)Write useful descriptions

Use descriptions to add more context to the flag. Unlike flag names, you can update descriptions. They can include detailed information, such as the date the flag was last reviewed, the purpose of the flag, and more.

Descriptions are fast ways to help other account members learn what a flag does and what its impact is.

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#minimize-flag-scope)Minimize flag scope

A flag should have limited scope. Having a flag that controls more than one feature action at a time can be confusing and can make it harder to troubleshoot problems.

Imagine the smallest unit of logic needed for the most responsive flag. If there are multiple parts to a feature that have to work together, you can create a main flag with other flags dependent on it.

For example, you launch a new dashboard with three widgets. To manage them, create four flags: one flag for each widget, with a dependency on a fourth flag for the main dashboard. In this scenario, if one widget causes problems, you can disable it and still serve the dashboard with the two remaining widgets.

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#only-using-flags-where-necessary)Only using flags where necessary

You do not need to use feature flags for every change you make to your codebase. Limit the use of flags in certain situations to help manage your flag debt.

We recommend against using flags in the following scenarios:

- As a replacement for secrets management, or for targeting on secrets or credentials.
- As a replacement for configuration management.
    - Don't use feature flags with configuration that is static or rarely changes. Only use flags for this type of configuration if you need an emergency shut-off switch.
    - Don't use feature flags on configuration that, if disabled, would completely block the application from starting. For example, a database hostname or API URLs.
- As a database or file store. Instead, keep variations small and avoid complex JSON payloads where possible. Consider breaking up complex flags into smaller individual flags.
- For every commit, sprint, or other small change. Flagging very small changes is usually not worth the cost of flag upkeep. Instead, wrap features as a whole.

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#mark-flags-as-temporary)Mark flags as temporary

When you create or edit a flag, you can indicate whether or not the flag is temporary by selecting the **This is a temporary flag** checkbox on the flag's settings page.

You can also filter flags based on whether they are temporary or permanent. This can help you find flags to archive. When someone tries to archive a permanent flag, a warning appears. This can help prevent flags from being archived unnecessarily.

When you conduct a flag review, confirm the **This is a temporary flag** checkbox is unchecked for every permanent flag.

To learn more, read [Other flag settings](https://docs.launchdarkly.com/home/flags/flag-settings).

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#use-effective-tagging-conventions)Use effective tagging conventions

Tags are strings you can attach to any flag within LaunchDarkly. They help you group resources together.

You can control the spread of technical debt with tags by including a tag with a sprint designation or deploy date. When you conduct your regularly scheduled reviews, you can search for specific sprints or deploy dates.

Tag case sensitivity

Tags are case sensitive. For example, searching for `Permanent` tags and `permanent` tags will yield different results.

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#include-flags-in-your-workflows-definition-of-done)Include flags in your workflow's definition of "done"

Each company and team within an organization may have their own standards for what constitutes "done" on a task or project. Done indicates the project can be removed from the list of current tasks. For example, a team may consider the code for a task to be incomplete until it has passed automated tests.

Done means different things for different teams. A feature may be done when it rolls out to 100% of contexts, or when it rolls out to a specific set of contexts. When a feature is fully rolled out, or an experiment is ended, that's the best time to clean up the flag. When scheduling the work for rolling out a feature, include the flag cleanup work in the schedule. A feature is done when the flag is archived.

If the flag you use for a release will convert to a permanent flag, the definition of done should be when the setting on the flag changes to indicate it is permanent. You can make archiving flags part of each sprint or project end. Using this method, you'll do the work to archive the flag when the context is fresh.

To learn more about integrating flag archiving behavior into your feature development processes, read the LaunchDarkly blog article [How to use feature flags without technical debt](https://launchdarkly.com/blog/how-to-use-feature-flags-without-technical-debt/).

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#plan-to-remove-flags-during-flag-creation)Plan to remove flags during flag creation

When creating a pull request to add a flag into your code, you can also create a second pull request which removes the flag. This pull request should simply remove the flag code without other changes. This minimizes the number of conflicts to resolve even if, as often happens, the code for the new feature is updated before the rollout is finished.

The code may change before you merge the branch, but creating it gives you somewhere to start when you're ready to clean up the code. The presence of the branch also serves as a reminder to remove the flag when it's no longer needed.

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#retire-inactive-projects)Retire inactive projects

You can identify entire projects that may be inactive by the age and activity level of its flags. If no one has created new flags within the project in the last three months, and it does not contain any active permanent flags, you may be able to delete the project. To learn how, read [Delete projects](https://docs.launchdarkly.com/home/account/project#delete-projects).

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#receive-flag-removal-alerts-in-slack)Receive flag removal alerts in Slack

The LaunchDarkly Slack app can send you notifications when it’s time to remove flags from code. To learn more, read [Receive alerts when flags are ready to remove](https://docs.launchdarkly.com/integrations/slack/notifications#receive-alerts-when-flags-are-ready-to-remove).

## [](https://docs.launchdarkly.com/guides/flags/technical-debt#methods-for-reducing-flag-debt-in-launchdarkly)Methods for reducing flag debt in LaunchDarkly

LaunchDarkly provides several tools to help you reduce flag debt.

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#use-the-flag-archive-checks)Use the flag archive checks

On the **Flags** list, use the **Display** menu to show archive checks for your flags. When archive checks are selected, the **Flags** list indicates whether a flag is needs code removal or is ready to archive. You can also use the **Filter** menu to filter for flags that need code removal or are ready to archive. To learn more, read [Archiving flags](https://docs.launchdarkly.com/home/flags/archive) and [Flag statuses and lifecycle stages](https://docs.launchdarkly.com/home/observability/flag-status).

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#use-the-flag-health-metric)Use the flag health metric

Engineering insights is an Enterprise feature

Engineering insights is available to customers on an Enterprise plan. To learn more, [read about our pricing](https://launchdarkly.com/pricing/). To upgrade your plan, [contact Sales](https://launchdarkly.com/contact-sales/).

If you use engineering insights, you can use the flag health metric to help reduce flag debt. For most organizations, a lower stale flag percentage is desirable.

When you look at flag health in one environment, you might want to decrease your stale flag percentage because most stale flags represent tech debt that you need to clean up or remove.

We strongly recommend looking at flag health across environments as well. Differences in flag statuses between environments could indicate a problem. For example, if a flag is "Launched" in all but one environment and "Inactive" in the final environment, maybe you forgot to roll it out. You can use the "Select environments to compare status" feature as an opportunity to double-check your release procedures. To learn more, read [Flag health](https://docs.launchdarkly.com/home/observability/flag-health).

Here are some strategies to decrease your stale flag percentage:

- Rolling out flags in all relevant environments
- Removing or archiving flags when you're done with them
- Marking flags permanent, when it's warranted

Focusing too much on decreasing your stale flag percentage can lead to bad practices in your flag health processes. For example, you can mark a temporary flag as permanent to decrease your stale flag percentage, because only temporary flags can be stale. But most of the time, you should archive a temporary flag when it is no longer needed, not mark it as permanent.

Instead, discuss your overall goals for flag health as a team. You can talk through the flag lifecycle and decide on organizational standards for topics including naming conventions, tags, making flags permanent, and deprecating, archiving, and deleting flags.

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#deprecate-archive-and-delete-flags)Deprecate, archive, and delete flags

LaunchDarkly provides the options to deprecate, archive, and delete flags. We strongly recommend deprecating or archiving flags rather than deleting them, because an archived flag's history remains in your LaunchDarkly project. To learn how, read [Deprecating, archiving, and deleting flags](https://docs.launchdarkly.com/home/flags/archive-delete).

If you use engineering insights, you can archive flags directly from the flag health page.

Deprecate or archive flags instead of deleting them whenever possible

If you delete a flag, LaunchDarkly deletes all references to the flag, including its history. Deleting a flag also means a member could make a new flag with the same key as the old deleted flag. If this happens and the old flag's key still exists in your codebase, your code could begin referencing the wrong flag. This can have serious and unpredictable effects on your app performance.

LaunchDarkly SDKs consider archived flags "gone." When you select a flag to archive, the panel takes you through the archiving process. LaunchDarkly warns you if you try to archive a flag that is still serving variations, or that is detected in your code through code references.

A healthy project has a high ratio of archived to unarchived flags. A general guideline is that any project over three months old should have archived at least one flag. If it has not, you may want to examine your archival practices. An appropriate time-to-archive varies depending on your business needs, but a general best practice is to archive flags quarterly. This means a healthy time-to-archive is in the 90-120 day range.

Generally, a project should have fewer deleted flags than archived flags. If you have more deleted flags than archived flags, or if a project has more than ten deleted flags, you may need to review your archiving and deleting practices. You may choose to restrict who can delete flags by assigning them a custom role. To learn more, read [Custom roles](https://docs.launchdarkly.com/home/account/custom-roles).

Custom roles is an Enterprise feature

Custom roles are available to customers on an Enterprise plan. To learn more, [read about our pricing](https://launchdarkly.com/pricing/). To upgrade your plan, [contact Sales](https://launchdarkly.com/contact-sales/).

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#schedule-regular-flag-reviews)Schedule regular flag reviews

Schedule regular review cycles on a monthly or quarterly basis to identify flags to archive. Some companies dedicate sprints to tackling technical debt. If you do this, include a review of your feature flags, too.

Some teams schedule a regular "Flag Cleanup Day." In preparation, a team member produces a list of flags to be cleaned up. The list is divided up amongst the team. Then, each team member goes through their assigned flags and, for each flag, produces a patch or pull request which removes the flag from the code.

In addition to temporary flags, you should also review any permanent flags to determine that they are still necessary. As features change, the need for the flags associated with them can also change.

For example, you can filter by flags that you or your team maintain, and by the [lifecycle stage](https://docs.launchdarkly.com/home/observability/flag-status) of the flag. LaunchDarkly automatically indicates each flag that is "Ready for code removal" or "Ready to archive." You can save your list filter configurations to return to later, making it easy to regularly check for flags to archive. To learn how, read [Save shortcuts to filtered Flags lists](https://docs.launchdarkly.com/home/flags/list#save-shortcuts-to-filtered-flags-lists).

If you use engineering insights, you can also filter and archive flags from the flag health page. The stale **Flags** list shows information about flags in a selected environment that we recommend you remove.

You can use the search and filter options to refine this list into a different subset of flags:

- Search by flag key
- Filter by flag maintainer, tags, and ready to archive or needs review
- Sort by flag age

You can select additional environments to compare the flag state against. This helps you verify that you can archive the flag without unintended consequences.

[![Compare environments.](https://docs.launchdarkly.com/static/1729099785191.195811726/6af66/eng-insights-flag-health-compare-env.png)](https://docs.launchdarkly.com/static/1729099785191.195811726/0486e/eng-insights-flag-health-compare-env.png)

Compare environments.

If you choose additional environments, LaunchDarkly performs the checks again and highlights stale flags. To learn more, read [Flag health](https://docs.launchdarkly.com/home/observability/flag-health).

### [](https://docs.launchdarkly.com/guides/flags/technical-debt#use-code-references-to-find-and-remove-references-to-flags)Use code references to find and remove references to flags

Archiving a flag removes it from the **Flags** list and your app's contexts no longer encounter it.

Before you do this, remove the flag from your codebase. Code references let you quickly find where in your source code feature flags are referenced. This simplifies the process of finding code to remove in projects and files.

To access code references:

1. Navigate to the **Flags** list and find the flag you wish to remove.
2. Click the flag's name to view the flag's details.
3. Click the repository name in the "Code references" section of the right sidebar to view the flag's code references:

[![The "Code references" tab of a feature flag.](https://docs.launchdarkly.com/static/1729099785211.195811762/6af66/flag-code-references.png)](https://docs.launchdarkly.com/static/1729099785211.195811762/10c1e/flag-code-references.png)

The "Code references" tab of a feature flag.

The flag health metric also automatically verifies whether or not there are code references for your flags.

After you remove all code references mentioning that flag from the codebase and rerun the scanning tool, LaunchDarkly creates an extinction event. This event appears as a message on the **Code references** tab of the feature flag. To learn more, read [About extinction events](https://docs.launchdarkly.com/home/observability/code-references#about-extinction-events).

## [](https://docs.launchdarkly.com/guides/flags/technical-debt#conclusion)Conclusion

In this guide, you learned about:

- Challenges of technical debt
- The flag lifecycle
- Processes and features within LaunchDarkly to help control flag debt

For additional discussion on the lifecycle of a feature flag, read the ebook [Effective Feature Management](https://learn.launchdarkly.com/effective-feature-management/).