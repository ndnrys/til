# venv
## 概要
Pythonの仮想環境のコマンドなど
## 詳細

### venv仮想環境作成
```cmd
py -m venv 仮想環境名
```

### 仮想環境起動
```cmd
venvで作成したディレクトリ名\Scripts\activate
```

### pipインストール
```cmd
py -m pip install --upgrade pip
```

### requirementsファイルによってパッケージをインストールする
requirementsファイルは pip install でインストールする依存関係の一覧が記載されているファイル

作成したディレクトリ  
├── myvenv  
│   └── ...  
└─── requirements.txt

作成したディレクトリにrequirements.txt追加
```txt
Django~=3.2.10
```

### Djangoインストール
```cmd
pip install -r requirements.txt
```

続き：  
https://tutorial.djangogirls.org/ja/django_start_project/