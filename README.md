# git管理スタート
- `git init` : .gitディレクトリ(ローカルリポジトリ)が作成される.(とりあえず場所に移動したらはじめにこれをする)

# リモートとローカルを結びつける
- `git remote add origin <URL>` : originというショートカットでurlのリモートリポジトリを登録する

# ファイルやフォルダをステージ
- `git add <ファイル名>` : ファイルの変更をステージ
- `git add <ディレクトリ名>` : ディレクトリの変更をステージ
- `git add .` : 全ての変更をステージ
- `git status` : 変更内容について確認できる

# コミット
- `git commit` : コミットできる(ターミナル上でコッミットメッセージを編集)
- `git commit -m "メッセージ"` :　メッセージ付きコミット
- `git commit -v` : 変更内容を確認できる
- `git commit --amend` : 直前のコミットを修正できる.(pushしたコミットをやり直したらだめ)

# リモートにコミットした内容をpush
- `git push origin master` : ローカルリポジトリの内容をリモートリポジトリにpush
- `git push -u origin master` : 次回以降,git pushのみでpushできる.



# branchとmerge
- `git branch` : branchを表示(今いるbranchは*マークが付く)
- `git branch <ブランチ名>` :　新規ブランチの作成
- `git checkout <ブランチ名>` : ブランチの切り替え
- `git checkout -b <新規ブランチ名>` : 上２つの作業を一度に行いたい場合
- `git branch master origin/master` : github上のmasterをローカルのmasterとして作成
- `git merge <ブランチ名>` : ブランチの内容を取り込む
- `git merge origin/<ブランチ>` : github上のブランチを取り込む
- `git branch -m <ブランチ名>` : 今いるbranchの名前を変更するとき
- `git branch -d <ブランチ名>` : branchの消去ができる(masterにmergeされていない場合は止まってくれる)
- `git branch -D <ブランチ名>` : branchの強制消去ができる

- `git rebase <ブランチ名>` : 別ブランチのcommitをブランチに取り込むことができる.(mergeをしながらcommitまでも取り込むことができる.
履歴を整えられる)
- `git config --global merge.ff false(true)` : falseにすればmergeするときもcommitメッセージを残すことができる.
なお、githubにプッシュしたコミットをリベースしてしまうのはだめ。

- `git reflog` : 今のブランチのすべてのコミット履歴を表示する.

- `git reset --hard HEAD@{数字}` : 元に戻したいポイントの数字を入力すれば元に戻る.

**作業の履歴を残したければmerge、履歴を消してきれいにしたければrebase**

# その他もろもろ
- `git clone <リポジトリ名>` : ワークツリーと.gitディレクトリがコピーされる
- `git diff <ファイル名>` : ファイルにおいてステージに上げた後の差分を表示
- `git diff --staged` : git addした後の差分を表示
- `git log` : 変更履歴を確認できる
- `git log` --oneline : 一行で変更内容を確認できる
- `git log -n コミット数` :表示する履歴コミット数を指定できる.
- `git rm <ファイル名>` : ファイルの消去
- `git em --cached <ファイル名>` : gitのワークツリーから消去したいがファイルは残したい場合
- `git mv <旧ファイル> <新ファイル>` : ファイルの移動ができる.

## コマンドにエイリアスをつける.
- `git config --global alias.ci commit` : commitするときにciと入力すれば済む
- `git config --global alias.st status` : statusのときstと入力すれば済む
- `git config --global alias.br brunch` : brunchのときbrと入力すれば済む
- `git config --global alias.co checkout` : checkoutのときcoと入力すれば済む

## 変更をもとに戻す(ctrl + Z的な)
- `git checkout -- <ファイル名>` : ファイルへの変更を取り消す
- `git checkout -- .` : 全変更の取り消し

## stageした変更をもとに戻す
- `git reset HEAD <ファイル名>` : stageした変更をもとに戻す
- `git reset HEAD .` : stageした変更をすべてもとに戻す

## リモートから情報を取得する
- `git fetch origin` : リモート(github上で追加されたファイルを取得する)
- `git checkout master` : マスターブランチに戻る
- `git merge origin/master` : マスターブランチに取得した情報をmergeする
- `git branch -a` : git branchのすべての情報を表示する
- `git checkout <ブランチ名>` :　ブランチに移動する.(ブランチ名はgit branchコマンドで探す)
origin/masterとすればgithub上のmasterブランチをmerge,fetchできる。

## リモートから情報を取得する(pull)fetchのmasterとmergeする作業を一度にできる
- `git pull origin master` : fetchとmergeを一度に行うことができる.

## リモート名の変更,消去
- `git remote rename <旧リモート名> <新リモート名>` : リモート名の変更
- `git remote rm <リモート名>` : リモートの消去

## コミットに対してタグを作成する
- `git tag -a <タグ名> -m "メッセージ"` : メッセージ付きでタグを付ける
- `git tag <タグ名>` : メッセージなしでタグを付ける
- `git tag <タグ名> <コミット名>` : 後からコミットに対してタグ付けできる
- `git show <タグ名>` : タグの情報を表示する.
- `git push origin <タグ名>` : タグをリモートに送信する
- `git push origin --tags` : すべてのタグをリモートに送信する

## キャッシュについて(.gitignoreファイル作成時に便利)
- `git rm -r --cached <ファイル名>` : ファイルを残したまま、gitの管理から外す(キャッシュの消去). 既にcommitしてしまったファイルをあとからignoreしたい場合に使うと改めてignoreできる.
