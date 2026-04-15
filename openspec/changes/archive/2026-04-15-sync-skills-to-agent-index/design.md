## Context

- `index.html` 是单文件静态页面（内嵌 CSS + JS + 可选 File System Access API 导出），通过 `localStorage` 的简易密码 token 控制访问；页面按 `article.dex-card` 渲染每个 Agent，技能树 `.skill-tree` 内以 `.st-phase` 分 Phase、`.st-row` 表示单个 SKILL。
- `AI Agent Skills Analysis/可开发SKILL清单.md` 是当前 SKILL 总账：77 个活跃（66 draft + 10 blocked + 1 planned）+ 17 已归档。状态字典：`draft = 可开发`、`blocked = 阻塞`、`planned = 规划后期`、`ex/ = 已归档`。
- `SKILLS/` 是每个 SKILL 的设计目录（如 `bs-intake-classifying/SKILL.md`），本次只读，不改动。
- BS 部门在现 `index.html` 中已标注 4 个 ✅ 已上线 SKILL（BS-01~04），此为线上事实，不在 SKILL 索引文档的 draft/blocked/planned 范畴内，需要保留。
- 约束：不得破坏 auth overlay、模式切换（编辑/保存/导出）、TOC 锚点、打印样式、响应式栅格（960px / 640px / 520px 三个断点）。
- 读者：内部同事扫一眼能看出"哪些能力已上线 / 在开发 / 规划中 / 卡住了"，并识别出 5 个跨部门通用 Skill。

## Goals / Non-Goals

**Goals:**
- 每个 Agent 卡片的技能树与 `可开发SKILL清单.md` 的 SKILL 列表、状态一致。
- 新增一张「通用能力」卡片，独立渲染 5 个 `common-*` SKILL，状态为 🔨 开发中。
- 新增 ⛔ 阻塞 状态（色系：红/砖色系，与现有绿/橙区分），用于 10 个 blocked SKILL。
- 保留 BS 的 4 个 ✅ 已上线 SKILL 不变。
- 顶部计数、统计条与 TOC 反映"9 张卡片"。

**Non-Goals:**
- 不重写 Agent 的自我介绍、"找我做/别找我做"、"试试这样对我说"文案。
- 不新增 Osto、Sage 等 Agent 独立卡片（本次只新增通用能力卡片；新 Agent 接入留待后续变更）。
- 不改动 JS 逻辑（编辑模式/保存/导出/auth）。
- 不拆分 `index.html` 为多文件。

## Decisions

### 决策 1：状态映射

| SKILL 文档状态 | 卡片显示 | 说明 |
|----------------|---------|------|
| 线上已上线（仅 BS-01~04 既有事实） | ✅ 已上线（保留） | 不在 SKILL 文档状态集中，属于部署事实 |
| `draft`（可开发） | 🔨 开发中 | 默认取"开发中"语义——SKILL 已设计完成、进入开发排期 |
| `blocked` | ⛔ 阻塞 | 新增状态标签，配色 `#b91c1c / #fee2e2` |
| `planned` | 📋 规划中 | 对应后期规划（如 compliance-periodic-review-notifying） |
| `ex/` 归档 | 不在卡片显示 | 合并至卡片尾部 `st-footnote` 作为说明 |

**备选考虑**：把 `draft` 映射为"📋 规划中"更保守。拒绝的理由：当前 `index.html` 既有 Agent 的绝大多数 SKILL 已是"🔨 开发中"，文档中的 draft 语义更贴近"立刻可开发 → 已进入开发队列"，保留"开发中"能继承既有视觉。

### 决策 2：Agent ↔ SKILL 映射

| 卡片 | 主要来源 Section | SKILL 数 |
|------|------------------|---------|
| NO.001 Star（BS） | BS（8） | 保留现有 BS-01~04 已上线；BS-05~12 映射到 8 个 SKILL |
| NO.002 Lumi（HR） | HR：Sage（3）+ Lumi（2）+ blocked hr-workday-querying + blocked hr-account-permission-automating | 7 |
| NO.003 Grant（Treasury） | Treasury（2）+ blocked treasury-payment-reviewing | 3 |
| NO.004 Astro（HR 招聘） | Astro（5）+ HR-Astro（6）+ blocked astro-voice-interview-conducting | 12 |
| NO.005 Amy（Compliance） | Compliance（4）+ planned periodic-review-notifying | 5 |
| NO.006 Finley（NS-Finance） | NS-Finance（3）+ blocked internal-transfer-approval-suggesting | 4 |
| NO.007 Grove（OSM） | OSM（8） | 8 |
| NO.008 松饼（Cango） | Cango（2 blocked） | 2 |
| **NO.Common 通用能力（新）** | Common（5） | 5 |

> Osto（AA 财务运营，15+5 SKILL）与 Memo/Platform/Reporting/Vault 等 Agent 在 `可开发SKILL清单.md` 存在，但未在当前图鉴中立卡；本次以通用能力卡片为唯一新增，后续若要为 Osto 立卡，通过独立 proposal 完成。

### 决策 3：新增「通用能力」卡片的主题

- 占位位置：插在 NO.008 松饼 之后（卡片栅格末尾），保持双列网格自然收尾。
- NO 编号：`NO.009`（延续连号）。
- 主题色：新增 `theme-common`，用靛蓝/紫罗兰调（与顶部 `--dex-violet/--dex-iris` 同一家族），避免与现有 8 色冲突。字母 N 头像（用 `.dex-avatar-letter`）。
- 卡片骨架复用：头像 + 名字行 + `.dex-role` + `.dex-status` + `.dex-tags` + 关于我 + 找我做/别找我做 + 试试这样对我说 + 技能树。
- 技能树：单 Phase（Phase 1.0 · 通用化沉淀），5 行 SKILL，全部 🔨 开发中。
- 脚注解释：本卡片承接 `common-*` 系列 SKILL，目的是避免多个 Agent 重复开发同一能力。

### 决策 4：HTML 修改范围

仅修改三处：

1. CSS 区块末尾追加 `.theme-common` 主题类 + `⛔ 阻塞` 状态 class `.st-st--blk` / `.chip-blocked`。
2. `.dex-top .stats` 文案更新：`8 Agents` → `9 Agents`，部门列表末尾追加 `Common`。
3. `nav.toc ul` 追加一条 TOC；`.cards-grid` 内重写 9 张卡片的技能树 + 新增通用能力卡片。

### 决策 5：技能命名规范

技能树 `.st-id` 沿用现有简短编号（如 `BS-01`、`HR-01`、`Compliance-01`），不直接暴露长 kebab-case；`.st-name` 用中文短名 + 可选英文括注，把完整 `common-rag-qa-responding` 等技术标识放进 `.st-footnote` 作为 `<code>` 列表，兼顾扫读与可追溯。

## Risks / Trade-offs

- **Risk**：`可开发SKILL清单.md` 后续会再更新，手工维护 `index.html` 会漂移。
  → **Mitigation**：CLAUDE.md 规则 5 已锁定"SKILL 增删改走 opsx 流程并同步 index.html"。后续提一个"自动生成 index.html 的技能树片段"的独立变更（超出本次范围）。
- **Risk**：SKILL 命名从 `BS-01` 这类序号切换为 kebab-case 可能破坏老截图/分享链接。
  → **Mitigation**：保留序号 ID，kebab-case 仅进脚注。
- **Risk**：新增 ⛔ 阻塞 可能让卡片看起来"更惨"。
  → **Mitigation**：图例清晰标注"阻塞 = 外部依赖未就绪"，并在脚注给出阻塞原因摘要与解锁依赖。
- **Trade-off**：未为 Osto/Sage 等新 Agent 立卡。
  → 接受：本次只动能力同步与通用能力卡片，避免单个 PR 改动面过大；Osto 立卡走独立变更。

## Migration Plan

1. 以单次 commit 在 `index.html` 内完成 CSS 追加 + Agents 技能树重写 + 通用能力卡片新增。
2. 在浏览器（Desktop ≥ 960、Mobile ≤ 520）手动验证：
   - auth 门仍然生效
   - 编辑/保存/导出按钮可见
   - TOC 9 项 + 滚动锚点
   - 打印样式（预览）卡片不跨页截断
3. 不涉及数据库/后端/依赖；回滚 = `git revert`。

## Open Questions

- 是否要在附录（`#appendix`）追加"已归档 17 个 SKILL"说明？**默认不加**，避免喧宾夺主，后续有需要再追加。
- `common-*` 的头像是否需要自定义 PNG？**本次用字母占位 `N`**，保持本次零资源依赖。
