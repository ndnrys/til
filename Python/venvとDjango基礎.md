# venvとDjango基礎
## 概要
Pythonの仮想環境のコマンドやDjangoの基礎  
djangogirlsで学習
## 仮想環境関連

### venv仮想環境作成
```pwsh
py -m venv 仮想環境名
py -m venv myvenv
```

### 仮想環境起動
```pwsh
\venvで作成したディレクトリ名\Scripts\activate
\myvenv\Scripts\activate
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
django-admin.exe startproject mysite .
```
以下の構成になる  
djangogirls  
├── manage.py  
├── mysite  
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
py manage.py startapp blog
```
以下の構成になる
djangogirls  
├── blog  
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

## Django基礎
__: アンダーバー２つ、呼び方はダンダー（ダブルアンダースコア）

### 新しいモデルをDjangoに登録する
```pwsh
py manage.py makemigrations アプリ名
py manage.py makemigrations blog
```

### Djangoが作った移行ファイルをDBに追加
```pwsh
py manage.py migrate アプリ名
py manage.py migrate blog
```

### 管理者アカウント作成
```pwsh
py manage.py createsuperuser
```

### PythonAnywhereとgithubの連携について
参考：https://ios-docs.dev/20210813support-for-password/  
ユーザー名はgithubのもの
パスワードは上記サイトの操作をしたトークンを実行
```pwsh
pa_autoconfigure_django.py --python=3.6 https://github.com/<your-github-username>/my-first-blog.git
```

### Django Shell起動
```pwsh
python manage.py shell
```

### Post Select
```py
from blog.models import Post
Post.objects.all()
```

### Post Insert
```py
from django.contrib.auth.models import User
me = User.objects.get(username='ola')
Post.objects.create(author=me, title='Sample title', text='Test')
```

### Post Select - 条件付き
```py
# titleを含む情報を抽出
Post.objects.filter(title__contains='title')
# 現在より以前の情報を抽出
from django.utils import timezone
Post.objects.filter(published_date__lte=timezone.now())
```
### 公開
```py
 post = Post.objects.get(title="Sample title")
 post.publish()
 ```

 ### ソート
 ```py
 # 昇順
 Post.objects.order_by('created_date')
 # 降順
 Post.objects.order_by('-created_date')
 ```

 ### メソッドチェーンによる複雑なクエリ
 ```py
 Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
 ```
