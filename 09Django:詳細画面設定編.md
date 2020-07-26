# Djangoの勉強録
+ 参考サイト
> [Django入門](http://www.tohoho-web.com/ex/django.html)
# 詳細画面
+ HTML作成

./templates/books/detail_book.htmlを作成
```
{% extends 'layout.html' %}
{% block content %}
<table>
  <tr><th>Book ID</th><td>{{ book.book_id }}</td></tr>
  <tr><th>Title</th><td>{{ book.title }}</td></tr>
  <tr><th>Author</th><td>{{ book.author }}</td></tr>
</table>
<div class="basic-block">
  <button onclick="location.href='/books/'">Return</button>
</div>
{% endblock %}
```
+ ビューファイル追記

./apps/books/views.pyに以下を追加
```
def detail_book(request, book_id):
    try:
        book = Book.objects.get(book_id=book_id)
    except Book.DoesNotExist:
        book = None

    context = {
        'title': 'Detail Book',
        'book': book,
    }
    template = loader.get_template('books/detail_book.html')
    return HttpResponse(template.render(context, request))
```
+ urls.py に登録

./apps/books/urls.pyに以下を追加
```
urlpatterns = [
    path('', views.list_books, name='list_books'),
    path('<str:book_id>', views.detail_book, name='detail_book'),
]
```
+ 開発サーバーの起動
```
python manage.py runserver
```
ブラウザで http://127.0.0.1:8000/books/ にアクセスして、Book ID のリンクをクリックして、詳細画面が表示されれば成功
