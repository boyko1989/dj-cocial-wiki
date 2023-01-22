# Jupiter Notebook

У меня будет использоваться именно **Notebook**, а не **JupyterLab**

Для этого согласно [руководству](https://jupyter.org/install) вводим следующую команду:

```shell
pip install notebook
```

Для интеграции Jupiter и Django нужно поставить расширение *django-extensions*

```shell
pip install django-extensions
```

В соответствии с [этим](https://django-extensions.readthedocs.io/en/latest/installation_instructions.html) прописываем приложение в `INSTALLED_APPS`, затем для поддержания асинхронности, добавляем в `serrings.py` следующую строку:

```python
os.environ['DJANGO_ALLOW_ASYNC_UNSAFE'] = 'true'
```

Командой `python manage.py shell_plus --notebook`  запускаем сервер Jupiter. Нас должно перекинуть в браузер.

Создаём новый `Django Shell-Plus` и можем приступать к написанию команд.

## Темы Jupiter

[Здесь](https://github.com/dunovank/jupyter-themes) можно посмотреть как установить темы для Jupiter:

```shell
pip install jupyterthemes
```

Командой `jt -l` выводим список тем,
выбираем одну из них  и устанавливаем `jt -t <theme_name>`. Командой `jt -r` сбрасываем тему в дефолт.

**Светлыми темами являются:**

- grade3
- gruvboxl      (песочный)
- solarisedl    (песочный)

**Тёмные:**

- chesterish
- gruvboxd
- monokai
- oceans16
- onedork
- solarizedd

При помощи этого пакета также можно изменить шрифт.

## Автозавершение кода

Установим `jupyter-tabnine`:

```shell
pip install jupyter-tabnine --user
jupyter nbextension install --py jupyter_tabnine --user
jupyter nbextension enable --py jupyter_tabnine --user
jupyter serverextension enable --py jupyter_tabnine --user
```

Чтобы не вызывались никакие ошибки доутсановим `python-language-server`:

```shell
pip install python-language-server
```

После перезагрузки сервера Jupiter всё должно работать очень хорошо.
