# Codebase Onboarding Pro

分析陌生代码库，并在开发结束后按需维护项目 `AGENTS.md` 与关联文档。

本 skill 基于 [ECC 的 codebase-onboarding](https://github.com/affaan-m/ECC/tree/d2ef2680594f9a17526a6e1a2e18b3d242c5d17b/skills/codebase-onboarding) 改进，由 **Lhbacxc** 维护。保留原版的完整入门分析，新增增量维护模式，使用中文说明和面向不同 AI 编码代理的项目指令。

## 安装

使用支持 SKILL.md 的 skills CLI：

```powershell
npx skills add https://github.com/lhbacxc/codebase-onboarding-pro --skill codebase-onboarding-pro
```

安装器会提示选择代理和安装范围。只查看可发现的 skill：

```powershell
npx skills add https://github.com/lhbacxc/codebase-onboarding-pro --list
```

安装器需要 Node.js、npm 和 Git。skill 本身是 Markdown 指令，不包含服务程序，也没有 Python 依赖。

## 两种工作模式

| 场景 | 模式 | 结果 |
|------|------|------|
| 首次接手陌生项目、了解架构 | A：完整入门分析 | 入门指南与项目 AGENTS.md |
| 为已有项目创建或更新代理指令 | B：增量维护；证据不足时补查 | 必要的 AGENTS.md 或关联文档更新 |
| 开发、重构或排障改变了长期项目事实 | B：增量维护 | 同步命令、约束、目录职责等已确认事实 |
| 普通局部修改，没有长期事实变化 | 检查后结束 | 不改文档，不重复生成入门指南 |

### 模式 A：完整入门分析

依次检查项目概况、梳理架构、识别约定并生成入门资料。覆盖依赖与框架、入口、目录职责、请求处理流程、测试和 Git 约定。

### 模式 B：开发后的增量维护

复用当前任务已读取的代码、配置、差异与验证结果，只补查受影响的事实。保留已有用户规则、人工内容及有效约定；详细事实更新到项目已有文档，`AGENTS.md` 保持简洁并链接对应入口。

## 使用示例

- “带我了解这个代码库。”
- “用当前项目约定更新 AGENTS.md。”
- “把测试入口改成新脚本，并修好环境路径问题。”

支持显式引用技能名的代理也可使用 `$codebase-onboarding-pro`。代理是否自主选用 skill 取决于其发现机制和任务匹配；本 skill 提供工作流程，不是后台监控程序。

如希望项目明确要求开发后检查文档，可以把下面规则合并到该项目已有 `AGENTS.md`，并遵循项目原有组织方式：

```markdown
## 项目文档维护

- 开发或维护前读取适用的 AGENTS.md 及其文档入口。
- 结束任务前检查是否改变了长期项目事实；有变化时使用 codebase-onboarding-pro 的增量维护模式。
- 只同步经代码、配置或实际验证确认的事实，保留用户规则和有效约定。
- 详细内容更新到已有项目文档，AGENTS.md 保留执行规则、关键约束与相对路径入口。
- 没有长期事实变化时不写文档，不重复执行完整入门分析。
```

仅安装 skill 不会自动把这段规则写入你的项目或全局配置。

## 相比原版的主要改进

| 项目 | ECC 英文原版 | Pro 版 |
|------|-------------|--------|
| 项目指令入口 | CLAUDE.md | AGENTS.md；沿用已有大小写变体 |
| 工作流程 | 完整入门分析，更新指令时执行阶段 1–3 | 完整分析与增量维护分开选择 |
| 触发范围 | 首次接手项目、用户请求入门或生成指令 | 扩展到开发结束后长期事实变化时自主检查与维护 |
| 检查成本 | 为生成或更新指令执行项目分析 | 优先复用当前任务证据，仅补查相关事实 |
| 无事实变化 | 没有独立的增量跳过规则 | 不改文档，不生成额外入门资料 |
| 文档组织 | 重点维护单个 CLAUDE.md | 尊重现有文档分层，AGENTS.md 只保留关键入口与规则 |
| 语言与写入约束 | 英文原版 | 中文说明与模板，明确 UTF-8 和相对路径 |
| 代码定位 | 定向 Glob/Grep 与选择性读取 | 已配置索引时遵循项目要求优先使用，并考虑新鲜度 |

更完整的对照、保留内容和版本依据见 [升级差异说明](./docs/upstream-differences.md)。

## 仓库文件

- [SKILL.md](./SKILL.md)：可安装的技能入口，保留本地 Pro 版原文。
- [升级差异说明](./docs/upstream-differences.md)：与固定 ECC 版本的逐项比较。
- [CHANGELOG.md](./CHANGELOG.md)：发布记录。
- [AGENTS.md](./AGENTS.md)：维护这个 skill 仓库时使用的项目规则。
- [LICENSE](./LICENSE)：MIT 许可证与原作者、修改者版权声明。

## 来源与许可证

对照上游提交 `d2ef2680594f9a17526a6e1a2e18b3d242c5d17b` 中的 `skills/codebase-onboarding/SKILL.md`；原作者为 Affaan Mustafa。本版本是独立维护的衍生 skill，新增与修改内容由 Lhbacxc 维护，遵循 MIT 许可证。

这是本地 Pro 版的首次公开发布，不代表已自动合并未来上游更新。
