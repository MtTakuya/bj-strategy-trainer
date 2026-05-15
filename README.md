# BJ Strategy Trainer

ブラックジャック ベーシックストラテジー暗記用ブラウザアプリです。

- **技術構成**: HTML / CSS / JavaScript のみ（1ファイル `index.html`）
- **外部依存なし**: ライブラリ・サーバー・API 不要
- **成績保存**: ブラウザの `localStorage` に保存（`bj_strategy_trainer_stats`）
- **問題数**: Hard 100問 / Soft 80問 / Pair 100問 = **計 280問**

---

## ローカルで動作確認する方法

### 方法① ファイルをブラウザで直接開く

```bash
open index.html
```

または Finder から `index.html` をダブルクリックします。

> ※ Chrome / Safari / Firefox いずれでも動作します。  
> ※ iPhone 実機確認は後述の GitHub Pages URL を Safari で開いてください。

### 方法② ローカルサーバーを使う（推奨）

```bash
# Python 3
python3 -m http.server 8080

# Node.js (npx)
npx serve .
```

起動後 → `http://localhost:8080` をブラウザで開きます。

---

## GitHub Pages で公開する手順

1. **GitHub にリポジトリを作成**

   ```
   https://github.com/new
   ```

   - Repository name: 例 `bj-strategy-trainer`
   - Public を選択
   - 「Create repository」

2. **ファイルをプッシュ**

   ```bash
   cd /path/to/このフォルダ
   git init
   git add index.html README.md
   git commit -m "initial commit"
   git branch -M main
   git remote add origin https://github.com/<ユーザー名>/bj-strategy-trainer.git
   git push -u origin main
   ```

3. **GitHub Pages を有効化**

   リポジトリ画面 → **Settings** → **Pages**  
   - Source: `Deploy from a branch`
   - Branch: `main` / `/ (root)`
   - **Save** をクリック

4. **アクセス URL**

   数分後に以下の URL で公開されます：

   ```
   https://<ユーザー名>.github.io/bj-strategy-trainer/
   ```

---

## iPhone のホーム画面に追加する手順（PWA風に使う）

1. Safari で GitHub Pages の URL を開く
2. 画面下部の **共有ボタン**（□に↑のアイコン）をタップ
3. 「**ホーム画面に追加**」をタップ
4. 名前を `BJ Trainer` に設定して「**追加**」

> ホーム画面から起動すると全画面表示になり、自作アプリのように使えます。  
> 一度読み込んだあとはオフラインでも動作します（Safariのキャッシュ）。

---

## 問題データを追加・編集する

`index.html` 内の以下の3つのテーブルを編集してください。

```javascript
const HARD_TABLE = [ ... ];  // ハードハンド
const SOFT_TABLE = [ ... ];  // ソフトハンド（A+X）
const PAIR_TABLE = [ ... ];  // ペア
```

各行の形式：

```javascript
{ hand: '16', a: ['S','S','S','S','S','H','H','H','H','H'] }
//                  2   3   4   5   6   7   8   9  10   A
```

アクションコード：

| コード | 表示   | 意味             |
|--------|--------|------------------|
| `H`    | Hit    | ヒット           |
| `S`    | Stand  | スタンド         |
| `DD`   | Double | ダブルダウン     |
| `SP`   | Split  | スプリット       |

---

## 今後 PWA 対応を追加する場合

以下のファイルを追加するだけで対応できます。

1. **`manifest.json`** — アイコン・アプリ名などの設定
2. **`sw.js`** — Service Worker（オフライン対応）
3. `index.html` の `<head>` に以下を追加：

```html
<link rel="manifest" href="manifest.json">
<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('sw.js');
  }
</script>
```

---

## 注意事項

- 本アプリで使用しているベーシックストラテジーは一般的な多デッキルールを基にしています
- カジノのルール（デッキ数・DAS・サレンダー等）により最適解が変わる場合があります
- 個人情報・APIキー・ログイン機能・外部DBは一切使用していません
