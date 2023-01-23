# Django tutorial

Command
---------------  
creating a project:  
django-admin startproject (name)  

runserver ( change port or ip )  
py manage.py runserver(port or ip:port)  

creating a app:
py manage.py startapp (name)

migrate app and DB:
py manage.py migrate
py manage.py makemigrations name
py manage.py sqlmigrate polls 0001

Create superuser:  
py manage.py createsuperuser

Test:
python manage.py test (app name)

Program  
---------------
path(route,view,kwargs,name)
    route:URL pattern
    view:Find a view through patten
    kwargs:pass arguments 
    name:Naming your URL lets you refer to it unambiguously from elsewhere in Djang 

Database connect (example:postgresql)
---------------
note:  
setting project/settings.py this file argument 

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'Table name',
        'USER': 'User name',
        'PASSWORD': 'User Password',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}

Create Models 
---------------
Note:
create models (table structure)

class Tablename(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

Activating Model 
---------------
Note:  
1. To include the app in our project, we need to add a reference to its configuration class in the INSTALLED_APPS setting.
example:
INSTALLED_APPS = [
    'Folder.apps.classname'
]

2. By running makemigrations, you’re telling Django that you’ve made some changes to your models,then will generate 'Folder/migrations/0001_initial.py'
**Command : py manage.py makemigrations name**  

3. Show sql command(Non-essential)
**Command : py manage.py sqlmigrate polls 0001**  

4. Migrate 
**Command : py manage.py migrate**  

Change Model 
---------------
Note:  
redo migrate
**Command : py manage.py makemigrations name**  
**Command : py manage.py migrate**  

Create a admin interface for each object
---------------
Note:  
Register object in appname/admin.py
tell the admin this object have interface

from .models import object name
admin.site.register(object name)

Static file
---------------
Note:Use static parameter to find absolute URL

{% load static %}
href="{% static 'polls/style.css'

Use Customize admin html
---------------
Note:
Create templates folder in project folder  
create admin in templates folder and put new admin html in
change TEMPLATES in setting,add templates path to DIRS('DIRS': [BASE_DIR / 'templates'])


Django Note
---------------  
+ A project can contain multiple Apps  
+ Project urls direction to app urls Apps urls direction to view  
+ Django use models.py to create a database schema and a Python database-access API for accessing objects
+ Putting templates directly in app name/templates/app name/templates.html,if just put in name/templates Django might get a wrong file from other app templates folder
+ Add an app_name can help Django know which app view is realneed
+ Use generic views : just give model & template_name can generate view easily , if u want to change model do override get_queryset
+ add some TestCase into tests.py , make sure no issues in app
+ static file path have to add to setting , easy to manage
+ Create admin.ModelAdmin class to Customize admin page
  + fieldsets:set the inside show table
  + inlines:can connect to other table by PK
  + list_display:change show parameter on main page 
  + list_filter:Django provide a list filter by parameter type(DateTimeField:“Any date”, “Today”, “Past 7 days”, “This month”, “This year”)
  + search_fields:Django provide a search filter by parameter type
