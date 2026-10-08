# 本轮来源记录

核对日期：2026-10-08。记录本轮新增 30 个项目及用于重点比较的 8 个原有项目，共 38 份官方文件。原有其余项目的来源入口保留在 [README](../README.md)。本表不是全部 60 个项目的完整审计档案。

## 阅读与证据口径

- 新增项目已读取仓库元数据与 README 开头部分；全部可访问，元数据的 archived 均为 false。
- 阅读以默认分支为准；下面链接跟随分支，未来内容可能变化。
- “文件 SHA”来自 GitHub Contents API，是文件 blob 的指纹，**不是提交 SHA**。后续运行实验还需要固定 commit/tag、依赖和配置。
- 新增 README 读取范围为开头约 160–170 行；重点比较材料读取开头 130 行。未宣称完整阅读每个仓库、报告或实现。
- 能力描述以已读的官方文档为依据；未统一安装、检查实现、评测效果、核对许可证兼容性或开展用户访谈。
- “潜在组织收益”“适用场景”“建议组合”属于研究判断。官方报告中的结果需要另读完整方法并复现，本文没有将其作为组织收益实测。
- README 内安装提示、示例指令与数值仅是被研究材料，本轮没有据此执行安装或运行。

## 1. 新增 30 个项目

| 项目 | 官方文件 | 默认分支 | 文件 SHA | 仓库归档状态 |
| --- | --- | --- | --- | --- |
| Intelligent-Internet/zenith | [README](https://github.com/Intelligent-Internet/zenith/blob/main/README.md) | main | `8a3009f6837948fab942d559f552dc9166032bc4` | 未归档 |
| AMAP-ML/LongHorizon-Harness | [README](https://github.com/AMAP-ML/LongHorizon-Harness/blob/main/README.md) | main | `bccecc00ced6fdebdb1f563b9038c8a5b8203d37` | 未归档 |
| Flesymeb/HarnessOfHarness | [README](https://github.com/Flesymeb/HarnessOfHarness/blob/main/README.md) | main | `1c5b46dfef226cc4696a1803cd7f00eafcf7ef06` | 未归档 |
| EcuaByte-lat/Cortex | [README](https://github.com/EcuaByte-lat/Cortex/blob/main/README.md) | main | `74476f083a885ada50f5a0ccedb2b559bb09fd72` | 未归档 |
| rosehgal/handoff | [README](https://github.com/rosehgal/handoff/blob/main/README.md) | main | `c0f7571621009af9da64339fc8aec96157dcd464` | 未归档 |
| stefan-jansen/coding-agent-toolkit | [README](https://github.com/stefan-jansen/coding-agent-toolkit/blob/main/README.md) | main | `3daa75bba86892ca32e6b8da896e20b4b025d042` | 未归档 |
| ciumbar/continuity-handoff | [README](https://github.com/ciumbar/continuity-handoff/blob/main/README.md) | main | `030b087531cf6dca2f10193b4b4e3ad587a84c66` | 未归档 |
| nick-vi/agent-handoff | [README](https://github.com/nick-vi/agent-handoff/blob/main/README.md) | main | `6766668e81c1e616a748d0394cde77d5988b0c11` | 未归档 |
| majiayu000/harness | [README](https://github.com/majiayu000/harness/blob/main/README.md) | main | `76fc03ddaea2128b0b144b901cc4480b04069dd5` | 未归档 |
| lenileiro/harness | [README](https://github.com/lenileiro/harness/blob/main/README.md) | main | `fe68337a3019fccbe34781d82aef0b8775b3412d` | 未归档 |
| Tlahey/harness | [README](https://github.com/Tlahey/harness/blob/main/README.md) | main | `55c91fb768b252978b34267ce702f4b8f5e4c435` | 未归档 |
| JeiKeiLim/tenet | [README](https://github.com/JeiKeiLim/tenet/blob/main/README.md) | main | `6541ea731a0c846b45f8e82ac27407f84c00a0a7` | 未归档 |
| lordaeternus/agent-execution-harness | [README](https://github.com/lordaeternus/agent-execution-harness/blob/main/README.md) | main | `e15a8e9554110852d73829a3153d9a663358100a` | 未归档 |
| SUNRNEHUI/agent-harness | [README](https://github.com/SUNRNEHUI/agent-harness/blob/main/README.md) | main | `9c623777562f6d2692f49a2ad1fd4cad39bd7f3b` | 未归档 |
| moortekweb-art/agentic-harness | [README](https://github.com/moortekweb-art/agentic-harness/blob/main/README.md) | main | `f946ef463f2b1f3d92016eb250786e994f2cb4dd` | 未归档 |
| harnessworks/harness-starter-kit | [README](https://github.com/harnessworks/harness-starter-kit/blob/main/README.md) | main | `43059f6d27f38f223b98bd30d504688aa82215ae` | 未归档 |
| markhazlett/agent-harness | [README](https://github.com/markhazlett/agent-harness/blob/main/README.md) | main | `9b1e80ef117aecf537ece38a2806f9bbad91629f` | 未归档 |
| YuxiaoWang-520/harness-craft | [README](https://github.com/YuxiaoWang-520/harness-craft/blob/main/README.md) | main | `49682b483d73a9bb9a756610db0a25ecd1d36b9b` | 未归档 |
| clay-good/agent-replay | [README](https://github.com/clay-good/agent-replay/blob/main/README.md) | main | `f1b61530be6a8e38eade926ecd2fb423b3119be2` | 未归档 |
| tangle-network/traces | [README](https://github.com/tangle-network/traces/blob/main/README.md) | main | `d7520e28625247329d8209d650c94b89d39ff2fe` | 未归档 |
| nderman/agent-harness | [README](https://github.com/nderman/agent-harness/blob/main/README.md) | main | `a98d1b409072edcd89b44145adcb25103cd597e4` | 未归档 |
| hellock/agent-harness-eval | [README](https://github.com/hellock/agent-harness-eval/blob/main/README.md) | main | `aeb390fd2367136c14635e94974c2ddfe1972251` | 未归档 |
| zenixos/harness-bench | [README](https://github.com/zenixos/harness-bench/blob/main/README.md) | main | `915ff54a9d7b10714f389fffd067dba9c3e707b6` | 未归档 |
| ya5h-P/harnessbench | [README](https://github.com/ya5h-P/harnessbench/blob/main/README.md) | main | `1836efe81f7dbea76b1bd8f8c118af263273371d` | 未归档 |
| Heretek-AI/harness-benchmark | [README](https://github.com/Heretek-AI/harness-benchmark/blob/main/README.md) | main | `964ff51df23f52a55952669f2fb88d4628e7102d` | 未归档 |
| microsoft/Loopsbench | [README](https://github.com/microsoft/Loopsbench/blob/main/README.md) | main | `85af1a7894e52dd14e7efd05514ab88b303f3af8` | 未归档 |
| arielshad/balagan-agent | [README](https://github.com/arielshad/balagan-agent/blob/main/README.md) | main | `5d21abf0382d76f7406e84d9eeaad55c7f771d16` | 未归档 |
| SubhashPavan/agentfuzz | [README](https://github.com/SubhashPavan/agentfuzz/blob/main/README.md) | main | `a5d1400ba77212759fc6d946415bac21a6387301` | 未归档 |
| cyanseek/dsh-tool-chaos | [README](https://github.com/cyanseek/dsh-tool-chaos/blob/main/README.md) | main | `46239f7ec1e4b7b185aaf9710abf931f18a1c6ae` | 未归档 |
| microsoft/agent-lightning | [README](https://github.com/microsoft/agent-lightning/blob/main/README.md) | main | `19c3c7ea416050772baeb4dffdf04293469360e7` | 未归档 |

## 2. 重点比较的原有项目

| 项目 | 官方文件 | 文件 SHA |
| --- | --- | --- |
| uisee-ai/zaofu | [README.md](https://github.com/uisee-ai/zaofu/blob/main/README.md) | `ccbbc4b78b4372e31e0f2b460321a750b97318dc` |
| openai/symphony | [SPEC.md](https://github.com/openai/symphony/blob/main/SPEC.md) | `cd24131a1e2358cbfecc4f6efb028fc9fc6edefc` |
| gastownhall/gastown | [README.md](https://github.com/gastownhall/gastown/blob/main/README.md) | `e095adbcd7b4d422d35f2e91f43f45cfc38c88e2` |
| gastownhall/gascity | [README.md](https://github.com/gastownhall/gascity/blob/main/README.md) | `da5b98caa5f564f669970420b890b2b709dbf907` |
| gastownhall/beads | [docs/core-concepts/index.md](https://github.com/gastownhall/beads/blob/main/docs/core-concepts/index.md) | `0f56797c6c1052cf0f42495cd6aa57270092fc37` |
| langchain-ai/deepagents | [README.md](https://github.com/langchain-ai/deepagents/blob/main/README.md) | `efa13c884a5f984cf30c5da8f571fc9264e20216` |
| google-research/veriharness | [README.md](https://github.com/google-research/veriharness/blob/main/README.md) | `d4a9f5a7409393810c38feba80ea9aed01080e9f` |
| Yang-Jiashu/LongHorizonOS | [README.md](https://github.com/Yang-Jiashu/LongHorizonOS/blob/main/README.md) | `a9d372f3756500041231aa1a08b7031ff8f4941d` |

## 3. 后续证据记录模板

每次补充运行或使用证据，至少记录：

| 字段 | 内容 |
| --- | --- |
| 身份与版本 | owner/repo、commit/tag、依赖版本、许可证 |
| 任务与环境 | 原始目标、代码基线、模型版本、工具与权限、硬件或沙箱 |
| 验收与预算 | 验收条件、检查方式、停止条件、模型和人工预算 |
| 运行证据 | 开始结束时间、轨迹、命令、工件、代码版本、失败与介入记录 |
| 对照 | 原流程或另一配置，哪些条件相同、哪些条件不同 |
| 结果 | 通过验收、未完成、失败、质量问题、人工时间和总成本 |
| 结论边界 | 支持什么判断、不能推断什么、仍缺哪些证据 |

访谈证据单独标明自述。新增比较结果需保留失败和未完成任务，避免只记录成功案例。
