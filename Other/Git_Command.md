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
```
a/file.txt: ステージング  
b/file.txt: ワークツリー  
---, +++ で表現するという意味  
注意：+は追加の意味ではない  
@@ -0,0 +1,2 @@  
ステージングは0～0行目を表示します  
ワークツリーは1～2行目を表示します  

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

バージョン管理されているファイル名の変更
```bash
git mv 元ファイル名 変更したいファイル名
```