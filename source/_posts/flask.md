---
title: flask
date: 2018-12-14 09:13:26
tags:
---

# flask初体验 #
## 开发环境 ##
windows10、pycharm、mysql、python3
## 开发过程 ##
1. 打开pycharm，新建flask项目
2. 安装插件mysql-connector-python、Flask-SQLAlchemy、Flask-Script、Flask-Migrate
3. 配置数据库：a. 新建config.py

```
DIALECT = 'mysql'
DRIVER = 'mysqlconnector'
USERNAME = 'root'
PASSWORD = 'gwq091201211'
HOST = '127.0.0.1'
PORT = '3306'
DATABASE = 'myapp'

SQLALCHEMY_DATABASE_URI = "{}+{}://{}:{}@{}:{}/{}?charset=utf8".format(
	DIALECT, DRIVER, USERNAME, PASSWORD, HOST, PORT, DATABASE)

SQLALCHEMY_TRACK_MODIFICATIONS = False


```
b. 新建db.py

```
from flask_sqlalchemy import SQLAlchemy
db = SQLAlchemy()
```
c. 新建model.py
 
```
from ext import ext


class Tag(db.Model):
    __tablename__='tag'
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    name = db.Column(db.String(20), nullable=False)


class Article(db.Model):
    __tablename__ = 'article'
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    title = db.Column(db.String(50), nullable=False)
    content = db.Column(db.Text)
    tags = db.relationship('Tag', secondary='tag_article', backref=db.backref('articles'))


tag_article = db.Table(
    'tag_article',
    db.Column('tag_id', db.Integer, db.ForeignKey('tag.id'), primary_key=True),
    db.Column('article_id', db.Integer, db.ForeignKey('article.id'), primary_key=True)
)

```
d.新建manage.py

```
from flask_script import Manager
from flask_migrate import Migrate, MigrateCommand
from ext import db
from app import app
from model import Article, Tag
manager = Manager(app)
migrate = Migrate(app, db)
manager.add_command('db', MigrateCommand)

if __name__ == '__main__':
    manager.run()

```
**注：**要import所使用的model，注意`'__main__'`名称不能写错

e.主程序 app.py
创建Flask实例app，app设定数据库，db绑定app

```
from flask import Flask
from ext import db
import settings

app = Flask(__name__)
app.config.from_object(settings)
db.init_app(app)
```