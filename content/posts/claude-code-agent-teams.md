---
id: LazyVim
aliases: []
tags:
  - claudecode
category: Tech
date: 2026-03-02
published: 2026-03-02
title: Claude Code Agent Teams 详解
---


# Claude Code Agent Teams 详解

> 基于 Anthropic 官方文档：https://code.claude.com/docs/en/agent-teams
>
> ⚠️ Agent Teams 目前是**实验性功能**，默认关闭。已知存在会话恢复、任务协调、关闭行为方面的限制。

---

## 一、什么是 Agent Teams

Agent Teams 让你协调**多个 Claude Code 实例**共同完成一项任务。

- 一个 Session 担任 **Team Lead**，负责协调工作、分配任务、汇总结果
- 其余 Session 是 **Teammates**，各自独立工作，每人有自己的 context window
- Teammates 之间可以**直接互相通信**，不必经过 Lead 中转
- 用户也可以**直接和某个 Teammate 对话**，无需通过 Lead

### 与 Subagents 的区别

| 维度 | Subagents | Agent Teams |
|------|-----------|-------------|
| 运行位置 | 单个 Session 内部 | 各自独立的 Session |
| 汇报方式 | 只能向主 Agent 汇报 | 可互相直接通信 |
| Context | 共享主 Session 的 Context | 每人独立 Context Window |
| 适用场景 | 快速、专注、独立的子任务 | 需要协调、共享发现、相互质疑的复杂任务 |

---

## 二、启用方式

```bash
# 方式1：环境变量
export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1

# 方式2：settings.json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

启用后，直接用自然语言告诉 Claude 创建团队即可，无需写配置文件：

```
Create an agent team to review PR #142.
Spawn three reviewers:
- One focused on security implications
- One checking performance impact
- One validating test coverage
Have them each review and report findings.
```

---

## 三、核心架构

### 3.1 Team Lead 的职责

- 根据你的描述创建团队和任务
- Spawn Teammates 并传入初始 prompt
- 监控和协调整体进度
- 收到 Teammate 消息后中转或响应
- 最终汇总结果

**注意**：Claude 不会在未经你确认的情况下自行创建团队。无论是你要求还是 Claude 建议，都需要你先批准。

### 3.2 Teammate 的 Context

每个 Teammate 启动时自动加载：

- 项目的 `CLAUDE.md`
- 已配置的 MCP Servers
- Skills

**不会继承**：Lead 的对话历史。Teammate 从一张"白纸"开始，只拥有 Lead 传给它的 spawn prompt。

### 3.3 权限继承

Teammates 继承 Lead 的权限设置。可以在 spawn 后为单个 Teammate 修改模式，但不能在 spawn 时指定。建议在 spawn 前在权限设置里预先批准常用操作，以减少中断。

---

## 四、共享任务看板（Shared Task List）

这是 Agent Teams 协调的核心机制之一。

### 工作原理

任务看板是一个**共享的结构化列表**，所有 Teammates 都能读写。它支持依赖追踪：

- 任务可以设置依赖（blocked by 其他任务）
- 当阻塞任务完成后，被阻塞的任务**自动解锁**（无需人工干预）
- Teammates 完成当前任务后，自主认领下一个 available 的任务

### 任务状态流转

```
pending（有依赖未完成）
    ↓ 依赖全部 completed → 自动解锁
available（可认领）
    ↓ Teammate 认领
in_progress（执行中）
    ↓ Teammate 标记完成
completed（完成）
```

### 谁控制看板

| 操作 | 执行者 |
|------|--------|
| 初始化任务列表 | Lead Agent |
| 设置任务依赖关系 | Lead Agent（初始化时） |
| 认领任务（更新 owner + status） | Teammate 自主执行 |
| 标记任务完成 | Teammate 自主执行 |
| 发现新需求时创建新任务 | Teammate 可自主扩展 |
| 监控孤儿任务（无人认领） | Lead Agent 应定期检查 |

**关键设计理念**：Lead 只负责启动，任务流转由 Teammates 自驱动。系统通过依赖关系自动解锁，不需要 Lead 实时盯着每个人的进度。

### 文件锁防竞争

任务认领底层使用**文件锁机制（file-lock based claiming）**，防止多个 Teammate 同时认领同一任务产生竞争条件。

---

## 五、Agent 间通信（Mailbox 系统）

这是 Agent Teams 与 Subagents 的最大区别。

### 通信方式

**点对点消息（message）**：发给指定 Teammate
- Teammate 的文字输出对其他成员不可见
- 必须通过消息系统主动发送，对方才能收到

**广播（broadcast）**：发给所有 Teammates
- 代价高：发给 N 个 Teammate 需要 N 条独立消息
- 推荐优先用点对点消息

**消息自动送达**：Teammate 消息自动到达 Lead，无需 Lead 主动轮询。

### 什么时候必须发消息

以下情况需要显式发消息，否则其他 Agent 不会知道：

- 某个 Teammate 完成了会影响其他人工作的发现
- 需要通知某人跳过/注意某个模块
- 请求另一个 Teammate 的状态更新

### 团队和消息存储位置

官方文档说明：**团队和任务存储在本地**（本地文件系统），具体路径由系统管理。

---

## 六、共享文件 vs 私有 Context

### 什么存在共享文件系统（所有人可见）

- 任务看板（状态、依赖、owner）
- Teammate 之间的消息（通过消息系统写入）
- 工作成果（Teammate 主动写入的输出文件，如 findings.md）
- 项目代码文件（所有人通过 Read/Write 工具访问）

### 什么存在 Teammate 自己的 Context（只有自己可见）

- 分析过程和中间推理
- 读了哪些文件的历史
- 临时思路和草稿
- 对话历史

**规则**：需要别人知道的信息 → 写文件或发消息；自己的思考过程 → 留在 Context，会话结束后消失。

---

## 七、并发运行方式（Display Modes）

Agent Teams 支持三种后端运行方式，系统自动检测最佳方式：

| 模式 | 特点 | 适用场景 |
|------|------|---------|
| **tmux**（分屏）| 每个 Teammate 显示在独立的终端窗口分栏 | 需要可视化监控 |
| **iTerm2**（分屏）| 在 iTerm2 内显示分栏 | Mac 用户 |
| **in-process**（后台）| 不显示独立窗口，最快 | 纯自动化，不需要看进度 |

```bash
# 手动指定运行模式
export CLAUDE_CODE_SPAWN_BACKEND=tmux       # 显示分屏
export CLAUDE_CODE_SPAWN_BACKEND=in-process # 后台运行（最快）
```

在 in-process 模式下，按 **Shift+Down** 可以切换查看各个 Teammate 的输出。

---

## 八、Agent Teams 专用 Hooks

除了常规 Hooks，Agent Teams 有两个专用事件：

### TeammateIdle
当某个 Teammate 即将进入空闲状态时触发。
- 以 exit code **2** 退出 → 向 Teammate 发送反馈，让它继续工作
- 用途：防止 Teammate 提前退出，确保任务继续

### TaskCompleted
当某个任务即将被标记为完成时触发。
- 以 exit code **2** 退出 → 阻止任务完成，发送反馈
- 用途：在任务关闭前做验证（如运行测试、检查输出质量）

---

## 九、Token 成本

- **每个 Teammate 有独立的 Context Window**，Token 消耗随活跃 Teammate 数量**线性增长**
- 3 个 Teammate 的团队消耗约为单 Session 的 **3-4 倍**
- 广播消息会消耗 N 倍 Token（发给 N 个 Teammate）

### 官方建议

- 从 **3-5 个 Teammate** 开始，这是效率和协调成本的最佳平衡点
- 每个 Teammate 分配 **5-6 个任务**效率最高
- 如果有 15 个独立任务，3 个 Teammate 是好的起点
- 常规任务用单 Session 更划算；只在真正需要并行协调时才用 Agent Teams

---

## 十、已知限制（官方说明）

Agent Teams 目前是实验性功能，存在以下已知问题：

- **会话恢复**：无法可靠地恢复中断的 Agent Teams 会话
- **任务协调**：在复杂依赖场景下可能出现任务协调问题
- **关闭行为**：Lead 可能在所有任务实际完成前就决定团队结束

### 遇到问题的处理方式

**Teammate 因错误停止**：用 Shift+Down 查看其输出，直接给它额外指令，或 spawn 新 Teammate 继续工作。

**Lead 提前结束**：告诉它继续，或告诉它等 Teammate 完成后再进行汇总。

**tmux Session 残留**：
```bash
tmux ls
tmux kill-session -t <session-name>
```

---

## 十一、最佳适用场景

### 推荐使用 Agent Teams

- **并行研究/审查**：多个角度同时调查同一问题（如 PR 审查：安全、性能、测试各一人）
- **竞争假设调试**：多个 Teammate 分别测试不同理论并相互质疑，避免单一 Agent 的"确认偏误"
- **跨层功能开发**：前端、后端、测试各由不同 Teammate 负责，互不干扰
- **独立模块开发**：各 Teammate 拥有独立的代码区域，不会互相覆盖

### 不推荐使用 Agent Teams（用单 Session 或 Subagents 更好）

- 顺序依赖性强的任务（A 必须在 B 之前完成）
- 需要频繁修改同一个文件
- 依赖关系复杂的工作
- 日常简单任务（成本不划算）

---

## 十二、与 Subagents 的选择原则

**一句话判断标准**（来自官方文档）：

> 你的 workers 需要互相通信吗？
> - **不需要** → 用 Subagents
> - **需要** → 用 Agent Teams

如果你在用并行 Subagents 但遇到了 Context 限制，或者 Subagents 之间需要共享信息，Agent Teams 是自然的升级路径。

---

*参考文档：https://code.claude.com/docs/en/agent-teams*
*最后更新：2026年3月*
