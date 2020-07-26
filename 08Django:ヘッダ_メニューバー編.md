# Djangoの勉強録
+ 参考サイト
> [Django入門](http://www.tohoho-web.com/ex/django.html)

# ヘッダやメニューバーの表示
+ ヘッダやメニューバーを追加

./templates/layout.htmlに以下を追加
```
<body>
  <div class="header-block">
    @ Django Sample
  </div>
  <div class="menu-block">
    <a href="/books/">Book</a>
    <a href="/settings/">Settings</a>
  </div>
  <div class="content-block">
    <h1>{{ title }}</h1>
    {% block content %}{% endblock %}
  </div>
</body>
```
+ ヘッダやメニュー追加のためのスタイルを追記

./static/css/style.cssに以下を追加
* { margin: 0; padding: 0; }
.header-block { background-color: #000; color: #fff; line-height: 2rem;
    font-weight: bold; padding: 0 .5rem; }
.menu-block { background-color: #ddd; line-height: 2rem; padding: 0 .5rem; }
.content-block { padding: 0 .5rem; }
table { border-collapse: collapse; margin-bottom: .5rem; }
+ 開発サーバーの起動
```
python manage.py runserver
```
ブラウザで http://127.0.0.1:8000/books/ にアクセスして ヘッダやメニューが表示されれば成功。
