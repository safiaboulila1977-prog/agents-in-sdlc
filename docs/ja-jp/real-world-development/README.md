---
title: "実践的な開発"
slug: ja-jp/real-world-development
authors:
  - geektrainer
lastUpdated: 2026-09-16
---

現実的なシナリオ、完成したアプリケーション、共有バックログを使い、ソフトウェア開発ライフサイクル全体で GitHub Copilot を試します。変更の計画、コードの作成、動作のテスト、プルリクエストのレビュー、エージェントを使った作業の管理を繰り返しながら進めます。

## シナリオ

あなたは、開発者向けのテーマを使ったボードゲームのクラウドファンディングを提供する架空の会社、Tailspin Toys に加わったばかりの開発者です。チームのバックログは GitHub Issue として登録されており、作業を選べる状態です。アクセシビリティやコーディング標準などの品質改善に加え、フィルタリングやページネーションなどの機能も含まれます。

## 作業環境を選ぶ

GitHub Copilot は、使いたい環境に合わせて利用できます。開発方法に合った環境を選んでください。各ワークショップは独自のセットアップから始まり、共通の Tailspin Toys シナリオを使用します。

### [GitHub Copilot CLI][cli]

ターミナルでエージェント型アシスタントを使います。Plan モードと Autopilot モード、指示、スキル、カスタムエージェント、Playwright MCP、Agent Merge、実用的なスラッシュコマンドを試します。

### [GitHub Copilot app][app]

デスクトップアプリでエージェントの並列セッションを実行し、セッションモードを切り替え、Canvas で共同作業を行い、GitHub Issue とプルリクエストを管理します。

### [GitHub Copilot cloud agent][cloud]

GitHub Issue を非同期エージェントに割り当て、作業を案内して進捗を監視し、作成されたプルリクエストをレビューします。

### [Visual Studio Code][vscode]

Visual Studio Code と GitHub Codespaces で GitHub Copilot を使います。エディターを離れずに、Copilot Chat のエージェントモード、MCP サーバー、カスタムエージェントを試します。

[cli]: cli/
[app]: app/
[cloud]: cloud/
[vscode]: vscode/
