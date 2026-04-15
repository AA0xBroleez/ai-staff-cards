# Project Rules

## 基础规则

### 规则 1: 语言偏好
所有对用户的回答优先使用中文，除非有特殊说明。

### 规则 2: 开发工作流
涉及到需要进行开发的项目，使用以下标准流程：
1. 使用 `/opsx:propose` 命令进行规划
2. 规划完成后自动进行 `/opsx:apply` 进行程序计划执行
3. 任务执行完成后使用 `/opsx:archive` 进行归档

**注意**: 使用不审核模式运行。

### 规则 3: Git 提交
开发任务完成后，如果当前项目是有 git 进行管理的，需要提交当前分支的变更到远端。

### 规则 4: 并行任务执行
如果需要执行的任务数超过 3 个，并且彼此没有依赖管理，创建多个 subagents 同步进行任务执行。

### 规则 5: SKILL 变更同步到 index.html（仅限本项目）
在每一次 `/opsx:propose` 计划中，若涉及到 SKILL 分类的**新增、删除、修改**，或 SKILL **状态变更**（如：草稿 / 开发中 / 已上线 / 已下线 等），必须同步更新本项目根目录下的 `index.html`，以保持 Agent 能力清单与任务进行状态的一致性。

具体要求：
1. **触发条件**：`/opsx:propose` 生成的变更包内，`tasks.md` 或 `proposal.md` 中出现任何 SKILL 的增 / 删 / 改 / 状态变更动作。
2. **同步范围**：
   - Agent 能力清单（capability list）：新增/删除条目，或更新条目描述与归属分类。
   - 任务进行状态（task status）：与 OpenSpec 中的任务状态保持一致（待开始 / 进行中 / 已完成 等）。
3. **执行时机**：在 `/opsx:apply` 阶段执行 SKILL 相关任务的同时（或同一次提交内）更新 `index.html`，避免页面与实际能力脱节。
4. **归档校验**：`/opsx:archive` 之前需确认 `index.html` 已与最终的 SKILL 状态对齐，否则不允许归档。

## Read-Only Paths

The following paths are **read-only**. Agents must never create, edit, delete, or write any files under these directories:

- `知识库/` (symlink → `共享云端硬盘/知识库`)

These directories are knowledge-base references for reading only. Any write attempt is prohibited.
