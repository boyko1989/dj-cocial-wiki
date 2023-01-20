# Работа с приложениями

Новое приложение в Django создаётся командой `python manage.py <app_name>`. Однако этого мало, нужно добавить его в файле `settings.py` в массив `INSTALLED_APPS`. Также мы установили множество дополнительных пакетов, которые также выступают в роли приложений. Их точно также нужно прописать в эту константу.

Что касается наших приложений, то безусловно, можно сделать простую запись, просто используя то имя, которое мы ввели как параметр в команде создания. Работать будет, но медленнее. Поэтому лучше отправить фреймворк сразу на точку, где указывается ID интересующего приложения - это `<app_name>/apps.py::BlogConfig`. Поэтому для приложения *blog* будет следующая запись: `'blog.apps.BlogConfig',`.

Запятую всё же лучше ставить, чтобы при дальнейшей работе на это не отвлекаться.

По тем приложениям, которые мы установили через пакеты, стоит сказать, что нужно перепроверять условия их работы. Например, может быть принципиальным на каком месте находится запись о пакете в `INSTALLED_APPS`. Это касается пакета `django-cleanup`, который должен быть прописан последним. Поэтому читаем документацию в особенности раздел **Installed** и **Configuration**.

Для проверки работоспособности после добавления приложений, нужно произвести миграции и собрать статику:

```shell
python manage.py makemigrations
python manage.py migrate
python manage.py collectstatic
```