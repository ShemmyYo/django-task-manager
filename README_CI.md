Hello Django Instructions Sheet
Note: To create an editable version of this document, click File -> Make a copy. You will then be able edit and add your own notes to the document as you proceed.
Note: We will provide a full set of instructions for completing the Hello Django Project at the end of this Walkthrough series. 
Getting Set up
In the Browser:

#
Step
Code
Your Notes
1
Click to open the Github Template Link
Gitpod Template




In Github:

#
Step
Code
Your Notes
2
Click the ‘Use this Template’ button




3
Give your project a name
e.g. ci-fsf-hello-django
Note: You can also give your project a description
4
Click the ‘Create Repository from Template’ button




5
Click the Green ‘Gitpod’ Button





Part 1: Creating the ‘Say Hello’ App
Important Note: It is recommended when you are still learning this content that you type out each line of code, rather than copying and pasting. This will help you learn!

Key: 
PROJ_NAME = django_todo			APP_NAME = todo
Step 1: Create Project and App
In the Terminal:

#
Step
Code
Your Notes
1.
Install Django
pip3 install 'django<4'
Note: It's important to make sure that you download the official (and most supported) version of Django. As a result, you should download the latest version of 3. 
2.
Create Project 
django-admin startproject PROJ_NAME .
(Don’t forget the ‘.‘)
Note: Don’t forget the ‘.’ at the end of the command.
3.
Create a new App
python3 manage.py startapp APP_NAME


*
To run the server
python3 manage.py runserver






IMPORTANT NOTE: Hiding environment variables
In these videos, Chris does not hide his environment variables, as he doesn't push his code until the very end, right before deployment.

We recommend that you do create and hide your environment variables so you can push early and often, as taught in previous lessons. Use the env.py file as you've seen before, and make sure this is added to .gitignore as demonstrated before.

If you need a reminder on how to do this, look at this link (around 0:40 in the second video) or at this cheat sheet from one of our tutors, James.

DO NOT put settings.py in .gitignore in an effort to hide the hardcoded SECRET_KEY.
Step 2: Create your views
Note: Views hold the logic that is required to return information as a response, in whatever form, to the user. They ​​take a Web request and return a Web response.

In todo / views.py: 
#
Step
Code
Your Notes
1.
Create your views
from django.shortcuts import render, HttpResponse

# Create your views here.
def say_hello(request):
    return HttpResponse("Hello!")
Note: Create new functions / classes here
Note: Don’t forget the comma in the import!

Note: This little function is the equivalent of a console.log in a JavaScript file, it is useful to check that all the pieces of your Django project are wired up.


Note: Text in ‘bold’ is new code
Step 3: Create your URLs
Note: Urls.py contains the url patterns django uses to try to match the requested URL with the correct view logic (as described above).

In django_todo / urls.py: 

#
Step
Code
Your Notes
1.
Import the views function from views.py
...
from todo.views import say_hello


2.
Add your URL paths
urlpatterns = [
    …,
    path('hello/', say_hello, name = 'hello'),
]
Note: the path function takes 3 arguments:
the URL the user will type in
the view function it will return
a name parameter


Note: Text in ‘bold’ is new code

In the Terminal:

#
Step
Code
Your Notes
*
Run the server
python3 manage.py runserver


*
Add hello/ to the url in the browser
e.g. https//...url....io/hello/




----------------
Hello Django Instructions Sheet
Part 2: Returning a basic HTML Template
Step 1: Create your Template

Note: A template contains the static parts of the desired HTML output as well as some special syntax describing how dynamic content will be inserted. 
 
In the todo folder:

#
Step
Code
Your Notes
1.
In the app folder, todo, create a new folder called templates 
e.g. todo / templates


2.
In the templates folder, create a new folder called todo
e.g. todo / templates / todo


3.
Create a new file called todo_list.html
e.g. todo / templates / todo / todo_list.html






In todo / templates / todo / todo_list.html:

#
Step
Code
Your Notes
4.
Create your html 5 file including a h1 tag, “Things to do”
e.g. 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>Things to do</h1>
</body>
</html>
Note: You can use the Gitpod shortcut ‘!’ and then click the tab key


In todo / views.py:

#
Step
Code
Your Notes
5.
Replace the entire ‘say_hello’ function
def get_todo_list(request):
    return render(request, 'todo/todo_list.html')
Note: Here we’re saying when the get_todo_list view function is called, it will return the todo_list.html template.
6.
Remove the HttpResponse import
from django.shortcuts import render, HttpResponse
Note: Don’t forget to delete the comma



In django_todo / urls.py:

#
Step
Code
Your Notes
7.
Replace the ‘say_hello’ path 
urlpatterns = [
    …,
    path('', get_todo_list, name = 'get_todo_list')
]
Note: Here, we call the get_todo_list function in views.py at the url path ‘’
8.
Adjust the imports to import the correct function
...
from todo.views import get_todo_list




Note: Text in ‘bold’ is new code

In settings.py:

#
Step
Code
Your Notes
9.
Add your APP to INSTALLED APPS 
INSTALLED_APPS = [
    …,
    'todo',
]








In the Terminal:

#
Step
Code
Your Notes
10.
Run the server
python3 manage.py runserver




Note: Before running the server, make sure all files are saved.

-------------------------
Hello Django Instructions Sheet
Part 3: Migrations and Admin
Note: Migrations convert Python code into Database operations, i.e. they allow us to store our data in the database on the backend. 
Step 1: Make migrations
In the Terminal:

#
Step
Code
Your Notes
1
Make migrations --dry-run
python3 manage.py makemigrations --dry-run
Note: Runs a test migration run. 
2.
Show migrations
python3 manage.py showmigrations 
Note: Optional 
3
Make migrations
python3 manage.py makemigrations


4
Migrate
python3 manage.py migrate --plan
Note: Optional 
5
Migrate
python3 manage.py migrate




Note: Before making your migrations, make sure all files are saved.

Step 2: Create Superuser

Note: A django superuser is the most powerful user with permissions to create, read, update and delete data in the Django admin, which includes model records and other users. A superuser is also able to login to the admin site.

In the Terminal:

#
Step
Code
Your Notes
6
Create Super User
python3 manage.py createsuperuser


*
Create username and password


Note: The password will not appear on the screen as you type. Press Enter when you have finished typing the password.
7
Run the server
python3 manage.py runserver





In the Browser:

Note:  One of the most powerful parts of Django is the automatic admin interface. It reads metadata from your models to provide a quick, model-centric interface where trusted users can manage content on your site. The admin’s recommended use is limited to an organization’s internal management tool. It’s not intended for building your entire front end around.

#
Step
Code
Your Notes
8
Add /admin/ to the url
e.g. https//...url....io/admin/


*
Log in
Using the Superuser account details you just created.




--------------------
Hello Django Instructions Sheet
Part 4: Models
Note: A Django model is the built-in feature that Django uses to create tables, their fields, and various constraints. Django models simplify tasks and organize tables into models. Django models are used to store data in the database conveniently.

In todo / models.py:

#
Step
Code
Your Notes
1
Create a new class e.g. Item
class Item(models.Model):
    name = models.CharField(max_length=50, null=False, blank=False)
    done = models.BooleanField(null=False, blank=False)
Contains 2 fields: name, done


In the Terminal:

#
Step
Code
Your Notes
2
Make Migrations --dry-run
python3 manage.py makemigrations --dry-run
Note: Optional
3
Make Migrations 
python3 manage.py makemigrations


4
Migrate
python3 manage.py migrate
Note: This command creates the database, you can see this in the file tree on the left side of the screen, i.e. sqlite3.


Recommended Step (Not done in the video)
*
At this stage, we recommend you add sqlite to your gitignore file. 
…
cloudinary_python.txt
*.sqlite3
Note: By adding sqlite to gitignore at this point, when you git push the commit, any sensitive data within will not go to the github repo.
Note: You can skip this step in the later videos (Part 9), once you reach that point (Don’t worry you’ll just see the code is already in the gitignore file)


In todo / admin.py:

Note: In order to be able to see our models in the admin panel on the server, we first need to expose them in admin.py

#
Step
Code
Your Notes
5
Register Item in admin.py
from django.contrib import admin
from .models import Item

# Register your models here.
admin.site.register(Item)






Note: Text in ‘bold’ is new code

In the Terminal:

#
Step
Code
Your Notes
6
Run server 
python3 manage.py runserver




In the Browser:

#
Step
Code
Your Notes
7
Add admin to the url
e.g. https//...url....io/admin/


8
Click Items Folder




9.
Create New Item
e.g. Create Item class


10 
Mark New Item as ‘done’




11
Save Item




*
Repeat for 2nd item
e.g. Register Item Model







In todo / models.py:

#
Step
Code
Your Notes
12
Create a new __str__ dunder method
class Item(models.Model):
    name = models.CharField(max_length=50, null=False, blank=False)
    done = models.BooleanField(null=False, blank=False, default=False)

    def __str__(self):
        return self.name
Note: To allow the Item Names to be visible in the admin panel, override the string method in models.py
*
Run server to view changes
e.g. python3 manage.py runserver
In admin panel, items folder.


Note: For more examples of Models, check out Django Documentation Link.



----------------------------------------
Hello Django Instructions Sheet
Part 5: Rendering Data
Note: Now that we’ve saved our models data, we need to be able to render this data on our HTML templates for the users to be able to see.

5.1. Adding an item key
In todo / views.py:

#
Step
Code
Your Notes
1
Allow access to the item model in views.py
from django.shortcuts import render
from .models import Item

# Create your views here.
def get_todo_list(request):
    items = Item.objects.all()
    context = {
        'items': items
    }
    return render(request, 'todo/todo_list.html', context)
Note: Here we are importing all the items into the view and passing it into the template inside the context object. This means that we can display all the items' data inside.



5.2. Adding a ‘for’ loop
In todo / templates / todo / todo_list.html:

#
Step
Code
Your Notes
2
Render the items key from the context dictionary above. 
<body>
    <h1>Things to do</h1>
    {{ items }}
</body>
Note: Outputs a queryset (a type of list)


Note: Run server to view output

In todo / templates / todo / todo_list.html:

#
Step
Code
Your Notes
3
Adjust items key to use a for loop to create a table showing item.name and item.done
<body>
    <h1>Things to do</h1>
    {{ items }}

    <table>
        {% for item in items %}
            <tr>
                <td>{{ item.name }}</td>
                <td>{{ item.done }}</td>
            </tr>
        {% endfor %}
    </table>
</body>
Note: Can delete the items key

Note: Run server to view output

5.3. Adding an if statement

In todo / templates / todo / todo_list.html:

#
Step
Code
Your Notes
4
Add if / else statement 
<table>
        {% for item in items %}
            <tr>
                {% if item.done %}
                    <td><strike>{{ item.name }}</strike></td>
                {% else %}
                    <td>{{ item.name }}</td>
                {% endif %}
            </tr>
        {% endfor %}
    </table>




Note: For more examples of built in templates and tags, check out the Django Documentation Link
Note: Run server to view output

5.4. Handling empty list

In todo / templates / todo / todo_list.html:
#
Step
Code
Your Notes
4
Add empty tag
<table>
        {% for item in items %}
            <tr>
                {% if item.done %}
                    <td><strike>{{ item.name }}</strike></td>
                {% else %}
                    <td>{{ item.name }}</td>
                {% endif %}
            </tr>
            {% empty %}
            <tr><td>You have nothing to do</td></tr>
        {% endfor %}
    </table>
Note: Add just before the {{ endfor }} tag


Note: Run server to view output (must delete all items in list)


---------------------------------


