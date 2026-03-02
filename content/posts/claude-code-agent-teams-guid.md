---
id: LazyVim
aliases: []
tags:
  - claudecode
category: Tech
date: 2026-03-02
published: 2026-03-02
title: Claude Code Agent Teams 完整指南
---



# Claude Code Agent Teams 完整指南

> 基于 Anthropic 官方文档整理  
> ⚠️ Agent Teams 目前是**实验性功能**，默认关闭，存在已知限制

---

## 目录

1. [什么是 Agent Teams](#一什么是-agent-teams)
2. [内置工具清单](#二内置工具清单)
3. [核心架构：谁负责什么](#三核心架构谁负责什么)
4. [共享任务看板](#四共享任务看板)
5. [Agent 间通信机制](#五agent-间通信机制)
6. [共享文件 vs 私有-Context](#六共享文件-vs-私有-context)
7. [TeammateTool 的 13 种操作](#七teammatetool-的-13-种操作)
8. [Hook 系统](#八hook-系统)
9. [文件存储位置](#九文件存储位置)
10. [Token 成本与建议](#十token-成本与建议)
11. [已知限制与处理方式](#十一已知限制与处理方式)
12. [何时选择 Agent Teams vs Subagents](#十二何时选择-agent-teams-vs-subagents)

---

## 一、什么是 Agent Teams

Agent Teams 让你协调**多个 Claude Code 实例**共同完成一项复杂任务。

```
用户
 ↓
Lead Agent（主协调者）
 ├── Teammate A（独立 Context）
 ├── Teammate B（独立 Context）
 └── Teammate C（独立 Context）
```

- **Lead**：创建任务、spawn 成员、监控进度、汇总结果
- **Teammates**：各自独立工作，可互相直接通信，也可与用户直接对话
- **关键**：每个 Teammate 有自己完全独立的 Context Window，互相不可见

### 与 Subagents 的区别

| 维度 | Subagents | Agent Teams |
|------|-----------|-------------|
| 运行位置 | 单个 Session 内部 | 各自独立的 Session |
| 通信方式 | 只能向主 Agent 汇报 | 可互相直接通信 |
| Context | 共享主 Session | 每人独立 |
| 适用场景 | 快速独立子任务 | 需要协调、相互质疑的复杂任务 |

**一句话选择标准**：你的 workers 需要互相通信吗？不需要 → Subagents；需要 → Agent Teams。

### 启用方式

```bash
export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1
```

---

## 二、内置工具清单

Claude Code 共有以下内置工具：

### 文件读取与导航
| 工具 | 功能 |
|------|------|
| **Read** | 读取文件内容（优于 cat/head/tail） |
| **LS** | 列出目录（优于 ls 命令） |
| **Glob** | 按模式匹配文件名，结果按修改时间排序 |
| **Grep** | 基于 ripgrep 的高性能内容搜索 |

### 文件写入与编辑
| 工具 | 功能 |
|------|------|
| **Write** | 创建或覆写文件 |
| **Edit** | 对文件指定位置做精确编辑（优于 sed/awk） |
| **MultiEdit** | 单次操作批量编辑文件多处 |

### Notebook 支持
| 工具 | 功能 |
|------|------|
| **NotebookRead** | 读取 Jupyter Notebook |
| **NotebookEdit** | 编辑 Notebook 单元格 |

### 命令执行
| 工具 | 功能 |
|------|------|
| **Bash** | 在持久 bash 会话中执行 shell 命令 |

### Web 工具
| 工具 | 功能 |
|------|------|
| **WebFetch** | 获取指定 URL 的网页内容 |
| **WebSearch** | 搜索网络获取最新信息 |

### 任务管理
| 工具 | 功能 |
|------|------|
| **TodoRead** | 读取当前会话的任务列表 |
| **TodoWrite** | 创建和更新结构化任务列表 |

### Agent 编排
| 工具 | 功能 |
|------|------|
| **Task**（Agent 工具） | 启动专注的子 Agent 完成多步骤任务 |

### 流程控制
| 工具 | 功能 |
|------|------|
| **ExitPlanMode** | 退出计划模式，开始执行 |

---

## 三、核心架构：谁负责什么

### Lead Agent 职责

- 初始化任务看板（`TaskCreate`）
- 设置任务间的依赖关系（`TaskUpdate addBlockedBy`）
- Spawn Teammates 并传入初始 prompt
- 监控整体进度，处理孤儿任务
- 最终汇总结果

**重要**：Lead 只负责"启动蓝图"，不实时管理每个人。任务流转由 Teammates 自驱动。

### Teammate 职责

- 启动后读取任务看板，认领 available 任务
- 执行工作，把成果写入共享文件
- 标记任务完成
- 发现新需求时可自主创建新任务（动态扩展）
- 向其他 Agent 发消息通报关键信息

### Spawn 是什么

Spawn = 创建并启动一个新的独立进程。每个被 spawn 出来的 Teammate：

1. 是一个全新的 Claude 模型实例
2. 拥有空白的、独立的 Context Window（不继承 Lead 的对话历史）
3. 自动加载项目 `CLAUDE.md`、MCP Servers、Skills
4. 启动后独立运行，父子之间只通过文件系统和消息通信

---

## 四、共享任务看板

### 任务状态流转

```
pending（有未完成依赖）
    ↓ 所有依赖 completed → 自动解锁（无需人工干预）
available（可认领）
    ↓ Teammate 认领
in_progress（执行中）
    ↓ Teammate 标记完成
completed（完成）
```

### 依赖关系设置

```javascript
TaskCreate({ id: "1", subject: "安全审查" })
TaskCreate({ id: "2", subject: "性能审查" })
TaskCreate({ id: "3", subject: "汇总报告" })

// #3 依赖 #1 和 #2，两者都完成后 #3 自动解锁
TaskUpdate({ taskId: "3", addBlockedBy: ["1", "2"] })
```

### 防竞争机制

任务认领底层使用**文件锁（file-lock based claiming）**，防止多个 Teammate 同时认领同一任务。

### 孤儿任务问题

如果某个 Teammate 意外退出（Context 耗尽、进程崩溃），它负责的任务会变成"孤儿"（available 但无人认领）。**生产级设计**中，Lead Agent 应定期轮询任务看板，发现孤儿任务后：

- 自己认领并执行
- 或重新 spawn 新 Teammate 接手
- 可配合任务超时机制自动重置 in_progress 状态

---

## 五、Agent 间通信机制

### 核心原则

> Teammate 的文字输出对其他团队成员**不可见**。必须通过消息系统主动发送，对方才能收到。

### 通信方式

**点对点消息**（SendMessage operation: "message"）
```javascript
SendMessage({
  operation: "message",
  target: "security-reviewer",
  content: "支付模块第143行有注入风险，你分析性能时先跳过这个函数"
})
```

**广播**（SendMessage operation: "broadcast"）
- 发给所有 Teammates
- 代价高：N 个 Teammates = N 条独立消息
- 推荐优先用点对点

**关闭协商**
```javascript
SendMessage({ operation: "shutdown_request", target: "agent-b", reason: "任务完成" })
SendMessage({ operation: "rejectShutdown", request_id: "xxx", reason: "还有任务未完成" })
```

### 通信本质

通信底层是**异步消息传递**（写入文件系统的收件箱）+ **共享任务状态**，不是实时直连。类比：异步工作的远程团队用 Slack + 共享 Jira 看板协作。

---

## 六、共享文件 vs 私有 Context

```
┌─────────────────────────────────────────────────┐
│              文件系统（所有人可读写）              │
│  任务看板   ~/.claude/tasks/{team}/tasks.json   │
│  消息收件箱 系统管理                             │
│  工作成果   Agent 主动写入的输出文件              │
│  项目代码   所有人通过 Read/Write 工具访问        │
└─────────────────────────────────────────────────┘

┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  Agent A     │  │  Agent B     │  │  Agent C     │
│  私有Context │  │  私有Context │  │  私有Context │
│  · 分析过程  │  │  · 分析过程  │  │  · 分析过程  │
│  · 中间推理  │  │  · 中间推理  │  │  · 中间推理  │
│  · 临时思路  │  │  · 临时思路  │  │  · 临时思路  │
│  ← 不可见 → │  │  ← 不可见 → │  │  ← 不可见 → │
└──────────────┘  └──────────────┘  └──────────────┘
```

**规则**：需要别人知道的 → 写文件或发消息；自己的思考过程 → 留在 Context，消失就消失。

---

## 七、TeammateTool 的 13 种操作

最新版本将操作拆分到多个工具：

### Teammate 工具（团队生命周期）
| 操作 | 功能 |
|------|------|
| `spawnTeam` | 创建新团队，启动 Teammates |
| `cleanup` | 关闭所有 Teammate，释放资源 |

### SendMessage 工具（通信）
| 操作 | 功能 |
|------|------|
| `message` | 点对点发消息给指定 Agent |
| `broadcast` | 广播给所有 Agent |
| `shutdown_request` | 请求某 Agent 关闭 |
| `rejectShutdown` | 拒绝关闭请求 |
| `plan_approval_response` | 批准/拒绝执行计划 |

### Task 工具系列（共享任务板）
| 操作 | 功能 |
|------|------|
| `TaskCreate` | 创建新任务 |
| `TaskUpdate` | 更新状态/owner/依赖 |
| `TaskList` | 列出所有任务（Agent 用此认领工作） |
| `TaskGet` | 获取单个任务详情 |

### 其他
| 操作 | 功能 |
|------|------|
| `discoverTeams` | 发现现有团队 |
| `requestJoin` | 请求加入团队 |
| `approveJoin` | 批准加入请求 |

---

## 八、Hook 系统

Hook 是写在本地的脚本，在 Agent 执行特定动作时**自动触发**。

### 全部 Hook 事件

| Hook | 触发时机 | 特点 |
|------|---------|------|
| **PreToolUse** | 工具执行之前 | **唯一能阻止操作的 Hook** |
| **PostToolUse** | 工具执行之后 | 格式化、记录、测试 |
| **UserPromptSubmit** | 用户提交消息时 | 校验、增强输入 |
| **PermissionRequest** | Agent 请求权限时 | 自动批准/拒绝 |
| **Stop** | 主 Agent 完成响应时 | 验证、发通知 |
| **SubagentStop** | 子 Agent 完成时 | 收集子 Agent 结果 |
| **SessionEnd** | 会话终止时 | 清理、归档 |
| **Setup** | 项目初始化/维护时 | 配置环境 |
| **TeammateIdle** | Teammate 将进入空闲时 | exit 2 → 让它继续工作 |
| **TaskCompleted** | 任务将被标记完成时 | exit 2 → 阻止完成，先验证 |

### 三种 Hook 处理器类型

```json
{ "type": "command", "command": "npx prettier --write" }
{ "type": "prompt",  "prompt": "判断这个命令是否影响生产环境: $ARGUMENTS" }
{ "type": "agent",   "prompt": "检查修改的文件是否有对应测试" }
```

### 配置示例

```json
// ~/.claude/settings.json
{
  "hooks": {
    "PreToolUse": [{
      "matcher": "Bash",
      "hooks": [{ "type": "command", "command": "python3 ~/.claude/hooks/safety_check.py" }]
    }],
    "PostToolUse": [{
      "matcher": "Write",
      "hooks": [{ "type": "command", "command": "npx prettier --write $FILE" }]
    }],
    "Stop": [{
      "hooks": [{ "type": "command", "command": "python3 ~/.claude/hooks/verify_done.py" }]
    }]
  }
}
```

### Hook 数据流

```
Agent 准备执行工具
    ↓
工具参数通过 stdin 传给 Hook 脚本
    ↓
Hook 脚本运行（可读文件、写文件、调 API）
    ↓
stdout 输出 → Agent 读入自己的 Context
exit 0 → 继续执行
exit 1 → 阻止执行（仅 PreToolUse）
exit 2 → 发送反馈让 Agent 继续（TeammateIdle/TaskCompleted）
```

---

## 九、文件存储位置

### 全局目录 `~/.claude/`

```
~/.claude.json                          # 全局配置（项目映射、MCP设置）
~/.claude/
├── settings.json                       # 全局设置（hooks、权限）
├── projects/                           # 会话对话记录（JSONL格式）
│   └── -Users-你-项目名/
│       └── *.jsonl                     # 每行一条消息，实时写入
├── todos/                              # TodoWrite 写入的任务
│   └── {session-id}-*.json
├── plans/                              # Plan Mode 生成的计划
├── skills/                             # 全局 Skills
├── commands/                           # 全局自定义命令
├── teams/                              # Agent Teams 配置
│   └── {team-name}/
│       └── config.json                 # 团队成员、权限
└── tasks/                              # Agent Teams 任务看板
    └── {team-name}/
        ├── tasks.json                  # 共享任务状态（所有Agent读写）
        └── *.lock                      # 文件锁（防并发竞争）
```

### 项目级目录 `.claude/`（在项目根目录）

```
你的项目/
└── .claude/
    ├── settings.json                   # 项目共享设置（可提交 git）
    ├── settings.local.json             # 本机私有设置（gitignore）
    ├── CLAUDE.md                       # 项目说明，每次会话自动注入
    ├── agents/                         # Subagent 定义
    ├── commands/                       # 自定义 /命令
    ├── skills/                         # 项目级 Skills
    └── hooks/                          # Hook 脚本
```

### 关键设计细节

会话数据用 **JSONL 格式**存储：每条消息是独立的一行，生成后立即写入磁盘。即使程序崩溃，只有最后一条未完成的消息可能丢失，之前全部保留。

---

## 十、Token 成本与建议

- 每个 Teammate 有独立 Context Window，Token 消耗随 Teammate 数量**线性增长**
- 3 个 Teammate ≈ 单 Session 的 3-4 倍 Token 消耗
- 广播消息消耗 N 倍 Token

**官方建议**：

- 从 **3-5 个 Teammate** 开始
- 每个 Teammate 分配 **5-6 个任务**效率最高
- 有 15 个独立任务 → 3 个 Teammate 是好的起点
- 日常任务用单 Session；只在真正需要并行协调时才用 Agent Teams

---

## 十一、已知限制与处理方式

| 问题 | 处理方式 |
|------|---------|
| Teammate 意外停止 | 用 Shift+Down 查看输出，直接给它指令，或 spawn 新 Teammate 接手 |
| Lead 提前结束 | 告诉它继续，或让它等 Teammates 完成后再汇总 |
| tmux Session 残留 | `tmux ls` 查看，`tmux kill-session -t <name>` 清理 |
| 会话无法恢复 | 已知限制，实验性功能阶段暂无完整解决方案 |

---

## 十二、何时选择 Agent Teams vs Subagents

### 推荐使用 Agent Teams

- **并行审查**：安全、性能、测试三个角度同时审查同一 PR
- **竞争假设调试**：多个 Teammate 分别测试不同理论并互相质疑
- **跨层功能开发**：前端、后端、测试各自独立负责
- **独立模块开发**：各 Teammate 有独立代码区域，互不覆盖

### 不推荐使用 Agent Teams

- 顺序依赖性强的任务（A 必须在 B 之前完成，且无并行空间）
- 需要频繁修改同一个文件
- 日常简单任务（成本不划算）

---

*参考：[Anthropic 官方文档](https://code.claude.com/docs/en/agent-teams)*
