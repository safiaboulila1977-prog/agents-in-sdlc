---
title: "レッスン 10 - まとめと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプルリクエスト、再利用可能なカスタマイズ、追加リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Tailspin Toys の一連のワークフローで GitHub Copilot CLI を使いました。次の作業を行いました。

- Codespace を準備し、Copilot CLI をインストールして、プロジェクトを確認し、シードされたフィルタリング Issue を見つけました。
- 星評価を追加し、転送されたブラウザーで結果を確認して、最初のプルリクエスト (PR) を手動でマージしました。
- フィルタリング Issue から開始し、Plan モードでアプローチを定義し、Autopilot モードで構築して、Interactive モードでレビューしました。
- カスタム指示でエージェントを案内し、既存の `quality-checks` スキルをカスタマイズして、ユニットテスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルタリング機能を確認しました。
- 品質保証 (QA) カスタムエージェントを作成して選択し、要件、カバレッジ、スキルの結果、ブラウザーによる検証の証拠を評価しました。
- フィルタリングの変更全体をレビューし、フィルタリング PR の Agent Merge を許可しました。
- コンテキスト、モデル、共有、省略可能なクラウドへの委任に使うスラッシュコマンドを確認しました。

## 提出した成果

このワークショップには 2 つの PR の節目があり、それぞれ更新済みの `main` から作成した別々のブランチで作業しました。

1. **星評価:** ゲームカードに既存の `starRating` と、評価がない場合の状態を明示して表示します。
2. **フィルタリングと品質ワークフロー:** フィルタリングを実装し、指示を更新して機能に適用し、`quality-checks` の報告形式をカスタマイズし、QA プロファイルを作成して、関連テストを追加します。

フィルタリングの計画から PR の作成まで、同じ会話とブランチを使いました。ワークショップを効率よく進めるため、この作業を 1 つの PR にまとめました。

## 複数の方法で検証する

自動テスト、自分でのブラウザー確認、MCP を通じた Copilot のブラウザー操作など、複数の方法でコードを確認しました。`quality-checks` スキルではユニットテスト、lint、型チェックを実行し、新しい形式で報告しました。QA はこれらの結果を、要件とテストカバレッジのレビューにまとめてから PR を作成しました。

追加するテストは、実際に不足しているカバレッジを補うものである必要があります。QA の実行で追加テストが不要と判断される場合もあります。マージを許可する前に、コードと検証の証拠を確認し、変更後は影響する証拠を更新してください。

## ベストプラクティス

Copilot に与えるコンテキストとツールが、作業の結果に影響します。このワークショップでは、指示を更新し、スキルをカスタマイズし、QA プロファイルを作成して、MCP サーバーを設定しました。これらのカスタマイズは会話をまたいで再利用し、チームのニーズの変化に合わせて調整できます。指示は標準を設定し、スキルは繰り返し実行できるタスクを記述し、カスタムエージェントは専門家の役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認してください。

タスクに合わせて**モードとモデル**を選びます。実装前にアプローチを考えるには **Plan**、対象を絞った変更で対話を続けるには **Interactive**、範囲が明確なタスクには **Autopilot** を使います。定型的な編集には高速なモデルを、複雑な作業にはより高性能なモデルを選択します。

インフラストラクチャと同じくらい、コンテキストも重要です。何を、なぜ、どのように構築するのかを明確に伝えると、出力が大きく変わります。

## さらに確認する

主なワークフローを学びました。Copilot CLI の機能をさらに確認してみましょう。

- `/review` を使って、コードレビューエージェントに変更を分析してもらいます。
- `/rubber-duck` を使って問題について相談し、別の視点を得ます。
- `/fleet` を使って、独立したサブタスクを並列に調整します。
- `/worktree` を使って、別のタスクを分離します。
- `/delegate` を使って、Copilot cloud agent にタスクを送信します。

## 次のステップ

どのツールでも、上達するには使い続けるのが一番です。本番コード、趣味のコード、何年も作りたいと思っていた小さなアプリなどで活用してください。チームと学んだことを共有し、互いの経験から学びましょう。ドキュメントも引き続き確認してください。

ターミナルから Tailspin Toys を拡張する場合は、省略可能な [Foundry Backer Concierge シリーズ][foundry]に進んでください。別の環境と比較するには、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、または [Copilot cloud agent ワークショップ][cloud]を確認してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンドリファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプルリクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
