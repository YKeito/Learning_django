# Djangoの勉強録
+ 参考サイト
> [Django入門](http://www.tohoho-web.com/ex/django.html)
# http://127.,0.0.1:8000/books/ にアクセスしてHello world!を表示させる
+ ./config/settings.py編集 : Books.appsを定義
./books/apps.py に定義されたクラス名をアプリケーションとして ./config/settings.py の INSTALLED_APPS に登録。
```
INSTALLED_APPS = [
     'books.apps.BooksConfig', 
    'django.contrib.admin',
    'django.contrib.auth',
    .
    .
```
+ ./config/urls.py編集 : http://127.,0.0.1:8000/以降のurls表示を定義
./config/urls.py に、http://127.,0.0.1:8000/... が要求されたら、./books/urls.py を参照するように指定。
```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('books/', include('books.urls')),
]
```
`include('books.urls')`は./books/urls.pyを参照するという意味
+  ./books/urls.py編集 : http://127.,0.0.1:8000/...の表示を定義
./books/urls.py ファイルを新規に作成し、http://サーバアドレス/books/ の次に何もなければ、view.py の list_books 関数を呼び出すように指定。
```
from django.urls import path
from . import views

urlpatterns = [
    path('', views.list_books, name='list_books'),
]
```
+ ./books/views.py編集 : 
下記の様に修正。
```
from django.http import HttpResponse

def list_books(request):
    return HttpResponse("Hello world!")
```
+ 開発サーバーの起動
```
python manage.py runserver
```
ブラウザで http://サーバアドレス/books/ にアクセスして Hello world! が表示されれば成功。
