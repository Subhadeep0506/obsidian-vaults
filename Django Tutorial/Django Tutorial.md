# 1. Install Django and Create project
First install Django using pip command
`pip install django`

**NOTE**: It is always suggested to create a virtual environment before working with Django. We will use `virtualenv`  in this case. Install `virtualenv` using `pip install virtalenv` and then in the project folder run the following command to create a virtual environment having Python version 3.9: `virtualenv --python=python3.9 .venv` 

Now, in the project root, run this command to create the Django project:
```sh
django-admin startproject project_name .
```

After creating the project the folder structure should look something like this:
```
root
├── .venv
├── project_name
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
├── db.sqlite3
└── manage.py
```

1. `urls.py` contains all the URLs of the application, like `/admin`, `/dashboard` etc.
2. `settings.py` contains all the configuration of the project.

# 2. Working with the application
Now that we have all setup, we will make changes to the default application that was created for us. In the `settings.py` file, there is a section like :

```python
INSTALLED_APPS = [
	"django.contrib.admin",
	"django.contrib.auth",
	"django.contrib.contenttypes",
	"django.contrib.sessions",
	"django.contrib.messages",
	"django.contrib.staticfiles",
]
```

This handles different parts of the application, like session, authentication, authorization. It's like breaking down an  application into several parts. In large application these component applications might be many and handle several things. But for our application we will have only one one application where we will define all our databases, templates, views etc. 
To create application, use the following command:

```sh
python manage.py startapp application_name
```

The project will have the tree structure as such now:

```
root
├── .venv
├── base
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── views.py
├── project_name
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
├── db.sqlite3
└── manage.py
```

1. `views.py` will have functions or classes which define the pages that will be viewed when someone visits the particular URL.
2. `models.py` is where we configure database, create Schema etc.

At this moment, the Django project doesn't know about this newly created application. We need to connect this application to the project. 
We add the application to the connected apps list as such:

```python
INSTALLED_APPS = [
	.
	.
	"base.apps.BaseConfig"
]
```

# 3. Handling Requests and Responses
In our application there are only two `urls.py` file. One in the project and another in the `base` application. 
In the project `urls.py` file we will create our first request response cycle.

**`urls.py`(project)**
```python
from django.contrib import admin
from django.urls import path
from django.http import HttpResponse

def home(request):
	return HttpResponse('Home Page')

def rooms(request):
	return HttpResponse("Rooms")

urlpatterns = [
	path("admin/", admin.site.urls),
	path("", home),
	path("rooms/", rooms)
]
```

At this moment, our application only has two routes. But in real world use-cases, applications tend to have many routes. That is why Django has the application paradigm to create multiple applications for multiple routes.
So, now we will use our created `base` application to handle the routes.Move the two (`home`, `rooms`) routes into the `urls.py` file of `base` application,and remove the paths from the `urlpatterns`.

**`views.py`**
```python
from django.shortcuts import render
from django.http import HttpResponse

def home(request):
	return HttpResponse('Home Page')
def rooms(request):
	return HttpResponse("Rooms")
```

Now that our routes are setup, we need to setup their path. Create a `urls.py` in `base` application. Add the routes there as such:

**`urls.py`(base)**
```python
from django.urls import path
from . import views

urlpatterns = [
	path("", views.home, name="home"),
	path("rooms/", views.rooms, name="rooms"),
]
```

Notice that we add a `name` argument to path. This name can be used later to reference the path directly.
At this moment, if we try to access the site, we will be redirected to Django dashboard. This is because though we have added the routes to our application, we have not added them to project. We have to make the project aware that these routes exists.

**`urls.py`(root)**
```python
from django.contrib import admin
from django.urls import path, include


urlpatterns = [
	path("admin/", admin.site.urls),
	path("", include("base.urls"))
]
```

What we have done is, let project know about existence of base URLs. We use the `include` function from `django.urls` to do this. 

# 4. Templates
## 4.1 Setting up
To add templates, create a folder called `templates` in the root. And add a `home.html` and `rooms.html` file there.
The folder structure should now look like this:

```
root
├── .venv
├── base
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── views.py
├── studybud
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
├── templates
│   ├── home.html
│   ├── rooms.html
├── db.sqlite3
└── manage.py
```

**`home.html`**
```html
<h1>
	Home Page
</h1>
```

We need to tell Django about the templates folder we have created. To do so, we go `settings.py` file in project directory, add the following lines:

```python
# ...
TEMPLATES = [
	{
		"BACKEND": "django.template.backends.django.DjangoTemplates",
		"DIRS": [
			BASE_DIR / "templates" # this line
		],
		"APP_DIRS": True,
		"OPTIONS": {
				"context_processors": [
				"django.template.context_processors.debug",
				"django.template.context_processors.request",
				"django.contrib.auth.context_processors.auth",
				"django.contrib.messages.context_processors.messages",
			],
		},
	},
]
# ...
```

We have templates directory setup. Now we can use the templates in our application. 

**`views.py`**
```python
from django.shortcuts import render
from django.http import HttpResponse

def home(request):
	return render(request, "home.html")

def rooms(request):
	return render(request, "rooms.html")
```

## 4.2 Using template inheritance
When you want to use an existing template in the page, we use Template inheritance. To demonstrate this we will make a nav-bar for our application. Create a simple nav-bar.

```html
<a href="/">
	<h1>Logo</h1>
	</a>
<hr>
```

Now to use this template in multiple pages, we do as such.
In the `home.html` file:

```html
{% include 'navbar.html' %}

<h1>Home Page</h1>
```

Similarly for `rooms.html`. But, a more common way of template inheritance is by using a `main.html` file, where all templates are managed.

**`main.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>StudyBud</title>
</head>
<body>
	{% include 'navbar.html' %}
	{% block content %}
	{% endblock %}
</body>
</html>
```

The `{% block content %}...{% endblock %}` section acts as a template hook. All the contents get displayed there. We do this by including this file in the parent template. 

**`home.html`**

```html
{% extends "main.html" %}
{% block content %}

<h1>Home Page</h1>

{% endblock content %}
```

## 4.3 Using loops and conditions inside templates
Using Django templates we can also iterate a list and display contents based on conditions.

Create list of rooms in the `views.py` in base application. 

```python
rooms_list = [
	{'id': 1, "name": "Let's Learn Python"},
	{'id': 2, "name": "Django Unchained"},
	{'id': 3, "name": "React Group"},
	{'id': 4, "name": "Frontend Devs"},
]
```

Pass this list as argument into the render function.

```python
def home(request):
	return render(request, "home.html", {"rooms": rooms_list})
```

This makes the `rooms_list` list available to the Django template to make use of. The list is available as name `rooms`. Now we go to the `home.html` file and display the list content.

```html
{% extends "main.html" %}
{% block content %}
<h1>Home Page</h1>
<div>
	<div>
		{% for room in rooms%}
		<div>
			<h5>
				{{room.id}} -- {{room.name}}
			</h5>
		</div>
	{% endfor %
	</div>
</div>
{% endblock content %}
```

Templates organization is important in case of Django. The `main.html` and `navbar.html` both are required to be present globally. So they will be left as they are. But the `home.html` and `rooms.html` are to be moved to application folder. We will create a templates folder in base folder. And then again a folder named base has to be created to put the templates. This is how Django functions.

# 5. Database
Before working with database, we need to migrate Django first.
Run `python manage.py migrate` to  let Django do that automatically.

The database models are created inside `models.py` in base application. Django lets us create data models using python class and that gets converted to database tables. Here is an example:

```python
class Project(models.Model):
	title = models.CharField()
	description = models.TextField()
	id = models.UUIDField()
```

The class name will be the table name. The class has to inherit `models` from Django
The above Django model creates a Database table as such:

|id|title|description|
|---|---|---|
|1|...|...|
|2|...|...|
|3|...|...|
|4|...|...|
|5|...|...|
|6|...|...|

## 5.1 models datatypes and their properties

We will create a Room table for our database. It will have the below fields
1. `name`
```python
name = models.CharField(max_length = 200)
```

2. `description`
```python
description = models.TextField(null = True, blank = True)
```
`null = True` means that this field in the table can have null data. 
`blank = True` means that when the data is about to get saved, in the form this field can be empty.

3. `updated`
```python
updated = models.DateTimeField(auto_now = True)
```
`auto_now = True` means it will save the time stamp of that moment when the data is updated for that particular entry.

4. `created`
```python
created = models.DateTimeField(auto_now_add = True)
```
`auto_now_add = True` means that it takes the snapshot of the time when that room was created but not anytime later again.

## 5.2 Migrating after adding the table

After our table is designed, we need to migrate the database again. This migration is to be done every-time we make changes to the database. `python manage.py migrate` migrates the database to the latest migration.

```bash
python manage.py makemigrations && python manage.py migrate
```

To view the database, we will use Django's builtin admin panel, Django Admin. To use that first we need to create a superuser. Run the following command to do so.

```bash
╭─[subhadeep-ASUSVivoBook] with  (subhadeep)
╰──⮚ python manage.py createsuperuser
Username (leave blank to use 'subhadeep'): subhadeep
Email address: subhadeepdoublecap@gmail.com
Password: ********
Password (again): ********
Superuser created successfully.
```

But we cannot view our model yet. We need to register our model. We do that in `admin.py` file of `base` application. 

```python
from django.contrib import admin
from .models import Room

admin.site.register(Room)
```

## 5.3 Viewing the data in pages

In the `views.py` file make the changes:
```python
from django.shortcuts import render

from .models import Room

def home(request):
	rooms = Room.objects.all()
	context = {"rooms": rooms}
	return render(request, "base/home.html", context)

def rooms(request, pk):
	room = Room.objects.get(id = pk)
	context = {"room": room}
	return render(request, "base/rooms.html", context=context)
```

Now go to the pages and check if they are working.

## 5.4 Making relational tables

We will build our first relational table `Message`. This table will use `Room` table as a foreign key

```python
class Message(models.Model):
	# user =
	room = models.ForeignKey(Room, on_delete=models.CASCADE)
	body = models.TextField()
	updated = models.DateTimeField(auto_now=True)
	created = models.DateTimeField(auto_now_add=True)
```

- `on_delete=models.SET_NULL` means that when Room table is deleted, all the messages will remain the database, only the relation will be removed.
- `on_delete=models.CASCADE` means all the messages will be deleted if Room table is deleted.

For the user field we will use the builtin User model.
First import the User model from Django:

```python
import django.contrib.auth.models import User
```

```python
class Message(models.Model):
	user = models.ForeignKey(User, on_delete=models.CASCADE)
	room = models.ForeignKey(Room, on_delete=models.CASCADE)
	body = models.TextField()
	updated = models.DateTimeField(auto_now=True)
	created = models.DateTimeField(auto_now_add=True)
```

Now we will create the Topics table:

```python
class Topic(models.Model):
	name = models.CharField(max_length=200)
	
	def __str__(self) -> str:
		return self.name
```

Now we add a `topic` field to the Room table:

```python
class Room(models.Model):
	topic = models.ForeignKey(Topic, on_delete=models.SET_NULL, null=True)
	...
```

**NOTE:** Don't forget to migrate to latest changes after making changes to models.

```bash
python manage.py makemigrations && python manage.py migrate
```

And also, add the new models to `admin` panel.

```python
from django.contrib import admin
from .models import Room, Topic, Message

admin.site.register(Room)
admin.site.register(Topic)
admin.site.register(Message)
```

