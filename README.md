# Study Project - Python Django

[Course by Corey Schafer](https://www.youtube.com/watch?v=UmljXZIypDc&list=PL-osiE80TeTtoQCKZ03TU5fNfx2UY6U4p) 

2/17

- __Python Django Tutorial: Full-Featured Web App Part 1 - Getting Started__
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
    └── manage.py
    ```
  - Run Application - `./manage.py runserver`
  - Admin Panel - `http://localhost:8000/admin`
- __Python Django Tutorial: Full-Featured Web App Part 2 - Applications and Routes__
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