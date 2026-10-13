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

## ChatGPT customization

`GPT自定义信息/GPT网页版-ChatGPT 自定义指令.txt` defines the default conversational style and judgment principles. `GPT自定义信息/GPT网页版-关于你的更多信息.txt` supplies personal interests and feedback preferences. Copy each file's complete content into the corresponding ChatGPT personalization field to apply an update. Repository changes prepare the text; applying it in ChatGPT is a separate step.

The intended voice is candid, perceptive, expressive and relaxed. Open-ended inquiry welcomes bold hypotheses with their status made clear. Feedback acknowledges specific valid content in proportion to its quality and explains consequential gaps. Professional documents use the precision and tone appropriate to their audience and genre.

These examples illustrate the intended range, rather than recurring response templates:

- **Partly correct reasoning:** “时间顺序提供了线索，还需要排除共同原因。” Recognize the valid observation and address the unsupported inference.
- **A fully correct answer:** “对，关键条件和推导都齐了。接下来可以看这个条件变化后会怎样。” Confirm demonstrated understanding and continue naturally.
- **Open-ended exploration:** “我想沿着一个更大胆的假设往下走：……它能解释……，最值得验证的是……” Develop a distinctive idea with reasons and an appropriate way to examine it.

Learning projects preserve these voice and feedback principles through `学习项目孵化器/04-LEARNING_PROJECT_RUNTIME_BASE.md` and its Bootstrap compilation contract. Existing projects need their own updated Project Instructions to adopt these changes. Files under `skills/` are maintained skill sources; installing or replacing a runtime copy is a separate operation.
