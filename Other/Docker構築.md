# Docker構築
## 概要
Docker構築手順
## インストール
### URL
https://www.docker.com/products/docker-desktop/

### WSL2有効化 - Windows
```
wsl --install
```

## Hello World
### run
```
docker run ubuntu:20.04 echo hello world
```

### ローカルにあるイメージの一覧
```
docker images
```

### Bash を起動
```
docker run -it ubuntu:20.04 bash
```

### 終了
```
exit
```

## Ruby開発環境
Linuxと違い、sudoは不要
### update
```
apt update
```

### Ruby, RubyBundlerをインストール
```
apt install ruby ruby-bundler
```

### コンテナ確認
-a: 停止しているコンテナも表示
```
docker ps
```

### docker commit でイメージ化する
```
docker commit [コンテナID] [つけたいコンテナ名]:[つけたいタグ名]
```

### イメージ化したコンテナの起動例
例)  
my-ruby: コンテナ名  
commit: タグ名
```
docker run -it my-ruby:commit bash
```
※ docker commitでイメージ化するのは望ましくない  
手作業で環境構築してしまうとどのようにつくったのかわからない  
よって、Dockerfileを使う  
イメージ構築手順をコード化: Infrastructure as Code

## Dockerfile
### Dockerfile例
```
FROM ubuntu:20.04 // base image

RUN apt update
RUN apt install -y ruby ruby-bundler  // -y: インストール時のY/n
```

### Dockerfile build
.: 忘れないでつける
```
docker build -t [コンテナ名]:[タグ名] .
```

## ボリュームによるファイルの共有
$PWD: 現在のディレクトリ
-w: ホストとコンテナ内のディレクトリを紐づける
```
docker run -it -v ${PWD}/opt/myapp -w /opt/myapp my-ruby:dockerfile bash
docker run -v ${PWD}/opt/myapp -w /opt/myapp my-ruby:dockerfile ruby hello.rb
docker run -v ${PWD}/sinatra:/opt/myapp -w /opt/myapp -d -p 4567:4567 my-ruby:dockerfile ruby myapp.rb -o 0.0.0.0
```

