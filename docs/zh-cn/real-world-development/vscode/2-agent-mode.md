---
title: "练习 2 - 使用 Copilot 智能体模式添加功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是最简单的应用更新，通常也需要修改多个文件并执行一些操作，例如运行测试。作为开发者，你通常需要找到所有相关文件、进行修改、运行测试、调试、找出遗漏文件并再次更新……这样的工作似乎永无止境。

此时可以使用 Copilot 智能体模式。

Copilot 智能体模式可以更自主地在 IDE 中工作。它的行为类似开发者：先探索现有项目结构，进行必要更新，运行测试等任务，并自动修复发现的问题。现在来了解如何使用智能体模式为网站添加新功能。

> [!NOTE]
> 智能体模式和云智能体的名称相似，但适用于两种不同的体验。智能体模式在 IDE 中执行任务，可以快速反馈和交互。云智能体则像团队成员一样异步工作，通过议题和拉取请求与你协作。

在本练习中，你将了解以下内容：

- Copilot 智能体模式如何探索项目、查找相关文件并协调更改。
- GitHub Copilot 智能体模式如何跨 UI 和数据层实现新功能。
- 如何在将代码合并到代码库之前审查 Copilot 智能体模式生成的更改和测试。

## 场景

随着游戏列表不断增长，你希望让用户按类别和发行商筛选。上一练习已添加发行商辅助函数，现在将使用 Copilot 智能体模式完成其余的数据层、UI 和测试工作。

## 运行 Tailspin Toys 网站

进行更改之前，先探索 Tailspin Toys 网站，了解它当前的功能。

此网站是一个以开发者为主题的桌游众筹平台。用户可以浏览游戏列表和游戏详情页。它是一个单体 Astro 应用程序，在构建时将页面渲染为静态 HTML。页面通过 Drizzle ORM 在 frontmatter 中直接查询本地 SQLite 数据库，没有单独的后端 API 或客户端 UI 框架。可重复使用的数据访问辅助函数放在 `src/lib/` 中；交互功能使用少量范围明确的 Astro `<script>` 和标准 DOM API 实现。

### 启动网站

项目提供了 `npm run dev` 任务，用于启动单体 Astro 开发服务器。可以按照以下步骤在 GitHub Codespace 中运行：

1. 返回 codespace。上一练习结束后，你应该已切回 `main`。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux），在 Codespace 中打开新终端窗口。
3. 创建并切换到筛选工作的新分支：

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 运行以下命令启动网站：

   ```bash
   npm run dev
   ```

   Astro 开发服务器就绪后，会显示类似以下内容的横幅，其中包含 URL：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> 如果弹出对话框，询问是否要打开 `http://localhost:4321` 的浏览器窗口，请选择 **x** 将其关闭。

5. 在终端中按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），然后选择 Astro 服务器地址 `http://localhost:4321`，打开网站。

> [!NOTE]
> 使用 codespace 时，在 Codespace 终端中选择 localhost URL 链接会自动将你重定向到 `https://<your-codespace-name>-4321.app.github.dev/`。这是指向 codespace 的专用隧道，网站服务器正在其中运行！

### 探索网站

网站运行后，可以探索它的功能。网站主要包含以下功能：

- **主页**：显示桌游列表，包括标题、图片和描述。
- **游戏详情页**：选择游戏后会打开详情页，其中包含标题、描述、发行商和类别等信息。

## 使用 Copilot 探索待办列表

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 codespace，打开 Copilot Chat 面板，然后选择 **New Chat** 开始干净的对话。模式和模型选择因练习而异；每个相关步骤都会说明具体选择。

网站初始版本可以正常运行，但我们希望添加新功能来改进它。先查看待办列表。使用模板设置项目时，系统已自动创建议题待办列表。现在请 GitHub Copilot 显示这些项目。

1. 在 Chat 视图的智能体下拉列表中选择 **Agent**。**Agent** 智能体会自主规划并跨文件实现更改、运行终端命令和调用工具。

   ![显示 Chat 视图中智能体选择器的屏幕截图。](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本研讨会作者并未偏好某种模型。构建本研讨会时，我们使用了 Claude Sonnet 4.5，因此将它写入了说明，希望让你获得较一致的体验。不过，大型语言模型具有概率性，因此建议可能与研讨会中的描述不同。这完全正常。

> [!NOTE]
> 由于大型语言模型具有概率性，Copilot 可能会使用不同的 MCP 命令，但仍应能够完成任务。

3. 向 Copilot 发送以下提示，询问议题待办列表：

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. 选择 **Continue** 以运行列出所有议题的命令。
5. 查看生成的议题列表。

请注意，Copilot 甚至根据它认为对用户最有用的内容，帮你排定了议题优先级。

## 查看指令文件

在启动智能体生成代码之前，先查看将用于向 Copilot 提供上下文的指令文件。这里将使用 [UI 指令文件](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)，其中介绍了如何为网站添加功能。

1. 在 codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 留意其中提供的整体功能开发指导，包括：
   - 架构概述。
   - 组件设计、可测试性和无障碍原则。
   - 指向各类文件专用指令的链接，包括：
     - Astro
     - Tailwind CSS
     - Drizzle

> [!TIP]
> 指令文件可以引用其他指令文件和项目中的文件。这些路径相对于指令文件所在位置。这样可以重复使用指导、拆分复杂指令，并提供示例和模板。

## 实现筛选功能

完成筛选功能至少需要对应用程序进行三项独立更新：

- 添加或完善数据层 (`src/lib/`) 中剩余的筛选逻辑。
- 添加或更新筛选行为的测试。
- 更新游戏列表页面，加入筛选 UI。

此外，在将所有内容合并到代码库之前，测试必须运行并通过。Copilot 智能体模式可以帮你完成这些任务！现在添加功能。

1. 可以继续当前的 Copilot 对话，也可以选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions** 和 **ui** 指令文件。

   ![选择 UI 指令文件的示例屏幕截图](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图的智能体下拉列表中仍选中 **Agent**。

   ![显示 Chat 视图中智能体选择器的屏幕截图。](../../../_images/shared-chat-mode-selector.png)

4. 确认模型仍为 **Claude Sonnet 4.5**。
5. 使用以下提示，请 Copilot 根据待办列表中的相关议题实现功能：

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. 观察 Copilot 如何先探索项目并查找相关文件。你应该会看到它查找数据层辅助函数、UI 和测试，然后修改文件并运行测试。

   ![Copilot 探索项目文件的屏幕截图](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会执行多个任务，例如探索项目、修改文件和运行测试。根据任务和代码库的复杂程度，这可能需要几分钟。在此过程中，代码编辑器中可能会显示 **Keep** 和 **Undo** 按钮。Copilot 完成后，所有更改都会有 **Keep** 或 **Undo** 按钮，因此无需在工作进行期间选择它们。

7. 按 Copilot 提示选择 **Continue** 运行测试。

   ![Copilot Chat 面板中的对话框截图，提示用户确认是否运行测试](../../../_images/ex3-agent-mode-run-tests.png)

8. 工作过程中可能会有几次暂停，甚至会看到测试失败。这没有关系！Copilot 会在代码生成和测试之间不断迭代，直到完成任务且未检测到错误。

   ![完整 Copilot 智能体模式聊天会话的屏幕截图](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 检查生成的代码，查找潜在问题。

> [!CAUTION]
> 请记住，始终需要审查 Copilot 或其他 AI 工具生成的代码。

10. 返回运行网站的浏览器，探索新功能！
11. 确认一切正常并完成代码审查后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结和后续步骤

恭喜！在本练习中，你了解了如何使用 GitHub Copilot 智能体模式为 Tailspin Toys 网站添加新功能。你学习了以下内容：

- GitHub Copilot 智能体模式如何跨 UI 和数据层实现新功能。
- Copilot 智能体模式如何探索项目、查找相关文件并协调更改。
- 如何在将代码合并到代码库之前审查 Copilot 智能体模式生成的更改和测试。

接下来，[使用 Playwright MCP 服务器测试功能][next-lesson]并创建拉取请求。

### 额外探索练习 — 实现分页

随着游戏列表不断增长，需要添加分页。运用本练习中学到的技能，请 Copilot 更新网站以实现分页。编写代码时可考虑以下因素：

- 遵循现有最佳实践，包括使用已有指令文件。
- 考虑分页方式：允许用户选择每页大小，还是使用固定值。
- 编写提示时，提供必要指导，让 Copilot 按照你的设想实现功能。
- 你可能需要与 GitHub Copilot 迭代协作，要求更改并提供上下文。这是正常的协作流程！

## 资源

- [Copilot ask、edit 和 agent 模式：功能和适用场景][choose-mode]
- [VS Code 中的智能体模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
