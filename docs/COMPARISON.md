# Agent Harness 跨项目比较

核对日期：2026-10-08。本文依据官方 README、Symphony SPEC 和 Beads 核心概念文档比较产品职责。适用场景、组合方式和组织收益属于研究判断，尚未通过统一部署与组织任务实验验证。

项目问题清单见 [README](../README.md)，新增 30 个项目档案见 [扩展研究](EXTENDED_LANDSCAPE.md)，本轮读取范围与文件指纹见 [来源记录](SOURCES.md)。

## 1. 先确认组织卡在哪一步

| 环节 | 团队的典型问题 | 要研究的机制 | 候选项目举例 |
| --- | --- | --- | --- |
| 执行 | 模型能回答，实际开发工具难接入 | 文件读写、工具执行、会话、模型接入 | Pi、OpenCode、Codex、Goose、OpenHands SDK |
| 连续性 | 新会话忘了目标、进度和依据 | 持久状态、工作图、交接文档、版本绑定 | Beads、Cortex、handoff、Continuity Handoff |
| 编排 | 任务无人接、职责混乱、失败无人处理 | 调度、角色、依赖、工作区、重试和升级 | Symphony、Gas Town、Gas City、ZaoFu |
| 长任务循环 | 有局部进展，整体提前停止或反复空转 | 差距发现、重规划、独立检查、停止条件 | Ralph、Zenith、Harness-of-Harness、Tenet、LongHorizonOS |
| 完成验收 | 声明完成，需求或测试证据缺失 | 验收契约、可执行检查、证据关联、门禁 | ZaoFu、VeriHarness、Agent Execution Harness、Agentic Harness |
| 运行保障 | 崩溃后无法继续，开发环境难复现 | 检查点、持久执行、沙箱和快照 | LangGraph、Temporal 示例、E2B、Daytona 公开版本 |
| 分析与选型 | 看不清失败原因，不知框架差异来自哪里 | 轨迹、对照、消融、回归、故障注入 | Langfuse、Phoenix、Traces、Agent Replay、评测与 chaos 项目 |

这些环节可以由多个项目共同承担。表中的排列描述研究视角，不代表已经有现成兼容集成。

## 2. 长周期交付方案的主要差异

### 2.1 控制与编排

| 项目 / 官方依据 | 优先解决的问题 | 控制机制与边界 | 组织采用时最需要验证 |
| --- | --- | --- | --- |
| [ZaoFu](https://github.com/uisee-ai/zaofu/blob/main/README.md) | 长交付中的目标、角色、交接、验证和恢复不统一 | 任务契约、持久交接、独立验证、ThinJudge 完成门禁，以及 Supervisor / RunManager 的受控恢复；Developer Preview | 能否用现有项目的验收规则定义契约？证据怎样关联代码版本？接入和运行投入多大？ |
| [Symphony](https://github.com/openai/symphony/blob/main/SPEC.md) | Issue 到智能体执行依赖临时脚本 | 读取任务系统，管理按 Issue 划分的工作区、并发、重试与状态协调；WORKFLOW.md 定义行为；成功运行可以结束于人工审查交接状态 | 团队的 Issue 状态和工作流怎样映射？应用层怎样补足验收？所选实现的隔离和权限是否符合场景？ |
| [Gas Town](https://github.com/gastownhall/gastown/blob/main/README.md) | 多智能体工作区、任务、身份、消息与接续难管理 | 工作区与队伍管理、持久 hooks、Beads 工作记录和角色通信 | 并行工作是否产生合并阻塞？排查和运营多角色系统的成本是多少？ |
| [Gas City](https://github.com/gastownhall/gascity/blob/main/README.md) | 希望复用编排组件构建自己的系统 | 从编排需求抽出的 SDK，提供控制器协调、运行提供者、工作路由与配置组件 | 现有组件覆盖多少需求？自建平台后由谁维护？ |
| [Deep Agents](https://github.com/langchain-ai/deepagents/blob/main/README.md) | 需要规划、子智能体、文件系统和上下文管理的通用基础 | 基于 LangGraph 的通用 harness；应用任务的验收与业务状态需要集成者明确 | 能否接入代码库、CI 和任务系统？持久运行与业务完成之间如何衔接？ |
| [majiayu000/harness](https://github.com/majiayu000/harness) | 多个已有编码智能体缺少统一生命周期与策略管理 | Rust 控制平面，工作流、策略、复核、恢复、fleet 和轨迹组件 | fleet 数据库与认证运维成本；权限、恢复和门槛的实际执行效果 |
| [Tlahey/harness](https://github.com/Tlahey/harness) | 多角色流水线和配置难维护 | 在 OpenCode 上配置角色、模型、工具、权限和 pipeline，并保存事件 | 是否适合既有 OpenCode 工作方式？角色权限能否实际执行？ |

**ZaoFu 的分类：** 在本仓库四分类中属于第二类“长周期交付、任务连续性与多智能体编排”，同时覆盖第四类的验证能力。它的主线是控制交付如何推进、交接、验收和恢复，因此适合作为交付控制平面的研究对象。

Symphony 的规范明确把自身定义为调度/运行与任务读取服务；任务写入通常由执行智能体及其工具完成。规范也没有要求统一的审批或沙箱政策。研究某个 Symphony 实现时，需要记录该实现的实际选择。[官方规范](https://github.com/openai/symphony/blob/main/SPEC.md)。

### 2.2 持续推进与停止

| 项目 / 官方依据 | 连续执行方式 | 重点研究的问题 |
| --- | --- | --- |
| [Ralph](https://github.com/snarktank/ralph) | 新会话反复执行，用文件和 Git 保留进度 | 新上下文能否发现缺口？是否重复探索？总预算和停止条件怎样控制？ |
| [Zenith](https://github.com/Intelligent-Internet/zenith/blob/main/README.md) | 编排者逐轮读取状态，动态启动 worker / tester、重规划或停止 | 动态编排是否减少遗漏和无效循环？README 的报告结果在团队任务中能否复现？ |
| [Harness-of-Harness](https://github.com/Flesymeb/HarnessOfHarness) | Planner / Developer / 只读 QA 多轮规划、开发和验收 | QA 是否保持已验证功能？演示任务迁移到既有代码库时有哪些成本？ |
| [LongHorizon-Harness](https://github.com/AMAP-ML/LongHorizon-Harness) | 围绕真实环境验证、状态保存与恢复推进跨上下文任务 | GUI / CLI 后端能力是否一致？环境验证信号是否覆盖完成条件？ |
| [LongHorizonOS](https://github.com/Yang-Jiashu/LongHorizonOS/blob/main/README.md) | 在已有 harness 外观察运行片段、上下文增长、进展与成本，维护交接和恢复 | 怎样判断无进展？中止或接续是否保留有效状态？ |
| [Tenet](https://github.com/JeiKeiLim/tenet) | 规格、依赖图、逐工作项 critics 和项目知识更新 | 反复复核的质量与成本如何平衡？默认重试策略是否需要显式预算约束？ |

共同的研究问题是：**“继续运行”增加的时间和费用，是否带来更多通过验收的结果？** 需要同时记录未完成、重复劳动、提前停止和预算耗尽。循环次数本身不构成效率收益。

## 3. 状态、记忆和交接并不等价

| 项目 / 官方依据 | 主要保留什么 | 可能减少的人工工作 | 尚需检查 |
| --- | --- | --- | --- |
| [Beads](https://github.com/gastownhall/beads/blob/main/docs/core-concepts/index.md) | 持久的任务与依赖工作图、可执行前沿、领取状态 | 找任务、查依赖和重复分派 | 任务状态怎样更新？被标为完成是否有独立依据？ |
| [Cortex](https://github.com/EcuaByte-lat/Cortex) | 任务、尝试、决策、工件与验证证据的关系 | 重建工程背景、解释决策与验证状态 | 自动捕获覆盖哪些客户端？代码变化后的证据新鲜度？ |
| [handoff](https://github.com/rosehgal/handoff) | hooks 捕获的动作历史和精简交接文档 | 重新说明进度与下一步 | 自动捕获遗漏、过期上下文、日志体量 |
| [Continuity Handoff](https://github.com/ciumbar/continuity-handoff) | 可携带结构化状态与人类可读交接 | 跨会话或跨模型恢复目标 | 状态更新是否及时？实际模型切换由谁安排？ |
| [Agent Handoff](https://github.com/nick-vi/agent-handoff) | 按 topic 绑定的 CLI 会话、交接 brief、返回状态 | 手工复制任务与操作多个 CLI | 分支和会话是否对应？客户端升级是否破坏适配？ |
| [Coding Agent Toolkit](https://github.com/stefan-jansen/coding-agent-toolkit) | 需求、计划、Issue、交付和 handoff/continue 过程 | 需求到 GitHub 管理对象的手工搬运 | 与现有审查、授权和合并过程的兼容性 |

这里值得单独测量“接续后第一次有效行动的时间”，并安排状态不一致的任务：分支换了、测试旧了、依赖变了、上个执行者留下了错误结论。交接文件可读性和接手续作正确性需要分别观察。

## 4. 验证方案要检查谁产生证据

| 方案 / 官方依据 | 核心做法 | 研究时要区别的行为 |
| --- | --- | --- |
| [ZaoFu](https://github.com/uisee-ai/zaofu) | 把契约、独立验证、门禁和恢复放入交付控制 | 门禁接受的证据是否覆盖任务并对应当前版本 |
| [VeriHarness](https://github.com/google-research/veriharness/blob/main/README.md) | 同一模型的独立运行提出候选；处理分歧，也主动挑战一致结论，通过环境证据修订 | 多次一致不能直接证明正确；观察环境验证是否有效、额外推理成本多大 |
| [Agent Execution Harness](https://github.com/lordaeternus/agent-execution-harness) | 对计划、任务、声明、工件和检查做覆盖及完成前验证 | 文件齐全、声明有引用和实际满足需求之间的差异 |
| [Agentic Harness](https://github.com/moortekweb-art/agentic-harness) | 用用户控制的独立检查命令接受或拒绝完成 | 命令通过但需求遗漏、错误拒绝、修复循环和预算 |
| [Superpowers](https://github.com/obra/superpowers) 与技能工具包 | 通过可复用技能组织澄清、设计、开发、测试与复核 | 模型遵守约定的程度，以及 runtime 或 CI 实际执行的检查 |
| [PR-Agent](https://github.com/The-PR-Agent/pr-agent) | 对 PR 提供审查和变更建议 | 建议命中率、审查节省时间、误报处理与人工责任 |

本轮没有统一验证各项目如何处理“证据来自旧版本”“验收命令自身有问题”“模型结论错误”这些情况。它们应进入下一阶段试验，而不是在文档调查中默认已经解决。

## 5. 观测、评测与故障测试各自回答什么

| 要回答的问题 | 项目 / 官方入口 | 研究边界 |
| --- | --- | --- |
| 运行发生了什么、哪里花钱、哪一步失败？ | [Langfuse](https://github.com/langfuse/langfuse)、[Phoenix](https://github.com/Arize-ai/phoenix)、[Traces](https://github.com/tangle-network/traces) | 轨迹分析依赖采集完整度；看到失败不代表系统已能恢复 |
| 改提示词或模型后，行为哪里变了？ | [Agent Replay](https://github.com/clay-good/agent-replay)、[nderman/agent-harness](https://github.com/nderman/agent-harness) | 回看、cassette 重放与重新调用实时模型分别记录；环境副作用影响复现 |
| harness 选择会改变结果吗？ | [Agent Harness Eval](https://github.com/hellock/agent-harness-eval)、[zenixos/harness-bench](https://github.com/zenixos/harness-bench)、[ya5h-P/harnessbench](https://github.com/ya5h-P/harnessbench) | 固定模型、任务、工具与预算；zenixos 当前是 Building，不能当作完成的比较结论 |
| MCP、技能、插件、LSP 哪个有效？ | [Heretek-AI/harness-benchmark](https://github.com/Heretek-AI/harness-benchmark) | 消融设计、组件实际安装状态和工具权限会影响归因 |
| 能否持续演进代码并保持已完成部分？ | [LoopsBench](https://github.com/microsoft/Loopsbench)、[SWE-EVO](https://github.com/SWE-EVO/SWE-EVO)、[SWE-bench Pro](https://github.com/scaleapi/SWE-bench_Pro-os) | 任务跨度、依赖与验收不同，得分不能直接横比或转换成组织 ROI |
| 异常后能否恢复并满足验收？ | [BalaganAgent](https://github.com/arielshad/balagan-agent)、[Agentfuzz](https://github.com/SubhashPavan/agentfuzz)、[DSH Tool Chaos](https://github.com/cyanseek/dsh-tool-chaos) | 故障需确实触发，恢复需有任务结果；DSH 项目还有特定版本兼容与未发布状态 |
| 怎样用真实运行条件训练智能体？ | [Agent Lightning](https://github.com/microsoft/agent-lightning) | 属于训练研发；数据、GPU 和工程投入需要另算 |

## 6. 按组织场景安排小规模试用

下列是待验证的试用路径。项目组合需要另做兼容性检查。

| 团队现状 | 优先调查 | 期望改善 | 必须同时记录 |
| --- | --- | --- | --- |
| 两三个人反复接续同一开发任务 | handoff / Continuity Handoff / Cortex；选一种状态主来源 | 接续更快，少重复探索 | 首次有效行动时间、状态错误、记录维护时间 |
| 已用 Issues / PR，需要减少启动执行的人工操作 | Symphony / Coding Agent Toolkit / GitHub Agentic Workflows | 少搬运和调度任务 | 运行失败、审查等待、任务重复启动、配置维护 |
| 多个智能体分工，人工协调越来越多 | Gas Town / Gas City / majiayu000/harness | 降低分派和交接时间 | 合并冲突、重复劳动、总并发成本、运维时间 |
| 长功能常提前结束或偏离要求 | ZaoFu / Zenith / Tenet / Harness-of-Harness | 减少遗漏和完成误报 | 同一验收下的通过率、人工复核、总预算 |
| 已有 CI，但智能体宣称完成仍不可信 | Agentic Harness / Agent Execution Harness / ZaoFu 的验证机制 | 让完成与验收依据关联 | 旧证据、需求遗漏、误拒绝、补充测试时间 |
| 已经接入智能体，故障很难查 | Langfuse / Phoenix / Traces / Agent Replay | 缩短排查时间 | 采集成本、日志完整度、敏感数据处理和适配维护 |
| 有自建运行层，要上线或改关键组件 | 对照评测与 chaos 工具 | 提前发现行为和恢复回归 | 故障覆盖、有效恢复、失败成本与实验搭建成本 |

## 7. 值得做成开源实验的方向

以下是根据本轮项目覆盖提出的假设；尚未证明市场空白或付费需求。

### A. 面向真实任务的 Harness 比较记录库

与当前仓库最接近：用一致模板记录“任务 → 原流程 → 接入方式 → 验收结果 → 人工和总成本”。第一版选一类跨会话任务，对两个已有方案做可复现记录，再积累数据。价值假设是降低选型者阅读和复现实验的成本。

### B. 交接状态与证据新鲜度检查

为一个现有 CLI 先做适配，记录仓库、分支、代码版本、目标、未完成项和检查记录；继续任务时报告不一致。先用预设的分支变化与旧测试案例验证。价值假设是减少接手续作中的重复探索和错误信任。

### C. 完成声明与验收结果的关联层

把每项验收条件关联到命令、运行、输出和代码版本，生成可以人工查看的完成摘要。先接入一个已有任务循环与 CI。价值假设是减少追问与重复人工核查；需验证绑定记录是否真的降低完成误报。

### D. 编码智能体恢复测试集

围绕进程退出、工具超时、取消、分支冲突和环境重建定义小场景；验收恢复后的代码和状态，记录无效重试及人工介入。价值假设是降低长期运行系统的异常复现成本。

这些方向可以在本研究仓库先形成协议、样例和使用记录。等真实用户和任务证据积累后，再决定是否独立实现产品。
