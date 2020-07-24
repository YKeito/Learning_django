# Djangoの勉強録
+ 参考サイト
> [Django入門](http://www.tohoho-web.com/ex/django.html)
# Djangoのインストール

```
$ pip install Django==2.2.9
$ python -m pip list
```


以下が記述されたらOK
```
Package         Version
--------------- -------
          .
          .
Django          2.2.9
          .
          .
```
# プロジェクトの作成
+ 作業ディレクトリをDocumentsとする
```
$ cd ~/Documents/myproj
```
+ 実行するとプロジェクトに必要な雛形ファイルを作成configは任意の名前。
```
$ django-admin startproject config
$ mv ./config ./myproj
$ cd ./myproj
```
下記のファイルが作成される。
```
./myproj
./myproj/manage.py
./myproj/config
./myproj/config/__init__.py
./myproj/config/settings.py
./myproj/config/urls.py
./myproj/config/wsgi.py
```
# プロジェクトの設定ファイル
+ 言語設定とタイムゾーン設定
./config/setting.pyを開き、以下の内容に変更。
```
LANGUAGE_CODE = 'ja-JP'
TIME_ZONE = 'Asia/Tokyo'
```
# 開発サーバーの起動
```
$ cd myproj
$ python manage.py runserver
```
ブラウザで「 http://127.0.0.1:8000/ 」と入れ、インストール成功の画面が表示されるか確認。
# アプリケーション作成
```
python manage.py startapp books
```
下記のファイルが作成される。
```
./books/__init__.py
./books/admin.py
./books/apps.py
./books/models.py
./books/tests.py
./books/views.py
./books/migrations/__init__.py
```
![alt](https://drive.google.com/file/d/1E6OoBg7nxsfejg5S17hDejDAFHAoZ3SJ/view?usp=sharing)
