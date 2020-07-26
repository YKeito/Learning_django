# Djangoの勉強録
+ 参考サイト
> [Django入門](http://www.tohoho-web.com/ex/django.html)
> [osモジュール](https://qiita.com/No_217/items/fb605d55c3db564727a1)
> [os path joinとは](https://www.sejuku.net/blog/64408)
# アプリケーションディレクトリの集約
+ ディレクトリの整理

Django の標準では BASE_DIR(./) 直下にAppsディレクトリが乱雑に並んでしまう。
今回はbooksだけだが、A, B, c ..と複数のAppsを作成したとき邪魔くさい。そこで、Appsを集約して格納するための ./apps ディレクトリを用意。
```
$ mkdir ./apps
```
+ ./appsに集約したAppsを使えるようにする

./apps ディレクトリを ./config/settings.py に登録。
```
import os
import sys

BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
sys.path.insert(0, os.path.join(BASE_DIR, 'apps'))
```
`os.path.dirname()`は, 引数で渡したパス名からディレクトリ名の部分だけ抜き出す関数
`os.path.abspath()`は引数で与えたパス名の絶対パスを取得する関数
`os.path.join()`は引数に与えられた二つの文字列を結合させ、一つのパスにする関数

+ Appsディレクトリを ./apps 配下に移動
```
$ mv ./books ./apps
```
+ 開発サーバーの起動
```
python manage.py runserver
```
ブラウザで http://127.0.0.1:8000/books/ にアクセスして Hello world! が表示されれば成功。
