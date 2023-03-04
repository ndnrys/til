# venv
## 概要
Pythonの仮想環境のコマンドなど
## 詳細

### venv仮想環境作成
```pwsh
py -m venv 仮想環境名
```

### 仮想環境起動
```pwsh
venvで作成したディレクトリ名\Scripts\activate
```

### pipインストール
```pwsh
py -m pip install --upgrade pip
```

### requirementsファイルによってパッケージをインストールする
requirementsファイルは pip install でインストールする依存関係の一覧が記載されているファイル

作成したディレクトリ  
├── myvenv  
│   └── ...  
└─── requirements.txt

作成したディレクトリにrequirements.txt追加
```txt requirements.txt
Django~=3.2.10
```

### Djangoインストール
```pwsh
pip install -r requirements.txt
```

### プロジェクト作成
```pwsh
django-admin.exe startproject プロジェクト名 .
```
以下の構成になる  
djangogirls  
├── manage.py  
├── プロジェクト名  
│   ├── __init__.py  
│   ├── settings.py  
│   ├── urls.py  
│   └── wsgi.py  
├── myvenv  
│   └── ...  
└── requirements.txt  

manage.py: インストールすることなくコンピュータ上でWebサーバーを起動することができる  
settings.py: ウェブサイトの設定  
urls.py: urlresolver(Djangoがviewを見つける仕組み)で使われるパターンリスト  

### 設定変更
タイムゾーン変更
```py settings.py
TIME_ZONE = 'Asia/Tokyo'
```
言語変更
```py settings.py
LANGUAGE_CODE = 'ja'
```
静的ファイルパスの追加  
STATIC_ROOTをSTATIC_URLの下に入力
```py settings.py
STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR / 'static'
```
DEBUG: True + ALLOWED_HOSTSが空の場合、自動的に['localhost', '127.0.0.1', '[::1]']の3ホストに対してチェックされる  
これから使うPythonAnywhereのホストネームが含まれていないため、以下を設定
```py settings.py
ALLOWED_HOSTS = ['127.0.0.1', '.pythonanywhere.com']
```

### DBセットアップ
すでに書かれている（sqlite3）
```py settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

セットアップ実行
```pwsh
py manage.py migrate
```

### サーバー起動確認
manage.pyがあるディレクトリに移動
```pwsh
py manage.py runserver
```
以下にアクセス  
`http://127.0.0.1:8000/`  
Ctrl + Breakで停止

### アプリケーションの作成
```pwsh
py manage.py startapp アプリ名
```
以下の構成になる
djangogirls  
├── アプリ名  
│   ├── admin.py  
│   ├── apps.py  
│   ├── __init__.py  
│   ├── migrations  
│   │   └── __init__.py  
│   ├── models.py  
│   ├── tests.py  
│   └── views.py  
├── db.sqlite3  
├── manage.py  
├── mysite  
│   ├── __init__.py  
│   ├── settings.py  
│   ├── urls.py  
│   └── wsgi.py  
├── myvenv  
│   └── ...  
└── requirements.txt  

```py mysite/settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog.apps.BlogConfig', # 追加
]
```

続き：  
https://tutorial.djangogirls.org/ja/django_models/#%E3%83%96%E3%83%AD%E3%82%B0%E3%83%9D%E3%82%B9%E3%83%88%E3%83%A2%E3%83%87%E3%83%AB%E3%81%AE%E4%BD%9C%E6%88%90