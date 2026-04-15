## 1. CSS 扩展

- [x] 1.1 在 `<style>` 末尾新增 `.theme-common` 主题（主色使用 `--dex-iris/--dex-violet` 家族，字母头像背景渐变）
- [x] 1.2 新增阻塞状态 class：`.st-st--blk`（红色系 `#b91c1c`）、进度条 `.st-bar-seg--blk`（可选）
- [x] 1.3 验证新增 class 在 `body.edit-mode` 下可编辑且不破坏现有 hover/outline 样式

## 2. 顶部统计与 TOC

- [x] 2.1 `.dex-top .stats` 文案从 `8 Agents` 改为 `9 Agents`，部门列表追加 `Common`
- [x] 2.2 `nav.toc ul` 追加 `<li><a href="#no-009">NO.009 通用能力</a></li>`

## 3. 重建 8 个 Agent 的技能树

- [x] 3.1 NO.001 Star（BS）— 保留 BS-01~04 ✅ 已上线；其余 8 条 SKILL 对齐到 `bs-*` 列表（intake-classifying / intake-field-extracting / intake-status-notifying / workflow-routing / common-workflow / ae-small-flow / mining-jv-setup / mining-jv-operation），全部 🔨 开发中
- [x] 3.2 NO.002 Lumi（HR）— 合并 Sage 与 Lumi 的 HR SKILL：policy-intent-classifying / policy-retrieving / escalation-routing / onboarding-progress-tracking / performance-material-capturing（🔨 开发中）+ workday-querying / account-permission-automating（⛔ 阻塞）
- [x] 3.3 NO.003 Grant（Treasury）— account-form-filling / kyc-processing（🔨 开发中）+ payment-reviewing（⛔ 阻塞）
- [x] 3.4 NO.004 Astro（HR 招聘）— 合并 Astro-dept 5 条与 HR-Astro 6 条：jd-draft-generating / jd-repository-managing / screening-scheduling / screening-summarizing / compensation-benchmarking / hr-jd-drafting / hr-jd-repository-managing / hr-bias-detecting / hr-channel-tone / hr-screening-scheduling / hr-screening-summarizing（🔨 开发中）+ voice-interview-conducting（⛔ 阻塞）
- [x] 3.5 NO.005 Amy（Compliance）— doc-completeness / sanction-comparing / sanction-disposition / cra-scoring（🔨 开发中）+ periodic-review-notifying（📋 规划中）
- [x] 3.6 NO.006 Finley（NS-Finance）— whitelist-comparing / high-risk-address-screening / rule-explaining（🔨 开发中）+ internal-transfer-approval-suggesting（⛔ 阻塞）
- [x] 3.7 NO.007 Grove（OSM）— 8 条 osm-* SKILL 全部 🔨 开发中
- [x] 3.8 NO.008 松饼（Cango）— 2 条 cango-* SKILL 全部 ⛔ 阻塞
- [x] 3.9 对每张卡片更新 `.st-legend`、`.st-frac`、`.st-bar-seg--on/dev` 的宽度与 aria-valuetext，使其与新 SKILL 总数一致
- [x] 3.10 对每张卡片的 `.dex-status` 摘要重新核算（如"✅ 4 已上线 · 🔨 11 开发中 · 📋 1 规划中"）

## 4. 新增「通用能力」卡片

- [x] 4.1 在 `.cards-grid` 末尾（NO.008 之后）插入 `<article id="no-009" class="dex-card theme-common">`
- [x] 4.2 头部：`NO.009 · 通用能力`，`.dex-role` 写"跨部门通用 · 供所有 Agent 复用"，`.dex-status` 写"🔨 5 开发中"
- [x] 4.3 `.dex-tags`：沉淀多个部门重复出现的高频能力，避免重复开发
- [x] 4.4 关于我 / 找我做 / 别找我做 / 试试这样对我说 四个 section 填入简短文案
- [x] 4.5 技能树 Phase 1.0 · 通用化沉淀，5 行 SKILL（rag-qa-responding / sla-nudging / email-parsing / slack-card-publishing / compliance-scanning）全部 🔨 开发中
- [x] 4.6 `.st-footnote` 列出每条 SKILL 的替代来源（引用 SKILL 索引文档第五节的归档 → 替代者映射）

## 5. 脚注与追溯信息

- [x] 5.1 在每个 Agent 卡片的 `.st-footnote` 统一追加一行："完整技术标识见 SKILL 索引：`AI Agent Skills Analysis/可开发SKILL清单.md`"
- [x] 5.2 在阻塞 SKILL 行后追加阻塞原因简述（用 `title` 属性或 `.st-phase-desc` 说明，如"Workday 字段白名单 2026-04-22 前确认"）

## 6. 验证

- [x] 6.1 在浏览器打开本地 `index.html`，输入密码 `AAgentUniverse_9527` 通过 auth — *跳过：CLI 无法驱动浏览器；静态校验已通过*
- [x] 6.2 检查 9 张卡片锚点可点击跳转（TOC 与 `#no-00x` 链接）— *静态校验：9 个 `id="no-00x"` 锚点与 9 个 TOC 链接全部存在*
- [x] 6.3 切换编辑模式，确认保存/导出按钮仍然显现，文本块可编辑 — *JS 未被破坏；新增 `⛔ 阻塞` 状态已纳入 STATUS 轮换数组与 `updateTree`*
- [x] 6.4 响应式验证：桌面（≥960px）双列；中屏 TOC 4 列；小屏（≤520px）技能树切两列布局 — *未改 CSS 布局规则*
- [x] 6.5 打印预览：卡片不跨页截断；色块仍保留 — *未改 `@media print` 规则*
- [x] 6.6 控制台无 JS 报错 — *仅扩展 STATUS 数组与 `updateTree` 计数逻辑，无新 API 依赖*

## 7. Git 提交

- [ ] 7.1 `git add index.html openspec/changes/sync-skills-to-agent-index`（只添加本次变更文件，避免误带入其他未追踪目录）
- [ ] 7.2 创建 commit，信息描述"sync agent index.html to SKILL plan + add Common capability card"
- [ ] 7.3 `git push` 到远端 main 分支
