---
title: "练习 5：迭代 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

## 审查工作

在本实验中，你使用 GitHub Copilot 完成了多个改进用户体验和添加功能的任务。你请求 Copilot 为代码添加文档、实现供设计团队迭代的相关游戏功能，以及实现包含高对比度和浅色模式切换开关的无障碍功能。现在来检查代码更改；如有需要，也可以向 Copilot 提供反馈，改进其工作，然后再允许团队其他成员开始审查。

### 场景

如前所述，生成式 AI 不会改变软件设计和 DevOps 的基本原则。我们始终需要审查生成的代码，并遵循正常的 DevOps 流程。接下来，在开启团队审查之前，先审查 GitHub Copilot 为添加文档、实现相关游戏功能和无障碍功能提出的更改。

## GitHub Copilot 云智能体与安全性

由于 Copilot 云智能体在无人监督的情况下异步执行任务，系统设置了一些安全限制，以确保操作安全，其中包括：

- Copilot 只能读取存储库，并且**只能**写入用于编写代码的分支。
- 云智能体在 GitHub Actions 中运行，系统会为其创建单独的临时环境。
- 运行任何 GitHub Actions 工作流前，都必须由人工审批。
- 默认情况下，[对外部资源的访问受到限制](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)，MCP 服务器也在限制范围内。

## 审查生成的文档

先查看 GitHub Copilot 云智能体创建的第一个拉取请求 (PR)：为代码添加文档。你将使用 GitHub.com 上的标准 PR 界面。

> [!NOTE]
> 查看 PR 时，可能会看到 GitHub Copilot 被防火墙阻止的警告。这是**预期行为**，因为 Copilot 默认只能有限地访问外部资源，包括外部 MCP 服务器调用。如有需要，可以[自定义或禁用 Copilot 云智能体防火墙][agent-firewall]。

1. 返回 github.com 上的存储库。
2. 选择 **Pull Requests**，打开拉取请求列表。
3. 打开标题类似 **Add missing documentation** 的拉取请求，标题也可能更完整。

> [!NOTE]
> 如果 Copilot 仍在处理任务，拉取请求会带有 **[WIP]** 标记。此时请等待 Copilot 完成工作。这可能需要几分钟，你可以稍作休息，或回顾目前学到的内容。

4. 拉取请求准备就绪后，选择 **Files changed** 选项卡并审查更改。

    ![Files changed 选项卡](../../../_images/shared-pr-files-changed.png)

5. 查看新更新的代码，其中包括新生成的 TSDoc 文档注释和其他文档。具体更改会有所不同。

    浏览更改时，留意 TSDoc 文档注释、TypeScript 规范和注释头。这些内容来自你在练习 2 开始时查看的自定义指令文件。

6. 审查更新并确认符合预期后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有工作流正在等待审批的指示器。
8. 如果工作流正在等待审批，请选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)
9. 你应该会看到工作流在拉取请求的检查部分排队运行。如果一切正常，单体 Astro 应用程序的项目检查将通过。此过程可能需要几分钟。

## 请求 GitHub Copilot 更改

与 Copilot 协作并非单向过程。你可以像在拉取请求中提及团队成员一样，在评论或代码行内评论中提及 Copilot。Copilot 会读取这些评论，并启动新的会话来处理请求。由于结果并非确定，因此我们无法规定具体要向 Copilot 提出什么要求。你可以请求 Copilot 更新以下内容：

- 在每个代码文件顶部添加简要说明文件用途的注释头。
- 在 TypeScript 和 Astro 文件中添加 TSDoc 文档注释。
- 创建 README，介绍 Astro 应用程序结构。

1. 添加评论，请求更改生成的文档，并像提及用户一样标记 **@copilot**。你可以使用上述想法之一，也可以提出其他希望在代码库中看到的文档更改。
2. 选择 **View Session**，查看 Copilot 如何执行工作。留意 Copilot 如何启动新会话来完成更新。
3. 选择 **Back to pull request** 可返回拉取请求。

    ![Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Copilot 完成更改后，拉取请求中应会出现一项新提交。
5. 选择 **Files changed** 选项卡，审查更改。

可以继续迭代，直到满意为止。满意后，可以将 PR 从草稿转换为准备好审查，然后合并到 main 分支。

![将 PR 转为准备好审查](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

现在回到 Copilot 为解决“在游戏详情页显示相关游戏”议题而创建的 PR。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Show related games on the game details page** 的 PR，标题也可能更完整。
4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 审查更新并确认符合预期后，返回 **Conversation** 选项卡并向下滚动。
6. 查看是否有工作流正在等待审批的指示器。
7. 如果工作流正在等待审批，请选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)
8. 你应该会看到工作流在拉取请求的检查部分排队运行。如果一切正常，单体 Astro 应用程序的项目检查将通过。此过程可能需要几分钟。
9. **可选：**你也可以在 codespace 中切换到该分支，手动测试相关游戏功能。转到 codespace，打开终端并运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名称，例如 **copilot/fix-8**）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot 已经构建好相关游戏功能！与之前一样，你可以通过迭代请求 Copilot 更新。例如，可以请求 Copilot 调整显示的相关游戏数量，或添加注释头和 TSDoc 文档注释（请记住：分配此任务时，你还没有更新自定义指令！）。与之前一样，可以在 **Conversation** 选项卡中添加评论来提出请求，Copilot 会看到请求并启动新会话。

## 审查无障碍功能

最后，审查使用无障碍自定义智能体实现的功能。这个 PR 应包含练习 3 中请求的高对比度模式，以及练习 4 的任务控制中心中提出的浅色模式。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Add high contrast mode to website** 的 PR，标题也可能更完整。

> [!NOTE]
> 如果 Copilot 仍在处理任务，拉取请求会带有 **[WIP]** 标记。此时请等待 Copilot 完成工作，这可能需要几分钟。

4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 审查实现时，特别留意：
   - 用于切换模式的 UI 组件。
   - 用于保存用户偏好的本地存储。
   - 高对比度和浅色模式的 CSS 或样式更改。
   - 无障碍属性（ARIA 标签、键盘导航等）。
   - 管理模式切换的 JavaScript/TypeScript 代码。

6. 审查更新并确认符合预期后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有工作流正在等待审批的指示器。
8. 如果工作流正在等待审批，请选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)
9. 你应该会看到工作流在拉取请求的检查部分排队运行。如果一切正常，单体 Astro 应用程序的项目检查将通过。此过程可能需要几分钟。
10. **可选：**可以在 codespace 中切换到此分支，手动测试无障碍功能。转到 codespace，打开终端并运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名称）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    然后启动应用程序，在浏览器中测试高对比度和浅色模式切换开关，确认功能正常，并且在重新加载页面后仍会保留所选模式。

留意无障碍自定义智能体如何引导 Copilot 遵循无障碍最佳实践来实现这些功能。如果发现无障碍问题或可改进之处，可以像在前几个 PR 中那样，在评论中提及 **@copilot**，请求更新。

## 可选练习 — 继续委派任务

当你可以把真实待办事项交给云智能体并专注于其他工作时，云智能体最能发挥作用。若要培养这种习惯，可以向存储库提交更多议题并分配给 Copilot。以下是一些想法：

- 在游戏详情页创建支持者兴趣表单。
- 在游戏列表页实现分页。
- 为数据访问辅助函数添加输入验证和错误处理。

## 总结

你已完成云智能体练习路径。在这些课程中，你：

- **检查了本存储库自带的自定义指令文件**，以便之后观察它们对云智能体输出的影响。
- **将议题分配给 Copilot 云智能体**，并查看它如何设置环境、制定计划和异步执行任务。
- **创建并使用自定义智能体**来处理无障碍功能，添加高对比度和浅色模式切换开关。
- **使用 Copilot 智能体页面作为任务控制中心**，在无障碍会话进行期间监控并引导会话。
- **审查并迭代云智能体的拉取请求**，通过提及 `@copilot` 请求更改，并批准工作流。

## 审查和后续步骤

你已完成云智能体练习路径。如想继续探索，其他练习路径可补充本次所学内容：

- 🖥️ **[VS Code 练习路径](../../vscode/)** — 直接在 IDE 中探索 Copilot Chat 智能体模式和 MCP 集成。
- 💻 **[CLI 练习路径](../../cli/)** — 在终端中交付两项经过审查的更改，体验 Plan 和 Autopilot 模式、智能体技能、自定义 QA 智能体、Playwright MCP、Agent Merge，以及可选的 `/delegate` 云智能体桥接。

在自己的存储库中，可以尝试以下后续任务：

- 将重构或测试覆盖率议题分配给云智能体。
- 为其他领域创建自定义智能体。
- 为不同技术栈设置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot 智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot 云智能体防火墙][agent-firewall]

---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
