---
title: "练习 4 - 监控和管理代理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

在前几节练习中，你要求 Copilot 云代理处理了三个不同任务，以改进用户体验并添加功能。云代理虽然能够异步自主工作，但监控这些任务仍然很重要。

你可以使用多种工具管理分配给云代理的任务，包括 GitHub.com 上的[代理页面][agents-page]。在这个控制台中，你可以查看所有具有未关闭拉取请求 (PR) 的代理任务、检查已执行的操作，还可以引导正在进行的会话。

在本课中，你将：

- 浏览代理页面，监控云代理任务。
- 引导正在进行的会话，请求添加其他功能。

## 场景

将任务分配给代理以创建高对比度模式后，团队意识到也可以趁此机会添加浅色模式。由于代理已经在更新网站样式并添加切换功能，因此将这项功能一并纳入很合理。你将引导代理，确保它同时添加浅色和高对比度模式。

## 查看 Copilot 云代理任务

查看目前分配给 Copilot 云代理的所有任务的状态。

1. 打开 [Copilot 代理页面](https://github.com/copilot/agents)。
2. 查看主面板和左侧面板中的任务列表。你应能看到分配给 Copilot 的任务，包括：
    - 更新代码文档。
    - 生成用于修改游戏的 API。
    - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，查看 Copilot 已执行的工作，例如：
    - 从仓库检出代码。
    - 为 Copilot 创建工作环境。
    - 设置 MCP 服务器。
    - 执行完成分配任务所需的各种步骤。

> [!NOTE]
> 具体显示的步骤因 Copilot 当前的工作状态和执行方式而异。

4. 同时留意右侧显示的拉取请求 (PR) 面板。你可以在此查看 PR 和已更改的文件，以便进一步监控。

## 引导云代理

了解当前正在执行的任务后，我们来请求 Copilot 在实现高对比度模式的同时添加浅色模式。

1. 选择与添加高对比度模式相关的会话。具体标题取决于 Copilot 使用的名称和当前工作状态。

    ![代理控制台中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到 Copilot 完成设置并开始工作。此时，你会看到类似以下内容的消息。
3. 在 **Steer active session while Copilot is working** 对话框中，输入以下提示：

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![代理页面中突出显示 Steer active session while Copilot is working 对话框的云代理任务截图](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示。
5. 观察 Copilot 如何确认提示并将其纳入工作流程。

## 等待 Copilot 完成工作

与之前一样，Copilot 会开始处理更新后的任务。发送消息时，它会先完成当前步骤，然后将新要求加入工作流程。

这也需要几分钟。你可以利用这段时间回顾迄今为止学到和探索的内容。

## 总结和后续步骤

本课介绍了 Copilot 代理页面，这是监控和引导 GitHub Copilot 云代理任务的中心位置。在此控制台中，你可以跟踪所有正在进行和已完成的任务、评审执行中的工作，还可以调整正在进行的任务范围或提供进一步指导。

你了解了以下内容：

- 使用控制台和代理页面监控云代理任务。
- 引导正在进行的会话，请求添加其他功能。

Copilot 正在完成无障碍功能。接下来，我们将[迭代优化 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 代理页面][agents-page]
- [关于自定义代理][custom-agents]

---

| [← 上一课：自定义代理][previous-lesson] | [下一课：迭代优化 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
