---
title: "第 5 课 - 自定义并使用 quality-checks 技能"
description: "了解现有的 quality-checks 技能，自定义其报告格式，并用它验证筛选功能。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

编写代码不只是编写代码。我们已经能够手动验证代码是否正常运行，也使用指令文件确保代码遵循标准。测试、Lint 以及持续集成 (CI) 中的其他环节又该如何处理？

对于这类任务，**智能体技能**最适合不过！技能可帮助 Copilot 了解如何正确执行这些操作。

本课将介绍如何：

- 了解现有的 `quality-checks` 技能。
- 自定义其结果格式。
- 重新加载并运行该技能。

## 场景

Tailspin Toys 使用 `quality-checks` 技能运行单元测试、Lint 和类型检查。团队希望改进报告，让结果更易阅读。

## 指令、脚本和资源

智能体技能将可复用的任务说明、可执行脚本和辅助资源打包在一起，供智能体按需加载。技能的核心是一个以技能名称命名的文件夹，其中包含一个名为 `SKILL.md` 的 Markdown 文件。该 Markdown 文件包含 frontmatter，其中的名称和描述定义了技能的用途；正文介绍技能的功能及其适用场景。文件夹中还可以包含供技能使用的脚本和其他资源子目录。

> [!NOTE]
> 技能不一定需要额外的文件或文件夹。Tailspin Toys 的 `quality-checks` 技能只包含 `SKILL.md`，因为它使用项目现有的命令。

技能可以位于项目的 `.github/skills` 文件夹中，作为团队共享和复用的存储库资源；也可以放在用户技能文件夹 `~/.copilot/skills` 中。

## 探索技能

我们来看看 Tailspin Toys 团队创建的 `quality-checks` 技能，它用于运行单元测试、Lint 和类型检查。

1. 返回 Codespace。在 Codespaces 编辑器中打开 `.github/skills/quality-checks/SKILL.md`。
2. 阅读文件顶部的 `name` 和 `description`。描述有助于 Copilot 判断何时调用该技能。
3. 阅读说明，留意它如何引导 Copilot 执行测试和 Lint 流程。
4. 注意该技能目前没有 **Results output formatting** 部分。

## 更改前运行技能

你可以直接通过 Copilot CLI 调用技能，也可以使用自然语言请求。我们先让 Copilot 运行该技能中的三项检查。

1. 返回筛选功能的 Interactive 模式对话。
2. 使用以下提示：

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 留意最后生成的报告。

## 自定义报告

我们希望改进报告，说明运行了什么、是否成功，以及工具实际报告的内容。现在来更新技能，让它生成这样的报告！

1. 返回 `.github/skills/quality-checks/SKILL.md`。
2. 将以下部分添加到文件末尾：

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. 文件会自动保存。

## 运行更新后的技能

完成更改后，我们来看看效果！Copilot CLI 无需重启对话即可重新加载编辑后的技能。

1. 输入：

   ```plaintext
   /skills reload
   ```

2. 使用与之前完全相同的提示：

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 留意最后生成的报告，并将其与第一次报告进行比较。

## 总结和后续步骤

你已自定义并使用现有智能体技能。本课中，你：

- 了解了用于单元测试、Lint 和类型检查的 `quality-checks` 技能。
- 自定义了结果格式。
- 重新加载并运行了该技能。

这项更改将与筛选功能一起纳入功能 PR。接下来，你将通过 [Playwright MCP 服务器][next-lesson]让 Copilot 直接与网站交互。

## 更多技能示例

以下社区示例仅供参考，不是额外的任务：

- [Agent Skills 规范][skill-spec]
- [贡献工作流：`make-repo-contribution`][contribution-example]
- [需求文档：`prd`][prd-example]
- [图表和配套导出脚本：`drawio`][drawio-example]
- [浏览器测试：`webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
