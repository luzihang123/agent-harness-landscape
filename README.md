# Agent Harness Landscape

Market research on agent harnesses and organizational productivity in software delivery.

**以组织提效为目标的 Agent Harness 市场调查与研究。**

本仓库研究软件交付组织在引入 AI 智能体后，如何通过 harness 管理执行、上下文、任务状态、协作、验证和恢复，从而减少人工盯守、返工与协调成本，改善可验证的交付效率。

研究从 GitHub 项目和官方文档出发，逐步补充用户场景、产品对比、接入成本与实际使用证据，为组织选型和开源项目方向探索提供依据。

当前收录 **60 个项目**，按主功能分为 **4 类**。初始整理与本轮仓库状态核对日期：**2026-10-08**。

## 仓库目的

围绕“Agent Harness 在什么组织、什么任务、什么条件下能带来效率收益”开展市场调查，重点回答：

1. **需求在哪里？** 哪些交付环节存在持续的人工协调、状态丢失、验证和返工成本？
2. **产品怎样解决？** 现有项目通过什么机制改善这些环节，分别适合哪些用户？
3. **收益如何证明？** 交付周期、人工投入、质量和总成本是否出现可观察的改善？
4. **采用需要什么？** 接入既有工具链、维护流程和治理边界需要多少投入？
5. **机会在哪里？** 哪些高频问题仍缺少易用、可接入、可验证的方案？

## 阅读导航

- [项目总览](#项目总览)：60 个项目，按“解决什么问题 → 项目名称 → GitHub”查看。
- [扩展项目档案](docs/EXTENDED_LANDSCAPE.md)：新增 30 个项目的机制、场景、潜在收益与待验证项。
- [跨项目比较](docs/COMPARISON.md)：ZaoFu 等长任务方案的区别，以及交接、验证、观测工具如何配合。
- [研究计划](docs/RESEARCH_PLAN.md)：调研步骤、用户访谈、效率指标和证据口径。
- [来源记录](docs/SOURCES.md)：本轮阅读的官方文件、核对日期和文件指纹。

## 组织提效研究框架

下面是本仓库拟验证的收益路径。指标是研究设计，具体项目的改善幅度需要实际使用证据支持。

| 组织中的问题 | Harness 可以提供的机制 | 预期收益 | 如何观察 |
| --- | --- | --- | --- |
| 工程师需要频繁查看进度、催促继续和处理停滞 | 持久任务状态、监督、有限重试和升级处理 | 减少人工盯守，释放工程师时间 | 每个验收任务的主动人工分钟数、介入次数 |
| 会话切换或人员交接后，重新理解目标与进度 | 可携带的任务状态、上下文交接与证据记录 | 降低交接与重复探索成本 | 恢复到首次有效进展的时间、重复工作比例 |
| 多个智能体重复修改、相互阻塞或产生冲突 | 任务依赖、所有权、工作区隔离和结构化交接 | 降低协作成本，提高有效并行度 | 冲突处理时间、重复任务数、验收吞吐量 |
| 完成声明缺少依据，问题到人工审查时才暴露 | 明确验收条件、独立验证和完成门禁 | 减少误报完成与后续返工 | 首次验收通过率、返工时间、逃逸缺陷 |
| 长任务反复失败、空转或无法恢复 | 检查点、失败分类、受控恢复和预算边界 | 降低失败损失及无效资源消耗 | 恢复成功率、无进展耗时、每个验收任务的总成本 |
| 管理者难以看清任务进度、风险和交付依据 | 任务与运行轨迹关联、证据汇总和成本观测 | 减少排查与状态汇报成本 | 排查时间、汇报准备时间、证据完整性 |

组织提效同时观察**交付结果、人工投入、质量和总成本**。流程设计、工具维护与验证投入也计入采用成本。

## 调研范围

这里的 Agent Harness 指模型周围支撑实际执行的机制，包括工具调用、上下文与记忆、任务状态、控制循环、交接、验证和恢复。

本清单也收录与 harness 配套的基础设施、技能框架、观测工具和评测集。分类是本仓库的调研视角；一个项目可能同时覆盖多个类别，当前按主要职责归类。

## 项目总览

| 类别 | 关注的问题 | 数量 |
| --- | --- | ---: |
| 编码智能体与执行内核 | 如何让智能体读取、修改和运行代码 | 8 |
| 长周期交付、任务连续性与多智能体编排 | 如何让工作跨会话持续推进，并协调多个执行者 | 23 |
| 持久执行、隔离环境与训练配套 | 如何保存状态、隔离运行及支持智能体训练 | 5 |
| 开发流程、验证、评测与观测 | 如何检查过程与结果，并分析可靠性 | 24 |

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
| 构建工具型智能体时，会话、工具执行、恢复、审批和评测需要重复实现。 | Harness（lenileiro） | [lenileiro/harness](https://github.com/lenileiro/harness) | 通用运行框架与评测组件；广泛能力应逐模块验证。 |

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
| 长任务已有进展却过早结束，需要反复发现未完成项并调整执行计划。 | Zenith | [Intelligent-Internet/zenith](https://github.com/Intelligent-Internet/zenith) | 长任务 harness 与技术报告；报告效果限于其评测配置。 |
| 桌面应用和终端任务跨多个上下文执行时，目标、验证状态与进度容易丢失。 | LongHorizon-Harness | [AMAP-ML/LongHorizon-Harness](https://github.com/AMAP-ML/LongHorizon-Harness) | 长任务及 computer-use harness；支持范围需要逐后端核对。 |
| 多日软件开发需要持续发现缺口、开发和测试，同时保留已验证功能。 | Harness-of-Harness | [Flesymeb/HarnessOfHarness](https://github.com/Flesymeb/HarnessOfHarness) | 研究框架与公开项目演示；另有 HoH-lite。 |
| 任务、尝试、决策和验收证据分散，换智能体后难以恢复可信工程状态。 | Cortex | [EcuaByte-lat/Cortex](https://github.com/EcuaByte-lat/Cortex) | 任务可靠性与交接层；各客户端集成能力分别记录。 |
| Claude Code 或 Cursor 新会话需要重新解释工作目标、已完成项与后续步骤。 | handoff | [rosehgal/handoff](https://github.com/rosehgal/handoff) | Go CLI / hooks；README 的主要自动集成对象为 Claude Code 与 Cursor。 |
| 从粗略需求到 Issue、PR 和交付缺少统一流程，跨编码工具切换容易丢失状态。 | Coding Agent Toolkit | [stefan-jansen/coding-agent-toolkit](https://github.com/stefan-jansen/coding-agent-toolkit) | 技能 / 提示词 / 工作流工具包；部分步骤的客户端支持不同。 |
| 模型切换、上下文耗尽或运行限制后，下一执行者需要重新发现目标与验证进度。 | Continuity Handoff | [ciumbar/continuity-handoff](https://github.com/ciumbar/continuity-handoff) | 交接协议与技能；模型切换本身由使用者或运行系统安排。 |
| 多个 CLI 智能体相互委派工作时，任务主题和会话连续性容易混淆。 | Agent Handoff | [nick-vi/agent-handoff](https://github.com/nick-vi/agent-handoff) | CLI / 技能 / 会话注册工具；依赖所选智能体 CLI。 |
| 并行编码智能体需要统一管理生命周期、权限、复核、恢复与运行证据。 | Harness（majiayu000） | [majiayu000/harness](https://github.com/majiayu000/harness) | Rust 控制平面；fleet 功能另有数据库和认证依赖。 |
| 设计、编码、审查和测试职责混在同一智能体中，配置与运行记录难以维护。 | Harness（Tlahey） | [Tlahey/harness](https://github.com/Tlahey/harness) | 基于 OpenCode 的项目模板与 CLI。 |
| 长任务容易偏离规格、跳过测试，项目知识和执行计划也会过时。 | Tenet | [JeiKeiLim/tenet](https://github.com/JeiKeiLim/tenet) | 长任务编排 harness；无限重试的默认说明需要在采用时核对。 |
| 同一会话内的轻任务与跨会话或需审计的任务，所需状态和验收控制不同。 | Agent Harness（SUNRNEHUI） | [SUNRNEHUI/agent-harness](https://github.com/SUNRNEHUI/agent-harness) | 运行环境中立的技能与控制脚本。 |

## 3. 持久执行、隔离环境与训练配套

解决“执行状态如何保存、故障后怎样继续，以及代码在哪里运行”。另收录训练配套：Agent Lightning 支持智能体训练研发，采用条件和收益口径与交付运行基础设施分别记录。

| 解决什么问题 | 项目名称 | GitHub 仓库 | 项目形态 / 备注 |
| --- | --- | --- | --- |
| 多步骤智能体流程需要保存状态、设置检查点、等待人工输入并恢复执行。 | LangGraph | [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) | 有状态图运行时 |
| 智能体工作流需要持久化运行，让调用失败可重试、人工审批后可继续，并避免重放时重复模型调用。 | Temporal × OpenAI Agents | [temporalio/samples-typescript](https://github.com/temporalio/samples-typescript) | 集成示例；位于 openai-agents/ |
| AI 生成的代码需要在可创建、控制和销毁的隔离云沙箱中运行。 | E2B | [e2b-dev/E2B](https://github.com/e2b-dev/E2B) | 代码执行沙箱基础设施 |
| 智能体需要隔离的开发环境、环境生命周期管理和持久化快照。 | Daytona | [daytonaio/daytona](https://github.com/daytonaio/daytona) | 沙箱基础设施；该公开仓库已归档 |
| 训练智能体时，需要保留真实 harness 的工具、上下文、控制流和运行环境。 | Agent Lightning | [microsoft/agent-lightning](https://github.com/microsoft/agent-lightning) | 训练配套基础设施；收益属于训练研发环节。 |

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
| 智能体报告完成却缺少对应的测试、验收与执行证据。 | Agent Execution Harness | [lordaeternus/agent-execution-harness](https://github.com/lordaeternus/agent-execution-harness) | 本地执行流程与证据工具；严格模式行为需单独核对。 |
| 工作智能体的完成声明需要由独立、用户控制的检查决定是否接受。 | Agentic Harness | [moortekweb-art/agentic-harness](https://github.com/moortekweb-art/agentic-harness) | CLI / 本地 GUI / 完成门禁；受控演示与真实效果分别判断。 |
| 相同智能体错误反复发生，仓库规范与失败经验难以转成持久约束。 | Harness Starter Kit | [harnessworks/harness-starter-kit](https://github.com/harnessworks/harness-starter-kit) | 入门工具包与方法；效果需任务记录验证。 |
| 个人或小团队的目标、冲刺计划、编码、验证与提交缺少持续衔接。 | Agent Harness（markhazlett） | [markhazlett/agent-harness](https://github.com/markhazlett/agent-harness) | 开发工作流工具包；适用习惯需要核对。 |
| 项目记忆、长任务执行、协作和验收要求分散在临时提示与会话中。 | Harness Craft | [YuxiaoWang-520/harness-craft](https://github.com/YuxiaoWang-520/harness-craft) | 技能 / 规则库；执行保证需结合具体 runtime 验证。 |
| 失败日志难以阅读，提示词或模型变化后难定位行为差异。 | Agent Replay | [clay-good/agent-replay](https://github.com/clay-good/agent-replay) | 轨迹调试 CLI；轨迹回看与真实环境重执行的条件应分别验证。 |
| 多种编码智能体日志格式不同，难统一定位循环、工具失败、token 增长和缺少验证。 | Traces | [tangle-network/traces](https://github.com/tangle-network/traces) | CLI / SDK；标准轨迹契约与原生日志适配能力分别记录。 |
| 非确定性智能体的行为难在 CI 中做可重复的测试和回归检测。 | Agent Harness（nderman） | [nderman/agent-harness](https://github.com/nderman/agent-harness) | 测试与评估示范工程；与软件交付 harness 属于配套研究。 |
| 多个 harness 的效果容易与模型、API 条件和任务差异混在一起。 | Agent Harness Eval | [hellock/agent-harness-eval](https://github.com/hellock/agent-harness-eval) | 多 harness 评测框架；支持版本以其兼容表为准。 |
| 实际可安装编码 CLI 缺少可控条件下的对照研究。 | Harness Bench（zenixos） | [zenixos/harness-bench](https://github.com/zenixos/harness-bench) | README 标注 Building；已有 scaffold，评分运行仍待完成。 |
| 相同本地模型搭配不同编码 harness 时，效果与稳定性差异难系统测量。 | HarnessBench（ya5h-P） | [ya5h-P/harnessbench](https://github.com/ya5h-P/harnessbench) | 偏本地模型场景的编码 harness 评测集与运行脚本。 |
| 添加 MCP、技能、插件或 LSP 后，难判断哪个组件实际改善任务效果。 | Harness Benchmark（Heretek-AI） | [Heretek-AI/harness-benchmark](https://github.com/Heretek-AI/harness-benchmark) | 基准与自动化实验框架；组件集成应逐项核对。 |
| 单点改动题难揭示智能体在有依赖的长任务中如何持续推进与保持已完成部分。 | LoopsBench | [microsoft/Loopsbench](https://github.com/microsoft/Loopsbench) | 长任务 benchmark 与执行 harness。 |
| 智能体在工具超时、错误响应、上下文损坏或预算耗尽后可能无法正确恢复。 | BalaganAgent | [arielshad/balagan-agent](https://github.com/arielshad/balagan-agent) | 通用智能体故障测试框架；组织效率收益待验证。 |
| 工具边界发生超时、格式错误、限流或成本失控时，智能体行为缺少系统检查。 | Agentfuzz | [SubhashPavan/agentfuzz](https://github.com/SubhashPavan/agentfuzz) | 通用故障注入工具；示例数值不作为本调研的实测数据。 |
| DeepSeek Harness 的插件需要验证重试、取消、拒绝和不可信结果处理路径。 | DSH Tool Chaos | [cyanseek/dsh-tool-chaos](https://github.com/cyanseek/dsh-tool-chaos) | README 标注未发布 development candidate。 |

## 状态与来源说明

能力摘要依据各项目的官方 README、仓库说明和文档整理；表格中的 GitHub 链接是对应项目的来源入口。截至本轮已核对清单中 60 个仓库的可访问性与归档状态，尚未对这些项目进行统一安装或性能评测。

- **ZaoFu** 的 README 标注为 Developer Preview。本清单将其归入长周期交付编排，因为它以任务契约、角色协作、验证门禁和恢复路径管理交付过程。
- **SWE-agent** 的 README 说明主要开发投入已转向 mini-swe-agent，并建议新使用者优先关注后者。
- **Daytona** 的公开仓库已归档。其 README 说明核心开发自 2026 年 6 月迁入私有代码库；这里保留公开版本作为架构研究对象。
- **Zenith / Harness-of-Harness / LoopsBench** 的研究或演示结果需绑定各自任务与配置，不能直接当作团队收益。
- **zenixos/harness-bench** 的 README 标注 Building，评分运行仍待完成。
- **DSH Tool Chaos** 的 README 标注未发布开发候选版本。
- **Agent Lightning** 面向训练研发；**nderman/agent-harness** 的示例面向支付支持智能体，均作为配套研究收录。
- **Temporal × OpenAI Agents** 是样例仓库中的集成示例：[openai-agents/README.md](https://github.com/temporalio/samples-typescript/blob/main/openai-agents/README.md)。

研究项目、SDK、示例和评测集的职责不同，不能仅凭同一张清单推断它们具有相同的交付能力。后续能力对比应绑定具体版本、配置、任务和验收方法。

## 产品与市场调研维度

每个项目的深入调研同时记录组织需求、产品机制与采用条件：

| 维度 | 要回答的问题 |
| --- | --- |
| 目标用户与决策者 | 谁使用、谁维护、谁决定采用？面向个人、研究团队还是研发组织？ |
| 交付场景 | 面向缺陷修复、维护、产品开发、迁移还是多团队协作？ |
| 组织收益 | 主要减少哪一种人工投入、等待、返工或失败损失？收益有什么证据？ |
| 采用与维护成本 | 是否需要更改工作流？部署、配置、权限、培训和升级由谁承担？ |
| 替代方案 | 当前团队用人工协调、脚本、CI 或其他平台怎样完成同样的工作？ |
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
