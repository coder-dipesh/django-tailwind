# django-tailwind setup :rocket:

### Create django app

<hr>

Create virtual environment
   
```
virtualenv env
```
Activate virtual environment

```
./env/Scripts/activate
```

Install django in virtual environment

```
pip install django
```

Check the installed version

```
django-admin --version
```

Create new django project to work with tailwind 

```
django-admin startproject yourAppName
```

<hr>

### Install `django-tailwind`

<hr>

Install django-tailwind

```
python -m pip install django-tailwind
```



After installing django-tailwind

Add `'tailwind'` to `INSTALLED_APPS` in `settings.py`:

```
INSTALLED_APPS = [
  # other Django apps
  'tailwind',
]
```


Create a Tailwind CSS compatible Django app, I like to call it theme:

```
python manage.py tailwind init
```

Add your newly created `'theme'` app to `INSTALLED_APPS` in `settings.py`:

```
INSTALLED_APPS = [
  # other Django apps
  'tailwind',
  'theme'
]
```

Register the generated `'theme'` app by adding the following line to `settings.py` file:

```
TAILWIND_APP_NAME = 'theme'
```



Make sure that the `INTERNAL_IPS` list is present in the `settings.py` file and contains the `127.0.0.1` ip address:

```
INTERNAL_IPS = [
    "127.0.0.1",
]
```

Install Tailwind CSS dependencies, by running the following command:

Before running below command don't forgot to add `NPM_BIN_PATH= r"C:\Program Files\nodejs\npm.cmd"` in your `settings.py`

`Note: You must have installed Node.js in your system`


```
python manage.py tailwind install
```


Load this commands in your `templates` base file

```
{% load tailwind_tags %}
...
<head>
   ...
   {% tailwind_css %}
   ...
</head>
```

Let’s also add and configure `django_browser_reload`, which takes care of automatic page and css refreshes in the development mode. Add it to `INSTALLED_APPS` in `settings.py`:

[Read More](https://django-tailwind.readthedocs.io/en/latest/django_browser_reload.html)

```
INSTALLED_APPS = [
  # other Django apps
  'tailwind',
  'theme',
  'django_browser_reload'
]
```

Staying in `settings.py`, add the middleware:

```
MIDDLEWARE = [
  # ...
  "django_browser_reload.middleware.BrowserReloadMiddleware",
  # ...
]
```

Include `django_browser_reload` URL in your root `url.py`:

```
from django.urls import include, path
urlpatterns = [
    ...,
    path("__reload__/", include("django_browser_reload.urls")),
]
```

Finally, you should be able to use Tailwind CSS classes in HTML. Start the development server by running the following command in your terminal:

```
python manage.py tailwind start
```
