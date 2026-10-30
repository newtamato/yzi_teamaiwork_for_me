# Agent Project Template

为新项目或已有项目提供可维护的 Agent 工程机制：规则入口、文件记忆、Skill、定时触发、工作树协作和交付守卫。业务语言不限，工程工具使用 Node 22 内置模块，无额外运行依赖。

## 快速开始

```sh
npm run agent -- help
npm run agent -- memory-check
npm run check
```

先修改 `agent.config.json` 的项目名称和仓库配置（默认分支main、任务前缀taskPrefix默认codex/、可按agent改为空或其它前缀），再参考 [新项目接入](doc/getting-started.md)。已有项目使用 [渐进接入教程](doc/adopting-existing-project.md)，不要覆盖已有约定或历史文件。

## 目录与机制

| 位置 | 保存什么 |
|---|---|
| [AGENTS.md](AGENTS.md)、`rules/` | 入口与执行约束，正文只维护一份 |
| [memory/INDEX.md](memory/INDEX.md)、[记忆模板](memory/TEMPLATE.md) | 可检索的稳定知识、证据与失效条件；初始知识库为空 |
| `.agents/skills/` | 可重复操作；含 [task-delivery](.agents/skills/task-delivery/SKILL.md) 和 [scheduled-audit](.agents/skills/scheduled-audit/SKILL.md) |
| `templates/` | 未加载的Skill模板、定时配置和复盘输入示例 |
| `scripts/`、`tests/` | 确定性治理工具和合成验证 |
| `.delivery/memory/` | 任务审计回执，不当作记忆条目 |
| `.runtime/`、`.worktree/` | 本地运行产物与任务副本，不提交 |

## 工程命令

```sh
npm run agent -- task create improve-guide
npm run agent -- task status
npm run agent -- review --input .runtime/review-input.json
npm run agent -- capabilities sync
npm run agent -- capabilities check
npm run agent -- automation check templates/automation/scheduled-audit.json
npm run agent -- merge-check
```

`review` 在任务工作树执行，工具填入真实任务、分支、基线和源码指纹。`check`运行结构、任务回执及配置中的检查；`merge-check`是平台合并前的本地门禁，不会替你调用平台合并。具体行为以当前 help 和 [开发规范](rules/development.md) 为准。

能力登记默认关闭；启用后登记实际来源、命令或排除原因，sourceDirectories可自动发现指定目录里的新增来源，未映射的新文件会阻断。来源变更需要同步快照并完成 `cliReview`。模板不解析任意语言的API路由或自动证明输入语义；配置检查和发布钩子不等于平台CI或完整部署系统，不启用尚未接入的操作。

## 配套说明

- [模板抽取记录与长期演进](doc/extraction-and-evolution.md)：抽取范围、解耦改造、第一版验收、能力边界与长期维护方式。

- [架构与职责](doc/architecture.md)：规则、知识、流程、工具如何配合。
- [新项目接入](doc/getting-started.md)：初始化、第一次任务和验收。
- [已有项目接入](doc/adopting-existing-project.md)：保留原有内容，分阶段启用门禁。
- [维护与升级](doc/maintenance.md)：配置、版本、知识失效和检查边界。

本仓库只提供工程机制与合成示例，不包含业务源码、数据库、原件、实际记忆、真实定时配置或认证文件。初始发布的验证由维护者执行并记录，文档不预设测试数量。公开使用前请配置自己的仓库权限、CI与发布流程。
