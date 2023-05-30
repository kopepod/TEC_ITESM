# Django Pretrained Model Service

This project shows how to use a pretrained AI model to predict inputs using the Django framework.

1. Create a new project

```python
mkdir ai_service
cd ai_service
django-admin startproject ai_service .
cd ai_service
python manage.py migrate
python manage.py runserver
tree
firefox http://127.0.0.1:8000/
```
CTRL+C

2. Create a new APP

```python
python manage.py startapp my_app
nano ai_service/settings.py
```
Edit the setting to include your APP

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
3. Modify Project URLs

```bash
nano ai_service/urls.py
```
```python
"""
URL configuration for ai_service project.

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/4.2/topics/http/urls/
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
from my_app import views  # new

urlpatterns = [
    path("admin/", admin.site.urls),
    path("", views.counterView, name="counter"), # new
]

```
4. Modify Views

```bash
nano my_app/views.py
```
```python
from django.shortcuts import render

# Create your views here.
from django.http import HttpResponse
from django.template import loader  # new
from django.views.decorators.csrf import csrf_exempt


@csrf_exempt
def counterView(request):
    mssg = "0"
    if request.method == "POST" and "counter" in request.POST:
        try:
            request.session["counter"] += 1
        except:
            request.session["counter"] = 0
        mssg = str(request.session["counter"])
    elif request.method == "POST" and "reset" in request.POST:
        request.session["counter"] = 0
        mssg = str(request.session["counter"])
    elif request.method == "POST" and "salute" in request.POST:
        mssg = "Hi " + request.POST.get("textbox")

    # print(request.session['counter'])
    context = {
        "foo": mssg,
    }
    return render(request, "counter.html", context)
```

5. Add HTML

```bash
mkdir my_app/templates
mkdir my_app/static
```
```bash
nano my_app/static/style.css
```

```javascript
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
  background: url(https://images.unsplash.com/photo-1460667262436-cf19894f4774) no-repeat center center fixed; 
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
nano my_app/templates/counter.html
```
```html
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <title>Simple Counter</title>
</head>
<body>
   <style>
      body{
         background-color: gray;
         color: white;
      }
      .counter form .countcss{
         border:none;
         outline: none;
         background-color:green;
         color: white;
         font-size: 16px;
         padding: 15px 32px;
         color: white;
      }
      .counter form .resetcss{
         border:none;
         outline: none;
         background-color:cyan;
         font-size: 16px;
         padding: 15px 32px;
         color: black;
      }
      .counter form .salutecss{
         border:none;
         outline: none;
         background-color:orange;
         font-size: 16px;
         padding: 15px 32px;
         color: black;
      }
   </style>
   <div class="container counter text-center" style="margintop: 150px;">
      <h1 class="display-1 text-white">
       {{ foo }}
         </h1> 

         <form method="post"> 
         		<input name="textbox" type="text" value="Kopepod"></input> <br><br>
            <button name="counter" class="countcss">Count</button>
            <button name="reset" class="resetcss">Reset</button>
            <button name="salute" class="salutecss">Salute</button>
            
         </form>
   </div>
</body>
</html>
```

```bash
tree

.
├── ai_service
│   ├── asgi.py
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── __init__.cpython-39.pyc
│   │   ├── settings.cpython-39.pyc
│   │   ├── urls.cpython-39.pyc
│   │   └── wsgi.cpython-39.pyc
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── db.sqlite3
├── manage.py
└── my_app
    ├── admin.py
    ├── apps.py
    ├── __init__.py
    ├── migrations
    │   ├── __init__.py
    │   └── __pycache__
    │       └── __init__.cpython-39.pyc
    ├── models.py
    ├── __pycache__
    │   ├── admin.cpython-39.pyc
    │   ├── apps.cpython-39.pyc
    │   ├── __init__.cpython-39.pyc
    │   ├── models.cpython-39.pyc
    │   └── views.cpython-39.pyc
    ├── static
    │   └── style.css
    ├── templates
    │   └── counter.html
    ├── tests.py
    └── views.py
```
