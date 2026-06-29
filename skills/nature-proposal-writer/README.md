# nature-proposal-writer

Proposal-first 科研写作状态机。不是"帮我写论文"——它强制执行写作前的论证架构，写完跑四层 QA pipeline。

## 这是什么

三个模式 + 四层质量闸门：

```
你的输入                  模式           做什么
─────────────            ─────          ──────────────────
题目、方向、模糊想法  →  compose       9步：从 research canon 到 .docx 导出
已有段落/章节          →  revise        9步：差距分析 → 对比润色前后
已有草稿 + 要扩写      →  hybrid        compose + revise 组合
```

写完后自动跑 QA：

```
Gate 2: professor 专家审查（内容层）
  ├── 论文 → 方法论专家 + 领域专家
  ├── proposal → 可行性专家 + 创新性专家
  └── 综述 → 覆盖面专家 + 批判深度专家
      ↓
Gate 1: avoid-ai-writing（语言层，仅英文）
      ↓
Gate 3: 自动校验（citation？可复现？编号连续？）
      ↓
Gate 4: 评分阈值（≥7.0 通过，<7.0 定向回退 ≤3 轮）
```

## 核心原则

| # | 原则 | 说明 |
|---|------|------|
| 1 | 证据先于文字 | 起草前必须建立 research_canon 和 evidence_table |
| 2 | 论证先于章节 | 写正文前必须完成 argument_map |
| 3 | 契约先于段落 | 每节需要 purpose / allowed claims / forbidden claims |
| 4 | 动态专家 | 按失败模式召唤对应审查专家 |
| 5 | 内容先于语言 | 诊断科学逻辑后再做语言打磨 |
| 6 | 该停就停 | 平台期、证据缺失是停止理由 |

## 安装

```bash
# Codex
请从这个仓库安装 nature-proposal-writer：
https://github.com/Yuan1z0825/nature-skills.git
请把 skills/nature-proposal-writer/ 完整安装，包括 references/ 和 templates/

# Hermes / Claude Code
git clone https://github.com/Yuan1z0825/nature-skills.git
cp -r nature-skills/skills/nature-proposal-writer ~/.hermes/skills/research/
```

**前置依赖：**

```bash
hermes skills install nature-polishing    # 语言润色
hermes skills install nature-figure      # 图表制作
hermes skills install professor          # 动态专家审查
hermes skills install brainstorming      # 入口追问
```

## 使用示例

```
# 从零写 proposal
"用 nature-proposal-writer 帮我写一个关于钙钛矿稳定性优化的研究计划"

# 审查已有文本
"用 nature-proposal-writer 审查这段 discussion，paper 挡位"

# 快速扫读
"快速扫一下这个摘要"（只标记问题，不全跑 QA）
```

## 四挡位

| 挡位 | 场景 | 阈值 | 说明 |
|------|------|:---:|------|
| `paper` | 投稿论文 | 7.0 | 全跑 |
| `proposal` | 研究方案/开题 | 7.0 | 全跑 |
| `internal` | 内部汇报 | 5.0 | 跳过专家审查 |
| `quick` | 快速扫读 | — | 只标记 P0 问题 |

## 与 nature-skills 生态的关系

- 草稿写完后 → 用 `nature-polishing` 润色英文
- 需要配图 → 用 `nature-figure` 制图
- 需要文献支撑 → 用 `nature-literature-pipeline` 补充引用
- 审稿人反馈 → 用 `nature-reviewer` 模拟预审

## 文件结构

```
nature-proposal-writer/
├── SKILL.md                           ← 技能入口
├── README.md                          ← 本文件
├── references/
│   ├── compose-mode.md                ← compose 模式 9 步流程
│   ├── revise-mode.md                 ← revise 模式 9 步流程
│   ├── hybrid-mode.md                 ← hybrid 组合模式
│   ├── evaluation-rubric.md           ← 8 维 × 4 锚点评分体系
│   ├── research-anti-slop.md          ← 中文 proposal 语言清理
│   ├── chinese-review-writing-style.md ← 中文综述写作风格
│   ├── stopping-rules.md              ← 迭代循环控制
│   ├── professor-dispatch.md          ← 专家审查分派
│   ├── foundation-files.md            ← 基础文件建立
│   ├── project-structure.md           ← 项目目录和状态格式
│   ├── export-archive.md              ← .md + .docx 导出
│   ├── partial-proposal-scope.md      ← 分阶段写作范围控制
│   ├── ref-renumbering-cascade.md     ← 参考文献重编号
│   ├── review-paper-framework.md      ← 综述论文框架设计
│   ├── review-critique-methodology.md ← 综述批判方法论
│   ├── validation-checklist.md        ← 自动校验清单
│   ├── gpt-handoff-revision-brief.md  ← 交接修订简报
│   ├── within-approved-proposal.md    ← 本子框架内写作约束
│   ├── worked-example-proposal.md     ← 完整示例
│   └── 降承诺提案模式.md              ← 降承诺写作策略
├── scripts/
│   └── build_proposal_docx.py         ← .md → .docx 构建脚本
└── templates/                         ← 空模板（新建项目用）
```

## 作者

十五 (JL Lab) — 基于博士研究实战构建的写作框架。
