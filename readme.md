# Git / GitHub 基本操作チートシート

## この資料の目的

GitHub を使った開発で、初学者が最初に覚えるべき基本操作をまとめた資料です。

以下の流れが理解できることを目標とします。

```text
main ブランチから作業ブランチを作成
↓
開発
↓
コミット
↓
GitHubへPush
↓
Pull Request作成
↓
レビュー
↓
mainへマージ
```

---

# Gitの基本概念

Gitでは主に以下の4つを意識します。

```text
作業フォルダ
↓
ステージングエリア
↓
ローカルリポジトリ
↓
リモートリポジトリ(GitHub)
```

### 作業フォルダ

実際にソースコードを編集する場所

```text
Program.cs
index.html
README.md
```

### ステージングエリア

「次のコミットに含めるファイル」を選ぶ場所

```bash
git add .
```

### ローカルリポジトリ

自分のPC内のGit管理領域

```bash
git commit -m "ログイン画面を追加"
```

### リモートリポジトリ

GitHub上のリポジトリ

```bash
git push
```

---

# まず覚えるべきGitコマンド

## 現在の状態確認

```bash
git status
```

最も使用頻度が高いコマンドです。

以下を確認できます。

- 変更されたファイル
- ステージ済みファイル
- コミット対象ファイル
- 現在のブランチ

---

## 変更内容をステージングする

### 全て追加

```bash
git add .
```

### 個別追加

```bash
git add Program.cs
```

---

## コミットする

```bash
git commit -m "ログイン処理を追加"
```

例

```bash
git commit -m "ユーザー登録画面を追加"
git commit -m "エラーメッセージを修正"
git commit -m "READMEを更新"
```

---

## GitHubへPushする

```bash
git push
```

リモートリポジトリへ反映します。

---

## GitHubから最新を取得する

```bash
git pull
```

他の人の変更を取り込みます。

---

# プロジェクトを取得する

## 初回のみ

GitHubからリポジトリを取得

```bash
git clone https://github.com/user/sample-app.git
```

フォルダへ移動

```bash
cd sample-app
```

---

# ブランチとは

ブランチは「作業を分岐する仕組み」です。

例えば新機能を作る場合

```text
main
 └─ feature/login
```

main を直接編集せず、作業ブランチで開発します。

---

# ブランチ操作

## 現在のブランチ確認

```bash
git branch
```

例

```text
* main
  feature/login
```

`*` が現在いるブランチです。

---

## ブランチ作成

```bash
git branch feature/login
```

ブランチを作るだけです。

切り替えはされません。

---

## ブランチ作成と切り替え

実務ではこちらが多いです。

```bash
git switch -c feature/login
```

実行後

```text
main
 └─ feature/login
```

へ移動します。

---

## ブランチ切り替え

```bash
git switch main
```

または

```bash
git switch feature/login
```

---

# 初学者向け開発フロー

## ① mainを最新化

```bash
git switch main
git pull
```

---

## ② 作業ブランチ作成

```bash
git switch -c feature/login
```

---

## ③ コード修正

例

```text
LoginPage.jsx を作成
API処理を追加
```

---

## ④ 変更確認

```bash
git status
```

---

## ⑤ ステージング

```bash
git add .
```

---

## ⑥ コミット

```bash
git commit -m "ログイン機能を追加"
```

---

## ⑦ GitHubへPush

初回Push

```bash
git push -u origin feature/login
```

### 補足

`-u` を付けることで以後は

```bash
git push
```

だけでよくなります。

---

# Pull Request（PR）とは

Pull Request は

「この変更を main に取り込んでください」

と依頼する仕組みです。

GitHub上で作成します。

---

# Pull Request の流れ

```text
main
 ↓
feature/login 作成
 ↓
開発
 ↓
commit
 ↓
push
 ↓
Pull Request作成
 ↓
レビュー
 ↓
承認
 ↓
mainへマージ
```

---

# Pull Request 作成手順

GitHubへPush後、

GitHub画面で

```text
Compare & pull request
```

をクリック

↓

タイトル入力

```text
ログイン機能追加
```

↓

説明入力

```text
ログイン画面を追加
認証APIを接続
```

↓

```text
Create Pull Request
```

↓

レビュー依頼

---

# マージ後の作業

## mainを最新化

```bash
git switch main
git pull
```

---

## 不要ブランチ削除

ローカル

```bash
git branch -d feature/login
```

GitHub上

```text
Delete branch
```

をクリック

---

# よく使うコマンド一覧

## 状態確認

```bash
git status
```

## 変更履歴確認

```bash
git log --oneline
```

## ブランチ一覧

```bash
git branch
```

## ブランチ作成

```bash
git switch -c feature/sample
```

## ブランチ切り替え

```bash
git switch main
```

## ステージング

```bash
git add .
```

## コミット

```bash
git commit -m "説明"
```

## Push

```bash
git push
```

## Pull

```bash
git pull
```

---

# 初学者が覚えるべき最重要フロー

最初はこの流れだけ覚えれば十分です。

```bash
# mainを最新化
git switch main
git pull

# 作業ブランチ作成
git switch -c feature/sample

# 開発後
git add .
git commit -m "機能追加"

# GitHubへ送信
git push -u origin feature/sample

# GitHubでPR作成
# レビュー
# マージ

# 作業終了後
git switch main
git pull
git branch -d feature/sample
```

この流れが理解できれば、個人開発や小規模チーム開発に必要な Git / GitHub の基本操作は一通り扱えるようになります。