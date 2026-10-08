# 扩展项目研究：新增 30 个仓库

核对日期：2026-10-08。与 [README 的 60 项总览](../README.md) 配合阅读。

这一轮补充长任务循环、会话交接、角色流水线、完成门禁、轨迹分析、对照评测和故障测试。每个条目的“问题、机制、形态”来自官方 README；“潜在组织收益、适用场景、待验证项”是本仓库提出的研究判断。

当前工作属于文档调查，未统一安装这些项目。可访问、未归档或有演示，都不足以证明成熟度或组织提效。来源链接和读取时的文件指纹见 [来源记录](SOURCES.md)。同名 harness 项目用 owner 区分。

## 从组织问题找项目

| 组织中的问题 | 可进一步研究的项目 | 建议观察的结果 |
| --- | --- | --- |
| 智能体进展不少，但经常提前结束 | Zenith、Harness-of-Harness、Tenet | 遗漏需求、人工催促次数、验收成本 |
| 切会话或切工具后重复解释和探索 | Cortex、handoff、Continuity Handoff、Agent Handoff | 接续耗时、状态新鲜度、重复探索 |
| 多角色协作依赖临时脚本和人工安排 | majiayu000/harness、Tlahey/harness、Coding Agent Toolkit | 协调时间、冲突、配置维护 |
| 报告完成但没有可信验收依据 | Agent Execution Harness、Agentic Harness | 完成误报、首次验收通过、旧证据误用 |
| 同类开发错误反复发生 | Harness Starter Kit、Harness Craft、markhazlett/agent-harness | 重复错误率、规则维护和提示成本 |
| 失败日志难读，换框架后不能直接比较 | Agent Replay、Traces、Agent Harness Eval | 排查时间、适配覆盖、可复现性 |
| 选型结果混入模型和组件差异 | 三个不同的 Harness Bench/Benchmark、LoopsBench | 相同条件下的质量、总成本与方差 |
| 超时、限流、取消等异常路径无人测试 | BalaganAgent、Agentfuzz、DSH Tool Chaos | 故障后验收成功、恢复时间、无效重试 |

## 项目档案

## 1. 编码智能体与执行内核

### Harness（lenileiro）

- **GitHub：** [lenileiro/harness](https://github.com/lenileiro/harness)
- **解决的问题：** 构建工具型智能体时，会话、工具执行、恢复、审批和评测需要重复实现。
- **核心机制：** Python runtime 提供模型适配、持久会话和任务、工具执行及带防护与裸运行的对比评测。
- **潜在组织收益（待验证）：** 可能降低自建智能体运行与实验环境的工程投入。
- **适用场景（研究判断）：** 有能力维护自定义智能体运行层的工程或研究团队。
- **采用前要验证：** 外部 CLI 作为模型接入后由谁执行工具？框架维护成本是否低于复用现有 runtime？
- **项目形态与边界：** 通用运行框架与评测组件；广泛能力应逐模块验证。
- **官方来源：** [README](https://github.com/lenileiro/harness/blob/main/README.md)。

## 2. 长周期交付、任务连续性与多智能体编排

### Zenith

- **GitHub：** [Intelligent-Internet/zenith](https://github.com/Intelligent-Internet/zenith)
- **解决的问题：** 长任务已有进展却过早结束，需要反复发现未完成项并调整执行计划。
- **核心机制：** 编排者逐轮读取任务状态，动态安排 worker、tester、重规划与停止决策。
- **潜在组织收益（待验证）：** 可能减少人工催促继续和遗漏检查，并提高投入到未完成工作上的比例。
- **适用场景（研究判断）：** 多阶段功能开发、需要反复检查需求覆盖的长期任务。
- **采用前要验证：** 测试者是否覆盖原始需求？停止规则能否在较少运行成本下保持质量？
- **项目形态与边界：** 长任务 harness 与技术报告；报告效果限于其评测配置。
- **官方来源：** [README](https://github.com/Intelligent-Internet/zenith/blob/main/README.md)。
### LongHorizon-Harness

- **GitHub：** [AMAP-ML/LongHorizon-Harness](https://github.com/AMAP-ML/LongHorizon-Harness)
- **解决的问题：** 桌面应用和终端任务跨多个上下文执行时，目标、验证状态与进度容易丢失。
- **核心机制：** 以规划、执行、真实环境验证、检查点或恢复构成持续循环，支持多个已有智能体后端。
- **潜在组织收益（待验证）：** 可能减少跨应用操作与会话刷新后的人工作业恢复时间。
- **适用场景（研究判断）：** 同时涉及 GUI 与 CLI 的长任务、跨应用工作流。
- **采用前要验证：** 不同后端的电脑操作支持是否一致？验证信号是否足以反映实际完成？
- **项目形态与边界：** 长任务及 computer-use harness；支持范围需要逐后端核对。
- **官方来源：** [README](https://github.com/AMAP-ML/LongHorizon-Harness/blob/main/README.md)。
### Harness-of-Harness

- **GitHub：** [Flesymeb/HarnessOfHarness](https://github.com/Flesymeb/HarnessOfHarness)
- **解决的问题：** 多日软件开发需要持续发现缺口、开发和测试，同时保留已验证功能。
- **核心机制：** Planner、Developer、只读 QA Tester 在共享项目中反复规划、编码与测试，产物和证据进入下一轮。
- **潜在组织收益（待验证）：** 可能降低每轮重新规划的人工投入，形成可追踪的持续改进记录。
- **适用场景（研究判断）：** 产品原型、游戏或具有可操作验收体验的软件迭代。
- **采用前要验证：** 演示项目的结果如何迁移到维护既有代码库？多轮运行是否增加功能回归？
- **项目形态与边界：** 研究框架与公开项目演示；另有 HoH-lite。
- **官方来源：** [README](https://github.com/Flesymeb/HarnessOfHarness/blob/main/README.md)。
### Cortex

- **GitHub：** [EcuaByte-lat/Cortex](https://github.com/EcuaByte-lat/Cortex)
- **解决的问题：** 任务、尝试、决策和验收证据分散，换智能体后难以恢复可信工程状态。
- **核心机制：** 本地 SQLite、CLI/MCP 和捕获集成连接任务、证据、工件、验证与交接，并绑定仓库上下文。
- **潜在组织收益（待验证）：** 可能减少交接说明与重复探索，便于人工复查哪些状态有依据。
- **适用场景（研究判断）：** 混合使用多种编码智能体、跨会话维护、需要保留决策来源。
- **采用前要验证：** 哪些客户端能自动捕获？分支变化后旧证据怎样失效？团队同步成本如何？
- **项目形态与边界：** 任务可靠性与交接层；各客户端集成能力分别记录。
- **官方来源：** [README](https://github.com/EcuaByte-lat/Cortex/blob/main/README.md)。
### handoff

- **GitHub：** [rosehgal/handoff](https://github.com/rosehgal/handoff)
- **解决的问题：** Claude Code 或 Cursor 新会话需要重新解释工作目标、已完成项与后续步骤。
- **核心机制：** 通过生命周期 hooks 捕获动作，写入追加式 JSONL，并渲染精简交接文档供新会话加载。
- **潜在组织收益（待验证）：** 可能降低重复说明和重建上下文的时间，保留可人工阅读的历史。
- **适用场景（研究判断）：** 个人或小团队频繁跨天、跨会话继续同一项目。
- **采用前要验证：** 记录是否完整且不过量？仓库状态变化时如何避免加载过期说明？
- **项目形态与边界：** Go CLI / hooks；README 的主要自动集成对象为 Claude Code 与 Cursor。
- **官方来源：** [README](https://github.com/rosehgal/handoff/blob/main/README.md)。
### Coding Agent Toolkit

- **GitHub：** [stefan-jansen/coding-agent-toolkit](https://github.com/stefan-jansen/coding-agent-toolkit)
- **解决的问题：** 从粗略需求到 Issue、PR 和交付缺少统一流程，跨编码工具切换容易丢失状态。
- **核心机制：** 以 align、plan、GitHub issue、ship 与 handoff/continue 组织工作，磁盘状态和只读快照检查支持继续。
- **潜在组织收益（待验证）：** 可能减少手工搬运计划到 GitHub 的工作，提高交接与需求追踪一致性。
- **适用场景（研究判断）：** 已经以 GitHub Issues 和 PR 管理工作的团队。
- **采用前要验证：** 工作流与现有审批方式是否匹配？外部写入和合并步骤由谁授权？
- **项目形态与边界：** 技能 / 提示词 / 工作流工具包；部分步骤的客户端支持不同。
- **官方来源：** [README](https://github.com/stefan-jansen/coding-agent-toolkit/blob/main/README.md)。
### Continuity Handoff

- **GitHub：** [ciumbar/continuity-handoff](https://github.com/ciumbar/continuity-handoff)
- **解决的问题：** 模型切换、上下文耗尽或运行限制后，下一执行者需要重新发现目标与验证进度。
- **核心机制：** 可携带技能与辅助脚本在项目中维护结构化状态和人类可读交接文件。
- **潜在组织收益（待验证）：** 可能降低跨会话、跨模型接续时的理解成本。
- **适用场景（研究判断）：** 使用多种模型或 CLI 的开发者，想从小范围加入交接约定。
- **采用前要验证：** 状态是否被持续更新？接手者怎样发现记录与真实工作区不一致？
- **项目形态与边界：** 交接协议与技能；模型切换本身由使用者或运行系统安排。
- **官方来源：** [README](https://github.com/ciumbar/continuity-handoff/blob/main/README.md)。
### Agent Handoff

- **GitHub：** [nick-vi/agent-handoff](https://github.com/nick-vi/agent-handoff)
- **解决的问题：** 多个 CLI 智能体相互委派工作时，任务主题和会话连续性容易混淆。
- **核心机制：** 按 topic 固定会话，提供 Claude、Codex、Cursor 适配、交接 brief 和结构化返回状态。
- **潜在组织收益（待验证）：** 可能减少手工复制任务上下文和跨工具委派的操作成本。
- **适用场景（研究判断）：** 开发、复核等工作分配给不同 CLI 智能体。
- **采用前要验证：** 主题恢复是否绑定正确分支？各 CLI 升级后适配与返回状态是否稳定？
- **项目形态与边界：** CLI / 技能 / 会话注册工具；依赖所选智能体 CLI。
- **官方来源：** [README](https://github.com/nick-vi/agent-handoff/blob/main/README.md)。
### Harness（majiayu000）

- **GitHub：** [majiayu000/harness](https://github.com/majiayu000/harness)
- **解决的问题：** 并行编码智能体需要统一管理生命周期、权限、复核、恢复与运行证据。
- **核心机制：** Rust 控制平面包装已有智能体，支持工作流定义、策略执行、fleet 服务与轨迹观测。
- **潜在组织收益（待验证）：** 可能减少多智能体运营脚本与权限规则的分散维护。
- **适用场景（研究判断）：** 平台团队希望统一运行多个智能体任务或管理智能体队伍。
- **采用前要验证：** 单任务与 fleet 的运维成本分别是多少？恢复策略与验证门槛如何配置？
- **项目形态与边界：** Rust 控制平面；fleet 功能另有数据库和认证依赖。
- **官方来源：** [README](https://github.com/majiayu000/harness/blob/main/README.md)。
### Harness（Tlahey）

- **GitHub：** [Tlahey/harness](https://github.com/Tlahey/harness)
- **解决的问题：** 设计、编码、审查和测试职责混在同一智能体中，配置与运行记录难以维护。
- **核心机制：** 在 OpenCode 上以 YAML 定义角色和 pipeline，分配模型、工具与权限，保存事件并用评测支持提示词改进。
- **潜在组织收益（待验证）：** 可能降低多阶段开发配置成本，并让角色之间的交接更可检查。
- **适用场景（研究判断）：** 采用 OpenCode、想构建明确角色流水线的团队。
- **采用前要验证：** 权限是否实际阻止角色越界？提示词改进评测能否反映真实任务收益？
- **项目形态与边界：** 基于 OpenCode 的项目模板与 CLI。
- **官方来源：** [README](https://github.com/Tlahey/harness/blob/main/README.md)。
### Tenet

- **GitHub：** [JeiKeiLim/tenet](https://github.com/JeiKeiLim/tenet)
- **解决的问题：** 长任务容易偏离规格、跳过测试，项目知识和执行计划也会过时。
- **核心机制：** 从访谈与规格进入依赖图计划，每个工作项接受独立 critics 检查，再将学习结果纳入项目知识。
- **潜在组织收益（待验证）：** 可能减少需求理解偏差和人工逐项复核，并维护持续更新的项目记录。
- **适用场景（研究判断）：** 跨多小时或多会话的产品开发、重构和功能迭代。
- **采用前要验证：** critics 的误判和运行开销怎样控制？默认重试策略需要何种预算配置？
- **项目形态与边界：** 长任务编排 harness；无限重试的默认说明需要在采用时核对。
- **官方来源：** [README](https://github.com/JeiKeiLim/tenet/blob/main/README.md)。
### Agent Harness（SUNRNEHUI）

- **GitHub：** [SUNRNEHUI/agent-harness](https://github.com/SUNRNEHUI/agent-harness)
- **解决的问题：** 同一会话内的轻任务与跨会话或需审计的任务，所需状态和验收控制不同。
- **核心机制：** 先对齐目标与验收条件，再按 Native、Portable、Audited 模式使用原生计划、可携带契约或证据控制。
- **潜在组织收益（待验证）：** 可能减少目标不清造成的返工，同时控制流程与记录负担。
- **适用场景（研究判断）：** 多种编码运行环境中，希望按任务需要加入状态与验收约定。
- **采用前要验证：** 模式选择是否降低实际人工成本？技能要求有多少依赖模型遵守？
- **项目形态与边界：** 运行环境中立的技能与控制脚本。
- **官方来源：** [README](https://github.com/SUNRNEHUI/agent-harness/blob/main/README.md)。

## 3. 持久执行、隔离环境与训练配套

### Agent Lightning

- **GitHub：** [microsoft/agent-lightning](https://github.com/microsoft/agent-lightning)
- **解决的问题：** 训练智能体时，需要保留真实 harness 的工具、上下文、控制流和运行环境。
- **核心机制：** 以训练器、模型请求网关和 rollout controller 采集交互并训练策略，可在本地或 Kubernetes 运行。
- **潜在组织收益（待验证）：** 可能减少训练流程与真实智能体运行条件脱节造成的实验工作。
- **适用场景（研究判断）：** 拥有训练数据、算力和训练能力的智能体研发团队。
- **采用前要验证：** 训练改进能否迁移到组织任务？GPU、数据和工程成本是否合理？
- **项目形态与边界：** 训练配套基础设施；收益属于训练研发环节。
- **官方来源：** [README](https://github.com/microsoft/agent-lightning/blob/main/README.md)。

## 4. 开发流程、验证、评测与观测

### Agent Execution Harness

- **GitHub：** [lordaeternus/agent-execution-harness](https://github.com/lordaeternus/agent-execution-harness)
- **解决的问题：** 智能体报告完成却缺少对应的测试、验收与执行证据。
- **核心机制：** 以计划、任务、检查与结构化工件约束执行，验证声明与证据覆盖，并提供完成前检查。
- **潜在组织收益（待验证）：** 可能减少人工追问测试是否执行，以及报告和实际工作不一致的返工。
- **适用场景（研究判断）：** 希望在现有编码智能体上加入本地证据与完成检查。
- **采用前要验证：** 证据由谁产生？检查能否绑定当前代码版本，而非旧日志或手填结果？
- **项目形态与边界：** 本地执行流程与证据工具；严格模式行为需单独核对。
- **官方来源：** [README](https://github.com/lordaeternus/agent-execution-harness/blob/main/README.md)。
### Agentic Harness

- **GitHub：** [moortekweb-art/agentic-harness](https://github.com/moortekweb-art/agentic-harness)
- **解决的问题：** 工作智能体的完成声明需要由独立、用户控制的检查决定是否接受。
- **核心机制：** 保存目标和运行证据，执行配置的检查命令，未通过时拒绝完成或进入修复。
- **潜在组织收益（待验证）：** 可能减少提前接受未完成任务的返工与人工检查遗漏。
- **适用场景（研究判断）：** 已有测试、构建或其他可执行验收规则的项目。
- **采用前要验证：** 验收命令是否测到需求？错误拒绝与额外运行成本是多少？
- **项目形态与边界：** CLI / 本地 GUI / 完成门禁；受控演示与真实效果分别判断。
- **官方来源：** [README](https://github.com/moortekweb-art/agentic-harness/blob/main/README.md)。
### Harness Starter Kit

- **GitHub：** [harnessworks/harness-starter-kit](https://github.com/harnessworks/harness-starter-kit)
- **解决的问题：** 相同智能体错误反复发生，仓库规范与失败经验难以转成持久约束。
- **核心机制：** 以提示词驱动采用流程，把观察到的失败转为仓库说明、检查、决策记忆和评测项。
- **潜在组织收益（待验证）：** 可能降低重复指导与同类错误修复成本，改善规范传递。
- **适用场景（研究判断）：** 团队已积累具体智能体失败案例，希望逐步完善项目环境。
- **采用前要验证：** 新增规则是否过时或冲突？文档健康与实际错误减少有何关联？
- **项目形态与边界：** 入门工具包与方法；效果需任务记录验证。
- **官方来源：** [README](https://github.com/harnessworks/harness-starter-kit/blob/main/README.md)。
### Agent Harness（markhazlett）

- **GitHub：** [markhazlett/agent-harness](https://github.com/markhazlett/agent-harness)
- **解决的问题：** 个人或小团队的目标、冲刺计划、编码、验证与提交缺少持续衔接。
- **核心机制：** 用技能与 hooks 组织 weekly goals、demo、sprint、build 和 ship，并按文件修改范围安排工作。
- **潜在组织收益（待验证）：** 可能减少周计划到执行的手工分解和重复操作。
- **适用场景（研究判断）：** 采用 Claude Code、Pi 或 Conductor 的小团队开发流程。
- **采用前要验证：** 约定能否适应既有分支策略？自动保护能否覆盖实际编辑与提交路径？
- **项目形态与边界：** 开发工作流工具包；适用习惯需要核对。
- **官方来源：** [README](https://github.com/markhazlett/agent-harness/blob/main/README.md)。
### Harness Craft

- **GitHub：** [YuxiaoWang-520/harness-craft](https://github.com/YuxiaoWang-520/harness-craft)
- **解决的问题：** 项目记忆、长任务执行、协作和验收要求分散在临时提示与会话中。
- **核心机制：** 为 Claude Code 和 Codex 提供可组合技能与持续规则，围绕持久状态、证据与协作边界组织开发。
- **潜在组织收益（待验证）：** 可能降低团队重复编写开发约定与交接提示的成本。
- **适用场景（研究判断）：** 希望从技能和规则层改进现有编码智能体工作方式。
- **采用前要验证：** 技能之间是否冲突？长上下文规则的 token 成本与遵守率如何？
- **项目形态与边界：** 技能 / 规则库；执行保证需结合具体 runtime 验证。
- **官方来源：** [README](https://github.com/YuxiaoWang-520/harness-craft/blob/main/README.md)。
### Agent Replay

- **GitHub：** [clay-good/agent-replay](https://github.com/clay-good/agent-replay)
- **解决的问题：** 失败日志难以阅读，提示词或模型变化后难定位行为差异。
- **核心机制：** 本地 SQLite 记录轨迹，提供逐步查看、运行差异、分支重跑、评估和回归资料导出。
- **潜在组织收益（待验证）：** 可能降低故障排查和提示词变更验证的人工时间。
- **适用场景（研究判断）：** 需要调试已有智能体执行记录的工具开发者或平台团队。
- **采用前要验证：** 重跑是否能恢复原始环境？工具副作用、日志完整度和适配版本如何处理？
- **项目形态与边界：** 轨迹调试 CLI；轨迹回看与真实环境重执行的条件应分别验证。
- **官方来源：** [README](https://github.com/clay-good/agent-replay/blob/main/README.md)。
### Traces

- **GitHub：** [tangle-network/traces](https://github.com/tangle-network/traces)
- **解决的问题：** 多种编码智能体日志格式不同，难统一定位循环、工具失败、token 增长和缺少验证。
- **核心机制：** 读取标准 spans 或原生会话日志，运行确定性分析；可选模型分析、运行对比与轨迹契约检查。
- **潜在组织收益（待验证）：** 可能降低跨智能体的运行排查成本，帮助形成可验证的改进项。
- **适用场景（研究判断）：** 有多种智能体或希望在自建系统中统一轨迹格式。
- **采用前要验证：** 不同日志能回答哪些问题？缺失数据是否明确标记？适配维护由谁承担？
- **项目形态与边界：** CLI / SDK；标准轨迹契约与原生日志适配能力分别记录。
- **官方来源：** [README](https://github.com/tangle-network/traces/blob/main/README.md)。
### Agent Harness（nderman）

- **GitHub：** [nderman/agent-harness](https://github.com/nderman/agent-harness)
- **解决的问题：** 非确定性智能体的行为难在 CI 中做可重复的测试和回归检测。
- **核心机制：** 记录模型交互 cassette，重放黄金场景并断言工具顺序、策略结果和输出依据。
- **潜在组织收益（待验证）：** 可能降低回归测试对实时模型调用的依赖与重复运行费用。
- **适用场景（研究判断）：** 可控制工具行为的智能体应用测试；示例为支付支持智能体。
- **采用前要验证：** 重放覆盖的是保存路径还是新模型行为？外部工具怎样保证重现？
- **项目形态与边界：** 测试与评估示范工程；与软件交付 harness 属于配套研究。
- **官方来源：** [README](https://github.com/nderman/agent-harness/blob/main/README.md)。
### Agent Harness Eval

- **GitHub：** [hellock/agent-harness-eval](https://github.com/hellock/agent-harness-eval)
- **解决的问题：** 多个 harness 的效果容易与模型、API 条件和任务差异混在一起。
- **核心机制：** 在匹配模型与任务的配置下运行多个框架，保存结果、轨迹、耗时和成本。
- **潜在组织收益（待验证）：** 可能降低选型和比较实验的搭建成本。
- **适用场景（研究判断）：** 研发效能或研究团队比较不同智能体运行框架。
- **采用前要验证：** 适配器的工具与权限是否等价？评测任务能否代表团队实际工作？
- **项目形态与边界：** 多 harness 评测框架；支持版本以其兼容表为准。
- **官方来源：** [README](https://github.com/hellock/agent-harness-eval/blob/main/README.md)。
### Harness Bench（zenixos）

- **GitHub：** [zenixos/harness-bench](https://github.com/zenixos/harness-bench)
- **解决的问题：** 实际可安装编码 CLI 缺少可控条件下的对照研究。
- **核心机制：** 围绕固定模型、任务与 SWE-bench 评估协议设计配对实验，并记录成本与可靠性。
- **潜在组织收益（待验证）：** 可能为选型提供更可解释的比较方法与复现结构。
- **适用场景（研究判断）：** 研究 CLI harness 的差异、设计选型实验。
- **采用前要验证：** 哪些适配已运行？有多少可审阅的完成实验和结果？
- **项目形态与边界：** README 标注 Building；已有 scaffold，评分运行仍待完成。
- **官方来源：** [README](https://github.com/zenixos/harness-bench/blob/main/README.md)。
### HarnessBench（ya5h-P）

- **GitHub：** [ya5h-P/harnessbench](https://github.com/ya5h-P/harnessbench)
- **解决的问题：** 相同本地模型搭配不同编码 harness 时，效果与稳定性差异难系统测量。
- **核心机制：** 以隐藏执行测试评估多类任务，提供重复实验、预算控制与统计比较。
- **潜在组织收益（待验证）：** 可能减少本地模型环境中的工具选型试错。
- **适用场景（研究判断）：** 本地模型和单机环境下比较多个编码 CLI。
- **采用前要验证：** 合成任务对真实长周期交付有多大代表性？硬件和模型参数怎样固定？
- **项目形态与边界：** 偏本地模型场景的编码 harness 评测集与运行脚本。
- **官方来源：** [README](https://github.com/ya5h-P/harnessbench/blob/main/README.md)。
### Harness Benchmark（Heretek-AI）

- **GitHub：** [Heretek-AI/harness-benchmark](https://github.com/Heretek-AI/harness-benchmark)
- **解决的问题：** 添加 MCP、技能、插件或 LSP 后，难判断哪个组件实际改善任务效果。
- **核心机制：** 矩阵与消融实验在受控模型配置下组合组件，可输出报告并接入 GitHub Action。
- **潜在组织收益（待验证）：** 可能降低组件评估和工具链变更回归实验的工程成本。
- **适用场景（研究判断）：** 团队迭代已有 harness 的插件和工具组合。
- **采用前要验证：** 上游组件是否已配置可用？运行矩阵能否隔离单一变量？
- **项目形态与边界：** 基准与自动化实验框架；组件集成应逐项核对。
- **官方来源：** [README](https://github.com/Heretek-AI/harness-benchmark/blob/main/README.md)。
### LoopsBench

- **GitHub：** [microsoft/Loopsbench](https://github.com/microsoft/Loopsbench)
- **解决的问题：** 单点改动题难揭示智能体在有依赖的长任务中如何持续推进与保持已完成部分。
- **核心机制：** 将任务建模为可单独验证的开发单元与依赖图，在容器环境中运行智能体和验证器。
- **潜在组织收益（待验证）：** 可能帮助检查长任务过程中的规划、遗漏和回归问题。
- **适用场景（研究判断）：** 研究长周期执行循环，比较不同 continuation 或编排策略。
- **采用前要验证：** 任务依赖和验收规则是否贴近组织场景？通过率与真实采用收益如何连接？
- **项目形态与边界：** 长任务 benchmark 与执行 harness。
- **官方来源：** [README](https://github.com/microsoft/Loopsbench/blob/main/README.md)。
### BalaganAgent

- **GitHub：** [arielshad/balagan-agent](https://github.com/arielshad/balagan-agent)
- **解决的问题：** 智能体在工具超时、错误响应、上下文损坏或预算耗尽后可能无法正确恢复。
- **核心机制：** 对智能体注入受控故障，记录恢复质量、时间与压力测试报告。
- **潜在组织收益（待验证）：** 可能提前发现恢复缺陷，降低上线后排查和失败损失。
- **适用场景（研究判断）：** 开发自有智能体运行层，已有明确故障与恢复验收定义。
- **采用前要验证：** 被测适配是否覆盖编码工具链？恢复质量的判定是否依赖有效任务验收？
- **项目形态与边界：** 通用智能体故障测试框架；组织效率收益待验证。
- **官方来源：** [README](https://github.com/arielshad/balagan-agent/blob/main/README.md)。
### Agentfuzz

- **GitHub：** [SubhashPavan/agentfuzz](https://github.com/SubhashPavan/agentfuzz)
- **解决的问题：** 工具边界发生超时、格式错误、限流或成本失控时，智能体行为缺少系统检查。
- **核心机制：** 包装智能体并选择故障 profile，按类型输出结果、成本和失败轨迹。
- **潜在组织收益（待验证）：** 可能降低异常路径测试的搭建成本，暴露重试风暴和错误处理缺口。
- **适用场景（研究判断）：** 有可包装智能体接口的工程团队。
- **采用前要验证：** 文档示例中的数字是否来自可复现实验？所用适配器与实际系统一致吗？
- **项目形态与边界：** 通用故障注入工具；示例数值不作为本调研的实测数据。
- **官方来源：** [README](https://github.com/SubhashPavan/agentfuzz/blob/main/README.md)。
### DSH Tool Chaos

- **GitHub：** [cyanseek/dsh-tool-chaos](https://github.com/cyanseek/dsh-tool-chaos)
- **解决的问题：** DeepSeek Harness 的插件需要验证重试、取消、拒绝和不可信结果处理路径。
- **核心机制：** 在隔离配置中执行 baseline、dry-run 和确定性故障注入，按证据输出通过、失败或无法判断。
- **潜在组织收益（待验证）：** 可能减少插件异常路径的人工复现时间。
- **适用场景（研究判断）：** 开发或维护 DeepSeek Harness 插件与工具管线。
- **采用前要验证：** 固定 DSH 版本是否兼容？注入是否确实触发，恢复断言是否充分？
- **项目形态与边界：** README 标注未发布 development candidate。
- **官方来源：** [README](https://github.com/cyanseek/dsh-tool-chaos/blob/main/README.md)。

## 后续取证顺序

1. 用同一个跨会话任务比较交接方案，检查状态是否对应当前分支和文件。
2. 给完成门禁安排“测试通过但需求遗漏”“测试日志来自旧代码”等反例。
3. 在长任务中固定总预算，比较重开会话、动态编排和独立验证的投入与结果。
4. 给已接入的方案注入超时、进程中断和取消，检查恢复后能否通过同一验收。
5. 记录接入和维护时间，再判断任务运行节省的时间是否抵消这些投入。

取证方法与指标见 [研究计划](RESEARCH_PLAN.md)，组合方式见 [跨项目比较](COMPARISON.md)。
