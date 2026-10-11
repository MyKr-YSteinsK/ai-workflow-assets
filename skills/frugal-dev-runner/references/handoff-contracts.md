# Handoff Contracts — Runtime Reference

> `frugal-dev-runner` 的兼容与后备运行参考。仅在需要 Handoff 兼容说明、缺少正式返回合同，或明确需要 Checkpoint evidence packet 时读取相关部分。
>
> 本资产包的 TASK_RESULT 默认语义与 `Project-Incubator-v1/05-CODEX_PLAN_SPEC.md` 一致；该源规范用于资产维护，不是安装本 Skill 后必须存在的运行依赖。本参考正文自包含，不依赖未提供的外部模板。

## 1. `TASK_RESULT` contract

### 适用合同与旧项目

按当前用户授权确定有效项目合同、Plan 及 Revision。已有正式 Plan／TASK_RESULT 规范时遵循它；Plan 正文已提供的关键权限、冻结条件、验收和返回要求不被本参考的字段覆盖。无正式合同时，可使用下列简洁后备；普通任务无需因模板存在而升级为完整报告。

旧项目继续使用历史有效合同，包括状态词、命名、编号、已批准约束、实验结论与治理状态，不批量迁移。旧 MUST／SHOULD／HINT 按实际语义解释：保护硬要求，SHOULD 遵循原约定，HINT 仅为线索、不自动授权技术决策；产品优先级与技术权限分开。新旧实质冲突依当前任务明确授权的有效合同判断；不能安全确定时报告条款、版本、影响，暂停受影响动作。

新合同中的 FROZEN 必须保护，冲突或不可实现时报告建议；RECOMMENDED 可按代码／环境／验证证据优化并说明重要偏离；DELEGATED_TO_CODEX 允许明确委托的现场技术判断，不扩大文件、网络、Git、部署或目标修改权限。

正式 Plan 必须自带必要执行与返回要求，不能依赖不可访问的 ChatGPT 附件。必须读取的引用缺失时说明影响，不假称已读；缺少必要权限／验收依据则暂停受影响动作，Plan 已充分覆盖时可继续不依赖引用的工作。不固定本地合同目录，也不要求读取本资产包的维护源文件。

### 执行状态与证据

报告实际发生的工作，不把 Plan 描述当执行证据。新合同和无正式合同的后备采用：

| Status | 定义 |
|---|---|
| `COMPLETE` | 必要工作、必要验收及约定且适用的授权交付均完成 |
| `PARTIAL` | 已有有效成果但必要工作、验证或交付未完，且不属于更具体的阻塞／最终失败 |
| `BLOCKED` | 必要进展依赖当前不可得的输入、权限、环境、外部条件或用户决定 |
| `FAILED` | 必要工作或验收已实际执行，结果最终未满足合同，按授权预算／停止条件收口；不包括仍可正常修复的中间错误 |

多种情况同时存在时说明各项事实，以决定收口的原因判状态；不可得前置为 BLOCKED，已执行且最终不达标为 FAILED，其他未完为 PARTIAL。Shell／工具或 CI 一次报错不自动判 FAILED，先按语义操作和根因诊断。可信负面实验可以 COMPLETE；预定调查标准下的证据不足须标明限制；数据泄漏、协议失效、运行未完或关键证据缺失不得冒充可信负面结论。

必要 Push 未完成时，分别报告实现／验证与 Git 交付，整体不能 COMPLETE：不可得前置导致 BLOCKED，尚有可执行的未完交付为 PARTIAL，按停止条件确认最终失败为 FAILED。没有适用变更不造空提交，非 Git 工作区不自行初始化仓库。

验证采用 PASS / FAIL / NOT_RUN / UNAVAILABLE / NOT_APPLICABLE 或等价表达：PASS 为实际通过或明确来源与有效适用条件的证据复用；FAIL 为实际不达标；NOT_RUN 为适用但未执行；UNAVAILABLE 为环境、权限、数据或结果不可得；NOT_APPLICABLE 为不适用。失败、未执行或不可得不能放在“已通过”中。证据对应实际版本和环境，启动不证明最终指标，本地／静态／CI／浏览器不自动证明生产或真机。

### 必要验收与 Optional USER CHECK

Optional USER CHECK 是有明确价值时才提供的非阻塞体验提示，不等待、不追踪、不反复提醒，无价值则省略。**不能将 Plan 明确必要的验收降格为可选**，除非已批准替代验收。普通开发没有真机 Gate 时，缺少真机证据只说明边界；必要真机／PWA 升级 Gate 不可获得时报告 UNAVAILABLE 或 NOT_RUN 及原因，不宣称该项 PASS 或任务 COMPLETE。

### 简洁回传骨架

字段按任务合并或省略不适用项；重要失败、权限和验收事实不能省略。默认中文，保留稳定技术标识：

```markdown
# TASK_RESULT｜<Plan ID> / <Revision 或实际输入来源>

- Status：COMPLETE / PARTIAL / BLOCKED / FAILED；理由：...
- Base / Final Working State：项目、基线／最终分支与提交、工作树；非 Git 如实说明。
- Work & Technical Decisions：实际文件变更／实验；RECOMMENDED 调整；DELEGATED_TO_CODEX 选择及依据。
- FROZEN / Acceptance：逐项回应硬约束、关键目标与必要验收。
- Verification & Evidence：实际检查与结果、来源／位置、版本和环境、指标及证据限制。
- Git / Remote Delivery：提交、Push 远端与分支、核验方式及远端 SHA、Merge／Deploy（若相关）；未完成及原因。
- Deviations / Limitations：偏离、失败、未验证项与残余风险。
- Artifacts & Durable Findings：产物保存／清理、实际状态文件变更和可复用发现。
- Next / Required Decisions（如需）：下一边界、Checkpoint Signal 或用户决定。
- Optional USER CHECK（仅有价值时）：最少体验提示，不能代替必要验收。
```

有明确 Revision 则报告实际执行版本；历史输入未标修订时说明实际来源，不编造编号。必要实验证据包括数据版本、基线、指标、比较条件与停止依据；Agent／高风险任务按需补运行、迁移、安全和恢复证据。Project State 遵循实际项目路径、更新时点和权限；不得把对话建议称为已写入、已安装或已推送。

### Git 持久化与最终回执

按当前任务／项目约定保留有价值代码、Plan、报告和阶段证据，排除敏感或无合法共享权限的数据、巨大缓存、临时依赖及垃圾。Commit、Push、Merge、Deploy／Publish 分开；普通 Push 不自动授权生产发布或历史重写，触发部署的 Push 须核对该副作用已获授权。远端核验记录实际 remote／branch、观察到的 SHA 及方式；并行导致远端前进时核查预期提交是否被包含。

只有任务需要时才创建仓库结果文件；无此要求可直接对话回传。需要入 Git 时：

1. 文件记录任务事实、Plan ID／Revision、必要证据、已确定的基线／证据来源提交和结论，不要求包含自身最终 Commit SHA，也不预写未发生的 Push／核验成功。
2. 提交授权任务产物和报告，完成必要 Push／远端核验；文件结论以保存时点为准，后续交付由回执补全。
3. 最后一次 Commit／Push 后，在对话主结果中补充最终 SHA、远端核验、工作树和结果文件路径，不为回填自身 SHA 反复 Amend。发生新变更时重评受影响证据；不能自动把早前通过的构建／部署身份算作最终提交已验证。

只输出一份主结果，仓库文件与最终对话回执对应同一任务结论。UI/PWA 证据合并进 Verification & Evidence，缺失证据进限制，体验建议进 Optional USER CHECK；不附第二份完整专项报告或逐命令流水。Checkpoint Signal 仅是建议，不阻止仍可执行工作。TASK_COMPLETE、EVIDENCE_ACCEPTED、STAGE_ADVANCED 分开；提交或回传不自动授权主线合并、结论接受或阶段推进。

## 2. `CHECKPOINT_PACKET` contract

Only generate when a Development Architect Checkpoint Review is needed and the Project cannot directly inspect the current repository sufficiently. Follow an accessible, effective project-specific packet contract first; this self-contained structure is a fallback, not a dependency on an external template.

```markdown
# CHECKPOINT_PACKET — <Milestone / Date>

## Repository Identity
- Repository:
- Branch:
- HEAD:
- Working tree:

## Milestone Summary
- <what capability / stage was completed>

## Material Changes Since Last Checkpoint
- <architecture / product / data / release changes>

## Current Verification State
- <relevant tests / CI / browser / device / production evidence>

## Hotspots / Rework
- <areas with repeated changes or instability>

## Current Risks / Technical Debt
- <risk>

## Decisions Made
- <links/summary of new durable decisions>

## Open Questions for Review
- <what the Architect should independently reassess>

## Optional USER CHECK
- <only if useful; non-blocking, not tracked; omit section if none>
```

Keep it evidence-oriented and compact. Optional USER CHECK has the non-blocking meaning and necessary-acceptance exception defined above; it is not project backlog. Do not paste the whole Git history, all old Plans, or full test logs.
