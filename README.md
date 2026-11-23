# AI Workflow Assets

Long-term home for reusable AI workflow instructions, project bootstrap materials, and Codex skills.

## Contents

- `项目孵化器/` — project design, bootstrap, planning, and engineering governance materials.
- `学习项目孵化器/` — learning-project bootstrap and runtime materials.
- `Codex全局AGENTS/` — candidate global working agreements; a copy here does not install them into a Codex environment.
- `GPT自定义信息/` — ChatGPT customization text.
- `skills/` — reusable skills and their supporting references.

## Upload bundle maintenance

`项目孵化器/项目孵化器.zip` and `学习项目孵化器/学习项目孵化器.zip` are upload-ready packages for attaching to GPT conversations when starting a task. Keep them alongside their editable source files. Whenever a file included in a bundle changes, regenerate the corresponding ZIP in the same change and verify that every bundled file matches its current source before committing.

Bundle source Markdown uses LF line endings through `.gitattributes` so Git checkouts preserve the bytes used for ZIP comparison.

The engineering ZIP contains source files `01`–`06`; the learning ZIP contains `01`–`04`. Copy the corresponding startup prompt separately. Confirm the chat can read the required Markdown inside the ZIP. If it cannot unpack the ZIP or read a required file, extract it locally and upload the Markdown files or provide the missing text before generating a Bootstrap.

## Engineering handoff

The [engineering incubator](项目孵化器/01-INCUBATOR_INSTRUCTIONS.md) supports GPT Project Main, direct Codex work and a light Codex Hub for coordinating several Plans. Follow the [bootstrap contract](项目孵化器/03-BOOTSTRAP_CONTRACT.md) to land project-specific sources in the target project’s `docs/` and point its root `AGENTS.md` there. Users manually sync the project-specific instructions to GPT Project. Existing projects retain their active contracts until an upgrade is authorized.

For formal GPT → Codex handoffs, GPT Main creates an authorized Issue in the target repository with the full Markdown Plan and returns a short prompt. Example: “在 `<workspace>` 修复导出错误。先读 `<Issue URL>` 的完整正文，保留现有 API，完成相关验证。” For simple tasks, send a short prompt directly or continue the current Codex chat. Use readable Markdown or an authorized private source when GitHub is unavailable or the Plan contains restricted information. Save a local copy only at an agreed or user-specified location outside the repository; by default, keep the Plan out of Git history. See the [Plan spec](项目孵化器/05-CODEX_PLAN_SPEC.md).

## Learning project setup

Upload the learning ZIP and copy the [startup prompt](学习项目孵化器/05-START_PROMPT.md) separately. Approve the Preview for direct delivery, or choose one focused read-only Codex review when it would change a consequential design decision. Apply the final files using `00-START_HERE.md`. For an existing course, replace only approved files and instructions; keep its latest valid Checkpoint, active tracks and note names. See the [learning Bootstrap contract](学习项目孵化器/03-BOOTSTRAP_CONTRACT.md).

## GPT Project Skill routing

[MyKr-YSteinsK/ai-workflow-assets](https://github.com/MyKr-YSteinsK/ai-workflow-assets) is the source of record. Codex uses the same Skill files through its native installation paths; a GPT chat reading the files uses them as reference. Use a native Skill or plugin when the host provides it. A script needs an execution tool and task authorization.

| Task | Read on demand |
| --- | --- |
| Create, revise or review a substantive technical document, report or paper | [`skills/document-writing/SKILL.md`](skills/document-writing/SKILL.md) |
| Create or modify an editable PPTX | Use the available presentation tools and read [PPTX delivery checks](skills/document-writing/references/pptx-delivery-checks.md) directly, even for slide-only work. |
| Review or improve personal notes on material already studied | [`skills/study-review-notes/SKILL.md`](skills/study-review-notes/SKILL.md), with the course's sources, naming and existing Q&A rules |

Paste or adapt this short route in a Project's instructions if the work recurs. Omit the unused branch:

> 专业文档实质编写、修订或审查时，按需读取 `MyKr-YSteinsK/ai-workflow-assets` 的 `skills/document-writing/SKILL.md`；制作或修改可编辑 PPTX 时用当前可用的演示工具，直接读 `skills/document-writing/references/pptx-delivery-checks.md`；复盘已学个人笔记优先读 `skills/study-review-notes/SKILL.md`，并采用本课程的来源、命名与问答约定。当前对话能访问 GitHub 时读取正文，必要时再读关联 Reference，并核对实际读取的路径、版本（可见时）和一条适用规则。读不到时改用 Project 中标明原路径与版本的上传快照；仍不可得时说明缺口，依据实际任务和可读材料继续。普通问答、正在进行的教学和常规代码修复直接处理。

GitHub access varies by account, workspace and chat surface. A link or search result alone does not confirm that the body was read. For repeatable results, use a commit-pinned file or a labeled snapshot. When updating manually, copy the exact Skill text and only the referenced files needed; upload them with distinct names (e.g. `document-writing.SKILL.md`) and record the original path and commit in the Project setup or source description. When updating a snapshot, identify the active revision, confirm a new chat reads its contents, then retire the stale source. A same-name upload can leave both versions present. [Project instructions override global custom instructions](https://help.openai.com/en/articles/10169521-projects-in-chatgpt) inside that Project; neither instructions nor uploads update when this repository changes. See [GitHub access in ChatGPT](https://help.openai.com/en/articles/11145903-connecting-github-to-chatgpt) and [native Skills](https://developers.openai.com/plugins/build/skills).

## Update local Codex assets

Select a repository commit first. Compare the source with the copies in actual use: global AGENTS under the active Codex home (normally `~/.codex/AGENTS.md`, subject to an override), and the six Skill folders normally under `~/.agents/skills/`. Preserve local edits and update each Skill with its `SKILL.md` and required References together. This repository’s `skills/` directory is the maintenance source. Verify the updated files against the chosen commit and check which paths a new Codex session loads. See [AGENTS discovery](https://learn.chatgpt.com/docs/agent-configuration/agents-md) and [Skill discovery](https://learn.chatgpt.com/docs/build-skills).

## Project presentations

Save final PPT/PPTX project materials in the target project’s `docs/PPT/` by default. Treat them as public-ready unless the user or project specifies otherwise. Check for sensitive or restricted content before sharing; publishing still follows the project’s authorization. Keep partial exports and previews in the existing temporary area.

## ChatGPT customization

`GPT自定义信息/GPT网页版-ChatGPT 自定义指令.txt` defines the default conversational style and judgment principles. `GPT自定义信息/GPT网页版-关于你的更多信息.txt` supplies personal interests and feedback preferences. Copy each file's complete content into the corresponding ChatGPT personalization field to apply an update. Repository changes prepare the text; applying it in ChatGPT is a separate step.

The intended voice is candid, perceptive, expressive and relaxed. Open-ended inquiry welcomes bold hypotheses with their status made clear. Feedback acknowledges specific valid content in proportion to its quality and explains consequential gaps. Professional documents use the precision and tone appropriate to their audience and genre.

These examples illustrate the intended range, rather than recurring response templates:

- **Partly correct reasoning:** “时间顺序提供了线索，还需要排除共同原因。” Recognize the valid observation and address the unsupported inference.
- **A fully correct answer:** “对，关键条件和推导都齐了。接下来可以看这个条件变化后会怎样。” Confirm demonstrated understanding and continue naturally.
- **Open-ended exploration:** “我想沿着一个更大胆的假设往下走：……它能解释……，最值得验证的是……” Develop a distinctive idea with reasons and an appropriate way to examine it.

Learning projects preserve these voice and feedback principles through `学习项目孵化器/04-LEARNING_PROJECT_RUNTIME_BASE.md` and its Bootstrap compilation contract. Existing projects need their own updated Project Instructions to adopt these changes. Files under `skills/` are maintained skill sources; installing or replacing a runtime copy is a separate operation.
