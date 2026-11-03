---
title: "レッスン 9 - GitHub Copilot CLI のスラッシュコマンド"
description: "コンテキストの管理、モデルの選択、セッションの共有、省略可能なクラウドへの委任に使うスラッシュコマンドを確認します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

ほかの優れた CLI ツールと同様に、GitHub Copilot CLI には対話に使える多くのスラッシュコマンドがあります。これらのコマンドでは、高度な機能、内部情報、追加の構成オプションを利用できます。これまでに `/diff`、`/mcp`、`/skills`、`/agent`、`/pr` などのコマンドを使いました。ほかの便利なコマンドも確認しましょう。

このレッスンでは、次の作業を行います。

- `/context` と `/compact` を使って Copilot が会話のコンテキストを管理する方法を確認します。
- `/model` を使って利用可能なモデルを確認します。
- `/share` でセッションをエクスポートまたは共有する方法を学びます。
- 並列作業、worktree、cloud agent への委任に使う省略可能なコマンドを確認します。

## シナリオ

CLI の主なワークフローを完了しました。ここでは、コンテキストの管理、モデルの切り替え、セッションの共有、省略可能な [Copilot cloud agent][about-cloud-agent] への委任など、追加機能を確認します。

## Copilot CLI のコンテキストを確認する

大規模または複雑なタスクでは、モデルのコンテキストウィンドウの上限に達する場合があります。Copilot CLI は必要に応じて会話を自動的に圧縮します。また、スラッシュコマンドを使って状態を確認したり、自分で圧縮したりできます。

1. Codespace に戻り、Copilot CLI が起動していない場合はリポジトリのルートから起動します。
2. 次のコマンドを入力します。

   ```plaintext
   /context
   ```

3. モデル、現在のトークン使用量、システム指示、ツール、メッセージ、空き領域にコンテキストがどのように分けられているか確認します。
4. 会話を圧縮します。

   ```plaintext
   /compact
   ```

5. もう一度 `/context` を入力して結果を比較します。会話が短い場合は、大きな違いが見られないことがあります。

> [!NOTE]
> Copilot CLI はコンテキストウィンドウが埋まると、自動的にコンテキストを圧縮します。自分でタイミングを選ぶ場合は `/compact` を使います。関係のない別のタスクに移るときに新しい会話を始めるには、`/clear` または `/new` を使います。

## モデルを選ぶ

モデルによって得意な作業は異なり、開発者ごとに好みも異なります。Copilot CLI では、モデルの一覧表示と選択ができます。

1. 次のコマンドを入力します。

   ```plaintext
   /model
   ```

2. 使用可能なモデルと使用状況に関する情報を確認します。
3. 現在のモデルを使い続けるか、別のモデルを選択するか、<kbd>Esc</kbd> を押して一覧を閉じます。

## セッションを共有する

チームで作業し、学んだことを共有すると、全員が AI ツールをより活用できるようになります。`/share` コマンドを使うと、セッションを Markdown または HTML ファイルにエクスポートしたり、共有リンクを作成したり、GitHub gist を公開したりできます。

1. `/help` を入力し、インストール済みのバージョンにおける `/share` のオプションを確認します。
2. セッションを共有する場合は、ニーズに合った出力先を選択します。たとえば `/share file` は、ローカルに Markdown をエクスポートします。
3. エクスポートした内容を誰かに送信したり公開したりする前に確認します。エクスポートにはプロンプト、応答、プロジェクトの詳細が含まれる場合があります。

リンクや gist の公開は省略可能です。チームが共有するつもりのないリポジトリや会話の内容は公開しないでください。

## 省略可能: 作業の拡張や委任

ワークショップの主な作業は完了しました。Copilot CLI には、より大きなタスクで使えるコマンドもあります。

- `/fleet` は、独立したサブタスクをサブエージェントに分けて、並列に実行できます。
- `/worktree` は、別のタスクのために分離された Git worktree を作成できます。
- `/delegate` は、Copilot cloud agent にタスクを送り、非同期に作業してプルリクエストを作成できます。

これらのコマンドは追加の worktree やリモート作業を作成する場合があるため、省略可能です。試すときは、範囲の明確な新しいタスクから始め、通常のワークフローで結果をレビューしてください。非同期エージェントの作業について詳しく知りたい場合は、[cloud agent ワークショップ][cloud-workshop]に進んでください。

## まとめと次のステップ

Copilot CLI のスラッシュコマンドを使うと、設定やセッションの共有ができ、内部で起きていることを確認できます。このレッスンでは、次の作業を行いました。

- `/context` と `/compact` を使って Copilot が会話のコンテキストを管理する方法を確認しました。
- `/model` を使って利用可能なモデルを確認しました。
- `/share` でセッションをエクスポートまたは共有する方法を学びました。
- 並列作業、worktree、cloud agent への委任に使う省略可能なコマンドを確認しました。

Copilot CLI にはほかにもスラッシュコマンドがあります。次は[ここまでに学んだことと今後の学習方法を振り返り][next-lesson]、ワークショップを締めくくりましょう。

## リソース

- [Copilot CLI コマンドリファレンス][cli-reference]
- [Copilot CLI のコンテキスト管理][context-management]
- [Copilot cloud agent について][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
