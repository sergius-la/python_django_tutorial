# Study Project - Python Django

[Course by Corey Schafer](https://www.youtube.com/watch?v=UmljXZIypDc&list=PL-osiE80TeTtoQCKZ03TU5fNfx2UY6U4p) 

3/17

### **Python Django Tutorial: Full-Featured Web App Part 1 - Getting Started**
  - Install django
  - Admin commands `django-admin`
  - Start django project `django-admin startproject django_project`
    ```
    # Django Project Structure
    django_project/
    │
    ├── django_project/
    │   ├── __init__.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py # How django project app communicate with server
    ├── blog (app)/
    │   ├── __init__.py
    │   ├── urls.py
    │   ├── static/
    │   │   └── blog/
    │   │       └── *style.css
    │   └── templates/
    │       └── blog/
    │           └── *templates.html
    └── manage.py
    ```
  - Run Application - `./manage.py runserver`
  - Admin Panel - `http://localhost:8000/admin`
### **Python Django Tutorial: Full-Featured Web App Part 2 - Applications and Routes**
  - Create django app - `python manage.py startapp blog`
  - Adding app urls path to `project` urls
    ```python
    # django_project urls.py
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('blog/', include("blog.urls")), # http://localhost:8000/blog/

        path('', include("blog.urls")), # Make an app default home page - http://localhost:8000/
    ]
    ```
  - Adding app urls path to `app` blog urls
    ```python
    # blog app urls.py
    from django.urls import path
    from .import views
    
    urlpatterns = [
        # http://localhost:8000/blog/
        path('', views.home, name="blog-home"),
        # http://localhost:8000/blog/about/
        path('about/', views.about, name="blog-about"),
    ]
    ```
### **Python Django Tutorial: Full-Featured Web App Part 3 - Templates**

  - Add Installed apps into project `settings.py`
  ```python
  # <appname>.<apps.py>.<ClassName>
  INSTALLED_APPS = [
    "blog.apps.BlogConfig",
    'django.contrib.admin',
    'etc'
  ]
  ```
  - Render template - `views.py`
  ```python
  from django.shortcuts import render

  def home(request):       # appName/template.html
    return render(request, "blog/home.html")
  ```
  - Templates code block - `{% %}`
  - Access variable - `{{ <variable> }}`
  - HTML - `href="{% url 'blog-about' %}"`, in the `urls.py`
  ```python
  from django.urls import path

  urlpatterns = [
    path('about/', views.about, name="blog-about"),
  ]
  ``` 
  
### **Part 4 - Admin Page**

```shell script
python manage.py makemigrations
```

```shell script
python manage.py migrate
```

```shell script
python manage.py createsuperuser
```

### **Part 5 - Database and Migrations**

#### Models

```python
from django.db import models
from django.utils import timezone

class Post(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    # auto_now=True, auto_now_add=True
    date_posted = models.DateTimeField(default=timezone.now)
```