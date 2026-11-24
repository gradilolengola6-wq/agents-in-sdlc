---
title: "レッスン 8 - 機能 PR の作成とマージ"
description: "フィルタリング、指示、スキルの更新、QA プロファイル、テストをまとめてレビューし、PR を作成して Agent Merge を使います。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

フィルタリング機能、指示の更新、スキルの更新、品質保証 (QA) プロファイル、テストは、すべて 1 つのブランチに保存されています。まとめてレビューして、プルリクエストを開きましょう。星評価のプルリクエスト (PR) は手動でマージしましたが、今回は **Agent Merge** にマージの作業を任せます。

> [!NOTE]
> 通常は、機能、指示の更新、スキルの更新、QA エージェントを複数の PR に分けます。このワークショップでは作業を簡略化するため、フィルタリングと品質確認の一連の作業を 1 つの会話とブランチで進め、1 つの PR にまとめています。

このレッスンでは、次の内容を学びます。

- Agent Merge とは何か、マージまでの作業をどのように自動化するかを学びます。
- 機能全体の変更と検証の根拠を確認します。
- フィルタリング機能の PR を作成します。
- レビュー後にのみ Agent Merge を有効にし、PR がマージされたことを確認します。

## シナリオ

フィルタリングのワークフローを通じて、Copilot を使って機能を計画、実装、検証しました。次は、Tailspin Toys で PR に関する残りの作業を自動化します。ただし、マージを許可するかどうかは開発者が判断します。

## Agent Merge の概要

**Agent Merge** は、プルリクエストをマージするまでに必要な残りの作業を自動化します。有効にすると、Copilot は PR をブロックしている問題を解決します。たとえば、失敗した継続的インテグレーション (CI) のチェックやレビューコメントに対応し、必要に応じてリベースします。その後、リポジトリで許可されていれば、GitHub の自動マージを有効にします。

ここまでは自分で **Merge pull request** を選択していました。Agent Merge にその作業を任せることもできます。有効にする前に作業をレビューし、マージしてよい状態か判断してください。

## Agent Merge で PR を管理する

コードを作成したので、すべてまとめてレビューして PR を作成し、Agent Merge に残りの作業を任せましょう。

1. Codespace に戻ります。
2. `/agent` を入力してエージェントのダイアログを開きます。
3. 一覧から **Default** を選択し、<kbd>Enter</kbd> を押します。
4. `/pr create` コマンドを使って新しい PR を作成します。
5. `/pr agentmerge` を使って Agent Merge を有効にします。
6. Copilot が PR の継続的インテグレーションを監視します。すべてのチェックに成功すると、マージが実行されます。
7. Copilot から `PR #14 was squash-merged successfully.` のようなメッセージが表示されたことを確認します。

> [!IMPORTANT]
> Agent Merge は、必須の承認、ブランチ保護、マージキュー、リポジトリ設定、権限の不足を回避しません。処理がブロックされた場合は、報告された理由を確認し、リポジトリで許可される手順に沿ってレビュー済みのマージを手動で完了してください。

## まとめと次のステップ

コードの生成、テストと検証、プルリクエストの処理など、開発プロセスの一部を自動化しました。このレッスンでは、次のことを行いました。

- Agent Merge とは何か、マージまでの作業をどのように自動化するかを学びました。
- 機能全体の変更と検証の根拠を確認しました。
- フィルタリング機能の PR を作成しました。
- レビュー後に Agent Merge を有効にし、PR がマージされたことを確認しました。

次は、コンテキスト、モデル、セッション共有、省略可能なクラウドへの委任に使える[他の Copilot CLI スラッシュコマンドを確認します][next-lesson]。

## リソース

- [Copilot CLI でプルリクエストを管理する][manage-prs]
- [Copilot CLI コマンドリファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
