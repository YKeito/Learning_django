# Djangoの勉強録
+ 参考サイト
> [Django入門](http://www.tohoho-web.com/ex/django.html)
# テンプレートで共通なレイアウトページを参照する
+ 複数のテンプレートで共有するレイアウトを作成
{% block %} や extends を用いて、複数のテンプレートで共有するレイアウトを作成することができる。子テンプレート(list_books.html)で定義した title や content というブロックを、親テンプレート(layout.html)が参照して表示します。まず、./templates/layout.html を新規作成。
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>{{ title }}</title>
</head>
<body>
  <h1>{{ title }}</h1>
  {% block content %}{% endblock %}
</body>
</html>
```

./templates/books/list_books.htmlに下記を追記。
```
{% extends 'layout.html' %}
{% block content %}
<table>
  :
</table>
{% endblock %}
```
+ 開発サーバーの起動
```
python manage.py runserver
```
ブラウザで http://127.,0.0.1:8000/books/ にアクセスして 「List Books」のタイトルが表示されれば成功。
