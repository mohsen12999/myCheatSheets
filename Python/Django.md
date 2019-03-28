# Django

## install Django

[How to install Django](https://docs.djangoproject.com/en/2.1/topics/install/)

* Python includes a lightweight database called SQLite.
* install pip 
* install virtualenv: `pip install virtualenv`
  * `virtualenv ENV` for add
  * `source /path/to/ENV/bin/activate` for use
* install Django: `pip install Django`
  * `django-admin startproject projectname .` for make django project
  * `python3 manage.py runserver` for run and see in browser

```py
import django
print(django.get_version())
```

## make App Module

* `python3 manage.py startapp products` for add app (modules package)

* in app folder views.py

```py
from django.http import HttpResponse
from django.shortcuts import render

def index(request):
  return HttpResponse('Hello World!')
```

* add urls.py in app folder

```py
from django.urls import path
from . import views

urlpatterns = [
  path('',views.index)
]
```

* in main folder urls.py

```py
from django.contrib import admin
from django.urls import path,include

urlpatterns = [
  path('admin/', admin.site.urls)
  path('products/', include('products.urls')) # add app folder
]
```

## Make Model

* in app folder models.py

```py
from django.db import models

class product(models.Model):
  name = models.CharField(max_lenght=255)
  price = models.FloatField()
	stock = models.IntegerField()
	image_url = models.CharField(max_lenght=2083) # max size for link
```

* add app to migration list -> main folder `setttings.py` -> in `INSTALLED_APPS` add config class of app from app folder apps.py like `products.apps.ProductConfig` 
* make migration `python3 manage.py makemigrations`
* run migration `python3 manage.py migrate`
* for see sqlite data [sqlitebrowser](https://sqlitebrowser.org)

## Admin

* `python3 manage.py createsuperuser`

### add table to admin panel

* in app folder `admin.py`

```py
from django.contrib import admin
from .models import Product

admin.site.register(Product)
```

* after thet, we can access product to change in admin panel

### change view table in admin panel

* in app folder `admin.py`

```py
from django.contrib import admin
from .models import Product

class ProductAdmin(admin.ModelAdmin):
	list_display = ('name', 'price', 'stock')

admin.site.register(Product, ProductAdmin)
```

## Template
5:48





