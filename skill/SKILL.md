---
name: investor-sector-analysis
description: 多机构辩论模式分析行业赛道。当用户输入一个赛道/行业名称时，Codex 自动执行：通用六维分析→六个经典投资机构独立评估→辩论引擎识别共识/分歧/盲点→输出结构化报告+打分卡+辩论对比表。支持交互追问。触发词："帮我分析一下[赛道名]赛道"、"从投资人角度看看[行业]"、"用多机构辩论模式分析[领域]"
---

# 投资人赛道分析 Skill

## Overview

This skill transforms Codex into a virtual investment committee that learns from every session.

**Core philosophy:** Don't just generate a report. Create a multi-perspective debate that reveals where different investment philosophies agree, disagree, and why. Each session builds on the last.

## Skill Structure

```
investor-sector-analysis/
├── SKILL.md                           ← 本文件（薄编排层）
├── agents/openai.yaml                 ← UI 元数据
├── references/
│   ├── general-analysis-framework.md  ← 模块 1：六维分析框架
│   ├── institution-agent-protocol.md  ← 模块 2：机构 Agent 加载协议
│   ├── debate-engine.md              ← 模块 3：辩论引擎
│   ├── output-specs.md               ← 模块 4：输出规范
│   ├── interactive-query.md          ← 模块 5：交互追问处理
│   ├── sequoia.md                    ← 机构人设 1
│   ├── benchmark.md                  ← 机构人设 2
│   ├── softbank.md                   ← 机构人设 3
│   ├── hillhouse.md                  ← 机构人设 4
│   ├── buffett.md                    ← 机构人设 5
│   └── 3g-capital.md                 ← 机构人设 6
└── memory/
    ├── README.md                     ← 记忆系统说明
    ├── user-profile.json             ← 用户画像
    ├── case-library/index.md         ← 案例库索引
    └── insights.md                   ← 跨赛道洞察
```

---

## Workflow Overview

### Phase 0: 加载记忆 & 接收输入

1. **加载记忆系统：** 读取 `memory/` 下的用户画像、案例库索引、洞察文件
2. **接收赛道输入：** 确认用户要分析的赛道名称（模糊时澄清）

### Phase 1: 通用分析 → 加载 `references/general-analysis-framework.md`

执行六维客观分析，每个维度标注辩论触发点。

### Phase 2: 机构 Agent → 加载 `references/institution-agent-protocol.md`

依次加载六家机构的人设文件，每家独立输出观点备忘录。

### Phase 3: 辩论引擎 → 加载 `references/debate-engine.md`

运行三步骤辩论分析：共识检测 → 分歧检测（含根因分析和严重评级）→ 盲点检测。

### Phase 4: 输出四件套 → 加载 `references/output-specs.md`

生成完整报告 + 辩论对比表 + 打分卡 + 可追问状态。

### Phase 5: 保存记忆 & 进入交互追问 → 加载 `references/interactive-query.md`

1. 询问用户是否保存本次分析到案例库
2. 如果用户输入了个人洞见，保存到 `memory/insights.md`
3. 更新 `memory/user-profile.json` 中的 session_count
4. 进入交互追问模式

---

## Memory Integration Points

| 阶段 | 记忆系统交互 |
|------|-------------|
| Phase 0 加载记忆 | 读取 user-profile.json、case-library/index.md、insights.md |
| Phase 4 打分量表 | 使用 user-profile.json 中的自定义权重（如果存在）替代默认权重 |
| Phase 5 保存记忆 | 保存本次分析到 case-library/、更新 index.md、记录用户洞见 |
| Phase 4-5 引用历史 | 检查 case-library/ 有无相似赛道，做 cross-reference |

## Quality Guidelines

- **Objectivity first:** 通用分析必须中立。机构偏见只出现在 Phase 2 和 Phase 3。
- **Depth over breadth:** 聚焦 3 个深度维度优于 6 个浅层维度。让赛道特性决定重点。
- **Name your sources:** 标注数据来源；无来源时说明"基于估算/公开可比数据"。
- **Chinese primary:** 所有输出用中文，机构名和技术术语保留英文。
- **Conservative scoring:** 8 分以上应代表真正卓越。大多数赛道各维度在 4-7 分。
- **Acknowledge uncertainty:** 数据不可用时要坦诚——"缺乏足够的公开数据，这本身就是风险信号"。

## Modular Maintenance Guide

**如何更新本 Skill：**

| 需求 | 修改哪个文件 |
|------|-------------|
| 调整分析维度/指标 | `references/general-analysis-framework.md` |
| 修改机构人设 | `references/[机构名].md` |
| 增加/删除机构 | `references/institution-agent-protocol.md` + 新增/删除人设文件 |
| 修改辩论逻辑 | `references/debate-engine.md` |
| 调整输出格式 | `references/output-specs.md` |
| 修改追问处理 | `references/interactive-query.md` |
| 添加机构 | `references/` 下新建文件 + `institution-agent-protocol.md` 添加条目 |
| 重置用户画像 | 清除 `memory/user-profile.json` 内容 |

**原则：** 薄 SKILL.md + 厚模块文件。SKILL.md 只编排，不定义。所有具体逻辑在各模块文件中定义。
