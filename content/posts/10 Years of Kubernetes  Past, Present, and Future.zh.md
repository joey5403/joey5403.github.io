---
title: 十年Kubernetes：过去、现在和未来
image: https://img.joeyzheng.tech/ob-1748506572250.png-30
date: 2024-12-30
published: 2024-12-30
tags:
  - architect
category: Tech

---


# 十年Kubernetes：过去、现在和未来
翻译自[https://thenewstack.io/10-years-of-kubernetes-past-present-and-future/](https://thenewstack.io/10-years-of-kubernetes-past-present-and-future/)

Matt Butcher 回顾了事情的起点，Kubernetes走向成熟的历程，以及它在WebAssembly运动中的潜力。

2024年6月12日上午10:00 由 [Matt Butcher](https://thenewstack.io/author/mattbutcher/ "Posts by Matt Butcher") 撰写

今年，[Kubernetes](https://thenewstack.io/kubernetes/) 迎来了它的十岁生日。作为一个从社区早期就参与其中的开发者，我不禁回顾了Kubernetes的起点，如何走向成熟，以及它现在在[WebAssembly](https://thenewstack.io/4-big-developments-in-webassembly/) 运动中的潜力。

由于我是Taylor Swift的粉丝，我把这些回忆分成了几个时代，以致敬我最喜欢的音乐家。

## 时代一：Kubernetes的简易时代

最初，有 [Borg](https://research.google/pubs/large-scale-cluster-management-at-google-with-borg/)。我在2010年代初在Google工作了一段时间，然后离开了，加入了一个名为Deis的PaaS创业公司。我在Google的Nest部门工作（制造恒温器和烟雾报警器的部门）。与Google的其他部门不同，Nest当时使用Apache Mesos和Apache Zookeeper来协调其VM。然而，我也使用AppEngine构建了一个内部应用程序。通过此，我接触到了Google内部的LXC容器调度程序。Borg非常强大，它全球扩展，需要数百名工程师来维护。我一度想过加入Borg团队中的一个，最终选择了离开，去Deis构建一个开放源码的替代品。

Deis是[Docker](https://thenewstack.io/ebooks/docker-and-containers/the-docker-container-ecosystem/) 容器领域的早期进入者。团队成员参与了Docker网络架构的开发，并对CoreOS的工具进行了大量贡献。但我们正在寻找一个强大的编排系统来简化我们的PaaS调度代码。当 [Google将Kubernetes开源](https://thenewstack.io/a-kubernetes-documentary-shares-googles-open-source-story/)时，我非常激动。这里有所有Borg的好处，但包装更简洁。

简洁，这是当时我用来形容Kubernetes的词。

它是**简洁**的，因为与其描述一个生命周期或一组程序指令，我只需**声明**应该运行什么。Kubernetes接收这个声明并实现它。

它是简洁的，因为不需要编写代码，我只需写几行YAML（当时确实只有几行）。然后我只需使用一个简单的CLI上传那些YAML。

它是简洁的，因为只有几种Kubernetes对象。每天我都只需要用到Pods, ReplicationControllers, Services和Secrets。

在Deis，我们重构了整个PaaS平台，建立了Helm并创作了《儿童图解Kubernetes指南》。在容器生态系统中，我们都在快速行动（和破坏东西）。我仍然记得Kubernetes团队宣布可以运行 [1000节点集群](https://kubernetes.io/blog/2016/03/1000-nodes-and-beyond-updates-to-kubernetes-performance-and-scalability-in-12/) 的那一天。第一次KubeCon可以容纳在一个酒店的宴会厅里。CNCF作为Kubernetes知识产权的中立管理者成立。当[Brendan Burns](https://www.linkedin.com/in/brendan-burns-487aa590/)离开Google加入微软创建一个专门的Kubernetes团队时，我确信生态系统已经跨越了一个重要的门槛。

Kubernetes即将飞速成功。

## 时代二：成长的痛苦和收获

虽然从某种意义上说，Kubernetes早期的稀疏和简化是有吸引力的，但它也是有局限的。要在生产环境中运行微服务，还需要其他特性。ReplicationControllers被ReplicaSets取代，ReplicaSets又促成了Deployments, DaemonSets, StatefulSets等更高层级的控制特性。ConfigMaps加入了Secrets，存储系统也得到了成长和成熟。自动缩放器，作业，RBAC等进入了Kubernetes核心。第三方资源让位给了更灵活的自定义资源描述（CRDs）。CRDs现在已经成为扩展Kubernetes资源（类）系统的标准方式。

曾经简单的系统很快变得复杂起来，但这是必要的。如果Kubernetes要像曾经仅限于Borg的编排那样普及，它需要支持各种配置、用例和安全策略。

不仅仅是技术上的变化，Kubernetes周围的生态系统也在变化。CNCF成长为一个全面的、广泛的基金会。从TOC到SIGs再到TAGs，以及项目的孵化、沙箱和毕业的严谨结构，CNCF增添了生态系统所需的严谨性。至于Helm，我们“离开”了Kubernetes项目（曾是一个子项目），成为最早的CNCF沙箱项目之一，这使我们拥有了自己的发布节奏、构建基础设施和治理政策。这一切都是在CNCF蓬勃发展的过程中得以实现的。容器运行时的动荡导致了开放容器计划（OCI）的创建，OCI已经发展成一个保护容器规范核心的标准组织。

在当时，每一个变化都感觉是动荡的。我们都意识到，如果Kubernetes赢得当时称为“编排战争”，还有很长的路要走。Apache Mesos, CoreOS Fleet, Docker Swarm和HashiCorp Nomad都在[与Kubernetes一争高下](https://thenewstack.io/configuration-management-orchestration/)。即使Mesos是当时的垄断者，Kubernetes在技术和社区增长方面都超越了它（及其他）。声明式配置的思想引起了积极的共鸣，很快Kubernetes在一家公司接一家公司中出现。

## 时代三：稳定性与创新

每一个成功的开源项目都会遇到一个时刻，那就是功能开发的压力与稳定性的需求正面交锋。项目早期，开发者可以为了改进进行破坏性更改，用户接受甚至支持这种做法。在这些早期阶段，我们渴望改进，即便意味着烦人的迁移。

但当软件对于组织的运作变得至关重要时，对破坏性更改的容忍度会减少。稳定性是一个原因，因为破坏性更改会导致代价高昂的停机。另外，当更多公司、团队和项目加入这一技术时，每次软件新版本发布时重构所有工作负载变得集体昂贵（在金钱和时间上）。

Kubernetes，Helm等项目开始优先考虑稳定性而非速度。虽然这引起了许多想要合并和发布其功能的工程师的抱怨，但它巩固了Kubernetes在企业中的地位。

然而这种做法的一个缺点是，当添加新功能时，不能破坏现有的行为。这更为复杂。Kubernetes的代码库增大，YAML清单格式变得更加冗长。Helm开发早期，我们遇到了Kubernetes内部的一个有趣限制：任何一个Kubernetes清单的最大大小是1M。以比尔·盖茨的方式，我评论道，“谁会需要一个一兆的Helm图谱？这不就是YAML文件吗？”但随着Kubernetes YAML的复杂性增加，以及Helm的功能也变得更加复杂，我们打破了1M的限制。我们添加了图谱压缩，但几年后又再度遇到了限制。有一天在LinkedIn上，我看到一个工程师的职位标题是“Helm图谱开发者”。震惊之余，我意识到，即使我当初打造Helm时认为它是一个简洁的系统，它也已成长为一个复杂的工具，需要工程师培养特定技能。

2019年，我开始担忧Kubernetes会成长为一个庞大的项目，甚至那些参与其中的人也难以理解。即使一度存在这种风险，我们似乎安全地度过了这一问题。感谢技术领导层，Kubernetes设定了新的航向。开发者们不再专注于添加一个又一个功能，而是专注于构建扩展机制。稳健的CRD模式出现了。控制平面变得更加灵活。随着企业功能如策略控制固化，它们以允许各种扩展点的方式进行简化。简而言之，Kubernetes通过允许他人选择在哪里忍受附加组件的复杂性来避免内部复杂性。

这一举措拯救了Kubernetes，并为超越容器的未来奠定了基础。

## 时代四：未来是Wasm

Kubernetes的一个关键灵活点是容器运行时。Kubernetes曾经要求Docker守护进程，现在仅需与Kubernetes生命周期期望一致的调度系统。Containerd、CRI-O等低级容器工具将一度单片的容器运行时分解为功能单元。这是通往未来的门口。

WebAssembly ——简称Wasm（发音与“awesome”押韵）——最初是一种设计用于在网络浏览器中运行的字节码格式，伴随JavaScript一起。这一承诺是更强大的客户端编程。通过Wasm，我们可以编译旧的C库，然后从JavaScript中访问它们。我们可以将高性能特性如向量数学委托给比JavaScript更适合的语言。而这一切都在一个安全的沙盒中，甚至保护JavaScript运行时免受恶意字节码的影响。

2018年，我在微软的团队一部分时间维护Helm, Brigade等CNCF项目，另一部分时间尝试解决容器生态系统中的新问题。我们非常想解决一个问题，涉及无服务器函数（如AWS Lambda）。我们清楚以下两点：

- 现有的无服务器函数底层技术并不理想。虚拟机和容器的设计假设是来宾工作负载会运行数小时、数天或数月。启动时间不是一个巨大考量，因为启动相对不频繁。
- 最受欢迎的无服务器函数实现（AWS Lambda、Azure Functions、CloudFlare Workers等）由大型公司运营，运行在Kubernetes外部。

第二点，我们在微软经常听说，对那些标准化Kubernetes的企业来说是一个恼人的问题。如一位平台工程师对我说,“我们有一个漂亮且安全的Kubernetes集群托管我们的服务器工作负载，还有这个拼凑出来的策略控制、服务和流程混搭的怪物来支持我们的AWS Lambdas。”

WebAssembly几乎没有风险（也没有理由）取代容器。WebAssembly的优点，如快速启动时间、小巧的二进制文件和快速执行，非常适合无服务器工作负载，没有长时间运行的服务器过程。但这些都不能使WebAssembly显然更适合通常封装在容器中的长时间运行服务器过程。相反，事实是：目前，很少有服务器可以编译为WebAssembly而无需对代码（或WebAssembly运行时本身）进行重大更改。

当涉及到无服务器函数时，WebAssembly亚毫秒冷启动、接近本机的执行速度和强壮的安全沙盒使它成为理想的计算层。

如果WebAssembly不会**取代**容器，那么我们的设计目标应是**补充**容器。在Kubernetes内部运行WebAssembly应涉及与现有Kubernetes功能的最深入集成。这就是 [SpinKube](https://www.spinkube.dev/) 的作用。由微软、Fermyon、Liquid Reply、SUSE等公司创建的一组开源工具，SpinKube直接将WebAssembly支持插入到Kubernetes。一款WebAssembly应用可以使用秘密、配置映射、卷挂载、服务、附加容器、网状等。这是开箱即用的。不仅如此，容器和WebAssembly可以在同一个Pod中并排运行。一个应用可以拥有一个长时间运行的服务器进程在一个容器中运行，还有一堆WebAssembly附加容器以无服务器函数的形式运行。前所未有地，可以在一个操作单元中无缝混合无服务器和服务器工作负载。

由于WebAssembly需要的系统资源要少得多，Kubernetes集群中的一个节点可以运行数百甚至数千个WebAssembly应用。虽然你的集群可能永远不需要那么多，但有了这些轻巧的应用，你肯定会从你的Kubernetes集群中获得更多价值，因为你集群所需的计算能力（因此集群成本）会大幅减少。

这段故事令人印象深刻的是，Kubernetes本身是WebAssembly大获成功的原因。过去几年为使Kubernetes具备可扩展性、可插拔性和高度可配置性所做的努力在这里得到了回报，因为即便一个全新的运行时也可以与默认的容器运行时并肩工作！

## 超越原本的目的

正如我之前所说，简要看一下软件教会了我们项目演变的一些深刻东西。好的软件项目会达成其原始设计初衷。伟大的项目则会超越这些初衷。TCP/IP最初仅用于美国政府沟通。HTML被设计为传输物理学论文。JavaScript用于弹出浏览器警报并与Java Applet通信。

从其创建之初，Kubernetes社区就对我们共同构建的东西有[明确的理解](https://web.archive.org/web/20151216232631/http://kubernetes.io/)：

Kubernetes是一个开源的Docker容器编排系统。它负责计算集群上节点的调度并主动管理工作负载以确保它们的状态与用户声明的意图匹配。通过“标签”和“Pod”的概念，它将组成应用程序的容器分组为逻辑单元以便于管理和发现。

项目确实达成了那个早期目标，现在已经超越了。

Kubernetes曾是Docker编排器。WebAssembly曾是浏览器运行时。两者正在我们眼前超越其原始设计。每个都展示了其作为伟大技术的潜质。两者结合将带来分布式计算的新视野。

Matt Butcher 是Fermyon的联合创始人兼CEO，Fermyon是一个WebAssembly云公司。Matt是Helm, Brigade, CNAB, OAM, Glide和Krustlet的原始创建者之一。他撰写并合作撰写了许多书籍，包括《Learning Helm》和《Go in Practice》。他是《儿童图解Kubernetes指南》系列的共同作者。这些天，他主要从事WebAssembly项目，如Spin, Fermyon Cloud和Bartholomew。他拥有哲学博士学位，居住在科罗拉多州。

[链接](https://www.linkedin.com/in/mattbutcher/)

[链接](https://www.linkedin.com/in/mattbutcher/)
