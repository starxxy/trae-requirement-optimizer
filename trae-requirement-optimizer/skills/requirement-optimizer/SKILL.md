---
name: "requirement-optimizer"
description: "模拟主流 AI 软件（如 Trae Code）内置的'优化您的输入'功能：对用户指令进行结构化分析、按需提问澄清、确认后执行。当用户提出新的开发/实现型需求时，自动调用本技能进行指令优化与确认。Simulates mainstream AI tools' built-in 'Optimize Your Input' (e.g., Trae Code): structurally analyzes user instructions, asks clarifying questions only when needed, and executes only after confirmation. Automatically invoked for new development or implementation requests."
---

# Requirement Optimizer（优化您的输入）

本技能模拟主流 AI 软件（如 Trae Code）内置的"优化您的输入"功能。核心定位为**输入分析与优化**：对用户指令进行结构化分析，识别模糊表述、信息缺失、逻辑不清晰等问题，在**确有需要时才进行交互式提问**，最终产出优化后的指令供用户确认，**只有在用户明确确认后才能开始执行**。

This skill simulates mainstream AI tools' built-in "Optimize Your Input" feature (e.g., Trae Code). Its core role is **input analysis and optimization**: structurally analyze user instructions to identify vague expressions, missing information, and unclear logic. Ask questions interactively **only when truly needed**, produce an optimized instruction for user confirmation, and **never execute until the user explicitly confirms**.

## 语言偏好（Language Preference）

首次调用本技能、且无法从对话上下文明确判断用户语言时，先进行语言确认：

When this skill is invoked for the first time and the user's language cannot be clearly determined from context, confirm the language first:

- 以中英双语简短询问：**Choice 1: 中文（简体）** / **Choice 2: English**
- 用户选定后，整个优化流程（提问、优化结果展示、确认请求）均使用该语言；本会话后续调用直接沿用，不再重复询问。
- 若已能明确判断用户语言（如用户用英文输入指令），则跳过确认，直接使用对应语言。

- Briefly ask in both languages: **Choice 1: 中文（简体）** / **Choice 2: English**.
- After the choice, use that language throughout the optimization flow (questions, optimized output, confirmation requests); keep it for the rest of the session without re-asking.
- If the user's language is already clear (e.g., the user writes in English), skip the confirmation and use the matching language directly.

## 何时使用（When to Use / Trigger Conditions）

在以下任一场景触发本技能：

Trigger this skill in any of the following scenarios:

- 用户提出一个新的功能需求或开发任务
- 用户的指令模糊、信息不全、或逻辑不清晰
- 指令存在多个可能的理解方向，需要澄清
- 用户明确要求"优化我的输入/需求/指令"

- The user submits a new feature request or development task.
- The user's instruction is vague, incomplete, or logically unclear.
- The instruction has multiple possible interpretations that need clarification.
- The user explicitly asks to "optimize my input / request / instruction".

## 核心原则（Core Principles）

1. **分析为主，提问为辅** —— 核心是结构化分析并优化指令；提问仅在"确有信息缺失或歧义"时进行，不做无谓提问。
2. **按需提问** —— 指令已清晰、无关键缺失时，不提问，直接产出优化结果供确认。
3. **对话式交互** —— 当需要提问时，在对话中自然提出，不一次性输出长篇文档。
4. **确认后执行** —— 未获得用户明确确认前，**绝不开始执行任何指令**。

1. **Analysis first, questions as support** — the core is structured analysis and optimization; ask only when there is genuine missing information or ambiguity, never for its own sake.
2. **Ask on demand** — when the instruction is already clear without critical gaps, do not ask; produce the optimized result directly for confirmation.
3. **Conversational interaction** — ask questions naturally in the conversation; do not dump long documents.
4. **Execute only after confirmation** — never begin executing any instruction before explicit user confirmation.

## 工作流程（Workflow）

### 阶段 1：接收并分析原始指令（主功能）/ Stage 1: Receive and Analyze the Raw Instruction (Core)

接收用户指令，从以下维度做结构化分析：

Receive the user instruction and analyze it structurally across the following dimensions:

**关键要素检查 / Key element checks:**
- **目标 / Goal**：要达成的最终结果是什么？是否清晰？What is the final outcome? Is it clear?
- **范围 / Scope**：包含什么 / 不包含什么？边界是否清楚？What's in / out? Are the boundaries clear?
- **约束条件 / Constraints**：技术栈、时间、资源、兼容性限制？Tech stack, time, resources, compatibility limits?
- **输入/输出 / Input/Output**：输入数据是什么？期望输出形式？What is the input? What output format is expected?
- **用户/受益对象 / Users**：为谁而做？Who is it for?
- **验收标准 / Acceptance criteria**：什么样的结果算"完成"？What counts as "done"?

**常见问题识别 / Common issues to detect:**
- 模糊表述（"尽量""优化一下""弄好看点"等）/ Vague wording ("make it better", "optimize it a bit", etc.)
- 信息缺失（缺少目标、范围、约束、技术选型等）/ Missing information (no goal, scope, constraints, tech choice, etc.)
- 逻辑不清晰 / 自相矛盾 / Unclear or contradictory logic
- 存在多个歧义理解方向 / Multiple ambiguous interpretations

### 阶段 2：判断是否需要提问（按需）/ Stage 2: Decide Whether to Ask (On Demand)

基于阶段 1 的分析结果，判定是否提问：

Based on Stage 1, decide whether to ask:

- **需要提问的情形 / When to ask**：检测到**确实影响实现**的关键信息缺失、逻辑矛盾或歧义。Detect critical missing information, logical contradiction, or ambiguity that genuinely affects implementation.
- **无需提问的情形 / When not to ask**：指令已足够清晰、无关键信息缺失。The instruction is sufficiently clear with no critical gaps.

**判定原则 / Decision rule:**
- 确有缺失/歧义 → **提问**（进入阶段 3）/ Genuine gap or ambiguity → **ask** (go to Stage 3)
- 已清晰、无缺失 → **不提问**，直接进入阶段 4 产出优化结果 / Clear, no gaps → **don't ask**, go directly to Stage 4

### 阶段 3：在对话中实时提问（仅有需要时）/ Stage 3: Ask Questions in Real Time (Only When Needed)

仅在确定需要澄清时，立即在对话中提出问题。

Ask in the conversation immediately, only when clarification is truly needed.

**提问要求 / Requirements:**
- 数量：2-4 个关键问题，避免过多 / 2-4 key questions at most
- 每个问题聚焦一个具体决策点 / Each question targets one concrete decision point
- 优先使用 AskUserQuestion 工具提供选项，便于用户快速回答 / Prefer the AskUserQuestion tool with options for quick answers
- 对每个问题简述"为什么需要知道"，帮助用户理解 / Briefly state why the question matters

**提问示例格式 / Example format:**
```
好的，我来帮你优化这条指令。为保证准确理解，我需要先确认几个关键点：
Sure, let me optimize this. To get it right, I need to confirm a few key points:

1. 【目标/Goal】你希望最终达到什么效果？What is the desired outcome?
2. 【技术栈/Stack】这个功能是基于现有的 XX 技术，还是可以重新选型？Built on existing tech or open to new choices?
3. 【范围/Scope】是否包含 XX？还是仅限 XX？Does it include XX, or only XX?
4. 【验收/Acceptance】什么样的结果算完成？What counts as done?
```

### 阶段 3.5：等待并整合用户反馈（仅在提问后）/ Stage 3.5: Wait for and Integrate User Feedback (Only After Asking)

- 等待用户回答，收到答案后，将所有反馈整合进指令。/ Wait for answers, then integrate all feedback into the instruction.
- 若用户回答仍不清晰，可继续追问（最多追问 2 轮）。/ If still unclear, follow up (max 2 rounds).
- 根据用户反馈**动态调整**优化策略，不强加先验假设。/ Dynamically adjust the optimization strategy; don't impose assumptions.

### 阶段 4：产出优化后的指令（供确认）/ Stage 4: Produce the Optimized Instruction (For Confirmation)

无论是否提问，都梳理出优化后的指令，并**主动请求用户确认**。提供优化前后对比。

Whether or not questions were asked, produce the optimized instruction and **actively request confirmation**, with a before/after comparison.

**确认格式 / Confirmation format:**
```
## 优化后的指令 / Optimized Instruction

[重写的一份清晰、完整、可执行的指令描述，已整合用户所有反馈（如有）]
[A rewritten, clear, complete, executable instruction, incorporating all user feedback (if any)]

## 主要变更点（优化前后对比）/ Key Changes (Before → After)
- 原始：XXX → 优化后：XXX / Before: XXX → After: XXX
- 补充了：XXX / Added: XXX
- 明确约束：XXX / Clarified: XXX

---

**这条指令是否满足你的需求？/ Does this instruction meet your needs?**
- ✅ 没问题 / 可以执行 / Yes, go ahead
- ✏️ 需要调整：请说明 / Needs adjustment: please specify

我将仅在得到你的明确确认后开始执行。
I will start only after your explicit confirmation.
```

### 阶段 5：等待明确确认后才执行 / Stage 5: Wait for Explicit Confirmation Before Executing

**严格执行触发条件 / Strict trigger rule:**
- 仅当用户明确回复"没有问题""可以执行""确认"等肯定信号后，才开始执行优化后的指令。/ Start executing only after an explicit affirmative ("OK", "confirmed", "go ahead", etc.).
- 若用户要求修改，根据反馈更新指令并**再次请求确认**，直到用户确认。/ If changes are requested, update and re-confirm until approved.
- 用户未确认前，不得擅自开始执行。/ Never execute before confirmation.

## 交互流程总览（Flow Overview）

```
用户输入 User input → 结构化分析（主功能）Structural analysis (core)
    → 判定是否需要提问？Need to ask?
        ├─ 有缺失/歧义 → 对话中提问 → 用户补充 → 整合
        │  Gaps/ambiguity → ask in chat → user input → integrate
        └─ 已清晰 → 不提问
           Clear → no questions
    → 产出优化后的指令 + 对比 → 用户确认
      Produce optimized instruction + comparison → user confirms
        → 明确确认 → 执行指令
          Confirmed → execute
```

## 功能要求清单（Feature Checklist）

- [x] 输入分析与优化：结构化分析，识别模糊表述、信息缺失、逻辑不清晰等问题（主功能）/ Input analysis & optimization (core)
- [x] 实时交互式疑问：仅在确有缺失/歧义时在对话中实时提问 / Real-time interactive questions only when needed
- [x] 用户确认机制：产出优化后的指令并请求确认，支持优化前后对比 / User confirmation mechanism with before/after comparison
- [x] 执行触发条件：仅用户明确确认后才执行 / Execute only after explicit confirmation
- [x] 根据用户反馈动态调整优化策略 / Dynamically adjust to user feedback
- [x] 保持对话连贯性和上下文理解 / Maintain conversational continuity and context
- [x] 双语支持：SKILL.md 中英双语，首次使用确认用户语言 / Bilingual support: bilingual SKILL.md; confirm user language on first use

## 提问质量规范（Question Quality Standards，按需提问时适用 When Asking）

**好问题的特征 / Good questions:**
- 具体、聚焦，针对某个影响执行的决策点 / Specific and focused on a decision point that affects execution
- 与当前指令直接相关 / Directly relevant to the current instruction
- 说明提问原因 / Explain why you're asking

**避免 / Avoid:**
- 空泛问题（"还有其他需求吗？"）/ Vague questions ("Anything else?")
- 问题过多造成负担 / Too many questions (burdensome)
- 追问琐碎细节 / Nitpicking trivial details
- **无需提问时的无谓问题 / Needless questions when none are required**

**提问类别参考 / Question categories:**
- 技术方案 / 技术栈 / Solution & tech stack
- 功能范围（含什么、不含什么）/ Feature scope (in / out)
- 集成与兼容性（现有系统、数据库）/ Integration & compatibility (existing systems, databases)
- 安全 / 性能要求 / Security & performance
- 用户体验与交付形式 / UX & delivery format
- 验收标准 / Acceptance criteria

## 对话示例（Dialogue Examples）

**示例 A：指令有缺失，需提问 / Example A: Missing information → ask questions**

**用户 / User：** "添加用户登录功能" / "Add user login"

**AI（阶段 1，检测到技术方案/集成不明）→ 提问 / Stage 1, tech/integration unclear → asks:**
"好的，我来帮你优化这条指令。为保证准确实现，我需要先确认几个关键点：
Let me optimize this. I need to confirm a few key points first:

1. 【登录方式 / Sign-in】仅支持用户名/密码，还是也需要邮箱登录？是否需要第三方登录（如微信、Google）？/ Password only, or also email / third-party (e.g., Google, WeChat)?
2. 【会话管理 / Sessions】使用 JWT 还是传统 Session？需要'记住我'功能吗？/ JWT or sessions? 'Remember me'?
3. 【集成 / Integration】是否已有用户数据库？需要与现有系统无缝集成吗？/ Existing user DB? Seamless integration with current systems?"

**用户 / User：** "只需用户名/密码登录，用JWT，需要记住我，有现成的用户表" / "Username/password only, JWT, remember me, existing users table"

**AI（阶段 4 / Stage 4）：**
"收到，我已根据你的反馈完善指令。/ Got it, I've refined the instruction.

## 优化后的指令 / Optimized Instruction
设计并实现一个安全、用户友好的用户登录功能……并与现有用户表无缝集成 / Design and implement a secure, user-friendly login feature ... seamlessly integrated with the existing users table.

## 主要变更点 / Key Changes
- 明确登录方式：用户名+密码（不含第三方登录）/ Clarified: password only
- 明确认证方案：JWT，支持'记住我'/ Clarified: JWT + remember me
- 明确集成：复用现有用户表 / Clarified: reuse existing users table

---
**这条指令是否满足你的需求？/ Does this meet your needs?**（确认后执行 / waited for confirmation）"

**示例 B：指令已清晰，不提问直接产出 / Example B: Clear instruction → no questions, produce directly**

**用户 / User：** "把主页的标题改成'我的工作台'，字体加粗，并移除右侧的搜索栏" / "Change the homepage title to 'My Workspace', make it bold, and remove the right search bar"

**AI（阶段 1 检测到无关键缺失 → 阶段 4，不提问 / No critical gaps → Stage 4, no questions）：**
"## 优化后的指令 / Optimized Instruction
对主页进行以下三处视觉调整：1) 将页面标题修改为'我的工作台'；2) 将该标题文字设置为加粗样式；3) 移除页面右侧的搜索栏。不涉及其他元素的改动。
Make three visual changes: 1) change title to 'My Workspace'; 2) bold it; 3) remove the right search bar. No other changes.

## 主要变更点 / Key Changes
- 明确改动范围：仅标题、字体、搜索栏三处 / Scope: only title, font, search bar
- 明确预期结果：无歧义 / Outcome: unambiguous

---
**这条指令是否满足你的需求？/ Does this meet your needs?**（确认后执行 / waited for confirmation）"

## 最佳实践（Best Practices）

1. **分析先行**：先做结构化分析，再判断是否需要提问。/ Analyze first, then decide whether to ask.
2. **按需提问**：确有缺失/歧义才问，指令清晰时不问。/ Ask only when truly needed.
3. **对话自然**：需要提问时用自然语言交流，不用正式文档腔。/ Be conversational, not formal.
4. **认真倾听**：将用户所有反馈完整融入优化后的指令。/ Incorporate all user feedback fully.
5. **保持简洁**：优化后的指令要详细但不冗长。/ Optimized instructions should be detailed but concise.
6. **未确认不执行**：牢牢守住"确认后才执行"这一红线。/ Never execute before confirmation.
7. **使用用户语言**：与用户使用相同语言交流（见"语言偏好"）。/ Use the user's language (see Language Preference).

## 边界说明（Scope Boundaries）

本技能**只负责优化指令**（让指令更清晰、完整、可执行），**不负责**：

This skill **only optimizes instructions** (making them clearer, complete, executable) and does **not**:

- 制定实施计划 / 任务拆分 —— 交给 `writing-plans` 等技能（在指令确认后）/ Create implementation plans or task breakdowns — delegate to `writing-plans` and similar skills (after confirmation)
- 写代码 / 测试用例 / 架构设计 / Write code, tests, or architecture design
- 执行任何实际开发工作 / Perform any actual development work

这些动作均应在用户确认优化后的指令之后再介入。

These actions should happen only after the user confirms the optimized instruction.

## 重要注意事项（Important Notes）

- 核心是**输入分析与优化**；交互式提问仅为辅助，仅在必要时进行。/ Core: input analysis & optimization; interactive questions are auxiliary, only when necessary.
- 疑问（如需提出）必须在对话中实时进行，不得在"最后一次性抛出一堆问题"。/ Questions must be asked in real time in the conversation, never dumped at the end.
- 优化后的指令在整合反馈（如有）后生成，并交付用户确认。/ The optimized instruction is produced after integrating feedback (if any) and delivered for confirmation.
- 用户确认是执行的硬性前置条件。/ User confirmation is a hard prerequisite for execution.
- 本技能聚焦指令清晰度，而非实现细节。/ Focus on instruction clarity, not implementation details.
- 语言偏好默认遵循用户语言，首次确认后本会话沿用。/ Language follows the user; confirm once on first use, then reuse for the session.