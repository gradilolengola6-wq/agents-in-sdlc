---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

技術的負債に悩む組織は少なくありません。未解決のセキュリティ問題、更新が必要なレガシーコード、実装する時間がなくバックログに残った機能リクエストなど、さまざまな問題があります。GitHub Copilot cloud agent は、コードの更新や機能の追加などを自律的に実行できます。作業が完了すると、人間の開発者がレビューできるドラフト PR を作成します。これにより、手間のかかる作業を任せて開発を加速し、開発者はより大きな課題に集中できます。

Copilot cloud agent を使って、次の内容を学びます。

- コード生成環境をカスタマイズする方法
- 操作を安全に行う方法
- issue の範囲を明確に定めることの重要性
- Copilot に issue を割り当てる方法

## シナリオ

Tailspin Toys では、解決したい技術的負債があります。サイトの最初のバージョンを開発した委託先は、ドキュメントを適切に整備していませんでした。実際、ドキュメントはほとんどありません。まず、アプリケーションのすべてのエクスポートされた関数に TSDoc のドキュメントコメントを追加します。

また、デザインチームはゲームを見つけやすくしたいと考えています。各ゲームの詳細ページに、同じカテゴリの他のゲームを表示して、閲覧を続けられるようにします。現時点では、洗練された実装は必要ありません。UX の受け入れテストに使える状態にすることが目的です。この作業はブロッカーですが、さらに優先度の高い issue もあります。

このように、優先度が下がりやすい作業は Copilot cloud agent に任せるのに適しています。Copilot cloud agent が非同期で作業している間、開発者は別の作業に取り組めます。その後、戻って成果をレビューし、要件を満たしていることを確認できます。

## GitHub Copilot cloud agent の概要

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、人間の開発者と同じようにバックグラウンドで作業できます。たとえば、[GitHub issue を Copilot に割り当てる](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)方法があります。割り当てると、Copilot は進行状況を追跡するドラフトプルリクエストを作成し、環境をセットアップして作業を開始します。作業中でも完了後でも、Copilot のセッションを確認できます。提案された解決策のレビュー準備ができると、プルリクエストで通知されます。

## 範囲を明確にした指示の重要性

GitHub Copilot に魔法のような力はありません。考える作業を省略できるわけではありません。一見簡単そうな作業でも、詳しく調べると複雑な場合があります。[Copilot cloud agent に依頼する作業の範囲][cloud-agent-best-practices]を慎重に決めてください。AI ペアプログラマーとして扱い、段階を踏んで学び、試し、適応させます。生成 AI を加えても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

前の演習では、カスタム指示とその役割を確認しました。カスタム指示を実際に使う演習をすでに完了している場合は、`.github/copilot-instructions.md` が機能することを確認できています。まだの場合は、内容を簡単に確認しておきましょう。Copilot cloud agent に作業を割り当てる前に、このリポジトリに含まれる指示ファイルを読み取り専用で確認すると、後でその影響を判断しやすくなります。

リポジトリの GitHub Web UI、または起動済みの Codespace で、次のファイルを開きます。

- `.github/copilot-instructions.md` — **Code standards** セクション、特に TypeScript の規約と TSDoc のドキュメントコメントに関する要件を確認します。
- `.github/instructions/unit-tests.instructions.md` — `applyTo` フロントマターで、`**/*.test.ts` ファイルに指示が適用されることを確認します。

次のセクションで `Code lacks documentation` issue を cloud agent に割り当てたら、作成されたプルリクエストで TSDoc コメント、TypeScript の規約、ファイルヘッダーコメントを確認します。これらの内容は指示ファイルに基づいています。後の演習で PR をレビューするときにも取り上げます。

## Copilot cloud agent の開発環境をセットアップする

誰が作業する場合でも、コードを作成するには通常、特定の環境やセットアップスクリプトが必要です。タスクを Copilot に割り当てる場合も同様です。Copilot はソフトウェアエンジニアと同じように作業します。

Cloud agent は [GitHub Actions][github-actions] を使って作業環境を用意します。作業開始前に実行する[専用のセットアップワークフロー][setup-workflow]を `.github/workflows/copilot-setup-steps.yml` に作成して、環境をカスタマイズできます。これにより、必要な開発ツールや依存関係を利用できるようになります。このラボでは、Node.js、プロジェクトの依存関係、エンドツーエンドテスト用のブラウザーバイナリ、単一の Astro アプリ用にマイグレーションとシードを実行した SQLite データベースを Copilot が使えるよう、あらかじめ設定しています。

```yaml
name: "Copilot Setup Steps"

# Allows you to test the setup steps from your repository's "Actions" tab
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Set the permissions to the lowest permissions possible needed for *your steps*. Copilot will be given its own token for its operations.
    permissions:
      # If you want to clone the repository as part of your setup steps, for example to install dependencies, you'll need the `contents: read` permission. If you don't clone the repository in your setup steps, Copilot will do this for you automatically after the steps complete.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Frontend / app setup - Node.js (the whole app is now Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migrate + seed the local SQLite database so builds and tests have data.
      - name: Set up the database
        run: npm run db:setup
```

一般的な GitHub ワークフローと同じですが、次の点を確認してください。

- `copilot-setup-steps` という 1 つのジョブがあります。このジョブは、Copilot がプルリクエストに取り組む前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーを使うと、リポジトリの **Actions** タブからワークフローを手動で実行できます。Copilot が実行するのを待たずに、ワークフローが正常に動くかテストできます。

## ドキュメントを追加する

ドキュメントの重要性は広く認識されていますが、多くのプロジェクトには古い情報しかなかったり、ドキュメント自体がなかったりします。このような技術的負債は放置されやすく、生産性を下げ、コードベースの保守や新しい開発者の参加を難しくします。Copilot はドキュメントの作成を得意としているため、この作業を Copilot cloud agent に割り当てるのに適しています。バックグラウンドでドキュメントを作成してもらい、後の演習で成果をレビューします。

1. 新しいブラウザータブで github.com のリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次の内容を入力します。

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して、割り当てダイアログを開きます。

  ![Copilot を issue に割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

  ![Copilot の割り当て詳細](../../../_images/ex4-assign-copilot-details.png)

10. **Pull Requests** タブを選択します。
11. 新しく作成されたプルリクエスト (PR) を開きます。タイトルは `[WIP]: Code lacks documentation` のようなものです。PR が表示されない場合は、少し待ってからブラウザーを更新してください。
12. 数分後、Copilot が ToDo リストを作成したことを確認できます。

> [!NOTE]
> Copilot が PR に ToDo リストを作成するまで数分かかる場合があります。Copilot は、前に説明したワークフローを実行して環境を作り、プロジェクトを分析し、問題に取り組む方法を決めています。

13. リストと、これから実行するタスクを確認します。
14. プルリクエストのタイムラインを下にスクロールし、Copilot が issue の作業を開始したことを示す更新を確認します。
15. **View session** ボタンを選択します。

  ![Copilot セッションの表示](../../../_images/ex4-view-session.png)

> [!CAUTION]
> インジケーターの更新を確認するために、ブラウザーを更新する必要がある場合があります。

16. ライブセッションをスクロールして、Copilot の作業を確認します。コードを調べて状態を把握し、計画を考えて決め、コードを作成する様子を確認できます。

完了まで数分かかる場合があります。Copilot cloud agent の主な目的の 1 つは、非同期で作業して、別の作業に取り組めるようにすることです。この機能を活用して、もう 1 つのタスクを cloud agent に割り当ててから、アプリケーションに機能を追加するコードの作成に取り組みます。

## ゲーム詳細ページに関連ゲームのセクションを追加する

GitHub Copilot cloud agent の大きな利点の 1 つは、作業を分担できることです。デザインチーム向けに関連ゲームのセクションを追加するのに時間がかからないとしても、その時間を別の作業に使えます。この作業も Copilot cloud agent に割り当てましょう。

1. github.com でリポジトリを開き直します。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次の内容を入力します。

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して、割り当てダイアログを開きます。

  ![Copilot を issue に割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

まもなく、Copilot が作業を始めたことを示す 👀 が issue の最初のコメントに表示されます。

![Copilot が issue に取り組んでいることを示す目の絵文字](../../../_images/ex4-issue-eyes-emoji.png)

Copilot は 2 つ目の依頼に取り組んでいます。Copilot cloud agent はソフトウェアエンジニアと同様に作業するため、完了まで積極的に監視する必要はありません。完了後にレビューすればよいでしょう。次は、カスタムエージェントの作成と使用を確認します。

## まとめと次のステップ

このレッスンでは [GitHub Copilot cloud agent][copilot-agents] を確認しました。cloud agent に issue を割り当てると、非同期で作業を依頼できます。技術的負債の解消、新機能の作成、別のフレームワークへのコード移行などに活用できます。

このレッスンでは、次の内容を学びました。

- コード生成環境をカスタマイズする方法
- 操作を安全に行う方法
- issue の範囲を明確に定めることの重要性
- Copilot に issue を割り当てる方法

Cloud agent がバックグラウンドで作業している間に、次はカスタムエージェントの作成と使用を確認します。[Copilot cloud agent は MCP サーバーも使用できます][cloud-agent-mcp]。また、前のモジュールで確認したカスタム指示も利用できます。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップワークフローのベストプラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタムエージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
