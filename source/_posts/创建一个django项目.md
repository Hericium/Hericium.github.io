---
title: 创建一个django项目
date: 2019-03-07 20:14:49
tags: python
---

> 记录创建一个django项目的注意点

# 1.创建项目 

1.在Pycharm里面新建一个django项目,并且选择环境
或者
```
django-admin startproject project
```

2.安装django


```  
  pip install django  
  pip install django==1.11 #指定版本
```

3.新建一个项目

```
django-admin startapp project 
```
<!-- more -->

4.在生成的project同级创建templates,用来放置HTML模板,配置
```
# 本块代码位于：settings.py
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [
            os.path.join(BASE_DIR,'templates')
        ],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```
5.修改中文语言和时区
```
# 本块代码位于：settings.py

LANGUAGE_CODE = 'zh-hans'

TIME_ZONE = 'Asia/Shanghai'
```
6.设置静态文件路径,static文件夹，用于放置静态文件

```
# 本块代码位于：settings.py

STATIC_URL = '/static/'
STATICFILES_DIRS = (
    os.path.join(BASE_DIR,"static"),
)

```

7.设置媒体文件路径
```
# 本块代码位于：settings.py

MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR,'media')

```

8.启动项目
 ```
  python manage.py runserver
 ```

9.应用数据模型

```
# 本块代码位于：settings.py

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME':'xxx',
        'USER':'xxx',
        'PASSWORD':'xxx',
        'HOST':'127.0.0.1',
        'PORT':'3306'
    }
}

```

10.安装 mysql

```
 pip install MySQL-python
```

11.创建数据库, 迁移数据库
  ```
# 本块代码位于：videolearn\videolearn\settings.py
# 添加app
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'project'
]

# bash
$ python manage.py makemigrations 
$ python manage.py migrate
 
  ```

12.django命令

```
python manage.py -h :查看命令;
例如：
changepassword：用于更改用户密码；
createsuperuser：用于创建超级用户，后台管理员；
dbshell：用于进入 Django 模型 shell 中；
loaddata：用于从文件中加载数据；
migrate：用于检测数据模型的改变；
makemigtations：用于创建数据模型改变的迁移；
startapp：用于创建一个 Django 应用；
startproject：用于创建一个 Django 项目；
collectstatic：用于收集汇总静态文件；
runserver：运行自带调试服务器，默认运行在本地 8000 端口之上
```
