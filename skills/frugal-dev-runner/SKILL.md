---
name: frugal-dev-runner
description: 用于软件实现、bug/refactor/测试修复、repository bootstrap，以及 Agent/ML/研究工程中已授权的实现、实验运行和验收。提供风险驱动验证、证据复用、CI/环境排障及异步操作收口。不用于一般知识讨论或纯研究综述。
---

# Frugal Dev Runner

在实际用户授权和项目合同内持续推进。此 Skill 提供执行方法，基本权限、必要验收和 Git 操作由项目与当前任务决定。

## 1. Preflight 与按需加载

核对目标 workspace/repo、分支、用户改动和实际适用的 AGENTS。工作输入可来自直接对话、对话内规划或有效 Plan；核对任务身份、基线、实际权限与验收，沿用旧项目有效合同及编号。先读相关目标和状态，按需查运行方法，不扫描整个仓库。

- 已建档的 canonical 环境优先复用，包括新工作树；核对依赖锁与命令语义，避免裸 `uv` 或包管理器隐式同步或新建第二套环境。GPU 占用、磁盘、后台作业等按本次任务增量核实。运行前确认工作目录及默认输出、临时位置和实际写入边界。
- 新项目接入、恢复入口或环境档案有缺口时，按需查 [仓库接入参考](references/repository-bootstrap-contracts.md)。正式交接或 Hub 续接确需细节时，查 [任务交接参考](references/handoff-contracts.md)；普通任务无需读取。
- 实际启动、接管或续跑预计耗时较长的实验，或验证中断恢复时，按需查 [实验运行与续跑](references/experiment-run-recovery.md)。普通快速检查与方案讨论无需加载。
- ChatGPT Project 附件、资产候选文件和未来路径不自动构成本地规则。必要内容需实际可读或由任务自足提供；缺权限或验收依据时说明影响，暂停依赖缺口的动作。

## 2. 连续执行与任务协调

在目标、必要约束、验收、数据和已授权操作内，自主调查、试验、选择或调整技术方案，处理可修复错误。任务按依赖拆分，不按时长或步数机械拆分。影响目标、验收口径或重大方向的变更、无法获得必要前提或超出授权的高风险操作，才需要相关决策。

多个输入汇合时，按 Issue 链接或其他实际来源识别任务，适用时核对编号和修订，再对齐依赖与资源，复用可共享的工作。重叠写入、共享资源或不兼容协议不能安全隔离时串行；只暂停受实质冲突影响的工作。Worktree 仅隔离代码检出，不隔离环境、GPU 和输出。在现有状态中保留证据、下一步及重取输入的线索；接手时按实际有效输入核对权限与验收。

## 3. Failure-mode-based verification

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

## 4. Verification reuse

对本轮已经 PASS 的昂贵验证做轻量影响判断，不建立永久 evidence ledger。

复用前检查该结论依赖的 source、configuration、dependencies、environment、artifact/build identity 与 runtime/deployment assumptions。只有相关条件没有 material change 时，旧证据才适用；不能只按 docs/tests/CI/config 文件标签决定。

- README 纯文字修改且不参与构建，可以复用无关 build evidence；CI 改变 runtime/build environment 时，必须重新评估 build/test evidence；
- 旧功能测试不能自动证明新发布产物 identity 或 production deployment；
- build 已包含 compile/typecheck 且上述证据边界仍成立时，不重复 standalone 命令，除非隔离失败；
- 开发中 targeted，任务/集成/release 边界再按风险扩大；
- 第二种检查只有能发现第一种证据容易漏掉的 materially different failure mode 时才值得增加；自动几何检查与真实触控观察即使目标相近，也可能有不同漏检边界。

区分影响安全、正确性或必要前置条件的 blocking check 与增强证据/诊断便利的辅助检查；辅助检查自身失败不自动阻止主任务。必要条件已有可靠 PASS 且依赖未 material change 时复用现有证据；不要为了“更保险”继续新增 probe、hash、snapshot 或 diagnostic gate，除非它能覆盖尚未解决的具体 failure mode。

## 5. 异步与外部状态

对 network、browser、background queue、cache、Service Worker 等异步流程：

> Success / failure 由 observable state 或明确 timeout/deadline condition 判定；不能因为固定时间已经过去就认定操作成功。

Timer 可用于 polling interval、timeout/deadline、retry backoff、rate limiting，以及时间本身就是业务条件的场景。它是调度工具，不是成功证据。

外部下载、runner、网络、部署传播等失败不可无限重试；相同条件重复且没有新证据时停止机械尝试，改变调查方法。只有必要条件确实不可获得时才报告受阻，不用产品代码补偿环境问题。

Retry / STOP 以同一 semantic operation 与 root cause 判断，不累计无关命令的 non-zero exit。真实 provider/service/install/runtime/live operation 的结果不确定时，先查询当前状态，再决定是否重试；不得盲目重复。

## 6. Failure classification

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

## 7. CI failure progression

失败次数本身不决定任务状态。先分类并检查可获得证据；按同一 CI semantic operation / root cause 判断机械重复，不按所有 non-zero command 的总次数计数。Shell parse、path 和证据解析错误按上节分类，本身不算 CI/runtime attempt。

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

## 8. 交付与项目状态

保护用户已有工作和历史，只提交当前任务的授权变更。核对实际 remote、目标分支和 Push 副作用；Commit、Push、Merge、Deploy／Publish 分开判断。需要远端交付时查询实际远端 ref，本地 tracking ref 不算远端证据。普通文件工作区不自行初始化，无变更不造空提交。按价值和权限保留证据，清理明确可重建且无用的本次临时产物。

在授权内把实质变化写回项目已有入口：当前事实、长期决定、环境和运行限制、可复用故障，以及必要的路线或阶段结果。区分局部实现、证据接受及正式推进。项目保留给 Main 或用户的决定按原权限；其他已委托的技术和阶段判断可以由 Codex 执行。普通任务无需增加管理文件。正式 Plan 默认不提交到项目 Git 历史。

普通任务用简洁对话回执，注明实际工作、关键验证与缺口、适用的真实交付。正式交接补实际来源、适用编号／修订及必要证据；按任务要求给一份主结果。区分实际通过、未运行、不可得与失败；可信负面实验可以完成调查，必要验收缺失仍是交付缺口。Optional USER CHECK 只在有价值时作为非阻塞体验提示，不能替代已经要求的真机、发布或其他必要证据。
