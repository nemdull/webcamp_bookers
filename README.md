# Bookers (Rails 5)

学習用のシンプルな Ruby on Rails アプリケーションです。書籍の「タイトル」と「感想（本文）」を投稿・閲覧・編集・削除でき、トップページから一覧・投稿画面へ遷移します。

## 技術スタック

- 言語: Ruby 2.6.3
- フレームワーク: Rails 5.2.6 (ERBテンプレート)
- データベース: SQLite3（開発・テスト）
- アプリサーバ: Puma
- JavaScript: Turbolinks, CoffeeScript（設定あり）
- JSON: Jbuilder（導入済み・未使用）
- テスト: RSpec, Capybara, FactoryBot, Faker
- 開発支援: Spring, Web Console, Listen, Bootsnap
- CI/CD: 現状なし（`.github/workflows` 未配置）

根拠となる主なファイル: `Gemfile`, `config/database.yml`, `app/**`, `spec/**`, `package.json`（依存空）

## 主な機能

- BookのCRUD（`title`, `body`）
- バリデーション: `title`, `body` の必須チェック（`app/models/book.rb`）
- フラッシュメッセージ表示（作成・更新・削除）
- 入力エラーの画面表示（一覧・編集画面にエラー要約を表示）
- トップページ（`homes#top`）から一覧/投稿へリンク
- ルーティング: `resources :books`, `root to: 'homes#top'`
- Strong Parameters によるパラメータ許可

## 設計・実装の工夫

- Rails標準のMVC構成で責務を分離（一覧+新規投稿フォームを同一画面で実装）
- モデルにバリデーションを集約し、コントローラで成功/失敗を分岐（`render :index`でエラー再表示）
- フラッシュメッセージで成功通知（作成/更新/削除）
- RSpecによるモデルテスト・システムテストを用意（`spec/models/*`, `spec/system/*`）
- FactoryBot + Fakerでテストデータを生成

## セットアップ & 動作確認

前提: Ruby 2.6.3, Bundler, SQLite3 が利用可能であること（Node/Yarnは必須ではありません。`package.json` は依存空）。

1) 依存インストール（推奨）

```bash
bundle install
# 初回セットアップは bin/setup でも可（DB作成・ログ/一時ファイル掃除まで実行）
bin/setup
```

2) データベース作成・マイグレーション

```bash
bin/rails db:setup   # or: bin/rails db:create db:migrate
```

3) アプリ起動

```bash
bin/rails s
# http://localhost:3000 にアクセス（トップ -> 一覧/投稿）
```

## テスト実行

```bash
bundle exec rspec
```

## 改善ポイント / TODO（事実ベースで抽出）

- テスト: コントローラスペックは未整備（`spec/controllers` なし）。モデル/システムは有り。
- エラーハンドリング: `ActiveRecord::RecordNotFound` 等の例外専用ハンドリングは未実装（`ApplicationController`に記述なし）。
- メッセージ: 削除時のフラッシュ文言にタイプミスあり（`destroyd`）。
- CI/CD: 自動テスト実行の定義なし（GitHub Actions 等未設定）。
- ドキュメント: `.gitignore` が最小限（`.DS_Store` のみ）。`/log`, `/tmp`, `*.sqlite3` などの一般的エントリ追加余地あり。
- パッケージ: `package.json` は存在するが依存ゼロ。利用しないなら整理、利用するなら管理方針を明記。
- コンテナ: Docker/Docker Compose 定義なし。必要に応じて導入検討。

## 強調したいポイント（本リポジトリで示しているスキル）

- Rails 5でのCRUD実装（バリデーション、Strong Parameters、フラッシュ/エラー表示）
- RSpec/Capybara/FactoryBotを用いたモデル・システムテストの整備
- 単純で読みやすいコントローラ/ビュー構成（学習・レビューに適した最小構成）
