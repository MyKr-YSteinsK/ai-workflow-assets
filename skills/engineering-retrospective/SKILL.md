---
name: engineering-retrospective
description: 用于任务明确要求的工程取证、阶段/事故复盘、流程/成本/返工分析，以及跨项目工程经验或指令资产规则归纳；覆盖软件、Agent、ML、竞赛和研究实验。依据实际代码/版本、Plan/回传、运行/评测、验收与时间记录区分事实、单项目经验、独立跨项目规律和推断。普通实现、即时排障、一般代码审查、论文综述或业务指标分析不自动触发；不把单次事故、负面实验或复制规则升级为全局结论。
---

# Engineering Retrospective

## 0. 适用范围与合同

复盘目标是从已有过程与结果证据解释工程问题、成本和可复用经验；不是普通实现任务自动附带的审计。单项目也可使用，不为形成跨项目结论扩读未授权项目或要求凑齐固定数量案例。

先明确待回答命题、项目／阶段／时间范围及证据入口，遵循当前授权、实际可读的项目规则和有效 Plan。正式任务的冻结边界、必要验收、交付及 TASK_RESULT 以该合同为准；保留有效旧合同，不依赖未提供的 ChatGPT 附件或 Runner 自动触发。缺失必要合同／证据时说明影响，暂停受影响动作，不猜测权限或补造事实。

## 1. 默认只读

默认只读取证。任务要求报告／文档时可在授权路径输出；源码、测试、数据或有效规则的修改，以及 Commit／Push／Merge／Deploy／Publish，分别按当前授权处理，不能从“复盘”推导。确有修复授权时保留修复前证据，后续结果标明对应版本，不重写历史记录掩盖事故。

不为取证擅自重跑昂贵训练／Agent 对局、调用有成本或副作用的工具、提交竞赛结果或操作生产环境；确需新实验时报告它要补什么证据，并按已有授权与预算执行。遵守项目工作区／输出边界，保护原始证据、用户修改和敏感数据；不初始化缺失的 Git 或新增空治理文件。

## 2. 命题与证据适配

证据价值取决于待证明的命题（claim / proposition），不存在跨所有命题的统一等级：

| 待证明命题 | 优先直接证据 |
| --- | --- |
| 哪些代码／配置发生变化 | Git diff / history；非 Git 项目用可核实的前后文件／产物记录 |
| 哪些检查实际运行并通过 | 对应 test / CI result |
| production 正在运行哪个 build | deployment record + production endpoint identity |
| 某个真实设备交互是否符合目标 | real-device observation / user acceptance |
| 为什么作出某个决定 | 当时的 Plan / Decision / discussion |
| 实际投入多少人工时间 | explicit timing / operation records |
| Agent 实际调用了什么、在哪一步失败 | 对应运行 trace、工具请求／结果、停止原因及环境／策略版本 |
| 实验是否执行、比较是否有效 | run 记录、数据／分割／标签边界、参数、基线、指标及评价协议 |
| 哪条路线被正式接受、阶段是否推进 | Main／用户的实际决定与对应状态版本；分支指标或 TASK_RESULT 不能代替 |

证据冲突时，先核对是否描述同一版本、环境、条件，并回答同一个命题。CI green 不能否定用户在 iPhone Safari 观察到的遮挡/黑闪；二者可能验证不同 failure mode。

不可得数据写 `UNAVAILABLE`，不要补造精确值。

证据应对应实际版本、环境、run／数据身份及观察时间。旧证据依赖已变化时只能支持历史命题，不能扩称当前已验证。提交、推送、合并、部署、运行成功、证据接受和阶段推进分别取证；没有 Git／CI／发布链的项目不因此缺失全部工程证据。

## 3. 证据标签

- `FACT / MEASURED`：直接可验证；
- `SINGLE-PROJECT LESSON`：一个独立项目支持；
- `CROSS-PROJECT PATTERN`：多个项目独立出现同类问题；
- `INFERENCE`：合理推断；
- `RECOMMENDATION`：最终建议。

两个最终资产写了同一句话，不自动算两份证据。先检查是否来自共同旧 Prompt/规则。

这些标签描述结论的证据性质，不是任务状态或验证结果。跨项目规律应列明独立事件、共同条件、已知反例或未覆盖条件及适用范围；同项目多次事故可加强单项目经验，不能仅凭次数变成跨项目证据。未确认根因标为 INFERENCE，不把相关性写成因果，也不把缺少记录当成没有问题。

## 4. 重建开发循环

按项目实际 milestone／Plan／incident／实验迭代重建，标明分支并行、回路和证据缺口；不强制所有项目走相同线性步骤。软件项目可参考：

```text
requirement
→ plan
→ implementation
→ local verification
→ commit/push
→ CI/repair
→ release/deploy
→ human acceptance
→ rework
```

Agent／ML／研究可参考：问题或假设 → 数据／工具／评价协议与基线 → 实现／运行 → 指标与错误分析 → 对照／重复或停止 → 证据归档 → Main 的路线判断。无意义的 CI、发布或人工验收节点省略；研究结论不确定时如实保留，不伪造生命周期完成。

执行失败、有效负面结论与无效实验分开：未超过基线不自动代表工程事故或任务失败；泄漏、评价协议失效、运行未完和关键证据缺失不能冒充可信负面结论。结论是否已被接受另行核对，不从局部 TASK_COMPLETE 推出 STAGE_ADVANCED。

只有项目确有正式路线／阶段决策时才核对相应 Main 接受；小任务无需补建阶段治理或审批表，同一主线对话可承担多种职责。

## 5. 成本与返工

尽可能区分：

- investigation；
- implementation；
- focused verification；
- full/browser/build；
- CI wait/diagnosis；
- Agent 工具调用／对局、训练／推理／评测、数据准备及计算等待；
- fixture/environment；
- rework；
- release/publish；
- human acceptance。

commit timestamp interval ≠ actual engineering time；CI duration ≠ human effort；calendar elapsed time ≠ active work time。

人工、模型／工具费用、计算资源与等待时间分别核算，注明来源、单位、范围和共享资源／并行条件，避免重叠计入。提交数、消息数、token 或 run 次数可以作为有边界的代理指标，不能无依据换算成人工工时或工程质量。

没有真实计时数据时，只给有依据的范围/方向，并标 estimated；不要生成伪精确数字，无依据则写 UNAVAILABLE。

## 6. Incident 分类

至少区分：

```text
requirement gap
plan diagnosis/design
implementation
architecture/coupling
test/fixture
environment/CI
tooling/process
Agent/tool integration/permission
data/experiment/evaluation
human acceptance
context/instruction
process overhead
```

按实际事故选择类别，不把分类表全部填一遍。每个典型事故回答：发生了什么、已确认根因／竞争解释、为什么没提前发现、应在哪层阻止、最低成本替代做法；证据不足时保留不确定性。

工具语法／路径／诊断错误与真实运行失败分开，重试按同一语义操作及根因分析；有副作用操作结果不确定时，先看实际状态查询证据，不能按所有 non-zero exit 总数判定事故严重度。

## 7. Plan / Agent / Harness 分责

不要把所有返工都归因给模型：区分 Planner 过度规定／技术委托不足、Executor 机械执行／越界、repository 或 experiment harness 覆盖不足、工具集成、评价／数据协议、目标反转、外部环境等。复盘建议不直接修改既定目标、接受研究路线或推进阶段；状态事实与项目决策按现有权限落地。

## 8. Cross-project synthesis

比较多个项目时，对每个主题至少记录：

```text
Project A evidence
Project B evidence
independent or inherited
consistent/conflicting
can generalize?
canonical owner
recommendation
confidence
```

优先寻找能同时解释两边事实的更高层规则，而不是简单折中。

## 9. Instruction architecture

区分规则的权威维护位置与必要执行入口，不将“唯一 owner”解释为每处只能出现一次。按职责判断归属，沿用项目实际文件布局：

| 规则职责 | 适当维护位置／执行入口 |
| --- | --- |
| 跨任务最低权限、工作区与真实报告底线 | 实际适用的全局／项目 AGENTS；当前任务入口仍需可访问 |
| 稳定个人偏好与适用产品／UX 模块 | Personalization 或项目模块；不由偏好授予额外权限 |
| 目标、不变量、数据／评价边界、长期决定与现状 | 项目合同／Project State，决策与实施事实分别维护 |
| 规划、技术委托、主线审查与阶段判断 | Architect 行为规则；实际决定由有权限的工具写入项目记录 |
| 本次范围、冻结条件、验收、交付与回传 | 有效 Task Plan／项目合同，不能只藏在规划端附件 |
| 风险验证、证据复用、失败／CI 执行方法 | Runner 等专业执行 Skill |
| 界面／真机、PWA 更新、复盘取证方法 | 对应专项 Skill，仅保存自身专业机制 |

不把单项目目录、工具偏好、环境事故或特定 UX 决定升级为全局硬规则；跨项目建议说明适用条件、已知反例或尚未覆盖的边界，不为填栏目编造案例。对候选全局规则与资产源文件，核查实际安装／访问情况，不能假定编辑后所有实例已生效。

同义重复先判断是否是失效副本，还是自包含 Plan、未安装全局规则或不同执行端所需的简短硬约束。仅在有效替代来源与实际读取入口成立后，按本次授权删除／合并冗余；不因追求唯一 owner 删掉 Runner 仍有用的保护。优先消除竞争定义和过时权威暗示，不复制完整模板或新增 Registry／同步框架。

需要跨资产修订时，指出具体 owner、拟改内容、依赖与迁移影响；只落地当前授权文件。必要合同摘要可在任务入口保留，其语义应来自有效权威，不通过循环引用或“保持一致”口号代替实际接入。

## 10. Counterfactual

回答：

> 如果从头再做，怎样在保留明确正确性、数据安全、Acceptance 和关键产品目标的前提下，用更少成本达到足够高的实际质量？

先保留 correctness、data safety、explicit Acceptance 与 durable product invariants 等硬约束，再讨论可减少的非必需 feature scope、polish、validation duplication、process overhead 或 speculative infrastructure。不要对不可测质量给伪精确百分比。

把建议落到 stage、Plan、validation、可选 human smoke、CI、state、release 等具体流程。

研究型项目同时考虑数据／评测协议、基线与预算／停止条件。已有必要 Gate 不得被反事实建议或 Optional USER CHECK 降格；减少验证须有风险与证据依据，不能为报告“节约”牺牲可复现性或隐去失败。

## 11. 输出

按当前问题与证据量选择有用内容，不要求每次完整输出全部栏目：

- 时间线/关键指标；
- 高返工区域；
- 高价值验证与低价值重复；
- Plan/Agent/Context 问题；
- 跨项目稳定规律；
- 单项目经验；
- 冲突与更高层规则；
- instruction ownership；
- 应保留/删除/合并的资产；
- 少量真正需要用户决策的分叉。

普通复盘输出一份主结果；正式 Plan/Handoff 按当前项目／Plan 的 TASK_RESULT 合同及有效旧字段回传，复盘结论合并或引用授权报告，不另立完成状态定义。FACT／INFERENCE 等结论标签与 PASS／FAIL／NOT_RUN／UNAVAILABLE／NOT_APPLICABLE 等验证状态分开；必要证据缺失影响哪些结论和验收须明示，不能写成已通过，辅助资料不可得也不机械阻塞全部分析。

Optional USER CHECK 仅用于有实际价值的非必要体验提示，不等待、不追踪、不反复提醒；已批准的必要人工／真机／线上 Gate 单独按合同处理，缺失时不能宣称任务 COMPLETE。只报告实际写入的事实／决策和真实交付，建议、报告完成与 Main 接受／阶段推进分别说明。
