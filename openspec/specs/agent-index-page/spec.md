# agent-index-page Specification

## Purpose
TBD - created by archiving change sync-skills-to-agent-index. Update Purpose after archive.
## Requirements
### Requirement: 卡片总览对齐 SKILL 索引文档

`index.html` 的卡片集合 SHALL 与 `AI Agent Skills Analysis/可开发SKILL清单.md` 保持"Agent ↔ SKILL ↔ 状态"的一致性。每个 Agent 卡片中列出的 SKILL 条目 MUST 覆盖该 Agent 在索引文档中所有 draft/blocked/planned 状态的 SKILL，不多不少（不含已归档 `ex/` SKILL）。

#### Scenario: 用户在图鉴中查看某 Agent 的能力
- **WHEN** 用户打开 `index.html` 并展开任意 Agent 卡片的「技能树」
- **THEN** 卡片中 SKILL 条目数量与 `可开发SKILL清单.md` 中该 Agent 的"可开发 + 阻塞 + 规划中"总数一致
- **AND** 每条 SKILL 的中文短名与索引文档中的"描述摘要"语义匹配
- **AND** 每条 SKILL 的技术标识（如 `bs-intake-classifying`）以 `<code>` 形式在卡片脚注可见

#### Scenario: SKILL 索引文档归档某 SKILL
- **WHEN** 某 SKILL 在索引文档中被移入 `ex/` 归档
- **THEN** 该 SKILL MUST 从 Agent 卡片技能树中移除
- **AND** `index.html` 渲染结果不应包含该 SKILL 的行

### Requirement: SKILL 状态语义映射

技能树 SHALL 使用以下四种状态呈现 SKILL：`✅ 已上线`、`🔨 开发中`、`⛔ 阻塞`、`📋 规划中`。状态映射规则为：

- 线上部署事实为"已上线"的 SKILL 显示 `✅ 已上线`（当前仅 BS-01~04）
- 索引文档状态 `draft` 的 SKILL 显示 `🔨 开发中`
- 索引文档状态 `blocked` 的 SKILL 显示 `⛔ 阻塞`
- 索引文档状态 `planned` 的 SKILL 显示 `📋 规划中`

每条 SKILL 行 MUST 只显示一个状态标签。

#### Scenario: 阻塞 SKILL 的展示
- **WHEN** 某 SKILL 在索引文档中标记为 `blocked`
- **THEN** 对应行 MUST 显示 `⛔ 阻塞` 标签
- **AND** 使用区别于绿色（已上线）、橙色（开发中）、灰色（规划中）的红色系配色
- **AND** 图例区 (`.st-legend`) MUST 在该 Agent 有阻塞 SKILL 时显示阻塞计数

#### Scenario: BS 已上线 SKILL 的保留
- **WHEN** 渲染 NO.001 Star（BS）卡片
- **THEN** BS-01 至 BS-04 SHALL 保持 `✅ 已上线` 状态
- **AND** 这 4 条 SKILL 不依赖索引文档的 draft/blocked/planned 状态字段

### Requirement: 技能树计数与进度条

每个 Agent 卡片的技能树头部 SHALL 展示"已上线 / 开发中 / 阻塞 / 规划中"四类计数，并在 `.st-progress-row` 以进度条可视化。进度条的"已上线"段与"开发中"段宽度 MUST 按该 Agent 实际 SKILL 数占比精确计算。

#### Scenario: 计数与 SKILL 行数一致
- **WHEN** 渲染任意 Agent 卡片的 `.st-legend`
- **THEN** 图例中四类状态的计数之和 MUST 等于 `.st-phase` 下所有 `.st-row` 的总数
- **AND** `.st-frac` 显示的 "x / total" 中 total MUST 等于该总数

#### Scenario: 进度条宽度计算
- **WHEN** 某 Agent 有 `n_on` 个已上线 SKILL、`n_dev` 个开发中 SKILL、总数 `n_total`
- **THEN** `.st-bar-seg--on` 的 `style.width` MUST 等于 `n_on / n_total * 100%`
- **AND** `.st-bar-seg--dev` 的 `style.width` MUST 等于 `n_dev / n_total * 100%`

### Requirement: Phase 分组

每个 Agent 的 SKILL 条目 SHALL 按阶段（Phase 1.0 / Phase 2.0 / 分册）分组展示，每个 `.st-phase` 块包含标题（如 `Phase 1.0`）与简短主题描述（`.st-phase-desc`）。阶段划分 MUST 与该 Agent 既有的 Phase 语义一致（沿用 2025 年图鉴中的阶段命名），新 SKILL 按其业务属性归入最贴切的 Phase。

#### Scenario: Phase 描述与 SKILL 组合
- **WHEN** 渲染任一 Agent 的 `.st-phase` 头部
- **THEN** `h4` 中包含 Phase 标题（`Phase x.y` 或 `分册`）
- **AND** 包含 `.st-phase-desc` 斜体描述
- **AND** 该 `.st-phase` 下至少包含一条 `.st-row`

### Requirement: 通用能力卡片

`index.html` SHALL 包含一张独立的「通用能力」卡片（NO.009），位于 8 张 Agent 卡片之后。该卡片 MUST 展示 `common-*` 系列 SKILL，当前包含：`common-rag-qa-responding`、`common-sla-nudging`、`common-email-parsing`、`common-slack-card-publishing`、`common-compliance-scanning`。

通用能力卡片 MUST：
- 使用独立主题类 `theme-common`（区别于 8 个部门 Agent 的主题色）。
- 在头部 `.dex-role` 标注 "跨部门通用 · 供所有 Agent 复用"。
- 在技能树图例与进度条中把 5 条 SKILL 状态全部渲染为 `🔨 开发中`。
- 在页面顶部 TOC (`nav.toc ul`) 与 `.dex-top .stats` 统计条中被一并计入"9 Agents"与部门列表。

#### Scenario: 用户查看通用能力卡片
- **WHEN** 用户滚动至页面底部或点击 TOC 中的"通用能力"入口
- **THEN** 可见一张名为"通用能力"的卡片，列出 5 个 `common-*` SKILL
- **AND** 每条 SKILL 状态显示为 `🔨 开发中`
- **AND** 卡片 `.dex-tags` 说明"承接多个部门重复需求的通用化沉淀"

#### Scenario: 通用能力卡片引用关系追溯
- **WHEN** 查看通用能力卡片的脚注 `.st-footnote`
- **THEN** 对每条 `common-*` SKILL 应列出其替代来源（对应 `可开发SKILL清单.md` 第五节的"归档 SKILL → 替代者"映射）

### Requirement: 不回归的保护项

修改 `index.html` 时 MUST NOT：
- 破坏 auth overlay (`#authOverlay`) 的 DOM 与其 XOR 校验脚本。
- 改动编辑模式、保存、导出按钮的 JS 行为。
- 删除或重命名 CSS 变量 (`:root` 中 `--ink/--muted/--surface/--card/--radius/--dex-*`)。
- 删除现有 Agent 卡片的 `article[id]` 锚点（保持 `#no-001` ~ `#no-008` 可用）。

#### Scenario: 认证层仍然生效
- **WHEN** 用户在 localStorage 无有效 `dex-auth-v1` token 时打开页面
- **THEN** 认证覆盖层 SHALL 出现并阻塞页面交互
- **AND** 输入正确密码后覆盖层消失，页面正常显示

#### Scenario: 编辑模式可用
- **WHEN** 点击 `.mode-toggle`
- **THEN** `body` 应添加 `edit-mode` class
- **AND** 保存/导出按钮应显现，文本块可编辑

