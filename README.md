# 需求优化助手（Requirement Optimizer）
> 你是否还在为"加个登录功能""优化一下页面""把数据导出来"这类模糊需求而头疼？AI 理解偏差、结果不尽如人意——现在只需一条命令，让每一条需求都清晰可执行。
专为 AI 协作打造的通用 Skill，模拟主流 AI 软件（如 Trae Code）内置的"优化您的输入"功能，在你提出开发需求之后、AI 开始执行之前，插入一个关键的"需求优化"环节：结构化分析、按需提问澄清、确认后执行。

---

> ### 🇨🇳 国内用户 / China Access Guide
> GitHub 在国内访问可能较慢，推荐下列任一方式快速获取：
> - **直接下载打包件**：到本仓库的 **Releases** 页面，下载 `trae-requirement-optimizer.zip` 或 `需求优化助手.skill` 压缩包，解压即用，无需克隆仓库。
> - **加速下载 GitHub 文件**：给任意 GitHub 链接添加前缀 `https://ghproxy.com/`（示例：`https://ghproxy.com/https://github.com/starxxy/trae-requirement-optimizer/archive/refs/heads/master.zip`）。
> - **结合加速工具**：使用 Watt Toolkit / dev-sidecar 等工具可提升 GitHub 整体访问速度。
>
> ---
> **国内用户（China）**: GitHub 访问可能较慢。Recommended options — ① download the ready-packaged `trae-requirement-optimizer.zip` / `需求优化助手.skill` from **Releases**; ② prepend `https://ghproxy.com/` to any GitHub link for faster download; ③ use an acceleration tool like Watt Toolkit / dev-sidecar.

---

## 中文说明

### 一、核心功能

- **需求结构化分析**：从目标、范围、约束、输入/输出、用户对象、验收标准 6 个维度分析指令，识别模糊表述、信息缺失、逻辑不清等问题
- **按需提问澄清**：仅在确有信息缺失或歧义时，在对话中实时提问（2-4 个关键问题）；指令清晰则不打扰
- **优化前后对比**：产出"优化后的指令 + 主要变更点"，让你清楚知道改了什么、为什么
- **确认后执行**：未获得你明确确认前，绝不开始执行任何指令，守住执行红线
- **全局自动生效**：安装后所有项目每次提出开发需求自动先优化，无需手动调用
- **多方式触发**：支持手动命令 `/优化`、自然语言"帮我优化"、以及自动触发三种方式

### 二、使用环境

- **适用人群**：开发人员、内容创作者及任何频繁向 AI 提出需求的用户
- **运行平台**：支持 Skills 与手动命令的 AI 编程 / 办公软件（如 Trae Work、TraeCode、WorkBuddy、Codex 等；Windows / macOS / Linux）
- **适用场景**：开发需求、任务描述、文案创作等一切需要向 AI 传达指令的场景
- **输入格式**：任意自然语言指令（中文 / English 均可）

### 三、使用教程（三步完成）

**第 1 步 · 安装 Skill**：将下面这段话直接复制发给 AI 软件：
> 请访问 GitHub 仓库 https://github.com/starxxy/trae-requirement-optimizer ，将其中名称为 requirement-optimizer 的 skill 安装到当前环境，并应用到全局。

**第 2 步 · 调用 Skill**：在输入框输入 `/优化 你的需求`，或复制以下提示词发送：
> 请优化：我想添加用户登录功能。

**第 3 步 · 获得结果**：AI 结构化分析你的指令 →（仅在有需要时）实时提问澄清 → 展示"优化后的指令 + 变更对比" → 你确认后，AI 才开始执行。

### 四、使用效果

| 维度 | 优化前 | 优化后 |
| --- | --- | --- |
| 需求描述 | "加个登录功能" | 完整结构化需求：目标 / 范围 / 安全 / 复用技术 / 验收标准 |
| 模糊表述 | 未识别，AI 自由发挥 | 自动识别并按需提问澄清，消除歧义 |
| 执行方式 | 直接执行 | 优化指令 + 变更对比，确认后才执行 |
| 多需求混杂 | 可能遗漏或混淆 | 结构化拆解，条理清晰 |

### 五、目录结构

```
trae-requirement-optimizer/
├── README.md                                    # 介绍与安装说明
├── skills/
│   └── requirement-optimizer/
│       └── SKILL.md                            # 技能定义与使用说明
├── user_rules/
│   └── requirement-optimize.md                 # 全局规则（自动触发）
└── commands/
    └── 优化.md                                 # 手动命令（/优化）
```

### 六、许可说明

开源免费使用，可自由分享和修改，请保留原作者信息。

---

## English

### Overview
> Are you still frustrated by vague requirements like "add a login feature", "tidy up the page", or "export the data"? AI outcomes can miss the mark. Now, with a single command, every requirement becomes clear and executable.
**Requirement Optimizer** is a cross-platform AI skill that simulates mainstream AI tools' built-in "Optimize Your Input" (e.g., Trae Code). After you state a requirement and before the AI executes, it inserts a critical optimization step: structural analysis, on-demand clarification, and execution only after your confirmation.

### 1. Key Features

- **Structural analysis**: examines instructions across 6 dimensions — goal, scope, constraints, input/output, target users, acceptance criteria — to detect vague wording, missing info, and unclear logic
- **On-demand clarification**: asks 2-4 key questions in chat only when real gaps or ambiguity exist; stays quiet when the instruction is clear
- **Before/after comparison**: presents the optimized instruction with key changes, so you always know what improved and why
- **Confirm before executing**: never executes anything before your explicit confirmation
- **Global by default**: auto-runs on every development request in every project after installation
- **Multiple triggers**: `/优化` command, natural language ("help me optimize / please optimize"), or automatic invocation

### 2. Environment

- **Target users**: developers, content creators, and anyone who frequently gives instructions to AI
- **Platform**: AI programming / office tools with Skills & manual-command support (e.g., Trae Work, TraeCode, WorkBuddy, Codex; Windows / macOS / Linux)
- **Scenarios**: development requests, task descriptions, content creation — any place you brief the AI
- **Input**: any natural-language instruction (Chinese or English)

### 3. Usage (3 Steps)

**Step 1 · Install the Skill**: copy and send the following message to the AI software:
> Please visit the GitHub repository https://github.com/starxxy/trae-requirement-optimizer , install the skill named requirement-optimizer into the current environment, and apply it globally.

**Step 2 · Invoke the Skill**: type `/优化 <your requirement>` in the input box, or send the following prompt:
> Please optimize: I'd like to add a user login feature.

**Step 3 · Get the Result**: the AI structurally analyzes your instruction → (only if needed) asks clarifying questions in chat → shows the "optimized instruction + key changes" → only after your confirmation does the AI start executing.

### 4. Effects (Before vs After)

| Dimension | Before | After |
| --- | --- | --- |
| Requirement | "add a login feature" | Full structured spec: goal / scope / security / reuse / acceptance |
| Vague wording | Not detected, AI improvises | Auto-detected and clarified on demand |
| Execution | Runs immediately | Confirmed first, then executed |
| Mixed requests | May be missed or muddled | Structurally broken down and organized |

### 5. Directory Structure

```
trae-requirement-optimizer/
├── README.md                                    # Intro & install guide
├── skills/
│   └── requirement-optimizer/
│       └── SKILL.md                            # Skill definition & guide
├── user_rules/
│   └── requirement-optimize.md                 # Global rule (auto-trigger)
└── commands/
    └── 优化.md                                 # Manual command (/优化)
```

### 6. License

Open source and free to use. You may freely share and modify it; please keep the original author's information.