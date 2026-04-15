## Why

当前 `index.html` 中每个 Agent 的「技能树」还停留在 2025 年基于各部门零散 CSV 草拟的版本，而 `AI Agent Skills Analysis/可开发SKILL清单.md`（2026-04-15）已完成一次结构性梳理：新增 5 个跨部门通用 SKILL、参数化合并 3 组共 8 个原 SKILL、归档 17 个被替代的 SKILL，并明确了 66 draft / 10 blocked / 1 planned 的当前状态。为了让 AI 员工图鉴真实反映"正在开发/阻塞/规划"的能力布局，需要把 `index.html` 的能力清单与进度状态对齐到该索引文档，并新增「通用能力」卡片凸显可被多 Agent 复用的 Skill。

## What Changes

- 重新生成 8 个 Agent 卡片的技能树，使其 SKILL 名称/ID、Phase 分组、状态对应到 `可开发SKILL清单.md`。
- 新增一张「通用能力」（Common Capabilities）卡片，展示正在开发的 5 个跨部门通用 SKILL：`common-rag-qa-responding`、`common-sla-nudging`、`common-email-parsing`、`common-slack-card-publishing`、`common-compliance-scanning`。
- 引入「⛔ 阻塞」状态标签与配色，用于展示 10 个因外部依赖阻塞的 SKILL。
- 保留 BS（Star）已上线的 4 个 SKILL 的 ✅ 已上线 标记，其余按 SKILL 文档的 draft/blocked/planned 映射为 🔨 开发中 / ⛔ 阻塞 / 📋 规划中。
- 顶部统计带（dex-top stats）从 `8 Agents` 更新为 `9 Agents`（含通用能力），总览计数同步更新。
- 不改动：auth overlay、模式切换/保存/导出逻辑、配色变量、现有"找我做/别找我做"与"试试这样对我说"文案。

## Capabilities

### New Capabilities
- `agent-index-page`: AI 员工图鉴单页视图的内容模型与渲染契约（卡片结构、技能树/Phase 分组、状态语义、通用能力卡片的展示规则）。

### Modified Capabilities
<!-- 无已有 spec，全部作为新 capability 建模。 -->

## Impact

- 修改文件：`index.html`（仅 `<body>` 内 Agent 卡片区域与 `dex-top .stats`；CSS 仅新增"阻塞"状态配色与通用能力卡片主题类）。
- 数据来源（只读）：`AI Agent Skills Analysis/可开发SKILL清单.md` 与 `SKILLS/` 目录。
- 无 JS/认证逻辑变更；不影响 `localStorage` 的 `dex-auth-v1` 与导出功能。
- 下游：后续任何 SKILL 的增删/状态变更都应以本 capability 的约束为入口同步更新 `index.html`（见 CLAUDE.md 规则 5）。
