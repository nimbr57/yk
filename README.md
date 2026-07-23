# 💬 Yuki's Realtime BBS

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Firebase](https://img.shields.io/badge/firebase-ffca28?style=for-the-badge&logo=firebase&logoColor=black)

**パスワード不要、完全匿名の次世代リアルタイム掲示板**  
シード値とSHA-256アルゴリズムを用いた独自の認証システムと、チャット欄から直接実行できる強力なコマンドライン・モデレーション機能を搭載しています。

---

## ✨ Features (主な機能)

* 🔒 **Secure ID System**
  * ユーザーが入力した「シード値」をSHA-256でハッシュ化し、Base64変換した先頭7桁を固有IDとして付与。
  * データベースにパスワードを保存しないため、安全かつ完全に匿名性を保ちます。
* ⚡ **Realtime Sync**
  * Firebase Realtime Databaseを利用し、ページリロードなしで瞬時にメッセージを同期。
* 🛡️ **Command-line Moderation**
  * 投稿フォームから `/ban` や `/clear` などのコマンドを打ち込むことで、直感的に掲示板を管理。
  * 厳格な権限システム（Root Owner 〜 Speaker）により、荒らし対策も万全です。
* 🎲 **Vanity ID Generator**
  * 非同期バッチ処理を用いた総当たり（ブルートフォース）計算により、好きな文字列が含まれるお気に入りIDとシード値を採掘できます。
* 🌙 **Dark Mode Support**
  * OSの設定やウィジェットから、目に優しいダークモードへワンタッチ切り替え。

---

## 📁 Project Structure (構成ファイル)

| ファイル名 | 概要 |
| :--- | :--- |
| **`home.html`** | サイトのポータル（ホーム）画面。各機能へのアクセスをカード型UIで提供。 |
| **`index.html`** | リアルタイム掲示板のメインシステム。チャットとコマンド処理を担う中核。 |
| **`id.html`** | お気に入りIDジェネレーター。指定文字列を含むIDを総当たりで検索。 |
| **`info.html`** | 管理者用ダッシュボード。権限一覧、BANリスト、NGワードを可視化。 |
| **`use.html`** | ユーザー向けの使い方やルールをまとめたヘルプページ。 |

---

## 👑 Role & Command System (権限とコマンド)

チャットの投稿フォームにコマンドを入力することで、権限に応じた管理アクションを実行できます。

### 権限階層
`Root Owner` > `Owner` > `Summit` > `Moderator` > `Manager` > `Speaker`

### 主要コマンド一覧

| コマンド | 説明 | 実行可能権限 |
| :--- | :--- | :--- |
| `/owner [ID]` | 指定IDにOwner権限を付与 / 剥奪（`/disowner`） | **Root Owner** (`KF81wqJ`) |
| `/summit [ID]` | 指定IDにSummit権限を付与 / 剥奪（`/dissumit`） | Owner以上 |
| `/manager [ID]` | 指定IDにManager権限を付与 / 剥奪（`/dismanager`） | Summit以上 |
| `/moderator [ID]` | 指定IDにModerator権限を付与 / 剥奪（`/dismoderator`） | Summit以上 |
| `/add [ID] [称号]` | ユーザー名の横にカスタム称号（ピンク文字）を付与 | Moderator以上 |
| `/color [色] [ID]` | ユーザー名の文字色を変更（例: `/color red KF81wqJ`）| Moderator以上 |
| `/NG [単語]` | 掲示板のNGワードを追加 / 解除（`/OK [単語]`） | Moderator以上 |
| `/ban [ID]` | 指定ユーザーのIPアドレスをアクセス禁止に設定 / 解除（`/unban`）| Manager以上 |
| `/clear` | 掲示板のすべての投稿履歴を完全に削除 | Manager以上 |
| `/del [No]` | 指定したレス番号の投稿を「削除されました」状態にする | Manager以上 |
| `/destroy [文字]`| 指定した文字列を含む投稿、または指定IDの投稿を一括削除 | Manager以上 |
| `/topic [文字]` | 掲示板上部の「今の話題」を更新 | Manager以上 |

> **Note:** 上記のコマンドを実行した際、システム処理と同時に「どのようなコマンドを打ったか」が掲示板にログとして残る仕様になっています。（誤爆防止のキャンセル時を除く）

---

## 🚀 Setup (導入方法)

1. リポジトリをクローンまたはダウンロードします。
2. Firebase Consoleで新規プロジェクトを作成し、Realtime Databaseを有効化します。
3. `index.html` と `info.html` の `<script type="module">` 内にある `firebaseConfig` を、ご自身のFirebaseプロジェクトの情報に書き換えます。
4. HTMLファイルをウェブサーバー（GitHub Pages, Vercel, Firebase Hostingなど）にデプロイして完了です。

---

## 👨‍💻 Author

**Yuki Youtube**
