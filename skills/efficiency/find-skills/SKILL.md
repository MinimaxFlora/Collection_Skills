---
name: find-skills
description: 当用户提出类似“如何做 X”“帮我找一个用于 X 的 skill”“有没有可以完成 X 的 skill”等问题，或者表达希望扩展能力时，帮助用户发现并安装 agent skills。
---

# 查找 Skills

这个 skill 帮助你从开放的 agent skills 生态系统中发现和安装 skills。

## 什么时候使用这个 Skill

当用户：

* 询问“如何做 X”，而 X 可能存在一个现有的 skill
* 说“为 X 找一个 skill”或“有没有适用于 X 的 skill”
* 询问“你能做 X 吗”，而 X 是一种专业能力
* 表达希望扩展 agent 的能力
* 希望搜索工具、模板或工作流
* 提到希望在某个特定领域获得帮助（设计、测试、部署等）

## 什么是 Skills CLI？

Skills CLI（`npx skills`）是开放 agent skills 生态系统的包管理器。Skills 是模块化的软件包，可以通过专业知识和工作流扩展 agent 的能力。

**主要命令：**

* `npx skills find [query] [--owner <owner>]` - 交互式搜索 skill，也可以通过关键词搜索，并可选择限定 GitHub owner
* `npx skills add <package>` - 从 GitHub 或其他来源安装 skill
* `npx skills update` - 更新所有已安装的 skills

**浏览 skills：** https://skills.sh/

## 如何帮助用户查找 Skills

### 第一步：了解他们需要什么

当用户寻求帮助时，确定：

1. 领域是什么（例如 React、测试、设计、部署）
2. 具体任务是什么（例如编写测试、创建动画、审查 PR）
3. 这是否是一个足够常见的任务，以至于很可能已经存在对应的 skill

### 第二步：首先检查排行榜

在运行 CLI 搜索之前，先查看 [skills.sh 排行榜](https://skills.sh/)，确认该领域是否已经存在知名的 skill。排行榜按照总安装量对 skills 进行排名，可以优先发现最热门、经过大量实际使用验证的选项。

例如，Web 开发领域的热门 skills 包括：

* `vercel-labs/agent-skills` — React、Next.js、Web 设计（每个 skill 超过 10 万次安装）
* `anthropics/skills` — 前端设计、文档处理（超过 10 万次安装）

### 第三步：搜索 Skills

如果排行榜没有覆盖用户的需求，则运行 find 命令：

```bash
npx skills find [query] [--owner <owner>]
```

例如：

* 用户问“怎么让我的 React 应用运行得更快？” → `npx skills find react performance`
* 用户问“可以帮我进行 PR 审查吗？” → `npx skills find pr review`
* 用户问“我需要创建一个 changelog” → `npx skills find changelog`

### 第四步：推荐之前验证质量

**不要仅仅根据搜索结果推荐一个 skill。** 始终验证：

1. **安装数量** — 优先选择安装量超过 1K 的 skills。对于低于 100 次安装的 skill 要谨慎。
2. **来源信誉** — 官方来源（`vercel-labs`、`anthropics`、`microsoft`）通常比未知作者更值得信任。
3. **GitHub Stars** — 检查源仓库的 GitHub Stars。来自 Stars 少于 100 的仓库的 skill 应谨慎对待。

### 第五步：向用户提供选项

找到相关 skills 后，向用户展示：

1. skill 名称以及它的功能
2. 安装数量和来源
3. 用户可以运行的安装命令
4. skills.sh 上的详细信息链接

示例：

```text
我找到了一个可能有帮助的 skill！“react-best-practices” skill 提供了
来自 Vercel Engineering 的 React 和 Next.js 性能优化指南。
（185K 次安装）

安装方式：
npx skills add vercel-labs/agent-skills@react-best-practices

了解更多：
https://skills.sh/vercel-labs/agent-skills/react-best-practices
```

### 第六步：提供安装选项

如果用户希望继续，可以帮助他们安装 skill：

```bash
npx skills add <owner/repo@skill> -g -y
```

`-g` 参数会进行全局（用户级）安装，`-y` 参数会跳过确认提示。

## 常见 Skill 类别

搜索时可以考虑以下常见类别：

| 类别     | 示例查询                                 |
| ------ | ------------------------------------ |
| Web 开发 | react、nextjs、typescript、css、tailwind |
| 测试     | testing、jest、playwright、e2e          |
| DevOps | deploy、docker、kubernetes、ci-cd       |
| 文档     | docs、readme、changelog、api-docs       |
| 代码质量   | review、lint、refactor、best-practices  |
| 设计     | ui、ux、design-system、accessibility    |
| 生产力    | workflow、automation、git              |

## 高效搜索技巧

1. **使用具体关键词**：“react testing” 比单独搜索 “testing” 更好
2. **尝试替代术语**：如果 “deploy” 没有结果，可以尝试 “deployment” 或 “ci-cd”
3. **检查热门来源**：许多 skills 来自 `vercel-labs/agent-skills` 或 `ComposioHQ/awesome-claude-skills`

## 没有找到 Skills 时

如果没有找到相关的 skills：

1. 承认没有找到现有的 skill
2. 提供直接使用你的通用能力帮助完成任务
3. 建议用户可以使用 `npx skills init` 创建自己的 skill

示例：

```text
我搜索了与“xyz”相关的 skills，但没有找到匹配项。
我仍然可以直接帮助你完成这个任务！你想让我继续吗？

如果这是你经常需要执行的任务，可以创建自己的 skill：
npx skills init my-xyz-skill
```
