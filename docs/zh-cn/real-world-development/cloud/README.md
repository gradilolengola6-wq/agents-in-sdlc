---
slug: zh-cn/real-world-development/cloud
title: "GitHub Copilot 云代理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[GitHub Copilot 云代理](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)可在云端异步处理工作。你在 GitHub 上分配任务后，云代理会在后台接手工作：探索仓库、进行更改并创建拉取请求，你则可以继续处理其他事务。

在这些练习中，你将添加云代理需要遵循的自定义指令，然后分配一个 GitHub issue，让它实现相应工作。你还将评审并使用自定义代理来指导其工作方式，通过代理仪表板监控和引导会话，最后评审它创建的拉取请求并迭代优化结果。

## 练习

| 练习 | 主题 | 说明 |
|----------|-------|-------------|
| [0. 先决条件][ex0] | 设置 | 创建仓库和 codespace |
| [1. 自定义指令][ex1] | 上下文 | 添加云代理将遵循的自定义指令 |
| [2. 云代理][ex2] | 异步代理 | 将 issue 分配给 Copilot 云代理 |
| [3. 自定义代理][ex3] | 专用代理 | 评审并使用自定义代理 |
| [4. 管理代理][ex4] | 监控 | 监控和引导代理会话 |
| [5. 迭代优化][ex5] | 评审 | 评审 PR、迭代改进 Copilot 的工作并选择后续步骤 |

## 先决条件

参加此工作坊前，请确保具备以下条件：

- [ ] 拥有有效的 **Copilot Student、Pro、Pro+、Business 或 Enterprise** 计划的 GitHub 帐户
- [ ] 已为你的帐户或组织启用 Copilot 云代理

> [!TIP]
> 没有付费计划？经过验证的学生可以通过 [GitHub Education][callout-student-plan-education] 免费使用 GitHub Copilot。**Copilot Student** 计划包含本工作坊使用的代理、MCP、代码评审和 Copilot CLI 功能，因此可用它完成所有练习。

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> Copilot Student、Pro、Pro+、Business 和 Enterprise 均提供云代理；只有 Copilot Free 计划不提供此功能。对于 Copilot Business 或 Enterprise，管理员必须为组织启用此功能。

> [!NOTE]
> 本练习不涉及 MCP。若要了解如何将 MCP 服务器与 Copilot 配合使用，请参阅 [CLI 练习][cli]或 [VS Code 练习][vscode]。

## 开始

**[从练习 0：先决条件开始 →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
[cli]: ../cli/
[vscode]: ../vscode/
