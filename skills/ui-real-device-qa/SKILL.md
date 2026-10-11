---
name: ui-real-device-qa
description: 用于实现、修复或验收 Web/移动界面的布局、响应式、safe area、fixed/sticky、滚动、触控、焦点/键盘、弹层、动画及 Safari/WebKit/standalone 界面表现；也用于定位“跳、闪、遮挡、错位、不丝滑”等可观察体验问题。纯文案且不影响布局、非 UI 逻辑、框架讨论或仅 PWA 更新协议不触发。按受影响边界验证，区分自动化、真机与主观证据；不默认增加完整设备矩阵或真机 Gate。
---

# UI Real Device QA

## 0. 适用边界与任务合同

先确认本次修改或问题实际影响哪些界面行为；文案改变了换行／几何时仍需相应布局检查。Safari／PWA standalone 的界面表现由本 Skill 处理，Service Worker／缓存／已安装客户端升级由 PWA 专项方法处理；两种风险同时存在时分别补证据，不互相替代，也不扩展为全套验收。

遵循当前用户授权、实际可读的项目 AGENTS 与有效 Plan；保护冻结约束及未被替代的旧合同。Skill 提供专业方法，不增加修改、设备访问、运行或发布权限，不要求额外安装／触发 Runner。必要合同缺失时报告影响，不能从不可访问的 ChatGPT 附件猜测验收。

验证范围由当前必要验收与真实 failure mode 决定。下列检查按相关性选择，不把 Skill 被触发当成完整检查表必须全部执行；已经适用的可靠证据按项目／Runner 的复用规则处理。

## 1. 先定义用户可观察目标

先明确：

- 用户做什么；
- 操作前后应看到什么；
- 哪个空间/状态连续性不能破坏；
- 哪些是确定性行为；
- 哪些只能真实设备或主观判断。

不要先写测试矩阵，也不要把“高级/丝滑/现代”当验收标准。

## 2. 自动化负责确定性事实

按风险选择少量检查，例如：

- 元素 visibility / clickability；
- state、URL、history、focus；
- scroll owner / scroll position；
- bounding box、clipping、overlap；
- computed style/geometry；
- normal animation path 是否真的进入、中间状态是否变化；
- reduced-motion；
- hydration/首帧与 runtime state 是否一致。

相同状态逻辑不要机械乘以多个 viewport × browser。

## 3. Viewport / browser 只覆盖 materially different boundary

- 状态逻辑：一个代表环境即可；
- layout：只增加会改变排版/几何的边界尺寸；
- browser：只有真实 API/兼容/compositing 风险时增加；
- screenshot：只保留能回答具体视觉问题的代表场景。

具体 viewport 由项目、目标设备和 Task 决定，不使用全局固定完整矩阵。

## 4. Real-device Oracle

桌面 Chromium/WebKit 通过不等于真实设备结论。

以下高风险项无法真实执行时必须标记：

`Real-device verification: not executed`

典型包括：

- iOS Safari/PWA standalone compositing；
- safe area 与物理屏幕边缘；
- browser-native gesture；
- touch feel / double-tap / edge swipe；
- 主观视觉层级、透明度、动效节奏。

自动化证据、真实设备观察与主观体验判断分别报告，注明实际平台、版本和场景；模拟触控或桌面 WebKit 不自动变成真机证据。

项目／Plan 没有必要真机或人工 Gate 时，未执行标记说明证据边界，不自动阻止任务完成，也不形成持续追踪待办。已批准的必要真机／人工验收未完成时，报告 NOT_RUN 或 UNAVAILABLE 及原因，整体状态按有效合同判定，不宣称该项 PASS 或任务 COMPLETE；不能自行改成 Optional USER CHECK，除非已批准替代验收。

## 5. Canonical UX baseline

如果用户已真实使用并确认某关键组件/交互：

- 优先读取已有 canonical baseline；状态维护获授权且确有长期价值时，记录已确认的核心层级、几何和行为，不为每个控件新增治理文件；
- 全局设计系统、共享 class 或重构前先比较 baseline；
- 没有明确 redesign 任务时，不因无关重构或技术简化默默改变已确认的核心层级、几何和行为。

## 6. Mobile / fixed / scroll

重点检查：

- 主操作是否被次要内容挤压；
- long text / real data；
- touch target；
- safe area；
- fixed/sticky layer 是否遮挡或制造假空白；
- DOM 顺序与视觉 grid 是否一致；
- 切换后的 scroll contract 是否确定；
- 短内容与长内容都不会产生错误 reserve/scroll owner。

## 7. Animation / transition

未被明确要求或纳入 baseline 的装饰性动画默认可无；功能在无动画和 reduced-motion 下必须正确。

若任务本身涉及动效，至少证明：

- normal path 真正进入；
- 中间 geometry/style 确实变化；
- final state 正确；
- reduced-motion 正确。

新浏览器 API 或 platform-specific transition 在目标平台未 spike 前只是候选实现，不是默认 MUST。

出现黑闪、错位、延迟、scroll 破坏时优先采用更简单可靠的实现，保持明确 Acceptance 与 canonical UX baseline。只有不属于明确需求、baseline 或必要状态反馈的装饰性 transition 才可直接删除。删除/降级会改变验收目标时，需要明确产品取舍；不能通过删除用户要求的体验目标宣称修复完成。

## 8. Human smoke

仅有明确体验价值时，给出与当前 failure mode 直接相关的最少 Optional USER CHECK；简单问题可以 1–2 步，复杂问题通常不超过 8 步。它们不阻塞、不等待、不追踪、不反复提醒，无明显价值时不输出。必要人工验收单独按项目合同报告，不能混进可选步骤规避 Gate。

当前控件涉及 focus/keyboard 等明确 failure mode 时按任务验证，不扩展为全站 accessibility / WCAG gate。

## 9. 最终报告

普通任务按实际需要简洁报告。正式 Plan/Handoff 遵循当前项目／Plan 的 TASK_RESULT 合同及有效历史字段，将专项证据合并进 Verification & Evidence、Deviations / Limitations 与有价值时的 Optional USER CHECK；不另立任务状态定义、不附第二份完整专项报告。

用项目约定的 PASS / FAIL / NOT_RUN / UNAVAILABLE / NOT_APPLICABLE 或等价表述，关联证据来源与实际版本；复用时说明有效范围。以下是可选证据维度，不是每次都要填满的报告模板：

```text
Automated evidence
Browser/viewport evidence
Real-device evidence actually executed
Device-specific evidence not available
Remaining visual/interaction uncertainty
```
