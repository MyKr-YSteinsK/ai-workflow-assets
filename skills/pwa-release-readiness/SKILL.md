---
name: pwa-release-readiness
description: 用于修改、排查或验收 Service Worker 注册/激活、PWA 离线/缓存生命周期、已安装客户端升级、更新 version probe、相关 base path/scope/precache、PWA 缓存/升级相关部署身份或明确的 PWA 发布就绪任务；包括旧版不更新、混合版本资源、升级后离线失效或本地数据丢失。未影响这些路径的普通 UI/业务 patch、仅提到 PWA/standalone、非 PWA 的构建 SHA 或部署身份不触发。分开验证部署身份与客户端更新，仅覆盖实际受影响或合同要求的 PWA 边界。
---

# PWA Release Readiness

## 1. 触发边界

使用于：

- Service Worker registration/install/waiting/activation/controllerchange；
- PWA offline/cache ownership / lifecycle；
- installed-client update；
- PWA 更新流程中的 app/version probe；
- PWA-specific base path/cache/scope 与 deployment identity；
- PWA release readiness。

普通 CSS、文案、纯业务逻辑任务不因项目采用 PWA 自动加载本 Skill；但若实际改变 precache、离线资源兼容或升级行为，仍需覆盖该受影响边界。只有 standalone 布局／触控问题时使用 UI 专项方法。普通非 PWA build SHA、deployment identity 或 production endpoint 问题由工程执行方法与 repo release rules 处理，不因此引入 Service Worker / installed-client gate。

遵循当前授权、实际可读的项目 AGENTS 与有效 Plan，保留未被替代的旧合同；本 Skill 不授予部署、设备访问或数据修改权限，不以 Runner 自动触发为运行前提。按必要验收与真实风险选择下列相关部分，不为普通 patch 自动建设完整更新系统或执行所有 release Gate。

## 2. 两条链分开

### Deployment identity

回答：

> 线上实际运行的是哪个 app version / build / commit？

需要单一 version/build identity 来源；正式部署应能从真实 production endpoint 回读，而不是只看 workflow 绿色。

关联实际源码／配置、构建产物和目标环境的身份。结果文档提交可晚于被验证构建；最终 Git SHA 不自动证明该构建或线上版本已经验证，也不要求将结果文件自身最终 SHA 回填进文件。

### Installed-client lifecycle

回答：

> 已安装旧客户端如何可靠发现、取得、激活新版，并在失败时保持可用？

按项目实际模型考虑：

```text
remote version known
registration ready
installing
waiting
activation
controller changed
reload/apply
failure / timeout / retry
```

不要把两条异步链压成一个“update available”布尔值。Production build identity 与 installed-client lifecycle 的证据不能互相替代。

## 3. 建设时机

原则：

> identity early；lifecycle before production。

- Prototype/首次部署：建立低成本 app/build identity、稳定 base/cache ownership；
- Stabilization：当 shell/数据模型稳定且存在真实安装环境时，建立可靠 installed update lifecycle；
- Production 前：按是否已有旧 production 安装版选择升级演练路径。

上述阶段名是建设时机示例，沿用项目真实阶段与当前授权；不由本 Skill 宣布阶段推进，也不要求每次触发都补齐整个生命周期。演练在授权的环境与数据范围内进行，不为取证向生产部署候选版。

首次上线尚无真实旧 production 安装版时，可在 production-equivalent 环境用连续两个候选构建演练：

```text
candidate A installed → candidate B deployed → update discovery
→ install/wait/activate → controller/reload/apply
→ local business data preserved
```

按当前实际相关条件检查 origin、base path、Service Worker scope、caching、resource serving 与 deployment behavior 的等价性；存在差异时说明 evidence limitation。正式部署后，production endpoint identity 仍需单独验证。

已有真实安装用户时，应覆盖适用的 old installed production build → new production build 更新路径。不能把 pre-production 演练声称为真实 production installed-client 验证。

不要在尚未验证产品模式时先建设复杂更新状态机，也不要拖到正式用户长期停旧版后再补。

## 4. App version 与 data/content version

如果应用代码与内容/离线包生命周期不同，分别建模；不要用一个 revision 同时表达两种变化，避免 app deploy 被误报成数据更新。

## 5. 验证

按变化边界选择：

- manager/state machine → 覆盖 materially different event ordering；
- artifact → manifest/precache/base/version metadata；
- deployment → exact tested source/build identity；
- production → 真实端点回读 version/commit；
- installed client → 旧版检测新版、apply/reload、业务本地数据仍在；
- failure → probe/registration/worker/deployment/cache 原因分开。

静态 artifact inspect 不能替代真实 Service Worker lifecycle；CI 成功也不能替代 installed-client 路径。

异步成功由实际事件／可观察状态及对应构建判定；timeout 是失败／不可得边界，固定等待结束不是成功证据。事件顺序检查按实际模型选取安装未完、waiting、控制权变化、失败恢复等不同风险，不机械枚举所有排列；复用证据须仍覆盖当前构建、配置、环境及生命周期假设。

## 6. 数据安全

正常更新不得依赖：

- 清站点数据；
- 重装应用；
- 丢弃本地业务数据。

若更新失败，优先保留当前可用版本并提供可恢复路径。

区分可重建资源缓存与不可丢失的业务数据；缓存迁移／清理只处理项目明确拥有且本次获准的范围，不能用全站清除、无关 cache 删除或重装绕过正常升级故障。

## 7. Release boundary

只有 PWA 路径受影响或明确 PWA release 时扩大 PWA gate；不把设备专属体验提示变成普通开发任务的默认 blocking gate。

Version classification 与 publish cadence 分离；具体版本、tag/publish、部署及回传规则按当前有效项目／Plan 合同和 AGENTS，不另建 Git 工作流。Push／Merge 不自动授予 Deploy／Publish；实际目标分支 Push 会触发部署时，先确认既有授权覆盖该副作用，否则暂停相应 Push 并报告交付缺口。

必要 installed-client／真机／线上 Gate 不可完成时，按有效合同报告缺失及原因，不将其降格为可选或仅凭构建成功宣称任务 COMPLETE。没有这类必要 Gate 的普通任务，只报告实际相关证据及限制，不因未做全套发布演练自动阻塞。

## 8. 证据边界 / Optional USER CHECK

目标平台真实安装、Safari/iOS standalone、更新触感等未实际执行时如实说明，不以 desktop browser、静态检查或候选演练冒充真实 production installed-client 证据。按项目约定的验证标签或等价表达报告 PASS / FAIL / NOT_RUN / UNAVAILABLE / NOT_APPLICABLE，注明版本、环境及实际观察或复用来源。

Optional USER CHECK 仅在有体验价值时附 1–3 个最少步骤，不要求用户现在执行、不等待、不追踪、不反复提醒。它不改变完成状态，也不替代已批准的必要验收；必要人工／真机 Gate 单独按合同处理。

证据合并进主结果；正式 Plan/Handoff 按当前项目／Plan 的 TASK_RESULT 合同及有效历史字段回传，将 PWA 证据放入 Verification & Evidence、Deviations / Limitations 与有价值时的 Optional USER CHECK，不重定义任务状态或另附完整 PWA report。
