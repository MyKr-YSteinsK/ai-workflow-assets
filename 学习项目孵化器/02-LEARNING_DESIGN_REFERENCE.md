# Learning Design Reference

This file is a **design toolbox** for the Learning Project Incubator. Do not treat it as a mandatory checklist.

## 1. General Principle

Different goals require different learning mechanisms. A mechanism earns its place only if it improves the target capability.

Prefer clear capability targets, real dependency structure, meaningful practice, low management overhead, adaptive teaching, transfer, and integration.

Avoid curriculum bloat, rigid textbook imitation, unnecessary chat splitting, artificial precision, repetitive testing, and decorative frameworks that never affect actual learning.

## 2. Common Learning Mechanisms

Possible mechanisms include conceptual explanation, mechanism tracing, guided examples, deliberate practice, worked-example fading, error diagnosis, comparison/boundary analysis, real tool operation, coding/debugging, mathematical derivation, proof/reasoning practice, primary-text reading, argument reconstruction, case analysis, literature mapping, paper reading, experiment reproduction, research design, writing/revision, language input/output, correction, spaced revisit, cumulative review, integrated anchor, capstone, oral explanation, mock interview, exam-style practice, and conditional prerequisite support.

Use the smallest useful combination that still gives the learner substantial understanding. Prioritize learning gains over minimizing text or artifacts.

## 3. Domain Heuristics

### Technical / Engineering
Prioritize problem solved, inputs-transformations-outputs, runtime/system position, data/control flow, interfaces/configuration, failure paths, code reading/modification, debugging, trade-offs, verification, and realistic workflows.

Prefer realistic program flows that contain meaningful dependencies, intermediate states, parameters and at least one nontrivial edge case when illustrating complex mechanisms. For difficult code, explain what materially helps understanding: object/data type, field/parameter meaning, user-defined names vs fixed APIs, data-flow order, scope/side effects, and important exceptional paths. Do not mechanically annotate trivial lines.

### Mathematics
Prioritize precise conditions, intuition, representation, derivation/proof structure, relations among definitions/theorems, representative problems, counterexamples/boundaries, and transfer to downstream use. For consequential formulas, work through a representative numeric case with relevant intermediate values, explicit substitutions and interpretation of the result and its conditions. A tiny symbolic case may define notation but should not stand in for substantial teaching. Do not front-load whole mathematical subjects when a just-in-time subset is enough.

### Natural Science
Prioritize model/assumptions, mechanism, evidence, measurement, causal structure where justified, experimental design, uncertainty/limitations, and connection between theory and observation.

### Philosophy / Humanities
Prioritize the problem, concept distinctions, primary argument structure, historical context where relevant, hidden premises, objections/responses, competing interpretations, source-text evidence, and clear reconstruction. Avoid reducing study to names, dates, definitions, and conclusions.

### Psychology / Social Science
Prioritize construct definition, measurement, study design, evidence hierarchy, correlation vs causation, statistical/sampling limits, competing explanations, replication/generalization, and academic evidence vs popular claims.

### Language Learning
Prioritize comprehensible input, active output, correction, high-frequency real contexts, vocabulary/grammar in use, contrasts between similar expressions, pronunciation/listening where relevant, and repeated retrieval/reuse. Do not turn all language learning into grammar lectures.

### Research / Academic Work
Prioritize research question, literature landscape, source quality, theoretical framing, hypothesis/claim, method, data, experiment/reproduction, result interpretation, limitations, reproducibility, and research communication. Distinguish established, disputed, inferred, and unknown.

### Exam / Certification
Use only when the user actually has that objective. Prioritize official scope, scoring, question types, representative past material, timing strategy, weakness diagnosis, targeted practice, and final simulation when useful.

### Tool / Workflow Learning
Prioritize minimum usable workflow, common tasks, parameter meaning, file/config structure, failure diagnosis, realistic operation, safe boundaries, and quick reference when useful. Avoid converting a small tool-learning need into a full academic curriculum.

## 4. Worked Examples and Comparison Design

For difficult mechanisms, choose a realistic-enough task to exhibit multiple interacting factors, rather than a contrived two-object demonstration. Complexity should be *relevant*: more entities, parameters or exceptions only when they reveal the mechanism. When numerical calculation is meaningful, show key intermediate arithmetic, units/dimensions and a domain-specific interpretation. Clearly identify invented teaching data versus measured or published data; source external facts where important.

When close methods or competing explanations are likely to be confused, organize by discriminating dimensions such as assumptions, inputs, transformations, outputs, failure conditions, computational demands and application decisions. This supports meaningful transfer, not just terminology memorization.

When learners already have background, build on it; neither repeat a complete introductory course nor omit difficult intermediate steps merely for brevity.

## 5. Integrated Anchors

For medium or large projects, consider one or more recurring anchors such as an evolving codebase, dataset, system problem, real case, primary text, long-form writing task, research question, language scenario, or cumulative design problem.

An anchor is useful only if it actually reappears in teaching, practice, review, or final output.

## 6. Conversation Topology Heuristics

Split conversations because of workflow independence or context quality, not prestige or project size.

Useful reasons to split:
- weakly dependent routes can progress in parallel;
- practice needs a different interaction style;
- primary-source reading would pollute main teaching context;
- a support prerequisite needs focused treatment;
- a long sequential route needs a clean rollover;
- review/assessment benefits from a separate context.

Do not split when the content depends on the previous explanation every few turns, a second chat would constantly need the newest state from the first, or separation adds user management without reducing confusion.

Prefer delayed creation of optional chats.

## 7. Note-Mode Heuristics

Persistent notes are especially useful when the project is long enough to benefit from reusable knowledge assets, the subject contains many relationships/comparisons/mechanisms/formulas/code patterns/arguments/frameworks, the user expects future review, or later stages benefit from cross-stage synthesis.

Notes may be unnecessary for very short tasks, primarily immediate-operation goals, almost entirely conversational practice, or cases where persistent artifacts add more overhead than value.

When enabled, the Runtime Base's fixed `NN-笔记主题_一级目录_课程名.md` naming contract applies after the user confirms its stable category/course values. The original notes are for future review; the optional post-teaching Codex notes Skill is a separate activity. Note content follows the project-specific Notes Quality Contract, not a universal template.

## 8. Assessment Heuristics

Possible evidence includes explanation, distinguishing close concepts, error diagnosis, justified approach selection, representative/new problem solving, code modification/debugging, workflow design, experiment interpretation, argument reconstruction, evidence critique, written artifacts, real language-use tasks, reproduction/extension, and capstones.

Prefer a few high-information assessments over large low-value question sets.

## 9. Route Adaptation Heuristics

The initial route is provisional. During runtime it may be appropriate to skip mastered material, compress easy prerequisites, add a local detour, activate a conditional support track, split a long stage across chats, merge redundant stages, move practice earlier, delay advanced theory, revisit fragility, create an integration task, or generate an integrative note after multiple stages.

Large project-level changes still require user approval.

This file is a reference toolbox. Execution authority, nine orchestration states, notes naming and lifecycle are defined in their dedicated files; do not duplicate or weaken them here.
