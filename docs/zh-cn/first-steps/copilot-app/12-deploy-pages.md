---
title: "第 12 课 - 使用 GitHub Pages 部署网站"
description: "使用 GitHub Copilot 应用配置 Pages 工作流、评审拉取请求，并验证太空问答游戏已上线。"
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

使用 GitHub Pages 部署太空问答游戏，让所有人都能访问。Copilot 可以准备工作流并引导部署，但你仍需负责评审更改并确认网站已上线。

在本课中，你将：

- 请 Copilot 配置 GitHub Pages 部署。
- 在合并前评审工作流和拉取请求。
- 跟进部署并验证已发布的网站。

## 场景

太空问答游戏已存储在 GitHub 仓库中，但其他人还无法轻松试玩。使用 GitHub Pages 发布这个单文件网站，无需添加服务器或运行时依赖，即可通过公共 URL 访问。

## 请 Copilot 准备部署

> [!WARNING]
> 创建拉取请求可能会提交并推送代码。发送此提示前，请检查审批设置和目标仓库。如果选择 **Approve all**，不要预期还会出现单独的确认提示。

在 Copilot 应用中打开 `space-quiz` 会话，并发送以下提示：

```plaintext
Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
```

## 评审工作流和拉取请求

1. 确认只有在仓库中尚无 README 时才添加 README。
2. 评审拉取请求中的更改，包括工作流的构建和部署步骤、触发条件及权限。
3. 确认工作流从默认分支部署，而不是从尚未合并的拉取请求部署。
4. 要求修正任何问题，并评审更新后的差异。授权合并前，等待所需的拉取请求检查通过。

## 授权合并和部署

> [!WARNING]
> 以下提示授权代理合并已评审的拉取请求、更改仓库 Pages 设置并发布网站。只有完成评审并确认仓库和拉取请求后，才发送此提示。根据审批设置，这些操作可能无需再次确认即可执行。

将 `<PR_NUMBER>` 替换为已评审的拉取请求编号，然后单独发送以下提示：

```plaintext
I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![三阶段示意图：已合并的 space-quiz 拉取请求；包含 Build website、Upload artifact 和 Deploy to Pages 步骤且运行成功的 GitHub Actions Deploy website 工作流；以及位于 yourname.github.io/space-quiz/ 的在线太空问答游戏。](../../../_images/first-steps-app-pages-deploy.svg)

## 验证部署

1. 跟进 GitHub Actions 部署工作流，直到运行成功。
2. 打开报告中的 URL，确认太空问答游戏已加载。

如果代理无法启用 Pages 或合并拉取请求，请按照它提供的具体说明操作。只有部署成功且网站可以访问后，才算完成任务。

## 总结和后续步骤

太空问答游戏现已作为在线网站发布，你也亲自验证了部署，而不是只依赖代理的报告。继续学习[第 13 课：评审和后续步骤][next-lesson]。

[next-lesson]: ../13-review/
