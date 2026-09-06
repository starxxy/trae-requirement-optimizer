---
alwaysApply: true
description: 在所有开发/实现型需求开始执行前，先调用 requirement-optimizer 技能优化用户指令。
---

# 需求优化强制规则

在任何开发/实现型需求开始执行之前，**必须**先调用 `requirement-optimizer` 技能对用户指令进行优化：

1. 当用户提出新的功能需求、开发任务或任何带有实现意图的指令时，**首先**调用 `requirement-optimizer` 技能（通过 Skill 工具，name = `requirement-optimizer`）。
2. 遵循该技能工作流：分析指令 →（仅在确有信息缺失/歧义时对话中提问澄清；指令清晰则不提问）→ 整合反馈 → 展示优化后的指令与变更对比 → 请求用户确认。
3. **只有在用户明确确认（"没问题"/"可以执行"/"确认"等）之后**，才允许开始执行具体实现工作。
4. 用户未确认前，不得擅自开始编码、改动文件或生成实现产物。

## 例外情况

以下情况**不需要**强制调用 `requirement-optimizer`：
- 纯问答、解释、查询类指令（不涉及实现）。
- 用户明确表示"直接执行，无需优化"。
- 正在优化/确认流程中（避免递归触发）。
- 对已有指令的轻微文字调整。

## 技能位置

- skill 名：`requirement-optimizer`
- 技能文件：`c:\Users\starynas\.trae-cn\skills\requirement-optimizer\SKILL.md`（全局安装）
