## Node.js サンプルアプリ（日本語ドキュメント）

**概要**
- **フレームワーク**: Express 4 + EJS
- **エンドポイント**: `GET /` – ビュー `public/index.html` を EJS でレンダリングし、環境名を表示
- **環境変数**: `APP_ENV`（`staging`/`production`/未設定時は `review app`）、`PORT`（未設定時は 5000）
- **デプロイ想定**: Heroku（`Procfile`/`app.json` あり）

---

## 必要要件
- Node.js（LTS 推奨）
- npm
- （任意）Heroku CLI と Git

---

## セットアップ & ローカル実行
1. 依存関係をインストール
```bash
npm install
```
2. （任意）`.env` を作成して環境を指定
```ini
APP_ENV=staging
PORT=5000
```
3. 起動
```bash
npm start
```
4. ブラウザで確認
- `http://localhost:5000/`
- ページ内のバッジに現在の環境（`APP_ENV`）が表示されます

---

## テスト
- テストフレームワーク: Mocha + Chai + chai-http
- ルート `GET /` に対して HTTP 200 が返ることを確認します
```bash
npm test
```

---

## プロジェクト構成
- `index.js`: Express アプリ本体（EJS 設定、`/` ルート、ポート設定）
- `public/index.html`: 表示用テンプレート（Tachyons CSS、`<%= env %>` で環境名を表示）
- `test/test.js`: 簡易 E2E 風リクエストテスト
- `package.json`: スクリプト・依存パッケージ定義
- `Procfile`: Heroku Dyno 定義（`web`/`worker`/`clock`/`release`）
- `app.json`: Heroku アプリ設定（buildpack 等）

---

## API/ルーティング
- `GET /`
  - テンプレート `public/index.html` をレンダリング
  - EJS 変数 `env` に `APP_ENV` の値（または既定値）を注入

---

## デプロイ（Heroku）
1. アプリ作成
```bash
heroku create
```
2. デプロイ（ブランチ名は `main` または `master` を利用中のものに置換）
```bash
git push heroku main
# または
git push heroku master
```
3. アプリを開く
```bash
heroku open
```

- `Procfile` により Web プロセス（`npm start`）が起動します。
- `worker`/`clock`/`release` の定義も含まれています（必要に応じて有効化してください）。

---

## ライセンス
- 本リポジトリは `package.json` に記載の **MIT License** に従います。
