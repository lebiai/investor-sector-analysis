# 投资人赛道分析 Skill

多机构辩论模式分析行业赛道。让六个经典投资机构的"虚拟合伙人"对同一赛道进行独立评估，自动识别共识、分歧与盲点。

## 核心功能

- **通用六维分析** — 市场/产业链/竞争/商业模式/风险/KSF
- **六机构辩论** — 红杉、Benchmark、软银愿景、高瓴资本、巴菲特、3G Capital 各抒己见
- **辩论引擎** — 共识检测、分歧评级（Fatal/Strategic/Cognitive）、盲点检测
- **四件套输出** — 分析报告、辩论对比表、打分卡、可追问状态
- **记忆系统** — 自动积累案例库，越用越聪明

## 安装

```bash
# 克隆到 Codex skills 目录（如果使用 Codex CLI）
cp -r skill/* ~/.codex/skills/investor-sector-analysis/
```

## 使用

分析一个赛道时，直接在对话中说：

> "帮我分析一下 **[赛道名称]** 赛道，用多机构辩论模式"

## 项目结构

```
investor-sector-analysis/
├── SKILL.md                          # 核心编排层
├── agents/openai.yaml                # UI 元数据
├── references/
│   ├── general-analysis-framework.md # 六维分析框架（模块）
│   ├── institution-agent-protocol.md # 机构加载协议（模块）
│   ├── debate-engine.md             # 辩论引擎（模块）
│   ├── output-specs.md              # 输出规范（模块）
│   ├── interactive-query.md         # 追问处理（模块）
│   └── [机构6个].md                  # 机构人设文件
└── memory/                          # 记忆系统（自动积累）
    ├── user-profile.json
    ├── case-library/
    └── insights.md
```

## 模块化设计

每个模块独立可修改：

| 需求 | 修改文件 |
|------|---------|
| 调整分析维度 | `references/general-analysis-framework.md` |
| 修改机构人设 | `references/[机构名].md` |
| 增加/删除机构 | `references/institution-agent-protocol.md` + 新建文件 |
| 修改辩论逻辑 | `references/debate-engine.md` |
| 调整输出格式 | `references/output-specs.md` |
| 修改追问处理 | `references/interactive-query.md` |
