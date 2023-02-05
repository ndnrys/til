# Gitコマンド
## 概要
コマンド
## 詳細

ユーザー名設定  
```bash
git config --global user.name "ここに名前"
```

ユーザー名確認
```bash
git config user.name
```

EMail設定  
```bash
git config --global user.email "ここにアドレス"
```

EMail確認
```bash
git config user.email
```


ディレクトリ確認
```bash
pwd
```

フォルダ作成
```bash
mkdir git_udemy
```

初期化
```bash
git init
```

ステージングエリアに追加する
.はそのディレクトリ全入れ
-uは変更のある全ファイルを入れる
```bash
git add ここにファイル名
git add .
git add -u
```

ステージングエリアを確認する
```bash
git ls-files
```

ローカルリポジトリへ登録する
```bash
git commit -m "メッセージをかく"
```

コミット履歴確認
```bash
git log
```

git log統計オプション（何行追加されて、何行削除されたか）
```bash
git log -stat
```

差分確認(ステージングエリア vs ワークツリー)
```bash
git diff
git diff コミット1 コミット2
```
a/file.txt: ステージング  
b/file.txt: ワークツリー  
---, +++ で表現するという意味  
注意：+は追加の意味ではない  
@@ -0,0 +1,2 @@  
ステージングは0行目から0行表示します  
ワークツリーは1行目から2行表示します  
２行目のコミット1，2はSHA-1ハッシュ値を指定  
SHA-1ハッシュ値はすべて入力しないでも大丈夫

git addとコミットを同時に行う  
※ 一度リポジトリに登録済みのファイルのみ(-aオプション)
```bssh
git commit -a -m "メッセージ"
```

差分確認(ローカルリポジトリ vs ステージングエリア)
```bash
git diff --cached
```
a/file.txt: ローカルリポジトリ  
b/file.txt: ステージング  

差分確認(ローカルリポジトリ vs ワークツリー)
```bash
git diff HEAD
```
a/file.txt: ローカルリポジトリ  
b/file.txt: ワークツリー  

バージョン管理のステータスを確認
```bash
git status
```

ステージングエリアに追加してしまったファイルを削除
```bash
git rm --cached ファイル名
```

ステージングとワークツリーからファイルを削除
-f：強制的
リポジトリに登録されていないファイルにrmするとエラーになる
よって、強制的に削除するには-fが必要
```bash
git rm -f ファイル名
```

ディレクトリ削除
-r：再帰的
```bash
git rm -r ディレクトリ
```

バージョン管理したくないファイルの設定
gitignoreファイルを作成
gitignore内に除外するファイル名を設定
```bash
touch .gitignore
```
gitignoreの書き方例
```
.DS_STORE
*.log
!example.log
```
.gitignoreもバージョン管理するのが一般的  

バージョン管理されているファイル名の変更
```bash
git mv 元ファイル名 変更したいファイル名
```

ブランチの表示
```bash
git branch
```

ブランチ作成
```bash
git branch ブランチ名
```

ブランチ切り替え
```bash
git checkout ブランチ名
```

マージ  
現在いるブランチに取り込む
--no-ff: ファストフォーワードマージを行える条件下で行わない場合  
-> 3方向マージ（新たなコミットを作成）  
```bash
git merge 取り込みたいブランチ名
git merge --no-ff 取り込みたいブランチ名
```

コンフリクトが起きた後は、git add, git commit

ブランチ削除  
大文字：マージされていなくても削除可能  
小文字：マージされているもののみ削除可能  
```bash
git branch -d ブランチ名
git branch -D ブランチ名
```

ブランチ名変更  
-m:moveの略
```bash
git branch -m 変更前ブランチ名 変更したいブランチ名
```

ブランチ作成→切り替え  
-b:ブランチの略
```bash
git checkout -b ブランチ名
```

コミットリセット
最新のコミットのひとつ前のSHA-1ハッシュ値を指定  
--hard: ワークツリーとステージングエリアにHEADの内容をコピーする  
--soft: ワークツリーとステージングエリアはそのまま -> git statusで差分表示される  
```bash
git reset --hard 戻したいSHA-1ハッシュ値
```

コミット打消し
```bash
git revert 打ち消したいSHA-1ハッシュ値
git revert HEAD
```

reset と revertの使い分け  
共同開発者がいる？
  -> yes: 共同開発者に影響を与える可能性があるのでresetは使わない  
  -> no: コミット履歴に残したい？  
    -> yes: revert  
    -> no: reset  