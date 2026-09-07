# 需求优化助手

> 让每一条需求都清晰可执行 —— 模拟 Trae Code 内置的"优化您的输入"功能

在日常开发中，我们常常会提出模糊的需求："加个登录功能"、"优化一下页面"、"把数据导出来"——这些指令不够明确，AI 执行的结果往往不尽如人意。

**需求优化助手** 正是在你提出需求之后、AI 开始执行之前，插入一个关键的"需求优化"环节：

1. 对原始指令进行**结构化分析**，识别模糊表述、信息缺失、逻辑不清等问题
2. **仅在需要时**在对话中实时提问澄清，指令清晰则不打扰
3. 产出**优化后的指令 + 变更对比**，让你确认
4. **你确认后**，再交给 AI 执行

## 为什么需要它？

| 场景 | 没有优化 | 使用需求优化助手 |
|------|---------|----------------|
| 你说"加个登录功能" | AI 可能做出一堆你不想要的方案 | 优化后变成清晰的需求描述，确认后再执行 |
| 你说"优化一下页面" | AI 无法确定具体改什么 | 自动识别模糊表述，引导你补充具体内容 |
| 多个需求混杂在一起 | AI 可能遗漏或混淆 | 结构化分析，拆解清晰 |

## 功能特点

- **输入分析与优化**：从目标、范围、约束、输入/输出、用户对象、验收标准 6 个维度分析指令
- **按需提问**：仅在确有信息缺失或歧义时才提问；指令清晰时直接产出优化结果，不做无谓打扰
- **确认后执行**：未获得用户明确确认前，绝不开始执行任何指令
- **优化前后对比**：清晰展示主要变更点，让你知道 AI 做了什么改进
- **全局可用**：安装后在所有项目中自动生效
- **手动触发**：支持通过命令 `/优化` 或自然语言"帮我优化"触发

## 系统要求

- Trae Work 或 TraeCode（支持 Skills 功能）
- Windows / macOS / Linux

## 安装步骤

### Windows

1. 解压本压缩包到任意位置
2. 将三个目录复制到 Trae 全局目录：
   ```powershell
   # 复制技能
   Copy-Item -Recurse "skills\requirement-optimizer" "$env:USERPROFILE\.trae-cn\skills\"
   
   # 复制全局规则
   Copy-Item "user_rules\requirement-optimize.md" "$env:USERPROFILE\.trae-cn\user_rules\"
   
   # 复制命令
   Copy-Item "commands\优化.md" "$env:USERPROFILE\.trae-cn\commands\"
   ```

3. 重启 Trae Work 或开启新会话

### macOS / Linux

1. 解压本压缩包到任意位置
2. 将三个目录复制到 Trae 全局目录：
   ```bash
   # 复制技能
   cp -r skills/requirement-optimizer ~/.trae-cn/skills/
   
   # 复制全局规则
   cp user_rules/requirement-optimize.md ~/.trae-cn/user_rules/
   
   # 复制命令
   cp commands/优化.md ~/.trae-cn/commands/
   ```

3. 重启 Trae Work 或开启新会话

### 其他 AI 软件安装

其他 AI 编程工具 / 助手（如 Cursor、Windsurf、GitHub Copilot、Claude/Cline、ChatGPT、WorkBuddy 等）：将项目地址提供给 AI，让 AI 自行阅读仓库内容，完成安装并应用到全局：

```
https://github.com/starxxy/trae-requirement-optimizer
```

## 使用方法

### 方法 1：自动触发（推荐）

直接提出开发需求，全局规则会自动引导 AI 先优化并等待你确认：

```
添加用户登录功能
```

### 方法 2：手动命令（最可靠）

使用 `/优化` 命令，100% 触发优化流程：

```
/优化 添加用户登录功能
```

### 方法 3：自然语言触发

以"帮我优化"、"请优化"等开头：

```
帮我优化：添加用户登录功能
```

## 工作流程

```
用户输入 → 结构化分析
    → 判定是否需要提问？
        ├─ 有缺失/歧义 → 对话中提问 → 用户补充 → 整合
        └─ 已清晰 → 不提问
    → 产出优化后的指令 + 对比 → 用户确认
        → 明确确认 → 执行指令
```

## 文件说明

```
trae-requirement-optimizer/
├── README.md                                    # 本说明文档
├── skills/
│   └── requirement-optimizer/
│       └── SKILL.md                            # 核心技能文件
├── user_rules/
│   └── requirement-optimize.md                 # 全局规则（自动触发）
└── commands/
    └── 优化.md                                 # 手动命令（/优化）
```

| 文件 | 说明 | 安装位置 |
|------|------|---------|
| `SKILL.md` | 核心技能定义 | `~/.trae-cn/skills/requirement-optimizer/` |
| `requirement-optimize.md` | 全局规则，确保每次开发需求都先优化 | `~/.trae-cn/user_rules/` |
| `优化.md` | 手动命令，输入 `/优化` 触发 | `~/.trae-cn/commands/` |

## 常见问题

### Q: 安装后没有生效？

**A:** 请确保：
1. 文件已复制到正确的全局目录
2. 已重启 Trae Work 或开启新会话
3. 检查文件路径是否正确（如 `~/.trae-cn/skills/requirement-optimizer/SKILL.md`）

### Q: 如何验证是否安装成功？

**A:** 在新会话中输入 `/优化 测试功能`，如果 AI 开始分析并请求确认，说明安装成功。

### Q: 可以只安装技能文件吗？

**A:** 可以。只复制 `skills/requirement-optimizer/` 目录即可，但需要手动触发（用"帮我优化"或提出模糊需求）。

### Q: 如何卸载？

**A:** 删除以下文件/目录：
- `~/.trae-cn/skills/requirement-optimizer/`
- `~/.trae-cn/user_rules/requirement-optimize.md`
- `~/.trae-cn/commands/优化.md`

### Q: 支持哪些语言？

**A:** 技能支持中英文，会根据用户输入语言自动切换。

## 技术支持

如有问题或建议，请联系技能作者或在 GitHub 提交 Issue。

## 许可证

本技能可自由分享和修改，请保留原作者信息。

---

**享受更清晰、更高效的 AI 协作体验！**
