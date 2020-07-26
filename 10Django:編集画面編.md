# Djangoの勉強録
+ 参考サイト
> [Django入門](http://www.tohoho-web.com/ex/django.html)
# 編集画面
+ 編集画面作成のためのHTML

./templates/books/edit_book.htmlを作成します。
```
{% extends 'layout.html' %}
{% block content %}
<form method="POST" action="{% url 'edit_book' book.book_id %}">
  {% csrf_token %}
  <input type="hidden" name="mode" value="{{ mode }}">
  <table>
    <tr>
      <th>Book ID</th>
      <td><input type="text" name="book_id" readonly value="{{ book.book_id }}"></td>
    </tr>
    <tr>
      <th>Title</th>
      <td><input type="text" name="title"
          {% if mode != 'input' %}readonly{% endif %} value="{{ book.title }}"></td>
    </tr>
    <tr>
      <th>Author</th>
      <td><input type="text" name="author"
          {% if mode != 'input' %}readonly{% endif %} value="{{ book.author }}"></td>
    </tr>
  </table>
  <div class="basic-block">
    {% if mode == 'input' %}
      <button type="button" onclick="location.href='{% url 'list_books' %}'">Return</button>
      <button type="submit">OK</button>
    {% elif mode == 'confirm' %}
      <button type="button" onclick="history.back()">Back</button>
      <button type="submit">OK</button>
    {% elif mode == 'result' %}
      <button type="button" onclick="location.href='{% url 'list_books' %}'">Return</button>
    {% endif %}
  </div>
</form>
{% endblock %}
```
+ ビュー作成

./apps/books/views.pyに以下を追記
```
def edit_book_input(request, book_id):
    try:
        book = Book.objects.get(book_id=book_id)
    except Book.DoesNotExist:
        book = None

    context = {
        'title': 'Edit Book(input)',
        'mode': 'input',
        'book': book,
    }
    template = loader.get_template('books/edit_book.html')
    return HttpResponse(template.render(context, request))

def edit_book_confirm(request, book_id):
    book = Book()
    book.book_id = request.POST['book_id']
    book.title = request.POST['title']
    book.author = request.POST['author']

    context = {
        'title': 'Edit Book(confirm)',
        'mode': 'confirm',
        'warning_message': 'Are you sure you want to save?',
        'book': book,
    }
    template = loader.get_template('books/edit_book.html')
    return HttpResponse(template.render(context, request))

def edit_book_result(request, book_id):
    try:
        book = Book.objects.get(book_id=book_id)
        book.book_id = request.POST['book_id']
        book.title = request.POST['title']
        book.author = request.POST['author']
        book.save()
    except Book.DoesNotExist:
        book = None

    context = {
        'title': 'Edit Book(result)',
        'mode': 'result',
        'success_message': 'Success!',
        'book': book,
    }
    template = loader.get_template('books/edit_book.html')
    return HttpResponse(template.render(context, request))

def edit_book(request, book_id):
    if request.method == 'GET':
        return edit_book_input(request, book_id)
    elif request.method == 'POST':
        if request.POST['mode'] == 'input':
            return edit_book_confirm(request, book_id)
        if request.POST['mode'] == 'confirm':
            return edit_book_result(request, book_id)
```
+ ビューを urls.py に登録

./apps/books/urls.pyを以下に変更
```
urlpatterns = [
    path('', views.list_books, name='list_books'),
    path('<str:book_id>', views.detail_book, name='detail_book'),
    path('<str:book_id>/edit', views.edit_book, name='edit_book'),
]
```
+ メッセージ表示欄追加

./templates/layout.htmlにメッセージ表示欄を追加。
```
  <div class="content-block">
    <h1>{{ title }}</h1>
    {% if success_message %}
    <div class="msg-success">{{ success_message }}</div>
    {% endif %}
    {% if warning_message %}
    <div class="msg-warning">{{ warning_message }}</div>
    {% endif %}
    {% if error_message %}
    <div class="msg-error">{{ error_message }}</div>
    {% endif %}
    {% block content %}{% endblock %}
  </div>
```
+ スタイルを追加

./static/css/style.cssにスタイルを追加。
```
button { line-height: 1.2rem; min-width: 6rem; }
input[type="text"], select { border: 1px solid #ccc; height: 1.5rem;
    border-radius: .2rem; padding: 0 .3rem; width: 20rem; }
input[readonly] { border: 0; }
.msg-success { padding: .2rem; color: #080; border: 1px solid #9c9;
    background-color: #cfc; margin-bottom: .5rem; }
.msg-warning { padding: .2rem; color: #880; border: 1px solid #cc9;
    background-color: #ffc; margin-bottom: .5rem; }
.msg-error   { padding: .2rem; color: #800; border: 1px solid #c99;
    background-color: #fcc; margin-bottom: .5rem; }
```
+ 開発サーバーの起動
```
python manage.py runserver
```
ブラウザで http://127.0.0.1:8000/books/ にアクセスして、[Edit] のリンクをクリックして、編集操作ができれば成功。
