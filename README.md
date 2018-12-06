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
15. [WE ARE HERE ON TUTORIAL](https://tutorial.djangogirls.org/en/deploy/)