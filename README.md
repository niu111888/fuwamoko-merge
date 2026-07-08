# ふわもこゲーム集 🐰🐷🐭

かわいい動物モチーフの、ブラウザで遊べる**1ファイル完結ゲーム集**です。
HTML・CSS・JavaScript だけで作られていて、**ビルド作業も外部ライブラリも不要**。
ファイルをブラウザで開けばすぐ動きます。

> このREADMEは「**新しいパソコンに移しても、すぐに続きの開発を始められる**」ための記録です。
> リポジトリと一緒に保存されているので、`git clone` すればこの説明ごと手に入ります。

---

## 🎮 ゲーム一覧（公開URL）

トップページ（`index.html`）は**ゲーム一覧のメニュー**で、そこから各ゲームへ移動できます。各ゲームには一覧に戻る 🏠 ボタンもあります。

| ゲーム | ファイル | 公開URL |
|--------|----------|---------|
| 🏠 ゲーム一覧（メニュー・トップ） | `index.html` | https://niu111888.github.io/fuwamoko-merge/ |
| ふわもこタイピング 3カ国語（英語/中国語/日本語） | `typing.html` | https://niu111888.github.io/fuwamoko-merge/typing.html |
| ふわもこマージ どうぶつ（スイカゲーム風） | `suika.html` | https://niu111888.github.io/fuwamoko-merge/suika.html |
| パンチヒーロー ぶたさん | `hero.html` | https://niu111888.github.io/fuwamoko-merge/hero.html |

- スマホ・PCどちらのブラウザでも遊べます（レスポンシブ＆タッチ操作対応）。
- スコアなどは各自のブラウザに自動保存されます（localStorage）。

---

## 🧰 使っている道具（環境）

| 道具 | 用途 | 必須？ | このPCでのバージョン（参考） |
|------|------|--------|------------------------------|
| **ブラウザ**（Chrome/Safari等） | ゲームを開いて動作確認 | 必須 | — |
| **git** | バージョン管理 | 必須 | 2.39.5 |
| **GitHub CLI (`gh`)** | リポジトリ作成・公開(Pages)・認証 | 公開する時に必須 | 2.94.0 |
| **Python 3** | ローカル簡易サーバー（`python3 -m http.server`） | 任意（無くてもファイルを直接開けばOK） | 3.14.5 |
| Node.js / npm | いまは未使用（将来ツールを足す場合に） | 不要 | v24.16.0 / 11.13.0 |

- **GitHubアカウント： `niu111888`**（このゲーム集の公開先）
- **OS（開発時）**：macOS 26.5.1 / Apple Silicon (arm64)。※他のOSでも上記の道具が入れば開発できます。

---

## 🚀 まったく新しいパソコンで始める手順

### 1. 道具を入れる
- **git** … [git-scm.com](https://git-scm.com/) から。Macなら `xcode-select --install` でも入ります。
- **GitHub CLI (`gh`)** … [cli.github.com](https://cli.github.com/)。Macは `brew install gh`、Windowsは `winget install GitHub.cli`。
- （任意）**Python 3** … 動作確認用の簡易サーバーに使います。無ければファイルを直接開けばOK。

### 2. GitHubにログイン（`niu111888`）
```bash
gh auth login --hostname github.com --git-protocol https
# → ブラウザ認証 or トークンで niu111888 としてログイン（スコープに repo を含める）
gh auth setup-git        # git が gh の認証を使えるようにする
```
※このPCには複数アカウントが入っていて有効アカウントが切り替わることがあります。push前に確認/切替：
```bash
gh auth status                       # 今どのアカウントが Active か確認
gh auth switch --user niu111888      # niu111888 に切り替え
gh auth setup-git
```

### 3. このリポジトリを取ってくる
```bash
git clone https://github.com/niu111888/fuwamoko-merge.git
cd fuwamoko-merge
```

### 4. 開発する
編集は `index.html` / `suika.html` を好きなエディタで開いて直すだけ。確認方法は2通り：
- **かんたん**：ファイルをダブルクリックしてブラウザで開く（リロードで反映）。
- **おすすめ**：ローカルサーバーを立てて開く（スマホ実機からも見られる）。
  ```bash
  python3 -m http.server 8123
  # ブラウザで http://localhost:8123/suika.html を開く
  ```

### 5. 変更を保存・公開する
```bash
git add -A
git commit -m "変更内容のメモ"
git push                 # niu111888/fuwamoko-merge に保存される
```
push すると **GitHub Pages が自動で再ビルド**して、数十秒後に公開URLへ反映されます。

---

## 📁 プロジェクト構成

```
fuwamoko-merge/
├── index.html   … ゲーム一覧メニュー（公開時のトップページ）
├── typing.html  … ふわもこタイピング 3カ国語（英語/中国語/日本語）
├── suika.html   … ふわもこマージ どうぶつ（スイカゲーム風）
├── hero.html    … パンチヒーロー ぶたさん（アクション）
├── README.md    … このファイル（開発ガイド）
└── .claude/
    └── launch.json … ローカルプレビュー用の設定（python http.server）
```

- 各ゲームは**1つのHTMLファイルに完結**（`<canvas>` + JavaScript）。依存関係なし。
- 画像も音声もなく、絵はすべてコード（Canvasの図形）で描いています。

---

## ☁️ 公開（GitHub Pages）の仕組み

- リポジトリ **`niu111888/fuwamoko-merge`** の `main` ブランチのルート(`/`)を GitHub Pages が配信。
- `index.html` がトップ（`https://niu111888.github.io/fuwamoko-merge/`）になり、
  他のファイルは `…/fuwamoko-merge/<ファイル名>` でアクセスできます。
- Pagesを一度有効化済み。新しいリポジトリで一から有効化する場合：
  ```bash
  gh api -X POST repos/<owner>/<repo>/pages -f "source[branch]=main" -f "source[path]=/"
  ```

---

## 🔧 git リモートと注意点

```bash
git remote -v
# origin      → https://github.com/niu111888/fuwamoko-merge.git   ← 今後の保存先
# old-gennri  → https://github.com/gennrikabushikigaisha-alt/pyokopyoko-runner.git  ← 旧公開先(push権限なし)
```
- **今後の保存先は `origin`（niu111888）** です。`git push` でここに保存されます。
- 旧 `old-gennri` には niu111888 の push 権限がありません（使いません。気になれば `git remote remove old-gennri` で削除可）。

---

## 🆘 困ったとき

- **push で `403 / Permission denied`** … 有効な `gh` アカウントが niu111888 以外になっています。
  `gh auth switch --user niu111888 && gh auth setup-git` で切り替えてから再push。
- **公開URLが真っ白／404** …
  - 404：push直後はPagesのビルド中。30〜60秒待ってリロード。
  - 真っ白：JavaScriptのエラーの可能性。ブラウザの「開発者ツール → Console」でエラーを確認。
  - 古い画面が残る：ブラウザを**リロード（キャッシュ更新）**。
- **ローカルで `python3` が無い** … ファイルを直接ブラウザで開けば遊べます（サーバーは任意）。

---

## 📝 開発の進め方メモ

- まず**少しだけ直す → ブラウザで確認 → コミット**、を小刻みに繰り返すのが安全。
- 既存のコードの書き方（命名・コメントの密度・パステルな色使い）に合わせると統一感が出ます。
- 新しいゲームを足す時は、`〇〇.html` を1ファイルで作れば、そのまま `…/fuwamoko-merge/〇〇.html` で公開されます。
