# Django 数据库操作

## 从现有数据库自动生成 Model

命令是

```python
python manage.py inspectdb #运行后会把表生成的model结构打印出来
python manage.py inspectdb > app/models.py #这一步是将上一步生成的写入文件
```

数据库基础设置在 settings.py 文件中，default 名必须存在，否则会报错。

django 数据库配置文件：

```python
DATABASES = {
    # 'default': {
    #     'ENGINE': 'django.db.backends.sqlite3',
    #     'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    # },
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME':'xxxxxxxx',
        'HOST':'xx.xx.xx.xx',
        'USER':'root',
        'PASSWORD':'xxxxxxxxxxxx',
        'PORT':'3306',

    },

}
```

