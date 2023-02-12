# Docker構築
## 概要
Docker構築手順
## URL
https://www.docker.com/products/docker-desktop/

## Dockerfile
Dockerfile: Dockerイメージを作成するために必要な設定ファイル  
ファイル名：Dockerfile
ファイルの中身
```txt
FROM nginx
```
FROM イメージの元となるイメージを指定
nginxはWebサーバの一つ  

### Dockerfile１からイメージ作成
-t: イメージに名前を付ける  
例ではnginx  
. は、現在のディレクトを指す
```docker
docker build オプション パス
例：docker build -t nginx .
```


### バージョン
```docker
docker --version
```

### コンテナ起動
```docker
docker run コンテナ名
```

### コンテナ操作
root@のようになれば、OK  
Linuxコンテナを捜査している状態  
抜けるにはCtrl + c
```docker
docker run -it ubuntu bash
```

### Dockerイメージダウンロード
```docker
docker pull イメージ名
```

### Dockerイメージの一覧確認
```docker
docker image ls
```

### Dcokerイメージのコンテナ起動
httpdというコンテナを起動  
-p: ローカルとコンテナのポートを紐づけ  
ローカル80ポートアクセスとコンテナの80ポートにアクセス
```docker
docker run -p 80:80 httpd
http://127.0.0.1:80
```
