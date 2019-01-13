# DJANGOGIRLS
###### v 0.0.0
is a learning project steps by [Django Girls](https://tutorial.djangogirls.org/en)

### Steps

1. create project folder
```
mkdir djangogirl && cd djangogirl
```
2. install django globaly
```
pip install django==2.1.7
``` 
3. install MySQL dependency
```
pip install mysqlclient
```
4. start django project
```
django-admin.py startproject mysite .
```
5. config setting for connect to MySQL `mysite/settings.conf`
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'djangogirls',
        'USER': 'root',
        'PASSWORD': 'root',
        'HOST': '127.0.0.1',
        'PORT': '3306',
    }
}
```
6. migrate project to database 
```
python manage.py migrate
```
7. create an app
```
python manage.py startapp blog
```
8. add blog to setting `mysite/settings.conf`
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog'
]
```
9. add post model `blog/models.py`
```python
from django.conf import settings
from django.db import models
from django.utils import timezone


class Post(models.Model):
    author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    title = models.CharField(max_length=200)
    text = models.TextField()
    created_date = models.DateTimeField(default=timezone.now)
    published_date = models.DateTimeField(blank=True, null=True)

    def publish(self):
        self.published_date = timezone.now()
        self.save()

    def __str__(self):
        return self.title
```
10. create migrate from model for blog
```
python manage.py makemigrations blog
```
11. migrate blog
```
python manage.py migrate blog
```
12. add post to `blog/admin.py`
```python
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```
13. create a supperuser for admin connection
```
python manage.py createsuperuser
```
14. run server
```
python manage.py runserver 127.0.0.1:8000
```
15. Deployment on PythonAnyWhere ( [Wiki](https://github.com/h-rafiee/djangogirls/wiki/Deployment-on-PythonAnyWhere) | [DjangoGirls](https://tutorial.djangogirls.org/en/deploy/) )
16. create a new route for our blog on `mysite/urls.py`
```python
from django.contrib import admin
from django.urls import path
from django.urls import include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')),
]
```
17. ok we see we add blog.urls so we need create or edit `blog/urls.py` as 
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.post_list, name='post_list')
]
```
18. we doesn't have any *post_list* function on views so we need create a one on `blog/views.py`
```python
from django.shortcuts import render

# Create your views here.
def post_list(request):
        return render(request, 'blog/post_list.html', {})
```
19. so we can create a html as *post_list.html* for view in `blog/templates/blog` directory
20. for add static files [Read this doc](https://docs.djangoproject.com/en/2.1/howto/static-files/)
21. for deploy on **Pythonanywhere.com** about static files [Read this doc](https://help.pythonanywhere.com/pages/DjangoStaticFiles) ; *I had to copy statics files form ./blog/static/blog to ./static/blog it was easier to me*
22. [WE ARE HERE ON TUTORIAL](https://tutorial.djangogirls.org/en/django_orm/)
