# Djangoの勉強録
+ 参考サイト
> [Django入門](http://www.tohoho-web.com/ex/django.html)
# Djangoのインストール
'''
$ pip install Django==2.2.9
$ python -m pip list
'''
以下が記述されたらOK
'''
Package         Version
--------------- -------
          .
          .
Django          2.2.9
          .
          .
'''
# プロジェクトの作成
+ 作業ディレクトリをDocumentsとする
'''
$ cd ~/Documents/myproj
'''
+ プロジェクトの作成
'''
$ django-admin startproject config
$ mv ./config ./myproj
$ cd ./myproj
'''
下記のファイルが作成される。
'''
./myproj
./myproj/manage.py
./myproj/config
./myproj/config/__init__.py
./myproj/config/settings.py
./myproj/config/urls.py
./myproj/config/wsgi.py
'''
# プロジェクトの設定ファイル
+ 言語設定とタイムゾーン設定
以下に変更
'''
LANGUAGE_CODE = 'ja-JP'
TIME_ZONE = 'Asia/Tokyo'
'''
# 
