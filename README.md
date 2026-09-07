# 需求优化助手

让每一条需求都清晰可执行 —— 模拟 Trae Code 内置的"优化您的输入"功能

## 这是什么？

**需求优化助手** 是一个 Trae 技能，在你提出开发需求之后、AI 开始执行之前，插入一个关键的"需求优化"环节：

1. 对原始指令进行**结构化分析**，识别模糊表述、信息缺失、逻辑不清等问题
2. **仅在需要时**在对话中实时提问澄清，指令清晰则不打扰
3. 产出**优化后的指令 + 变更对比**，让你确认
4. **你确认后**，再交给 AI 执行

## 快速安装

```bash
# 克隆仓库
git clone https://github.com/starxxy/trae-requirement-optimizer.git

# 复制技能到 Trae 全局目录
cp -r trae-requirement-optimizer/skills/requirement-optimizer ~/.trae-cn/skills/
cp trae-requirement-optimizer/user_rules/requirement-optimize.md ~/.trae-cn/user_rules/
cp trae-requirement-optimizer/commands/优化.md ~/.trae-cn/commands/
```

重启 Trae Work 或开启新会话即可使用。

## 使用方法

| 方式 | 示例 |
|------|------|
| 自动触发 | 直接提出开发需求 |
| 手动命令（推荐） | `/优化 添加用户登录功能` |
| 自然语言 | `帮我优化：添加用户登录功能` |

## 完整说明

详见 [trae-requirement-optimizer/README.md](trae-requirement-optimizer/README.md)