---
id: Reducing technical debt from feature flags

tags:
  - feature toggle
authors:
  - joey5403
category: Tech
date: "2024-10-20"
published: 2024-10-20
title: Reducing technical debt from feature flags
---

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



# 减少特性标志的技术债务

#### 阅读时间：16分钟

#### 最后编辑：2024年10月15日

## [](https://undefined/)概览

本指南提供了使用LaunchDarkly减少和消除与特性标志相关的技术债务的方法。像所有债务一样，技术债务会随着时间积累，但如果您在需要之前就建立有效的流程，就可以随着时间减轻这些债务。

在本指南中，我们将探讨：

- 技术债务的挑战
- 标志的生命周期
- 命名约定
- 使用标签
- 代码引用
- 弃用、归档和删除标志

就像特性标志应该是核心工程实践一样，解决技术债务的策略也应该是。LaunchDarkly可以通过自动识别需要代码移除或准备归档的标志来帮助您。

## [](https://undefined/)先决条件

要完成本指南，您必须具备以下先决条件：

- 熟练掌握在LaunchDarkly中创建特性标志
- 了解您组织的发布流程

## [](https://undefined/)概念

在阅读本指南之前，您应该了解以下概念：

### [](https://undefined/)技术债务

技术债务是软件开发中的一个概念，描述了由于未来需要重做的工作而产生的隐含成本，因为短期内采用了有限的解决方案。这通常是因为为了满足交付物或截止日期，必须延迟必要的工作而造成的。

随着这种债务的积累，系统和代码的维护变得更加困难，这可能会影响未来开发的速度和代码库的效率。

技术债务积累的一种方式是未能维护您的特性标志。

### [](https://undefined/)软件交付生命周期

软件交付生命周期（SDLC）是软件项目遵循的一个过程。该过程描述了如何开发、维护和修改软件。软件交付周期的阶段包括：

- 计划
- 分析
- 设计
- 实施
- 测试和集成
- 维护

### [](https://undefined/)临时和永久标志

标志要么是临时的，要么是永久的。临时标志有有限的生命周期。一旦标志实现了其业务目的，就将其从代码库中移除。临时标志包括用于发布管理、实验和互操作性测试的标志。

永久标志在功能发布后提供长时间的控制。它们可能会存在整个功能的生命期。永久标志包括用于权利、负载削减、自定义品牌或可访问性的标志。

## [](https://undefined/)技术债务的挑战

每个功能都应该有一个标志，但如果不定期归档标志，您可能会积累大量债务。

杂乱无章的代码更难维护和测试。不必要的代码仍然存在，因为没有人记得它为什么存在，并且担心如果移除它会导致问题。未能移除标志会导致代码杂乱无章。

您不仅希望从代码中移除标志的引用，还不希望发送您不需要的标志的评估设置。当您使用像数据导出这样的功能来跟踪您的发布影响时，您的数据库可能会被不必要的事件数据淹没。您不希望传输和存储应该在三个月前归档的标志的数据。

未能移除标志会使您的**标志**列表和代码变得杂乱无章。您不能快速找到需要切换的标志。这可能看起来像是一个次要的不便，但如果需要快速切换标志的目标，不得不滚动浏览数百个标志会增加时间。但是，代码杂乱和庞大的**标志**列表并不是唯一的挑战。

您还可能面临旧标志评估为无效或不理想状态的风险。当您推出新的更改，如更新的用户界面（UI）时，通常的做法是将当前UI作为默认版本，直到您对新版本有信心。一旦标志为100%的上下文服务了新UI，标志就达到了其生命周期的终点，应该被归档。未能这样做就有回退到不想要的旧UI的风险，如果标志被关闭，或者SDK失败导致使用回退值。

定期测试永久标志的回退值，以确保它们是最新的并提供有效的状态。要了解更多关于回退值的信息，请阅读[更改默认标志值](https://docs.launchdarkly.com/home/flags/variations#change-default-flag-values)。

## [](https://undefined/)标志生命周期

标志在其生命周期中可能会经历几个阶段，包括：

- 活跃
- 准备代码移除
- 准备归档
- 已归档
- 已弃用
- 已删除

生命周期阶段基于所有环境中发生的情况。并非所有标志都会经历所有生命周期阶段。

如果标志是临时标志，并且不再被评估（“非活跃”状态），或者对所有上下文提供相同的变体（“已发布”状态），则标志准备进行代码移除。“非活跃”状态可能意味着您不再运行评估标志的代码。“已发布”状态可能意味着任何新功能的逐步推出已经结束，现在该功能对所有上下文都是活跃的。标志仍然每次运行代码时都被评估，但由于它对每个人都返回相同的变体，因此不再需要。您现在应该从代码中移除标志，然后归档标志，或者将标志转换为永久标志，您可以使用它作为断路器完全禁用该功能。

例如，考虑这个标志：

[](https://undefined/)

一个状态为“非活跃”且生命周期阶段为“准备归档”的标志。

这个标志的状态是“非活跃”，并且被标记为“准备归档”。没有人使用这个标志。您可以从代码中移除它并归档它。

LaunchDarkly通过检查您的所有[关键环境](https://docs.launchdarkly.com/home/account/environment#critical-environments)中的标志、年龄、状态和是否为先决条件，自动确定标志是否准备归档。您可以从**标志**列表中查看准备归档的标志。每个准备归档的标志在**标志**列表中都有一个“准备归档”的指示器。单击指示器开始归档过程。

要找到所有需要代码移除或准备归档的标志，请导航到**标志**列表并打开**筛选器**菜单。在“生命周期”下，选择**需要代码移除**或**准备归档**。要了解更多信息，请阅读[归档标志](https://docs.launchdarkly.com/home/flags/archive)。

如果您不移除和归档没有人使用的标志，它们可能成为一种技术债务。然而，不要仅因为它们的状态就归档标志。确保标志不再被使用。要了解更多信息，请阅读[标志状态和生命周期阶段](https://docs.launchdarkly.com/home/observability/flag-status)。

有时您可能会在**标志**列表上看到您已经从代码中移除的标志，但它们似乎仍然活跃。要进行故障排除，请阅读LaunchDarkly知识库文章[如何调查看起来活跃的已移除标志](https://support.launchdarkly.com/hc/en-us/articles/26504511566363-How-to-investigate-removed-flags-that-appear-active)和[代码中已移除的标志仍然显示评估](https://support.launchdarkly.com/hc/en-us/articles/14030042957083-Flag-removed-from-code-is-still-showing-evaluations)。


###   编写有用的描述

使用描述为标志添加更多上下文。与标志名称不同，您可以更新描述。它们可以包括详细的信息，例如标志上次审查的日期、标志的目的等。

描述是帮助其他账户成员快速了解标志功能及其影响的便捷方式。

### 最小化标志范围

一个标志应该具有有限的范围。一个标志如果同时控制多个功能动作，可能会造成混淆，并且可能使得问题排查变得更加困难。

想象一下，对于最灵敏的标志所需的最小逻辑单元是什么。如果一个功能有多个部分需要协同工作，您可以创建一个主标志，并让其他标志依赖于它。

例如，您启动了一个带有三个小部件的新仪表板。为了管理它们，创建四个标志：每个小部件一个标志，以及一个依赖于主仪表板的第四个标志。在这种情况下，如果一个小部件出现问题，您可以禁用它，仍然可以用剩下的两个小部件提供仪表板服务。

### 仅在必要时使用标志

您不需要对代码库中的每个更改都使用特性标志。在某些情况下限制标志的使用，可以帮助管理您的标志债务。

我们建议不要在以下情况下使用标志：

- 作为秘密管理的替代品，或用于针对秘密或凭证的目标。
- 作为配置管理的替代品。
    - 不要将特性标志用于静态或很少更改的配置。只有在需要紧急关闭开关时，才使用标志进行此类配置。
    - 不要在禁用后会完全阻止应用程序启动的配置上使用特性标志。例如，数据库主机名或API URL。
- 作为数据库或文件存储。相反，保持变体小，并在可能的情况下避免复杂的JSON负载。考虑将复杂的标志分解为更小的单个标志。
- 对于每次提交、冲刺或其他小更改。标记非常小的更改通常不值得维护标志的成本。相反，将功能作为一个整体进行包装。

### 将标志标记为临时

当您创建或编辑标志时，可以通过在标志的设置页面上选择**这是一个临时标志**复选框来指示标志是否为临时标志。

您还可以根据标志是临时的还是永久的来过滤标志。这可以帮助您找到要归档的标志。当有人尝试归档一个永久标志时，会出现警告。这可以防止标志被不必要地归档。

当您进行标志审查时，确认每个永久标志的**这是一个临时标志**复选框未被选中。

要了解更多信息，请阅读[其他标志设置](https://docs.launchdarkly.com/home/flags/flag-settings)。

### 使用有效的标记约定

标签是您可以附加到LaunchDarkly中任何标志的字符串。它们帮助您将资源分组。

您可以通过包含带有冲刺指定或部署日期的标签来用标签控制技术债务的传播。当您进行定期审查时，可以搜索特定的冲刺或部署日期。

标签大小写敏感

标签是大小写敏感的。例如，搜索`Permanent`标签和`permanent`标签将产生不同的结果。

### 在工作流程的定义中包含标志

每个公司和组织内的团队可能都有自己的标准，以确定任务或项目何时算作“完成”。完成表示项目可以从当前任务列表中移除。例如，一个团队可能认为，除非任务的代码通过了自动化测试，否则任务的代码不完整。

对于不同的团队，“完成”意味着不同的事情。一个功能可能在它推广到100%的上下文中时算作完成，或者当它推广到特定一组上下文时算作完成。当一个功能完全推出，或者一个实验结束时，那是清理标志的最佳时机。在安排功能推广的工作时，将标志清理工作包含在计划中。当标志被归档时，一个功能就算完成了。

如果您用于发布的旗帜将转换为永久标志，则完成的定义应该是当标志设置更改以表明它是永久的时候。您可以使归档标志成为每个冲刺或项目结束的一部分。使用这种方法，当上下文新鲜时，您将完成归档标志的工作。

要了解更多关于如何将标志归档行为集成到您的功能开发流程中，阅读LaunchDarkly博客文章[如何在不产生技术债务的情况下使用特性标志](https://launchdarkly.com/blog/how-to-use-feature-flags-without-technical-debt/)。

### 在标志创建期间计划移除标志

当您创建一个拉取请求将标志添加到您的代码时，您也可以创建一个第二个拉取请求来移除该标志。这个拉取请求应该只移除标志代码，而没有其他更改。这最小化了即使通常发生的情况，即新功能代码在发布完成前更新，需要解决的冲突数量。

在您合并分支之前，代码可能会更改，但创建它为您提供了开始清理代码的起点。分支的存在也提醒您在不再需要标志时将其移除。

### 退役不活跃的项目

您可以通过标志的年龄和活动水平来识别可能不活跃的整个项目。如果在过去三个月内没有人在项目中创建新的标志，并且它不包含任何活跃的永久标志，您可能可以删除该项目。要了解如何操作，阅读[删除项目](https://docs.launchdarkly.com/home/account/project#delete-projects)。

### 在Slack中接收标志移除提醒

LaunchDarkly Slack应用程序可以在您需要从代码中移除标志时发送通知。要了解更多信息，请阅读[当标志准备好移除时接收提醒](https://docs.launchdarkly.com/integrations/slack/notifications#receive-alerts-when-flags-are-ready-to-remove)。

## 在LaunchDarkly中减少标志债务的方法

LaunchDarkly提供了几种工具，可以帮助您减少标志债务。

### 使用标志归档检查

在**标志**列表上，使用**显示**菜单显示标志的归档检查。当选择归档检查时，**标志**列表会指示标志是否需要代码移除或准备归档。您也可以使用**筛选器**菜单筛选需要代码移除或准备归档的标志。要了解更多信息，请阅读[归档标志](https://docs.launchdarkly.com/home/flags/archive)和[标志状态和生命周期阶段](https://docs.launchdarkly.com/home/observability/flag-status)。

### 使用标志健康度量

工程洞察是企业版功能

工程洞察适用于企业版计划的客户。要了解更多信息，请[阅读我们的定价信息](https://launchdarkly.com/pricing/)。要升级您的计划，请[联系销售](https://launchdarkly.com/contact-sales/)。

如果您使用工程洞察，您可以使用标志健康度量来帮助减少标志债务。对于大多数组织来说，较低的陈旧标志百分比是可取的。

当您在一个环境中查看标志健康度时，您可能希望减少您的陈旧标志百分比，因为大多数陈旧标志代表您需要清理或移除的技术债务。

我们还强烈建议查看跨环境的标志健康度。不同环境之间标志状态的差异可能表明存在问题。例如，如果一个标志在所有环境中都处于“已发布”状态，而在最后一个环境中处于“非活跃”状态，可能您忘记了将其推出。您可以使用“选择环境比较状态”功能作为双重检查您的发布程序的机会。要了解更多信息，请阅读[标志健康度](https://docs.launchdarkly.com/home/observability/flag-health)。

以下是一些减少您的陈旧标志百分比的策略：

- 在所有相关环境中推出标志
- 当您完成标志时，将其移除或归档
- 在适当的情况下，将标志标记为永久性

过分关注减少您的陈旧标志百分比可能会导致标志健康流程中的不良实践。例如，您可以将临时标志标记为永久性，以减少您的陈旧标志百分比，因为只有临时标志可以变得陈旧。但大多数情况下，当不再需要临时标志时，您应该将其归档，而不是将其标记为永久性。

相反，作为团队讨论您的标志健康总体目标。您可以讨论标志的生命周期，并为命名约定、标签、使标志永久化以及弃用、归档和删除标志等主题确定组织标准。

### 弃用、归档和删除标志

LaunchDarkly提供了弃用、归档和删除标志的选项。我们强烈建议尽可能弃用或归档标志，而不是直接删除它们，因为归档标志的历史记录会保留在您的LaunchDarkly项目中。要了解如何操作，请阅读[弃用、归档和删除标志](https://docs.launchdarkly.com/home/flags/archive-delete)。

如果您使用工程洞察功能，您可以直接从标志健康页面归档标志。

尽可能弃用或归档标志，而不是删除它们。

如果您删除了一个标志，LaunchDarkly会删除所有对该标志的引用，包括其历史记录。删除标志还意味着其他成员可以创建一个与已删除标志具有相同键的新标志。如果发生这种情况，并且旧标志的键仍然存在于您的代码库中，您的代码可能会开始引用错误的旗帜。这可能会对您的应用程序性能产生严重且不可预测的影响。

LaunchDarkly SDK将归档标志视为“已删除”。当您选择归档一个标志时，面板会带您完成归档过程。如果您尝试归档一个仍在提供变体的标志，或者通过代码引用在代码中检测到的标志，LaunchDarkly会警告您。

一个健康的项目应该有很高比例的已归档标志与未归档标志。一般准则是，任何超过三个月的项目至少应该归档一个标志。如果没有，您可能需要检查您的归档实践。适当的归档时间取决于您的业务需求，但一般最佳实践是每季度归档标志。这意味着健康的归档时间应在90-120天范围内。

通常，项目中被删除的标志数量应该少于被归档的标志数量。如果您有更多被删除的标志而不是被归档的标志，或者如果一个项目有超过十个被删除的标志，您可能需要审查您的归档和删除实践。您可以选择通过分配自定义角色来限制谁可以删除标志。要了解更多信息，请阅读[自定义角色](https://docs.launchdarkly.com/home/account/custom-roles)。

自定义角色是企业版功能

自定义角色适用于企业版计划的客户。要了解更多信息，请[阅读我们的定价信息](https://launchdarkly.com/pricing/)。要升级您的计划，请[联系销售](https://launchdarkly.com/contact-sales/)。

### 定期安排标志审查

定期安排每月或季度的标志审查周期以识别要归档的标志。一些公司会专门安排冲刺来处理技术债务。如果您这样做，请也包括对您的特性标志的审查。

一些团队会定期安排一个“标志清理日”。准备时，团队成员会制作一个要清理的标志列表。然后将列表分配给团队成员。之后，每个团队成员会处理他们分配到的标志，并为每个标志产生一个补丁或拉取请求，以从代码中移除该标志。

除了临时标志外，您还应该审查任何永久标志，以确定它们是否仍然必要。随着功能的变更，与之相关的标志的需求也可能发生变化。

例如，您可以根据您或您的团队维护的标志以及标志的[生命周期阶段](https://docs.launchdarkly.com/home/observability/flag-status)进行过滤。LaunchDarkly自动标记每个“准备进行代码移除”或“准备归档”的标志。您可以保存您的列表过滤配置以便以后返回，使定期检查要归档的标志变得容易。要了解如何操作，请阅读[保存过滤标志列表的快捷方式](https://docs.launchdarkly.com/home/flags/list#save-shortcuts-to-filtered-flags-lists)。

如果您使用工程洞察功能，您还可以从标志健康页面过滤和归档标志。陈旧的**标志**列表显示了我们建议您移除的标志在选定环境中的信息。

您可以使用搜索和过滤选项将此列表细化为不同的标志子集：

- 按标志键搜索
- 按标志维护者、标签和准备归档或需要审查进行过滤
- 按标志年龄排序

您可以选择额外的环境来比较标志状态。这有助于您验证您可以归档标志而不会产生意外后果。

[](https://undefined/)

比较环境。

如果您选择了额外的环境，LaunchDarkly会再次执行检查并突出显示陈旧的标志。要了解更多信息，请阅读[标志健康](https://docs.launchdarkly.com/home/observability/flag-health)。

### 使用代码引用查找和移除标志引用

归档一个标志会将其从**标志**列表中移除，您的应用程序上下文不再遇到它。

在这样做之前，请从您的代码库中移除该标志。代码引用让您可以快速找到源代码中引用了哪些功能标志。这简化了在项目和文件中查找要移除的代码的过程。

要访问代码引用：

1. 导航到**标志**列表并找到您希望移除的标志。
2. 单击标志的名称以查看标志的详细信息。
3. 单击右侧边栏中“代码引用”部分的存储库名称，以查看标志的代码引用：

[](https://undefined/)

功能标志的“代码引用”标签页。

标志健康度量也会自动验证您的标志是否有代码引用。

在您从代码库中移除所有提及该标志的代码引用并重新运行扫描工具后，LaunchDarkly会创建一个灭绝事件。此事件出现在功能标志的**代码引用**标签页上的消息中。要了解更多信息，请阅读[关于灭绝事件](https://docs.launchdarkly.com/home/observability/code-references#about-extinction-events)。

## 结论

在本指南中，您了解到：

- 技术债务的挑战
- 标志的生命周期
- LaunchDarkly内部帮助控制标志债务的流程和功能

有关功能标志生命周期的更多讨论，请阅读电子书[有效的功能管理](https://learn.launchdarkly.com/effective-feature-management/)。