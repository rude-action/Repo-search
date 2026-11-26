# GitHub Repository Search

キーワードで GitHub の公開リポジトリを検索できる、単一 HTML ファイルのシンプルな Web アプリです。ビルド不要で、ブラウザで開くだけで使えます。

対象ファイル: `C:\Users\User\Documents\github-search.html`

## 使い方

1. `github-search.html` をブラウザで開きます。
2. キーワード(例: `tetris`, `machine-learning`, `docker`)を入力して **Search** を押します。
3. リポジトリ名をクリックすると、新しいタブで GitHub のリポジトリページが開きます。

## 機能

- **検索** — GitHub Search API (`/search/repositories`) で公開リポジトリを検索
- **並べ替え** — ベストマッチ / スター数 / フォーク数 / 更新日の新しい順
- **リポジトリ情報の表示** — 説明・スター数・フォーク数・ウォッチャー数・使用言語
- **ページネーション** — 10件/ページで前後ページに移動(GitHub API の上限により最大100ページ)
- **エラー表示** — レート制限 (HTTP 403)・無効なクエリ (422)・ネットワークエラーを画面に表示

## GitHub トークン(任意)

コード内の `TOKEN` 変数に個人アクセストークンを設定すると、API レート制限が緩和されます。

```js
const TOKEN = ''; // e.g. 'ghp_xxxxxxxxxxxx'
```

トークンは https://github.com/settings/tokens で作成できます(パブリックリポジトリの検索のみなら権限は不要です)。

## レート制限について

GitHub Search API のレート制限は、トークンなしでは **10リクエスト/分**、トークンありでは **30リクエスト/分** です。制限に達すると「Rate limit exceeded」のエラーが表示されます。

## 仕組み

- HTML / CSS / JavaScript を 1 ファイルにまとめた構成で、依存ライブラリはありません。
- 検索結果は `fetch` で GitHub REST API を呼び出して取得します。
- リポジトリ名や説明などの外部テキストは `escapeHtml()` でエスケープしてから DOM に挿入しています。

## 注意

- トークンを直接 HTML に埋め込むと、ファイルを共有した際に漏れる恐れがあります。公開する場合は `TOKEN` を空のままにしてください。
