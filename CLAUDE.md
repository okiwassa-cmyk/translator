# WASSA TRANSLATOR APP

WASSA WASSA のスタッフ⇄ゲスト多言語コミュニケーションツール（通称：ホンヤクコンニャク／Staff Tool）。
沖縄・大宜味村の小さな宿（3室）で、海外ゲストとの接客に使う翻訳アプリ。

## ファイル構成

- `index.html` — 翻訳ツール本体（単一HTMLファイル）

## 対応言語

- 英語（en）/ 繁體中文（zh-TW・台湾向け）/ 简体中文（zh-CN）/ 한국어（ko）
- 日本語 ⇄ 各言語の双方向翻訳

## 主要タブ

ご挨拶 / 1F / 2F / 夕食 / 朝食 / チェックアウト / お知らせ / 自由入力 / デラックス / エリア案内 / チャット

## 翻訳エンジン

- **メイン：Claude API**（`claude-sonnet-4-6`）を直接ブラウザから呼び出し
  - エンドポイント: `https://api.anthropic.com/v1/messages`
  - ヘッダーに `anthropic-dangerous-direct-browser-access: true` を付ける
  - システムプロンプトに「大宜味の元プロ料理人夫婦の小さな宿」というキャラ設定と、沖縄の料理名・地名を残す指示を入れている
- **フォールバック：MyMemory**（無料API・低精度）。キー未設定時のみ使用
- 全ての翻訳（チャット `sendChat` / 自由入力 `doFT` / フレーズ / 編集欄）は `translate()` / `translateFrom()` を通る → この2関数を直せば全体に効く

## APIキー管理

- 画面右上 **🔑 翻訳AI** ボタン → モーダルでキー入力
- 保存先：**その端末の localStorage のみ**（キー名 `WASSA_ANTHROPIC_KEY`）
- GitHub Pages に公開しても**キーはソースに出ない**（端末ごとに1回入力する運用）
- 起動時に `updateApiKeyStatus()` でボタン表示を切替（キーありで `🔑 Claude ON`）

## データ保存

- フレーズ等のデータは localStorage（キー名 `LS_KEY`）に保存

## インフラ

- **GitHub Pages** — 公開（リポジトリ: `okiwassa-cmyk/wassa-system` 想定）
- 公開しているため、`index.html` 変更後は GitHub へのアップが必要 → Risa に伝える

## 作業ルール

- ファイルは `/Users/mizo/Desktop/WASSA TRANSLATOR　APP/index.html` に保存
- 正式コピー（旧）：`/Users/mizo/Desktop/要確認/WASSA webt/wassa translator/wassa-staff-translator 2.html`
- HONYAKU.gs とは**無関係**（このアプリは GAS を使わず、ブラウザから直接 Claude API を呼ぶ自己完結型）
- アレルゲン解析等は無し。チャット・翻訳は Sonnet を使用
