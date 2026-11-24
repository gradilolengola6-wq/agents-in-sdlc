---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前の 2 つの演習では、ユーザーエクスペリエンスの改善と機能追加を目的とする 3 つのタスクを Copilot cloud agent に依頼しました。cloud agent は非同期かつ自律的に作業しますが、進行中のタスクを監視することも重要です。

GitHub の[エージェントページ][agents-page]など、cloud agent に割り当てたタスクを管理するためのツールがいくつもあります。この mission control では、オープンなプルリクエスト (PR) があるすべてのエージェントタスクを確認できます。実行された操作を調べたり、進行中のセッションに指示を追加したりできます。

このレッスンでは、次の内容を学びます。

- エージェントページで cloud agent のタスクを監視する方法
- 進行中のセッションに指示を出し、機能を追加で依頼する方法

## シナリオ

エージェントにハイコントラストモードを作成するよう依頼した後、チームはライトモードも追加したいと考えました。サイトのスタイルと切り替え機能をすでに更新しているため、ライトモードも実装するのが適切です。ハイコントラストモードに加えてライトモードも追加されるよう、エージェントの作業に指示を出します。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたタスクの現在の状態を確認しましょう。

1. [Copilot agents ページ](https://github.com/copilot/agents)を開きます。
2. メインペインと左ペインの両方に表示されるタスクの一覧を確認します。次のような、Copilot に割り当てたタスクが表示されます。
    - コードベースのドキュメントを更新する
    - ゲームを変更する API を生成する
    - Web サイトにハイコントラストモードを追加する
3. 実行中のタスクを選択し、Copilot が実行した作業を確認します。次のような操作が含まれる場合があります。
    - リポジトリのチェックアウト
    - Copilot が作業する環境の作成
    - MCP サーバーのセットアップ
    - 割り当てられたタスクを完了するための各種操作

> [!NOTE]
> 表示される手順は、Copilot の作業状況や採用した方法によって異なります。

4. 右側に表示されるプルリクエスト (PR) ペインも確認します。ここから PR と変更されたファイルを確認し、進行状況を監視できます。

## cloud agent に指示を出す

実行中のタスクを確認できたので、cloud agent がハイコントラストモードを作成している間に、ライトモードの切り替え機能も追加するよう依頼します。

1. ハイコントラストモードの作成を示すセッションを選択します。Copilot が付けたタイトルや作業状況によって、具体的な表示は異なります。

    ![mission control に表示されるアクセシビリティセッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了し、作業を開始したことが表示されるまで数分待ちます。次のようなメッセージが表示されたら、作業が始まっています。
3. **Steer active session while Copilot is working** ダイアログに、次のプロンプトを入力します。

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Copilot agents ページで、作業中のセッションに指示を出すダイアログが強調表示されています](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot がプロンプトを認識し、作業計画に追加することを確認します。

## Copilot の作業を待つ

前と同じように、Copilot は更新されたタスクに取り組みます。メッセージを送信した時点で実行していた手順が終わると、新しい依頼が作業に反映されます。

完了まで数分かかります。その間に、これまでに学んだことを振り返りましょう。

## まとめと次のステップ

このレッスンでは、GitHub Copilot cloud agent のタスクを監視して案内するための中心的な場所である Copilot agents ページを確認しました。この mission control では、進行中や完了済みのタスクを追跡し、実行中の作業を確認できます。また、作業中のタスクの範囲を変更したり、追加のガイダンスを伝えたりできます。

このレッスンでは、次の内容を学びました。

- mission control とエージェントページで cloud agent のタスクを監視する方法
- 進行中のセッションに指示を出して、機能を追加で依頼する方法

Copilot がアクセシビリティ機能を実装している間に、次は Copilot が作成した[プルリクエストを改善する方法][next-lesson]を確認します。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタムエージェントについて][custom-agents]

---

| [← 前のレッスン: カスタムエージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
