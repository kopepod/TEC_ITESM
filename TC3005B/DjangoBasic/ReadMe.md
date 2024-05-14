# DjangoBasic

Based on https://djangocentral.com/create-a-hello-world-django-application/

```bash
Python 3.10.6 (main, Nov 14 2022, 16:10:14) [GCC 11.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import django
>>> django.VERSION
(3, 2, 17, 'final', 0)
>>> 
```

1. Install

```bash
pip install Django
```

2. Landing Page

```bash
mkdir project
cd project
django-admin startproject helloworld .
cd helloworld
python manage.py migrate
python manage.py runserver
tree
```

```bash
.
├── db.sqlite3
├── helloworld
│   ├── asgi.py
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── __init__.cpython-310.pyc
│   │   ├── settings.cpython-310.pyc
│   │   ├── urls.cpython-310.pyc
│   │   └── wsgi.cpython-310.pyc
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── manage.py


```

3. Creating APP

```bash
python manage.py startapp my_app
nano helloworld/settings.py
```

Add my_app the settings.py

```python
# django_project/settings.py
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "my_app",  # new
]
```

Modify the views.py file

```bash
nano my_app/views.py
```

```python
from django.shortcuts import render

# Create your views here.
from django.http import HttpResponse

def index(request):
    return HttpResponse('Hello, World!')

```

Modify the urls.py file

```bash
nano helloworld/urls.py
```

```python
"""helloworld URL Configuration

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/3.2/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
"""
from django.contrib import admin
from django.urls import path
from my_app import views # new

urlpatterns = [
    path('admin/', admin.site.urls),
    path('',views.index, name="homepage") # new
]
```

Run the server again

```bash
python manage.py runserver
```

4. Add HTML

```bash
mkdir my_app/templates
mkdir my_app/static
nano my_app/views.py
```

```python
from django.shortcuts import render

# Create your views here.
from django.http import HttpResponse
from django.template import loader #new

def index(request):
    template = loader.get_template('index.html')
    return HttpResponse(template.render())
```

```bash
python manage.py runserver
```

```bash
nano my_app/static/style.css
```

```css
.landing-section {
  min-height: 100vh;
  width: 100vw;
}


.landing-section {
  min-height: 100vh;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
} 

.landing-main { 
  background: url(https://github.com/kopepod/TEC_ITESM/blob/main/TC3005B/DjangoBasic/Background.jpg?raw=true) no-repeat center center fixed; 
  background-size: cover;
}


.landing-section-content {
  padding: 2rem;
  background: rgba(0,0,0,0.5);
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  color: #ccc;
}

.brand {
  margin: 0;
  color: #c55e00;
}

.brand-text {
  color: #c55e00;
}


.header {
  width: 100vw;
  display: flex;
  justify-content: flex-end;
  top: 0;
  left: 0;
  position: absolute;

  background: rgba(0,0,0,0.5);
}

.header-link {
  margin: 1rem;
  border-bottom: 3px solid #c55e00;
  font-size: 1.2rem;
  color: #222;
  text-decoration: none;
  color: #ccc;
}

.header-text {
  margin: 1rem;
  font-size: 1.2rem;
  color: #ccc;
}

```

```bash
nano my_app/templates/index.html
```

```html
{% load static %}
<title>Kopepod Django example</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="stylesheet" type="text/css" href="{% static 'style.css' %}">

<header class="header">
  <div class="header-text">Sign in via:</div>
  <a href="#" class="header-link">MySpace</a>
  <a href="#" class="header-link">Mail.ru</a>
</header>
<section class="landing-section landing-main">
  <div class="landing-section-content">
    <h1 class="brand">Kopepod</h1>
    <h2>
      <span class="brand-text">Ko</span>pe
      <span class="brand-text">p</span>od the drifter
    </h2>
    <p class="landing-main-text">
      My example TC3005b
      <br>
      Django python-based back-end
    </p>
  </div>
</section>
<section class="landing-section langing-features">
  <section class="landing-feature feature-music-services">
    <h2>Connect your favourite <span class="brand-text">mu</span>sic services</h2>
    <ul>
      <li>Spotify</li>
      <li>Deezer</li>
    </ul>
  </section>
  <section class="landing-feature feature-notifications">
    <h2>Get <span class="brand-text">n</span>otifications wherever you want them</h2>
    <ul>
      <li>Email</li>
      <li>Telegram</li>
    </ul>
  </section>
</section>

```

The final structure should look like ...

```bash
tree
```

```bash
.
├── db.sqlite3
├── helloworld
│   ├── asgi.py
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── __init__.cpython-310.pyc
│   │   ├── settings.cpython-310.pyc
│   │   ├── urls.cpython-310.pyc
│   │   └── wsgi.cpython-310.pyc
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
└── my_app
    ├── admin.py
    ├── apps.py
    ├── __init__.py
    ├── migrations
    │   ├── __init__.py
    │   └── __pycache__
    │       └── __init__.cpython-310.pyc
    ├── models.py
    ├── __pycache__
    │   ├── admin.cpython-310.pyc
    │   ├── apps.cpython-310.pyc
    │   ├── __init__.cpython-310.pyc
    │   ├── models.cpython-310.pyc
    │   └── views.cpython-310.pyc
    ├── static
    │   └── style.css
    ├── templates
    │   └── index.html
    ├── tests.py
    └── views.py

```

Run the server again

```bash
python manage.py runserver
```
