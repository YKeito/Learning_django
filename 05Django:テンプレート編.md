# Djangoの勉強録
+ 参考サイト
> [Django入門](http://www.tohoho-web.com/ex/django.html)
# テンプレートを使用する
+ Book の一覧をテーブル表示

HTMLテンプレートを使用して Book の一覧をテーブル表示。
まず、テンプレートディレクトリを作成します。
```
$ mkdir ./templates
```
+ templatesのpathを通す

./templates を ./config/settings.py に登録。
```
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
        'APP_DIRS': True,
           :
    },
]
```
Books のためのテンプレートディレクトリを作成。
```
mkdir ./templates/books
```
+ HTML作成

./templates/books の下に list_books.html テンプレートファイルを作成。
```
<table>
  <thead>
    <tr>
      <th>Book ID</th>
      <th>Title</th>
      <th>Author</th>
      <th>Action</th>
    </tr>
  </thead>
  <tbody>
    {% if books %}
      {% for book in books %}
        <tr>
          <td><a href="/books/{{ book.book_id }}">{{ book.book_id }}</a></td>
          <td>{{ book.title }}</a></td>
          <td>{{ book.author }}</a></td>
          <td><a href="/books/{{ book.book_id }}/edit">[Edit]</a></td>
        </tr>
      {% endfor %}
    {% else %}
      <tr>
        <td colspan=4>No books.</td>
      </tr>
    {% endif %}
  </tbody>
</table>
```
+ 

./apps/books/views.py ファイルを下記の様に修正。

```
from django.http import HttpResponse
from django.template import loader
from .models import Book

def list_books(request):
    books = Book.objects.all()
    context = {
        'title': 'List Books',
        'books': books,
    }
    template = loader.get_template('books/list_books.html')
    return HttpResponse(template.render(context, request))
```


+ 開発サーバーの起動
```
python manage.py runserver
```
ブラウザで http://127.,0.0.1:8000/books/ にアクセスして Bookのテーブル一覧が表示されれば成功。
