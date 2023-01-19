# Файл настроек settings.py

Наиболее рациональным будет следующий порядок работы с данным файлом в начале работы над проектом:

## Настройка разрешённых адресов

[Документация](https://docs.djangoproject.com/en/4.1/ref/settings/#allowed-hosts)

```python
ALLOWED_HOSTS = []
```

В списке нужно прописать список доменных имён и/или IP-адресов, с которых можно будет обратиться к нашему проекту. Это очень повышает защиту веб-приложения. Если нужно обартиться со всех адресов, то прописывается звёздочка (`'*'`)

## Работа со статикой

[Документация](https://docs.djangoproject.com/en/4.1/howto/static-files/)

[Документация про константы](https://docs.djangoproject.com/en/4.1/ref/settings/)

Нужно, чтобы были прописаны константы
+ STATIC_ROOT
+ STATIC_URL
+ STATICFILES_FINDERS

**STATIC_ROOT** - это папка в которой будут складываться все статические файлы. Собрать их можно [командой](https://docs.djangoproject.com/en/4.1/ref/contrib/staticfiles/#django-admin-collectstatic) `collectstatic`. Однако, необходимо произвести настройку `STATICFILES_FINDERS` Мы же прописываем
```python
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```

**STATICFILES_FINDERS** - массив утилит, которые могут обойти весь проект и собрать всю статику в одно место, указанное в *STATIC_ROOT*:

```python
[
    'django.contrib.staticfiles.finders.FileSystemFinder',
    'django.contrib.staticfiles.finders.AppDirectoriesFinder',
]
```

**STATIC_URL** - URI, по которому Django будет обращаться к статике. По умолчанию - это `static/`

После этого выполняем команду `python manage.py collectstatic` и вся уже имеющаяся на данный момент статика собирается по указанным путям.

В дальнейшем у нас будет расти количество приложений и чтобы Django было проще найти все статические файлы, можно будет указать из в [константе](https://docs.djangoproject.com/en/4.1/ref/settings/#std-setting-STATICFILES_DIRS) **STATICFILES_DIRS**

```python
STATICFILES_DIRS = [
    "/home/special.polls.com/polls/static",
    "/home/polls.com/polls/static",
    "/opt/webfiles/common",
]
```

## Настройка работы с медиафайлами

+ В файле `urls.py` в самой первой строчке прописываем:

```python
# -*- coding: utf-8 -*-
```
Это позволит обрабатывать кириллические названия медиафайлов, то есть тех, которые загружает пользователь.

+ В этом же файле прописываем следующее условие:
```python
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

Оно нужно для того, чтобы в debug-режиме можно было производить отладку приложения и совместно с пользовательскими данными.

+ Добавляем следующие импорты, чтобы вышеприведёный код работал:
```python
from django.conf.urls.static import static
from django.conf import settings
```

+ Добавляем в наш проект каталог `media/`
+ В файле `settings.py` добавляем следующие константы:

```python
import os.path

MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

## Производим необходимые миграции

Сначала проверяем не изменили ли мы модели объектов Django:

```python
python manage.py makemigrations
```

Скорее всего напишет, что никаких изменений не было. Следом вводим вторую команду:

```python
python manage.py migrate
```

Получив:
```shell
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying auth.0012_alter_user_first_name_max_length... OK
  Applying sessions.0001_initial... OK
```
Переходим к следующему шагу. Стоит только упомянуть, что при каждой миграции в процессе изучения или экспериментов, можно в константе `DATABASES` в поле имени базы данных постоянно прописывать новое имя, чтобы была возможность "откатиться".

## Создаём суперпользователя

```shell
python ../manage.py createsuperuser
```
```shell
Имя пользователя (leave blank to use 'p_boyko'): admin
Адрес электронной почты: jwbpa@yandex.ru
Password:
Password (again):
Superuser created successfully.
```

## Запуск сервера

```shell
python manage.py runserver
```

В браузере будет открыта главная страница..., которой нет (404 ответ), так как в файле `urls.py` мы не прописали путь до неё. Нам же нужно будет перейти по URL `http://<domain_IP>/admin/` и ввести логин/пароль, которые мы придумали на предыдущем шаге.
