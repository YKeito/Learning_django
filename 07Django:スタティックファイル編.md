# Djangoの勉強録
+ 参考サイト
> [Django入門](http://www.tohoho-web.com/ex/django.html)
# スタティックファイルを読み込む
CSS や JavaScript などのスタティックファイルを格納するスタティックディレクトリ(./static)を作成。
```
$ mkdir ./static
$ mkdir ./static/css ./static/js ./static/img
```
./static を ./config/settings.py に登録。
```
    :
STATIC_URL = '/static/'

STATICFILES_DIRS = (
    os.path.join(BASE_DIR, 'static'),
)
```
./static/css/style.css ファイルを作成。

```
table { border-collapse: collapse; margin-bottom: .5rem; }
table th, table td { border: 1px solid #999; padding: .1rem .3rem; }
table th { background-color: #ddd; }
button { line-height: 1.2rem; min-width: 6rem; }
```

./templates/layout.htmlから style.css を読み込ませる。
```
<head>
<meta charset="utf-8">
<title>{{ title }}</title>
<link rel="stylesheet" href="/static/css/style.css">
</head>
```
+ 開発サーバーの起動
```
python manage.py runserver
```
ブラウザで http://127.0.0.1:8000/books/ にアクセスして 表の枠線が表示されたら成功
