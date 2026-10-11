---
name: frugal-dev-runner
description: 用于软件实现、bug/refactor/测试修复、repository bootstrap，以及 Agent/ML/研究工程中的已授权实现、实验运行与工程验收。提供风险驱动验证、证据复用、CI/环境排障、异步副作用与交付收口；遵循有效项目/Plan 合同，UI/PWA 方法按受影响边界叠加。不用于纯论文综述、一般知识讨论或业务数据分析；不为简单操作强制增加管理文件或完整流程。
---

# Frugal Dev Runner

本 Skill 提供专业执行方法，不授予额外权限，也不替代项目的 Plan、TASK_RESULT 或阶段治理合同。已有工作空间、修改保护与基本执行规则继续保留；使用 Skill 不意味着重建治理文件或自动升级旧项目。

通用底线应通过实际适用的全局／项目 AGENTS 或自包含任务入口提供，不能以本 Skill 自动触发为前提。资产包里的全局候选不代表当前环境已安装；本 Skill 继续保留关键保护，负责风险驱动验证、证据复用、失败分类、CI 与异步副作用等专业方法。

## 1. Preflight

开始编辑前用最小成本确认：

- 当前 repository/package、branch 与 working tree；
- Task/Plan 是否明显属于当前 repo；
- 用户已有未提交修改；
- 当前 repo `AGENTS.md` 与本任务相关的 Project State。
- repo 已约定的 canonical/root 执行环境及命令语义。

先区分 Git 仓库与普通文件工作区；非 Git 工作区不为满足流程而初始化仓库。确认当前任务允许的读取、编辑、运行及产物位置，保护无关修改；用户指定边界优先，不默认向父目录、同级项目或其他位置写入。

Plan 名称、技术栈、路径、模块或任务语义与当前 repo 明显不匹配时停止并报告。
若 repo 定义了 canonical/root environment，新 worktree 也优先复用；运行 `uv`、Python 或 package manager 前先确认仓库约定，避免裸命令意外创建第二套 worktree-local virtualenv 或隐式 sync。Windows 下复杂 PowerShell inline expression 一旦出现 parser error，改用原子命令或更合适的工具，不继续修补 one-liner。


## 1.1 Runtime contract loading

按当前用户授权确定有效项目合同、Plan 及 Revision，读取其中点名的必要规范。项目正式合同及 Plan 正文的关键权限、冻结条件、验收和返回要求优先于 Skill 后备模板；未被明确替代的历史约束继续有效。

- ChatGPT Project 中的规范不自动存在于本地。引用路径须实际存在且可读；缺失时说明缺失项及影响，不能假称已读。缺少必要权限／验收依据时暂停受影响动作；Plan 已完整给出所需合同时可继续不依赖该引用的工作，不机械因辅助 Reference 缺失而阻塞全任务。
- 新项目尚无本地合同入口时，首个 Plan 必须自包含任务身份／适用基线、授权路径与操作、冻结约束、推荐与委托、必要验收、输出边界、交付和回传义务。只在授权内创建或合并本地入口及必要合同，实际落地并检查可读后再引用；已有项目先复用有效入口、编号、状态和历史合同，不默认迁移。后续任务仅加载与本任务相关的合同，无需复制整个孵化器。
- 涉及新 repo bootstrap、创建／修复 `AGENTS.md` 或 Project State 时，先遵守有效项目合同；需要后备结构时读取 [repository-bootstrap-contracts.md](references/repository-bootstrap-contracts.md) 相关部分，不凭印象造格式，不为一致性改写已有有效结构。
- 正式 Plan/Handoff 优先按当前合同回传；需要兼容说明或无正式合同的后备 TASK_RESULT 时，读取 [handoff-contracts.md](references/handoff-contracts.md) 的第 1 节。已完整提供返回合同的任务无需为加载另一模板而重复读取。
- 仅在明确需要 Checkpoint Review 且 Development Architect 无法充分读取 repo 时，读取同一 Reference 第 2 节的 CHECKPOINT_PACKET；项目已提供有效合同则遵循它。
- 普通 bug、feature、refactor 不为“可能以后有用”加载全部 References。必要生成合同不可访问且任务未提供足够内容时，报告并暂停受影响生成，不静默替换格式。

## 2. 读取与 Plan 解释

从目标行为、点名文件、直接调用方、相关测试/配置开始定向读取；信息不足再扩大，不默认全仓扫描。

新项目或明确升级项目按有效合同使用：

- `FROZEN`：已批准目标、验收、合法数据边界及必须保护的行为等硬约束；事实冲突、不可实现或重大问题时报告影响和建议，不静默绕过。
- `RECOMMENDED`：认真评估 Planner 有依据的建议，允许根据代码、环境与验证优化；回传重要偏离和理由。
- `DELEGATED_TO_CODEX`：对明确委托的技术判断自主调查、比较与实施；不扩大文件、网络、Git、部署或项目目标修改权限。

旧项目的 `MUST / SHOULD / HINT` 等按历史有效合同实际语义解释：保护硬要求，按原约定判断 SHOULD 的调整条件，HINT 仅为线索而非技术授权。不机械替换字段，不重置命名、编号、结论或治理状态；产品需求优先级与技术决策权限分开。实质冲突按当前任务明确授权的有效合同判断；不能安全确定时说明版本、条款和影响，暂停受影响动作。

先验证技术假设，在有效硬约束、scope 与 Acceptance 内自主选择更小、更一致、更可靠的实现；发现未知技术原因应继续合理调查，不把推荐细节当冻结事实。

`Optional USER CHECK` 是有价值时才提供的非阻塞体验建议，不等待、不追踪、不反复提醒。**Plan 明确规定的必要验收不能降格为可选**，除非已批准替代验收。普通 UI 任务没有真机 Gate 时可报告自动化与证据限制，另附真机建议；明确要求真机／PWA 升级验证但不可获得时，必须报告未验证及原因，不写 PASS 或 COMPLETE。自动化不能冒充真机／人工证据。

## 3. Scope

只做当前目标。不要顺便：

- 无关重构；
- 依赖升级；
- 全仓格式化；
- 新通用框架；
- 修低价值 warning；
- 扩展未请求功能。

邻近问题只有在阻塞当前任务，或构成立即正确性/安全风险且当前授权允许时一起处理；明确范围外的问题先报告，不因发现风险自行扩权。

## 4. 连续执行与决策门

一个 coherent Task/Plan 可以包含很多 Phase；不要按行数、Phase 数或开发时长机械拆分。

技术未知、前一阶段结果推翻后续技术前提时，先自主定向阅读、最小实验或局部验证，在当前 scope 内调整方案。“还没搞清楚技术原因”本身不足以移交用户。

只有出现以下情况才移交用户决定或报告 BLOCKED：

- 需要用户产品/UX/需求取舍；
- 必要信息、输入、权限、环境或外部条件当前无法获得；
- 下一步必须突破 FROZEN／有效旧硬要求、scope、硬边界或授权，包括扩大到无关核心架构；
- 需要未授权 destructive/live operation。

## 5. Failure-mode-based verification

先问：

> 这次变化最可能怎样失败，哪种证据能真正发现它？

再选最小有效验证。

常见映射：

- docs/copy/non-runtime metadata → diff/format/link 等直接检查；
- localized logic → 能让旧实现失败的 regression/invariant test；
- type/interface/data-flow change → 必要 typecheck；
- data/schema/migration → old/new/failure/compatibility path；
- Agent 策略/工具链 → 代表任务中的实际工具调用、关键行为、停止原因与任务结果；注册成功或一次调用成功不单独证明策略有效；
- ML/研究实验 → 与判定有关的数据/切分/标签边界、评价协议、真实基线及运行条件；核查结果可比性，区分有效负面结论与无效实验，不把启动成功当作实验验收；
- UI/platform-specific → 叠加 `ui-real-device-qa`；
- PWA/SW/installed-client update/PWA-specific deployment identity → 叠加 `pwa-release-readiness`；
- 普通非 PWA build/deployment identity → 本 Skill + repo 的 release rules，不因此加载 PWA lifecycle；
- release/high-risk cross-system → 在边界运行对应完整 gate。

不要用“更多命令”代替风险分析。

## 6. Verification reuse

对本轮已经 PASS 的昂贵验证做轻量影响判断，不建立永久 evidence ledger。

复用前检查该结论依赖的 source、configuration、dependencies、environment、artifact/build identity 与 runtime/deployment assumptions。只有相关条件没有 material change 时，旧证据才适用；不能只按 docs/tests/CI/config 文件标签决定。

- README 纯文字修改且不参与构建，可以复用无关 build evidence；CI 改变 runtime/build environment 时，必须重新评估 build/test evidence；
- 旧功能测试不能自动证明新发布产物 identity 或 production deployment；
- build 已包含 compile/typecheck 且上述证据边界仍成立时，不重复 standalone 命令，除非隔离失败；
- 开发中 targeted，任务/集成/release 边界再按风险扩大；
- 第二种检查只有能发现第一种证据容易漏掉的 materially different failure mode 时才值得增加；自动几何检查与真实触控观察即使目标相近，也可能有不同漏检边界。

区分影响安全、正确性或必要前置条件的 blocking check 与增强证据/诊断便利的辅助检查；辅助检查自身失败不自动阻止主任务。必要条件已有可靠 PASS 且依赖未 material change 时复用现有证据；不要为了“更保险”继续新增 probe、hash、snapshot 或 diagnostic gate，除非它能覆盖尚未解决的具体 failure mode。

## 7. 异步与外部状态

对 network、browser、background queue、cache、Service Worker 等异步流程：

> Success / failure 由 observable state 或明确 timeout/deadline condition 判定；不能因为固定时间已经过去就认定操作成功。

Timer 可用于 polling interval、timeout/deadline、retry backoff、rate limiting，以及时间本身就是业务条件的场景。它是调度工具，不是成功证据。

外部下载、runner、网络、部署传播等失败不可无限重试；相同条件重复且没有新证据时停止机械尝试，改变调查方法。只有必要条件确实不可获得时才报告受阻，不用产品代码补偿环境问题。

Retry / STOP 以同一 semantic operation 与 root cause 判断，不累计无关命令的 non-zero exit。真实 provider/service/install/runtime/live operation 的结果不确定时，先查询当前状态，再决定是否重试；不得盲目重复。

## 8. Failure classification

失败先分类，再修：

```text
requirement / plan
product implementation
test / fixture
tooling / process (local command or PowerShell syntax, path typo, temporary diagnostic code, evidence parsing)
environment / external
human acceptance
verification / workflow
```

未触发目标操作、没有改变目标状态且无未知副作用的 tooling/process failure，应修正工具调用后继续；不消耗 live/external retry，也不因累计数次无关 shell error 就把 Task 标为 Blocked。若命令已触发真实 provider/service/install/runtime/live operation，则按该语义操作分类；其结果不确定时先查状态，再决定下一步。

不要为了让测试变绿而削弱 Acceptance；如果修 test/fixture 必须改用户运行时行为，重新判断 scope 与 version impact。

## 9. CI failure progression

失败次数本身不决定任务状态。先分类并检查可获得证据；按同一 CI semantic operation / root cause 判断机械重复，不按所有 non-zero command 的总次数计数。Shell parse、path、临时诊断或证据解析失败按 Section 8 处理，本身不算 CI/runtime attempt。

```text
CI failure → classify → inspect evidence
新的、可操作的根因 + 当前 scope 内 + 成本合理
→ repair → 验证 new candidate SHA
同一 candidate SHA 需确认 flaky / external condition
→ 有限 same-SHA rerun
相同 failure / 外部条件下重复动作无新证据
→ 停止机械 rerun → 改变调查方法
必要进展依赖当前不可获得的信息、权限、环境、外部条件或用户决定
→ Blocked / handoff
```

区分 same-SHA rerun、修复后的 new candidate SHA 验证与 external/flaky failure，并将结果关联到实际 candidate。Task/repo 明确规定昂贵 CI 预算时遵循该预算；否则不设全局固定次数，但禁止没有新证据的重复动作。无法确定 CI 是否已启动或结果是否已产生时，先查 CI 状态再决定是否重跑。

## 10. Git / delivery

保护用户已有工作，不 force push、不重写已 push history、不丢弃或误提交无关修改。按项目规则保存有价值的阶段代码、Plan、结果与失败证据；不机械提交 secrets、敏感或无法合法共享的数据、巨型缓存、临时依赖和无价值生成物，不以 generated/temp 标签排除有价值的授权产物。

Commit、Push、Merge、Deploy／Publish 分开；操作和时点遵循当前授权及 repo 规则。本 Skill 不自行授权 Push 或生产发布；Push 会触发部署时先核对既有授权是否覆盖该副作用。必要 Push／远端核验未完成时，报告交付未完及原因，不能仅因实现测试成功而宣称 COMPLETE。无适用变更不造空提交，非 Git 工作区不自行初始化。

正式 GitHub 工程 Plan 通常要求聚焦 Commit、Push 到授权 remote／分支并核验真实远端 ref；本地 Commit 或本地 tracking ref 不单独证明远端已同步。Push 前识别实际分支的 CI／部署行为；授权不覆盖部署时暂停该 Push，报告交付缺口，只有任务已允许的安全目标分支才能作为替代。分支已 Push 不代表主线接受结论或允许 Merge；Merge 也不自动授权 Deploy／Publish。

TASK_RESULT 入 Git 时，仓库文件记录任务事实及已确定的基线／证据来源，不要求包含自身最终提交 SHA；最后一次 Commit／Push 后，在对话主结果中报告最终 SHA、实际远端核验与工作树状态，不为回填自身 SHA 反复 Amend。按任务需要持久化，不强制每个小任务新建报告；详细后备收口规则见 handoff Reference。

## 11. Project State

遵循项目状态路径、更新时点和权限约定。在 COMPLETE、PARTIAL、BLOCKED、FAILED、暂停或正式交接边界，仅在授权且当前事实 material change 时维护，不以成功为前提，也不为满足通用模板新增状态文件：

- `CURRENT_STATE`：当前能力、版本/发布状态、限制/风险、Active work 或当前相关 workflow/delivery facts 实质变化；
- `DECISIONS`：新增/替代会约束未来多个任务的长期决定；
- `PROJECT_BRIEF`：稳定产品定义、核心架构或长期不变量实质变化。

区分已验证能力和未验证/部分实现。状态维护已授权且事实发生变化时，同一任务结束前更新实现、测试、环境限制、实验运行、分支及交付事实，与本次变更一起提交；不一律等待下一轮 Planner 审查。实现完成但部署缺权限、部分迁移发现长期限制等留下真实快照，不把计划和待核验内容写成已完成。

研究路线正式接受、阶段推进、重要目标／已批准范围改变、主线合并和新重要方向，按既定权限由 Planner Main 审查，重大取舍仍需用户批准。明确委托且在范围内的技术决定可以记录依据，不假称获得额外项目批准。保留 TASK_COMPLETE、EVIDENCE_ACCEPTED、STAGE_ADVANCED 的责任区别，不将每个小任务变成三轮审批。

不要写临时失败、命令流水或 old SHA 历史，也不要因为“Task 完成”机械修改。Optional USER CHECK 不进入持续追踪队列；真正长期存在的证据限制放 Known limitations / risks。沿用项目已有文件或合并职责，不强制新建三份状态文档；主线保留的决策字段不得随事实更新被改写。

## 12. Completion / TASK_RESULT / Checkpoint signal

按当前有效合同判定收口。新合同及无正式合同的后备采用：COMPLETE＝必要工作、必要验收和约定且适用的授权交付均完成；PARTIAL＝已有成果但必要内容未完成且不属于更具体的阻塞／最终失败；BLOCKED＝必要进展依赖当前不可得的输入、权限、环境、外部条件或用户决定；FAILED＝必要工作／验收实际执行且最终未满足合同，按授权预算／停止条件收口，不是可正常修复的中间错误。多种情况同时存在时说明各项事实，报告实际决定收口的原因；有效旧合同的状态词按原约定回传。

一个 Shell 或 CI 错误不自动判任务 FAILED。正确执行、得到可信负面实验结论可以 COMPLETE；实验无效或关键证据缺失不能伪装为负面结论。必要 Push／真机／线上 Gate 缺失不能 COMPLETE；Optional USER CHECK 不改变状态。以后实际使用发现的 bug 作为新 Task/Plan 处理，不为可能的未来问题保持当前任务开放。

验证用 PASS / FAIL / NOT_RUN / UNAVAILABLE / NOT_APPLICABLE 或语义等价表达。PASS 只包括实际通过，或注明来源及有效适用条件的证据复用；失败、未运行或不可得不得放在“已通过”中。声明实际证据与版本，不将启动、静态检查、桌面浏览器或 CI 成功扩大为最终指标、真机或生产证明。

普通任务最终报告按实际需要简洁包含，不机械输出全部标题：

- 实际变化；
- 关键验证、实际结果及未执行／不可得事项；
- 真正的剩余风险、已知限制或证据边界；
- delivery 状态（若发生）；
- 末尾可附非常短的 Optional USER CHECK（仅有明确体验价值时）。

正式 Architect Plan/Handoff 或明确约定 TASK_RESULT 的任务，按已加载的有效项目合同／Plan 返回；回应 Plan ID／Revision、实际工作与技术决定、FROZEN 和关键验收、验证证据、Git／远端交付、偏离限制及产物。缺少正式返回格式时才按需读取 handoff Reference 的兼容后备，不能覆盖 Plan 已给出的条件。不能仅因消息含 Phase、Step 或 Plan 字样就升级普通任务。未标 Revision 的历史输入按实际来源识别，不编造修订号。

一项任务只输出一份主结果。UI/PWA 专项证据合并进该结果；正式 Handoff 使用 TASK_RESULT，不另附完整专项报告或逐命令流水。

若出现同一区域反复返工、新架构/共享状态、完整 milestone、跨模块高风险、真实体验持续不满意、验证 harness 成为主要成本或即将 Release 等强信号，额外提示：

`建议进行 Development Architect Checkpoint Review：<简短原因>`

没有明显收益时不要提示。Checkpoint signal 只是复盘建议，不自行停止当前仍可执行的工作。

## 13. 最终原则

按当前合同完成必要实现、验收与交付。对额外流程、重复验证或辅助产物，先问：

> 它现在具体推进了什么已批准目标、降低了什么风险，或产生了什么有价值的新证据？

答不出时就不要默认增加；有明确任务价值的实现、探索和交付，不因无法表述为“降低风险”而被排除。
