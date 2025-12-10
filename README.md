# git/ghコマンドの使い方


## git command
`git init`<br>
ローカルにあるフォルダとgithubを連携させる<br>
**最初に絶対入力しないとやばい 昔これ忘れてホームディレクトリ内のフォルダ全部突っ込んだことある**

`git remote add origin <リポジトリのURL/SSH>`<br>
リモートのgithubのリポジトリに接続し、originという名前をつける
pushする時に楽にするため

`git add .`<br>
カレントディレクトリでgithubにあげるファイルを取得<br>
**多分addの後ろについてる「.」がカレントディレクトリの意味**

`git commit`<br>
コミットを作成する<br>
様々なオプションもある
- `-m <コミットメッセージ>`メッセージ付きでコミット
- `-- amend`直前のコミットを上書き(修正)する
- `-a`勝手に`git add .`もしてくれる
- `-v`変更内容を確認しながらコミットメッセージを作れる
- `-p`変更箇所ごとにコミットするかどうかを指定できる
- `--no-edit`コミットメッセージを変更せずにコミットできる

`git push origin master`<br>
リモートのmasterブランチに上げるコマンド

## gh command(github cli)
`gh repo create`<br>
github上でリポジトリを作成する<br>


