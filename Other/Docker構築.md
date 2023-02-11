# Docker構築
## 概要
Docker構築手順
## 詳細
### URL
https://www.docker.com/products/docker-desktop/

## チュートリアル

### リポジトリのクローン
Getting Startedプロジェクトは、イメージをビルドし、コンテナとして実行するために必要なすべてのものを含む、シンプルなGitHubリポジトリです。

```docker
docker run --name repo alpine/git clone https://github.com/docker/getting-started.git
docker cp repo:/git/getting-started/ .
```

### イメージの構築
Dockerイメージは、あなたのコンテナのためのプライベートなファイルシステムです。これは、コンテナに必要なすべてのファイルとコードを提供します。
```docker
getting-started>docker build -t docker101tutorial .
```

### コンテナ実行
前のステップで構築したイメージに基づき、コンテナを起動します。コンテナを実行すると、マシンの他の部分から安全に分離されたプライベートなリソースでアプリケーションが起動します。
```docker
docker run -d -p 80:80 --name docker-tutorial docker101tutorial
```

### イメージを保存して共有する
Docker Hubにイメージを保存して共有することで、他のユーザーが簡単にイメージをダウンロードして、任意の宛先マシンで実行できるようになります。