# Django

## install Django

[How to install Django](https://docs.djangoproject.com/en/2.1/topics/install/)

* Python includes a lightweight database called SQLite.
* install pip 
* install virtualenv: `pip install virtualenv`
  * `virtualenv venv` for add
  * `source /path/to/venv/bin/activate` for use
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

class Product(models.Model):
  name = models.CharField(max_length=255)
  price = models.FloatField()
  stock = models.IntegerField()
  image_url = models.CharField(max_length=2083) # max size for link
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

* add folder `templates` in app folder
* add `index.html` for index

```html
<h1>Products</h1>
<ul>
    {% for product in products %}
        <li>{{ product.name }} (${{ product.price }})</li>
    {% endfor %}
</ul>
```

* `views.py`  in app folder

```py
from django.http import HttpResponse
from django.shortcuts import render
from .models import Product

def index(request):
  products = Product.objects.all()
  return render(request,'index.html', { 'products': products })

  # Product.objects.filter()
  # Product.objects.get()
  # Product.objects.save()
```

## add bootstrap (Base Template)

* add `base.html` in template folder
* copy [Starter template from bootstrap site](https://getbootstrap.com/docs/4.3/getting-started/introduction/#starter-template) to it
* add `{% block content %}{% endblock %}` for content span
* add `{% extends 'base.html' %}` first line of other template and content between `{% block content %}` & `{% endblock %}`

* for use template between base template for all app
  * make `templates` folder in root folder and make base template
  * in main folder `setting.py` -> TEMPLATES ->'DIRS':[os.path.join(BASE_DIR, 'templates')]



