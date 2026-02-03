# Django

## Overview
High-level Python web framework with batteries included

## Installation

```bash
pip install django
django-admin startproject myproject
cd myproject
python manage.py startapp myapp
```

---

## Project Structure

```
myproject/
├── manage.py
├── myproject/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── myapp/
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── models.py
    ├── views.py
    ├── urls.py
    └── templates/
```

---

## Models

```python
# myapp/models.py
from django.db import models

class User(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField(unique=True)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name
```

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## Views

### Function-based
```python
from django.http import JsonResponse
from .models import User

def user_list(request):
    users = list(User.objects.values())
    return JsonResponse(users, safe=False)
```

### Class-based
```python
from django.views import View

class UserListView(View):
    def get(self, request):
        users = list(User.objects.values())
        return JsonResponse(users, safe=False)
```

---

## URLs

```python
# myapp/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('users/', views.user_list, name='user-list'),
    path('users/<int:pk>/', views.user_detail, name='user-detail'),
]

# myproject/urls.py
from django.urls import path, include

urlpatterns = [
    path('api/', include('myapp.urls')),
]
```

---

## Django REST Framework

```bash
pip install djangorestframework
```

```python
# settings.py
INSTALLED_APPS = [
    ...
    'rest_framework',
]

# serializers.py
from rest_framework import serializers
from .models import User

class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = '__all__'

# views.py
from rest_framework import viewsets
from .models import User
from .serializers import UserSerializer

class UserViewSet(viewsets.ModelViewSet):
    queryset = User.objects.all()
    serializer_class = UserSerializer
```

---

## Admin

```python
# myapp/admin.py
from django.contrib import admin
from .models import User

@admin.register(User)
class UserAdmin(admin.ModelAdmin):
    list_display = ['name', 'email', 'created_at']
    search_fields = ['name', 'email']
```

```bash
python manage.py createsuperuser
# Access: http://localhost:8000/admin
```

---

## Running

```bash
python manage.py runserver
# http://localhost:8000
```

---

## Why Django?

- Batteries included (auth, admin, ORM)
- Great for full-stack apps
- Large ecosystem
- Excellent documentation
- Good for rapid development
