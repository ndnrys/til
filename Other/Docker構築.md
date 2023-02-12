# Docker構築
## 概要
Docker構築手順
## 詳細
### URL
https://www.docker.com/products/docker-desktop/

### バージョン
```docker
docker --vershion
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
