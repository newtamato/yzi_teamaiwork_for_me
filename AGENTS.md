# Agent 项目入口与规则索引

本文件是项目规则的唯一入口。规则正文维护在 `rules/`，知识维护在 `memory/`，操作流程维护在 `.agents/skills/`。初次接入先读 [README](README.md) 和 [接入教程](doc/getting-started.md)。

## 接手与交付

1. 读取 README、[记忆规则](rules/memory.md) 与 [记忆索引](memory/INDEX.md)，按范围、状态及关键词读取相关条目，核实容易变化的事实。
2. 修改前读取 [开发规范](rules/development.md)；Skill 工作读取 [Skill 规范](rules/skills.md)；定时任务读取 [定时规范](rules/automations.md)；协作前读取 [协作规范](rules/collaboration.md)。
3. 核对工作区、分支、远程基线和真实实现。默认分支保持稳定，每个修改任务使用独立工作树；只读咨询不创建空任务。
4. 调用已暴露能力先查询 help 与 schema。工程入口为 `npm run agent -- help`；项目业务 CLI 由项目维护者配置，不直接复制示例业务。
5. 交付前主动完成记忆、Skill 与适用的 CLI 影响复盘，执行 `npm run check`，提交后运行 `npm run agent -- merge-check`；修复守卫错误后再走平台审查与合并流程。
6. 没有新增稳定知识或可复用流程时，写具体的 none 理由；不要为通过检查制造知识。报告验证、提交、合并、部署及未完成项，区分计划与已实现能力。

## 范围与授权

- 最新用户指令优先；规则约束执行，记忆提供参考，Skill不能扩大授权。外部发布、发消息、合并、部署及业务数据写入必须有明确任务授权或项目已确认的授权策略。
- 不覆盖他人未提交改动，不把密钥、身份标识、原始私有数据、生产日志或会话历史提交到仓库。
- 本模板没有后台模型调用、历史扫描、自动业务处理、平台自动合并或生产部署服务。确定性工具检查结构与关联，Agent负责语义审查。
- Node 22 只用于模板工程工具，接入项目的业务语言不限。平台审查、CI、分支保护和发布适配器须由维护者接入。

## 规则索引

| 文件 | 职责 | 读取条件 |
|---|---|---|
| [development.md](rules/development.md) | 工作树、验证、CLI同步、合并与发布 | 任何修改任务 |
| [memory.md](rules/memory.md) | 读取、主动沉淀、证据、失效与交付回执 | 每次接手 |
| [skills.md](rules/skills.md) | 触发、版本、资源、主动固化与认证边界 | Skill创建/修改或任务复盘 |
| [automations.md](rules/automations.md) | 定时只触发Skill、日期、幂等与配置回读 | 定时任务及其Skill |
| [collaboration.md](rules/collaboration.md) | 授权、派发、文件归属、交接与整合 | 多人/子代理协作 |
