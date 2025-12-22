# Git/GitHub完全初心者ガイド

## GitとGitHubって何？

**Git（ギット）**
- ファイルの変更履歴を管理するツール
- 「いつ、誰が、何を変更したか」を記録できる
- 間違えても過去の状態に戻せる

**GitHub（ギットハブ）**
- Gitで管理しているファイルをオンラインで保存・共有できるサービス
- 他の人と一緒に開発するときに便利
- 自分のコードを公開したり、バックアップにも使える

## 最初にやること（初回のみ）

### 1. Gitのインストール

**Windows**
- [Git公式サイト](https://git-scm.com/)からインストーラーをダウンロード
- 基本的に全部「Next」で進めてOK

**Mac**
- ターミナルを開いて `git --version` と入力
- インストールされていない場合、自動でインストールが始まる
- または Homebrew で: `brew install git`

**インストール確認**
```bash
git --version
```
バージョン情報が表示されればOK

### 2. Gitの初期設定

自分の名前とメールアドレスを登録（コミット時に記録される）

```bash
git config --global user.name "あなたの名前"
git config --global user.email "your-email@example.com"
```

**確認方法**
```bash
git config --list
```

### 3. GitHubアカウントの作成

1. [GitHub](https://github.com/)にアクセス
2. 「Sign up」からアカウント作成
3. メール認証を完了させる

### 4. GitHubとの接続設定（SSH）

パスワードを毎回入力しなくて済むように設定

**SSHキーの生成**
```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```
- Enter連打でOK（パスフレーズは空でも可）

**公開鍵をGitHubに登録**
```bash
# 公開鍵の内容をコピー（Mac）
cat ~/.ssh/id_ed25519.pub | pbcopy

# Windows（Git Bash）
cat ~/.ssh/id_ed25519.pub | clip
```

1. GitHubの Settings → SSH and GPG keys
2. 「New SSH key」をクリック
3. コピーした内容を貼り付けて「Add SSH key」

**接続テスト**
```bash
ssh -T git@github.com
```
「Hi ユーザー名!」と表示されればOK

## 基本的な使い方

### はじめてのリポジトリ作成

#### パターン1: ローカルから始める

```bash
# 1. プロジェクトフォルダに移動
cd ~/your-project

# 2. Gitの初期化（⚠️ここで実行すること！）
git init

# 3. GitHubにリポジトリを作成（GitHub CLI使用）
gh repo create

# または GitHub上で手動作成して、以下を実行
git remote add origin git@github.com:ユーザー名/リポジトリ名.git
```

#### パターン2: GitHubから始める

```bash
# 1. GitHub上でリポジトリを作成
# 2. ローカルにクローン
git clone git@github.com:ユーザー名/リポジトリ名.git

# 3. フォルダに移動
cd リポジトリ名
```

### 日常的な作業の流れ

```bash
# 1. ファイルを編集・作成する

# 2. 変更を確認
git status

# 3. 変更をステージング（追加）
git add .

# 4. コミット（変更を記録）
git commit -m "何を変更したかのメッセージ"

# 5. GitHubにアップロード
git push origin main
```

### よく使うコマンド

**`git status`**
- 現在の状態を確認（何が変更されているか）
- **迷ったらまずこれ！**

**`git log`**
- コミット履歴を表示
- 終了は `q` キー

**`git diff`**
- 変更内容の詳細を表示

**`git pull origin main`**
- GitHubから最新の変更を取得

## よくあるトラブルと対処法

### エラー: "fatal: not a git repository"
→ `git init` をしていない。プロジェクトフォルダで実行する

### プッシュできない
```bash
# 最新の状態を取得してから再度プッシュ
git pull origin main
git push origin main
```

### 間違えてコミットした
```bash
# 直前のコミットを取り消し（変更は残る）
git reset --soft HEAD^

# 変更ごと完全に取り消し（⚠️注意）
git reset --hard HEAD^
```

### ブランチ名を変更したい（master → main）
```bash
git branch -M main
git push -u origin main
```

## 覚えておくべき用語

- **リポジトリ（Repository）**: プロジェクトの保管場所
- **コミット（Commit）**: 変更の記録・スナップショット
- **プッシュ（Push）**: ローカルの変更をGitHubにアップロード
- **プル（Pull）**: GitHubの変更をローカルに取得
- **ブランチ（Branch）**: 作業を分岐させる機能（後で学ぶ）
- **クローン（Clone）**: GitHubのリポジトリをローカルにコピー

## 最初のステップ

1. 簡単なプロジェクトで試してみる（例: README.mdだけのリポジトリ）
2. 変更 → add → commit → push の流れを何度か繰り返す
3. 慣れてきたら `.gitignore` やブランチなどを学ぶ

## 便利なリソース

- [GitHub公式ドキュメント](https://docs.github.com/ja)
- [GitHub Skills](https://skills.github.com/) - インタラクティブな学習
- [Git入門（サル先生）](https://backlog.com/ja/git-tutorial/) - 日本語の分かりやすい解説

## 注意点

- **`git init` は必ずプロジェクトフォルダで実行**
  - ホームディレクトリで実行すると大変なことに
- コミットメッセージは分かりやすく書く
- 機密情報（パスワードなど）は絶対にコミットしない
- 定期的にプッシュしてバックアップ
