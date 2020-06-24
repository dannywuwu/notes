# URLs/Views

- Requesting a page

Browser -> urls.py -> views.py

- The browser fires off a request to `urls.py` and decides which function to fire in `views.py` 
- This function controls what happens when the user visits the requested URL
- `views.py` sends the HTML template/response to the browser

```python
# urls.py
# . from same directory
from . import views
from django.urls import re_path

# use regex to pattern match urls
urlpatterns = [
  # calls views.homepage as a callback 
    re_path(r'^$', views.home),
]
```

```python
# views.py
from django.http import HttpResponse

def home(request):
    return HttpResponse('<h1>home</h1>')
```

- HttpResponse is HTML

# HTML Templates

- Return render of a template

```python
# views.py
from django.shortcuts import render

def home(request):
    return render(request, 'home.html')
```

# Apps

- Separate websites into apps for each section of a website

### `python manage.py startapp articles`

```python
# settings.py

INSTALLED_APPS = [
  ...
  'appname'
]
```

```python
# main/urls.py
urlpatterns = [
  path(..., include('app.urls'))
]
```

- Include new app urls 
- Whenever someone goes to `/app` it will first look at the urls in the `app/urls.py`

# Models

- Classes which represent a table in a database
- Each type of data is represented in a model
- Each model maps to a single table in a database 
- The database stores instances of each model

## [Field Types](https://docs.djangoproject.com/en/3.0/ref/models/fields/)

- Specify data type of Model fields

```python
# models.py
class Article(models.Model):
    title = models.CharField(max_length=100)
    slug = models.SlugField()
    body = models.TextField()
    date = models.DateTimeField(auto_now_add=True)
```

# Migrations

### `python manage.py makemigrations`

- Create a migration file
- Tracks changes to a model
- When we run `python manage.py migrate`, the migration file will mirror the model to the specified database table
- Every time we make/change a model we must make migrations and migrate them

### `python manage.py migrate`

- Migrate models to the database

# Django ORM

### `from dir.models import Cool`
- Import `Cool` model from `models.py` from the `dir` directory

### `Cool.objects.all()`

- Retrieve all rows (models/objects) from the table

### `me = Cool()`

- Create new `Cool` model instance

### `me.save()`

- Save model instance to database

### `Cool.objects.all()`

- Get all objects in the Cool table
- `Cool.objects.all()[0].title` gets the title property of the first index

### Formatting model retrieval

```python
def __str__(self):
    return self.title
```

- Now calling models ex. `Cool.objects.all()` will return the model title

# Django Admin

### `python manage.py createsuperuser`

- Create admin account
- No email necessary

## Model Registration

- Allows for GUI viewing/editing for models

```python
# admin.py
from .models import Article 

admin.site.register(Article)
```

- Import  Article model from `models.py` in the current directory
- Register Article model on admin site (GUI interface)

# Template Tags

- Insert Python logic data 