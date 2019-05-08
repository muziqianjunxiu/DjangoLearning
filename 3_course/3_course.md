# 第二节课

`pip list`	查看包安装列表

`python -m pip install --upgrade pip`	升级pip

`python -m pip install --upgrade virtualenv`	升级virtualenv

`django-admin	startproject	mysite`	创建**项目** `mysite` 

- ​	mysite                      python包
  - `__init__.py`		有这个文件，说明mysite是一个包，里面的文件都可以被其他地方引用
  - `settings.py`        项目的设置文件，**全局**设置文件
  - `urls.py`               路由控制，只有此处规定了的网址url，浏览器才可以访问，全局路由控制
  - `wsgi.py`              网站部署应用的文件，服务器使用
- ​    `manage.py`             Django项目管理文件

`python manage.py runserver`         启动服务（ctrl + c 关闭）

`python manage.py help`	查询帮助

```python
Available subcommands:

[auth]
    changepassword
    createsuperuser		#创建超级管理员

[contenttypes]
    remove_stale_contenttypes

[django]
    check
    compilemessages
    createcachetable
    dbshell
    diffsettings
    dumpdata
    flush
    inspectdb
    loaddata
    makemessages
    makemigrations
    migrate			#创建数据库文件
    sendtestemail
    shell
    showmigrations
    sqlflush
    sqlmigrate
    sqlsequencereset
    squashmigrations
    startapp
    startproject
    test
    testserver

[sessions]
    clearsessions

[staticfiles]
    collectstatic
    findstatic
    runserver
```

`python manage.py migrate`	创建数据库

`python manage.py createsuperuser`	创建admin管理员账户

# 第三节课

`python manage.py startapp 应用名称`	#创建**项目**的一个**应用**app

 	`python manage.py startapp article`

- ​	mysite
- ​    article
  - migrations
    - `__init__.py`
  - `__init__py`
  - `admin.py`             #设置应用在后台管理界面的展现
  - `apps.py`
  - `models.py`            #模型：定义页面显示的属性
  - `tests.py`
  - `views.py`
-   `manage.py`
- `db.sqlite3`

编辑`article\models.py`文件，自定义页面要显示哪些属性。

```python
class Article(models.Model):		#创建Article类，包含title和content两个属性
    title = models.CharField(max_length=30)	#CharField 字段类型
    content = models.TextField()	#TextField	字段类型
```

然后，要将应用名称（`article`）添加到 `mysite\settings.py` 的 `INSTALLED_APPS`中，记得要在结尾加逗号。

`python manage.py makemigrations`	制造数据库迁移文件

```python
Migrations for 'article':
  article\migrations\0001_initial.py
    - Create model Article
```

`python manage.py migrate`	将应用迁移至数据库

```python
Operations to perform:
  Apply all migrations: admin, article, auth, contenttypes, sessions
Running migrations:
  Applying article.0001_initial... OK
```

此时数据库文件 `db.sqlite3`中已经包含了models中创建的属性了。

设置`article\admin.py` 文件，设置应用在后台管理界面的展示

```python
from django.contrib import admin
from . models import Article
# Register your models here.
admin.site.register(Article)	#最快的方式注册应用的模型
```

将`admin`后台界面改为中文简体：

​	设置 `mysite\settings.py` 中的 `LANGUAGE_CODE = 'zh-Hans'`