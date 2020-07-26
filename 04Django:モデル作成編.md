# Djangoの勉強録
+ 参考サイト
> [Django入門](http://www.tohoho-web.com/ex/django.html)
> [returnの解説](https://techacademy.jp/magazine/18886)
> [classのお勉強](https://techacademy.jp/magazine/20615)
> [class defの解説](https://techacademy.jp/magazine/15637)
# 本(Book)を管理するモデル作成
+ モデル属性の定義。

本(Book)は、管理番号(book_id)、タイトル(title)、著者(author)の属性を持つものと定義。
./apps/books/models.pyを編集。
```
from django.db import models
class Book(models.Model):
    book_id = models.CharField(max_length=32)
    title = models.CharField(max_length=256)
    author = models.CharField(max_length=256)

    def __str__(self):
        return self.title
```
+ マイグレーションの実行

マイグレーション：DBの中身を一括して移行したり変更する作業のこと。
models.pyを自動的に読み取り、モデルで定義したテーブルやカラムを自動的に作成することができる。テーブルやカラムを変更して再度マイグレーションを行うことで、テーブル追加やカラム追加がマイグレーションされる。
```
$ python manage.py makemigrations
$ python manage.py migrate
```
+ 管理者サイトの使用

DBの情報などを管理しやすいよう②、あらかじめ作っているデータ操作画面。Modelのデータ追加、変更、削除などの管理をGUIで操作可能となる。
```
$ python manage.py createsuperuser
Username (leave blank to use 'root'): admin
Email address: admin@example.com
Password: ***password***
Password (again): ***password***
Superuser created successfully.
```
+ Books Appsのモデルを管理者サイトで管理できるようにする。

./apps/books/admin.pyを編集。
```
from django.contrib import admin
from .models import Book
admin.site.register(Book)
```
+ 開発サーバーの起動
```
python manage.py runserver
```
ブラウザで http://127.,0.0.1:8000/admin/ にアクセスし、管理用画面が表示されれば成功。
