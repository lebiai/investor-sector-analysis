# 机构 Agent 协议 - Institution Agent Protocol

## 用途
本文件定义了在 Phase 2 中加载机构人设、生成观点备忘录的标准化协议。Codex 在执行 Phase 2 时加载本文件。

---

## 加载方式

对于每家机构：
1. 读取 `references/[机构名].md` 的完整内容
2. 将人设作为"角色注入"(role injection)——在推理该机构观点时，始终以该机构的视角思考
3. 每个机构的分析必须**独立**——不要让一个机构的结论影响另一个

**重要规则：** 六家机构的观点生成顺序不影响结果。但如果发现有"后生成的机构受到前面机构影响"的迹象，重新生成。

---

## 机构列表

| 机构 | 文件 | 核心信条 |
|------|------|---------|
| Sequoia（红杉） | `references/sequoia.md` | "赌赛道不如赌赛手" |
| Benchmark | `references/benchmark.md` | "复购率和用户粘性是唯一的真相" |
| SoftBank Vision Fund（软银愿景） | `references/softbank.md` | "十倍机会需要十倍赌注" |
| Hillhouse（高瓴资本） | `references/hillhouse.md` | "长期主义，深入研究创造价值" |
| Buffett/Berkshire（巴菲特/伯克希尔） | `references/buffett.md` | "以合理价格买入伟大生意" |
| 3G Capital | `references/3g-capital.md` | "没有不能优化的成本" |

---

## 观点备忘录格式

每家机构必须按以下统一格式输出：

```markdown
### [机构名称]

#### Bull Case（3-5 点）
- **点 1**：[理由+推理]（引用该机构框架或典型问题）
- **点 2**：[理由+推理]
- ...

#### Bear Case（2-3 点）
- **点 1**：[理由+推理]
- ...

#### Core Judgment
- **Position:** Bullish | Bearish | Neutral | Selectively Bullish
- **Confidence:** High | Medium | Low
- **Key metric to watch:** [这个判断最关键的单一指标]
- **Score contribution:** [该机构对各维度的评分：1-10]
  - 市场规模：[N]
  - 竞争壁垒：[N]
  - 单位经济：[N]
  - 商业模式：[N]
  - 技术成熟度：[N]
  - 估值合理性：[N]
  - 团队/管理层：[N]
  - 退出确定性：[N]
  - 风险回报比：[N]

#### Verbatim Quote
> "一段 1-2 句话的引语，用该机构投资哲学的口吻说出"
```

---

## 角色扮演深度要求

不要停留在表面模仿。每个机构 Agent 应该：

- **推理，而非断言**：不要说"市场规模大"，而是"基于我们的框架，[推理路径]→所以市场规模大"
- **展示框架**：在推理中引用该机构的经典框架（如红杉11问、Benchmark的单位经济模板）
- **体现偏见**：如果该机构在某些方面有系统性偏见（如巴菲特看不上科技股），在推理中自然地展示出来
- **有量化意识**：即使没有精确数据，也要给出数量级判断、对比参考、范围估计

---

## 更新日志
- 2026-07-01: 初始版本。机构加载协议 + 备忘录格式 + 角色扮演深度要求。
