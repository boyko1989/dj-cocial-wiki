# Пояснения по файлу настроек

## Секция установленных приложений

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

+ django.contrib.admin
+ django.contrib.auth
+ django.contrib.contenttypes
+ django.contrib.sessions
+ django.contrib.messages
+ **[django.contrib.staticfiles](https://docs.djangoproject.com/en/4.1/ref/contrib/staticfiles/#module-django.contrib.staticfiles)** - приложение для работы со статическими файлами. Благодаря ему можно собрать все файлы HTML, CSS, JS в одном каталоге.
