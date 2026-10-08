# Agent Harness Landscape

A curated landscape of agent harnesses for software development: projects, problems solved, architectures, and comparisons.

面向软件开发智能体的开源项目调研：从**解决什么问题**出发，整理执行内核、长周期交付编排、运行基础设施，以及验证与评测工具。

当前收录 **30 个项目**，按主功能分为 **4 类**。初始整理与本轮仓库状态核对日期：**2026-10-08**。

## 调研范围

这里的 Agent Harness 指模型周围支撑实际执行的机制，包括工具调用、上下文与记忆、任务状态、控制循环、交接、验证和恢复。

本清单也收录与 harness 配套的基础设施、技能框架、观测工具和评测集。分类是本仓库的调研视角；一个项目可能同时覆盖多个类别，当前按主要职责归类。

## 项目总览

| 类别 | 关注的问题 | 数量 |
| --- | --- | ---: |
| 编码智能体与执行内核 | 如何让智能体读取、修改和运行代码 | 7 |
| 长周期交付、任务连续性与多智能体编排 | 如何让工作跨会话持续推进，并协调多个执行者 | 11 |
| 持久执行与隔离环境基础设施 | 如何保存运行状态、恢复工作及提供隔离环境 | 4 |
| 开发流程、验证、评测与观测 | 如何检查过程与结果，并分析可靠性 | 8 |

## 1. 编码智能体与执行内核

解决“智能体怎样读取代码、修改文件、调用工具并执行开发任务”。

| 解决什么问题 | 项目名称 | GitHub 仓库 | 项目形态 / 备注 |
| --- | --- | --- | --- |
| 需要精简、容易扩展的编码智能体内核，方便自行修改工具、提示词和工作方式。 | Pi | [earendil-works/pi](https://github.com/earendil-works/pi) | 可扩展 harness / CLI / SDK |
| 需要可选择模型的开源编码智能体，在终端或桌面中读取、修改和运行项目。 | OpenCode | [anomalyco/opencode](https://github.com/anomalyco/opencode) | 编码智能体 |
| 需要让编码智能体在本地代码仓库中执行开发任务。 | Codex CLI | [openai/codex](https://github.com/openai/codex) | 编码智能体 |
| 需要一个可连接模型和工具扩展的本地智能体，执行代码与其他工作流。 | Goose | [aaif-goose/goose](https://github.com/aaif-goose/goose) | 通用智能体 / 开发工具 |
| 需要让模型自主定位软件问题、修改代码并产出补丁。 | SWE-agent | [SWE-agent/SWE-agent](https://github.com/SWE-agent/SWE-agent) | 研究型编码智能体；主要开发已转向 mini-swe-agent |
| 需要容易理解、改造和评测的最小编码智能体，减少运行框架复杂度。 | mini-SWE-agent | [SWE-agent/mini-swe-agent](https://github.com/SWE-agent/mini-swe-agent) | 最小编码智能体 / 研究基线 |
| 需要可组合的软件智能体组件，构建自己的工具、会话和开发体验。 | OpenHands Software Agent SDK | [OpenHands/software-agent-sdk](https://github.com/OpenHands/software-agent-sdk) | SDK / 智能体执行组件 |

## 2. 长周期交付、任务连续性与多智能体编排

解决“任务跨会话继续推进、多个智能体协作，以及交付如何结束和恢复”。

| 解决什么问题 | 项目名称 | GitHub 仓库 | 项目形态 / 备注 |
| --- | --- | --- | --- |
| 长周期交付中，目标漂移、交接丢失、失败重试和未经验证的完成声明难以控制；需要任务契约、独立验证、完成门禁与受控恢复。 | ZaoFu / 造父 | [uisee-ai/zaofu](https://github.com/uisee-ai/zaofu) | 交付控制平面；Developer Preview |
| 需要将项目任务持续转换成隔离的自主执行运行，管理分配、重试和工作区。 | Symphony | [openai/symphony](https://github.com/openai/symphony) | 任务编排服务 / 规范 / 原型 |
| 一次上下文无法完成全部需求，需要以新会话反复执行，并用 Git 和文件保存进度。 | Ralph | [snarktank/ralph](https://github.com/snarktank/ralph) | 持续执行循环 |
| 智能体重启会丢失任务与依赖关系，需要持久化工作图，并找出当前可执行的任务。 | Beads | [gastownhall/beads](https://github.com/gastownhall/beads) | 依赖感知的任务状态与工作图 |
| 多个编码智能体同时工作时，工作区、身份、消息、任务和交接容易混乱。 | Gas Town | [gastownhall/gastown](https://github.com/gastownhall/gastown) | 多智能体工作区与编排系统 |
| 构建自定义多智能体编排系统时，需要复用运行提供者、工作路由、监督与声明式配置。 | Gas City | [gastownhall/gascity](https://github.com/gastownhall/gascity) | 编排构建 SDK |
| 需求文档太大，难以直接执行，需要拆成可跟踪、可继续细分且有依赖的任务。 | Task Master | [eyaltoledano/claude-task-master](https://github.com/eyaltoledano/claude-task-master) | 任务管理 / 需求拆解 |
| 仓库维护需要按事件或计划触发智能体，让 GitHub 工作流执行自然语言定义的任务。 | GitHub Agentic Workflows | [github/gh-aw](https://github.com/github/gh-aw) | GitHub 工作流工具 |
| OpenHands 运行需要按计划或 webhook 触发，并管理调度、运行历史与沙箱生命周期。 | OpenHands Automation | [OpenHands/automation](https://github.com/OpenHands/automation) | 自动化调度服务 |
| 多步骤智能体需要现成的规划、子智能体、文件系统、持久记忆和上下文管理能力。 | Deep Agents | [langchain-ai/deepagents](https://github.com/langchain-ai/deepagents) | 通用长任务 harness |
| 长时间运行的智能体可能重复消耗上下文、空转或丢失有效进度，需要外部监督、状态交接与停止机制。 | LongHorizonOS | [Yang-Jiashu/LongHorizonOS](https://github.com/Yang-Jiashu/LongHorizonOS) | 长任务监督与状态层；实验项目 |

## 3. 持久执行与隔离环境基础设施

解决“执行状态如何保存、故障后怎样继续，以及代码在哪里运行”。

| 解决什么问题 | 项目名称 | GitHub 仓库 | 项目形态 / 备注 |
| --- | --- | --- | --- |
| 多步骤智能体流程需要保存状态、设置检查点、等待人工输入并恢复执行。 | LangGraph | [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) | 有状态图运行时 |
| 智能体工作流需要持久化运行，让调用失败可重试、人工审批后可继续，并避免重放时重复模型调用。 | Temporal × OpenAI Agents | [temporalio/samples-typescript](https://github.com/temporalio/samples-typescript) | 集成示例；位于 openai-agents/ |
| AI 生成的代码需要在可创建、控制和销毁的隔离云沙箱中运行。 | E2B | [e2b-dev/E2B](https://github.com/e2b-dev/E2B) | 代码执行沙箱基础设施 |
| 智能体需要隔离的开发环境、环境生命周期管理和持久化快照。 | Daytona | [daytonaio/daytona](https://github.com/daytonaio/daytona) | 沙箱基础设施；该公开仓库已归档 |

## 4. 开发流程、验证、评测与观测

解决“怎样约束开发过程、验证交付、衡量能力，以及理解运行失败”。

| 解决什么问题 | 项目名称 | GitHub 仓库 | 项目形态 / 备注 |
| --- | --- | --- | --- |
| 编码智能体容易跳过需求澄清、设计、测试和复核，需要可复用的开发技能与方法。 | Superpowers | [obra/superpowers](https://github.com/obra/superpowers) | 技能框架 / 开发方法 |
| PR 增多后，人工难以及时完成初步审查、变更说明和改进建议。 | PR-Agent | [The-PR-Agent/pr-agent](https://github.com/The-PR-Agent/pr-agent) | PR 审查工具；社区维护版本 |
| 多次智能体运行可能互相矛盾，也可能一致犯错，需要主动从环境中取证、验证并修订结果。 | VeriHarness | [google-research/veriharness](https://github.com/google-research/veriharness) | 验证 harness；研究项目 |
| 需要用真实 GitHub 问题和测试，衡量智能体能否修复软件缺陷。 | SWE-bench | [SWE-bench/SWE-bench](https://github.com/SWE-bench/SWE-bench) | 软件工程评测集与评测工具 |
| 需要更困难、跨度更长的软件工程任务，衡量智能体处理复杂代码修改的能力。 | SWE-bench Pro | [scaleapi/SWE-bench_Pro-os](https://github.com/scaleapi/SWE-bench_Pro-os) | 长周期软件工程评测集 |
| 需要衡量智能体能否根据高层软件需求，持续演进复杂代码库。 | SWE-EVO | [SWE-EVO/SWE-EVO](https://github.com/SWE-EVO/SWE-EVO) | 软件演进评测集 |
| 智能体调用过程难以追踪，需要关联轨迹、成本、反馈、提示词和评估结果。 | Langfuse | [langfuse/langfuse](https://github.com/langfuse/langfuse) | LLM / 智能体观测与评估 |
| 需要查看智能体调用轨迹，分析失败并运行评估，支持持续改进。 | Phoenix | [Arize-ai/phoenix](https://github.com/Arize-ai/phoenix) | AI 观测与评估 |

## 状态与来源说明

能力摘要依据各项目的官方 README、仓库说明和文档整理；表格中的 GitHub 链接是对应项目的来源入口。本轮已核对全部 30 个仓库的可访问性与归档状态，尚未对这些项目进行统一安装或性能评测。

- **ZaoFu** 的 README 标注为 Developer Preview。本清单将其归入长周期交付编排，因为它以任务契约、角色协作、验证门禁和恢复路径管理交付过程。
- **SWE-agent** 的 README 说明主要开发投入已转向 mini-swe-agent，并建议新使用者优先关注后者。
- **Daytona** 的公开仓库已归档。其 README 说明核心开发自 2026 年 6 月迁入私有代码库；这里保留公开版本作为架构研究对象。
- **Temporal × OpenAI Agents** 是样例仓库中的集成示例：[openai-agents/README.md](https://github.com/temporalio/samples-typescript/blob/main/openai-agents/README.md)。

研究项目、SDK、示例和评测集的职责不同，不能仅凭同一张清单推断它们具有相同的交付能力。后续能力对比应绑定具体版本、配置、任务和验收方法。

## 后续调研维度

每个项目的深入调研可以记录：

| 维度 | 要回答的问题 |
| --- | --- |
| 目标用户 | 面向个人开发者、研究者，还是管理智能体团队的组织？ |
| 执行入口 | 使用 CLI、SDK、插件、服务，还是 GitHub 工作流？ |
| 状态与记忆 | 哪些状态持久化？能否跨会话、跨模型继续？ |
| 编排与交接 | 如何拆分任务、处理依赖、分配所有者和交接结果？ |
| 验证与完成 | 完成条件由谁定义？检查依据是测试、证据还是模型判断？ |
| 失败与恢复 | 如何处理崩溃、停滞、重复失败及需要人工介入的情况？ |
| 工作区与隔离 | 使用本机、Git worktree、容器还是云沙箱？ |
| 观测与成本 | 能否关联轨迹、任务状态、耗时和模型使用成本？ |
| 证据与成熟度 | 能力来自文档声明、可运行示例，还是可复现的实际评测？ |

## 贡献

欢迎通过 Issue 或 PR 补充项目、纠正描述和提交可复现的使用记录。

新增项目请提供 GitHub 仓库名、它聚焦的问题、建议分类，以及支持描述的官方文档链接。能力或状态发生变化时，请附上核对日期和具体来源。
