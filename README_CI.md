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


Hello Django Instructions Sheet
Part 6: Rendering a Create New Item page
Note: While our superuser has full functionality using the admin panel, we also want our general users to be able to Create, Read, Update, and Delete resources on the front end. This is referred to as CRUD functionality (Create, Read, Update and Delete). 

6.1. Duplicate the todo_list.html file

In todo / templates / todo:

#
Step
Code
Your Notes
1
Duplicate the todo_list.html file
e.g. Rename as “add_item.html”
Note: You can Copy and Paste the file in the same folder to duplicate.


In todo / templates / todo / add_item.html:

#
Step
Code
Your Notes
2
Delete the table and its contents
<table>
      ...
</table>


3
Update the heading
<body>
    <h1>Add a ToDo Item:</h1>
</body>




In todo / templates / todo / todo_list.html:

#
Step
Code
Your Notes
4
Add a link to the add_item file
<a href = "/add">Add an Item</a>
Note: Place below the table


6.2. Add views

In todo / views.py:

#
Step
Code
Your Notes
5
Create an add_item view
def add_item(request):
    return render(request, 'todo/add_item.html')
Note: Place below the get_todo_list method.



6.3. Add urls

In django_todo / urls.py:

#
Step
Code
Your Notes
6
Create new add_item path, and import add_item
from django.contrib import admin
from django.urls import path
from todo.views import get_todo_list, add_item

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', get_todo_list, name='get_todo_list'),
    path('add', add_item, name='add'),
]




Note: Run server to view output


6.4. Add an Add Item Form

Note: Django Forms are basically used for taking input from the user in some manner and using that information for logical operations on databases. For example, registering a user by taking input as his name, email, password, etc.

In todo / templates / todo / add_item.html:

#
Step
Code
Your Notes
7
Create a form to enter your new item information
    <form method="POST" action="add">
        <div>
            <p>
                <label for = "id_name">Name:</label>
                <input type="text" id="id_name" name="item_name" />
            </p>
        </div>
        <div>
            <p>
                <label for = "id_done">Done:</label>
                <input type="checkbox" id="id_done" name="done" />
            </p>
        </div>
        <div>
            <p>
                <button type="submit">Add Item</button>
            </p>
        </div>
    </form>
Note: Place below the h1 tag


6.5. Add a Template Tag

Note: Template Tags are used to secure the data being sent 

In todo / templates / todo / add_item.html:

#
Step
Code
Your Notes
8
Add csrf token tag
{% csrf_token %}
Note: Place just inside the form tag



6.6. Handle Form Submit Action

In todo / views.py:

#
Step
Code
Your Notes
9
import redirect
from django.shortcuts import render, redirect


10
Handle Form Submit
def add_item(request):
    if request.method == 'POST':
        name = request.POST.get('item_name')
        done = 'done' in request.POST
        Item.objects.create(name=name, done=done)

        return redirect('get_todo_list')
    return render(request, 'todo/add_item.html')


Note: Place within the add_item function


Note: Run server to view output

_________________________

Hello Django Instructions Sheet
Part 7: Modifying Data

7.1. Using Forms

In the File Tree:

#
Step
Code
Your Notes
1
In the APP folder i.e. todo, create a new file, forms.py
e.g. todo / forms.py




In todo / forms.py:

#
Step
Code
Your Notes
2
Add your imports
from django import forms
from .models import Item


3
Create your ItemForm class
class ItemForm(forms.ModelForm): 
    class Meta:
        model = Item
        fields = ['name', 'done']


Note: the Meta class gives our form some information about itself, such as which fields to render, or how to display errors

Note: Remember, the fields: ‘name’ and ‘done’, have already been defined in models.py



In todo / views.py:

#
Step
Code
Your Notes
4
Import the ItemForm
…
from .forms import ItemForm


5
Create an instance of the ItemForm and add the context
def add_item(request):
    if request.method == 'POST':
        …
        return redirect('get_movie_list')
    form = ItemForm()
    context = {
        'form': form
    }
    return render(request, 'todo/add_item.html', context)
Note: Don’t forget to return the context to the template in the render method





In todo / templates / todo / add_item.html:

#
Step
Code
Your Notes
4
Delete the initial 2 divs containing the input fields
<form method="POST" action="add">
        {% csrf_token %}
        <div>
            <p>
                <label for = "id_name">Name: </label>
                <input type="text" id="id_name" name="item_name" />
            </p>
        </div>
        <div>
            <p>
                <label for = "id_done">Done: </label>
                <input type="checkbox" id="id_done" name="done" />
            </p>
        </div>
        <div>
            <p>
                <button type="submit">Add Item</button>
            </p>
        </div>
    </form>
Note: Leave the div containing the submit button
5
Replace these divs with the form template variable
<form method="POST" action="add">
        {% csrf_token %}
        {{ form }}
        <div>
            <p>
                <button type="submit">Add Item</button>
            </p>
        </div>
    </form>




Note: At this stage, running the code will give an integrity error. This is because in views.py / add_item, we are still creating our form items manually, whereas we should let our new form ‘forms.py’ do this.


In todo / views.py:

#
Step
Code
Your Notes
6
Replace the name and done fields, and Item.objects.create
def add_item(request):
    if request.method == 'POST':
        form  = ItemForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('get_todo_list')
    form = ItemForm()
    context = {
        'form': form
    }
    return render(request, 'todo/add_item.html', context)




In todo / templates / todo / add_item.html:

#
Step
Code
Your Notes
7
Adjust the styling of the form
<form method="POST" action="add">
        {% csrf_token %}
        {{ form.as_p }}
Note: Adjusts to vertical styling



7.2. Editing an Item

In todo / templates / todo / todo_list.html:

#
Step
Code
Your Notes
1
Add an edit button to each table row 
 <table>
        {% for item in items %}
            ...
                {% endif %}
                <td>
                    <a href="/edit/{{ item.id }}">
                        Edit
                    </a>
                </td>
            </tr>
            ...
        {% endfor %}
    </table>
Note: Place it within the for loop, below the endif statement

Note: The Postgres database will automatically create an id for each item you add. You can then use this item id as a url identifier. 



In the File Tree:

#
Step
Code
Your Notes
2
In the todo / templates / todo folder, duplicate the add_item.html file
Rename to edit_item.html




In todo / templates / todo / edit_item.html:

#
Step
Code
Your Notes
3
Adjust the code
<body>
    <h1>Edit a ToDo Item:</h1>
    <form method="POST" action="add">
        {% csrf_token %}
        {{ form.as_p }}
        <div>
            <p>
                <button type="submit">Update Item</button>
            </p>
        </div>
    </form>
</body>
Important: Don’t forget to delete the action property, as shown.



In django_todo / urls.py:

#
Step
Code
Your Notes
4
Add path
urlpatterns = [
    ...
    path('edit/<item_id>', edit_item, name='edit'),
]
Note: edit/<item_id> links to the edit_item page for a particular item_id. This item_id has been automatically created. 
5
Import edit_item
...
from todo.views import get_todo_list, add_item, edit_item




Note: Run server to view output (form still incomplete)

In todo / views.py:

#
Step
Code
Your Notes
6
Create an instance of the form and return it as a context
def edit_item(request, item_id):
    item = get_object_or_404(Item, id=item_id)
    form = ItemForm(instance=item)
    context = {
        'form': form
    }
    return render(request, 'todo/edit_item.html', context)
Note: Don’t forget to add ‘item_id’ as a parameter to your function. 

Note: get_object_or_404 will either return the item if it exists or return a 404 error.
7
Import the get_object_or_404 shortcut
from django.shortcuts import render, redirect, get_object_or_404




Note: Run server to view output (update functionality still not working)

In todo / views.py:

#
Step
Code
Your Notes
6
Add the POST handle functionality (similar to add_item)
def edit_item(request, item_id):
    item = get_object_or_404(Item, id=item_id)
    if request.method == 'POST':
        form=ItemForm(request.POST, instance=item)
        if form.is_valid():
            form.save()
            return redirect('get_todo_list')
    form = ItemForm(instance=item)
    context = {
        'form': form
    }
    return render(request, 'todo/edit_item.html', context)




Note: Run server to view output

7.3. Toggling an Item

In todo / templates / todo / todo_list.html:

#
Step
Code
Your Notes
1
Add a toggle button to each table row 
   <table>
        {% for item in items %}
           ...
                {% endif %}
                <td>
                    <a href="/toggle/{{ item.id }}">
                        Toggle
                    </a>
                </td>
               ...
        {% endfor %}
    </table>
Note: Place below the endif statement above the edit row


In django_todo / urls.py

#
Step
Code
Your Notes
2
Add a path
urlpatterns = [
    ...
    path('toggle/<item_id>', toggle_item, name='toggle'),
]


3
Import toggle_item
…
​​from todo.views import get_todo_list, add_item, edit_item, toggle_item




In django_todo / urls.py

Note: As our imports are now getting quite long, we can instead import from views.

#
Step
Code
Your Notes
4
Remove the existing imports
…
​​from todo.views import get_todo_list, add_item, edit_item, toggle_item


5
Replace with import views
…
​​from todo import views


6
Adjust each path view by adding views.(view_name)
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.get_todo_list, name='get_todo_list'),
    path('add', views.add_item, name='add'),
    path('edit/<item_id>', views.edit_item, name='edit'),
    path('toggle/<item_id>', views.toggle_item, name='toggle'),
]
Note: Don’t forget to adjust the rest of the paths as well as the toggle path



In todo / views.py

#
Step
Code
Your Notes
7
Add toggle_item view function
def toggle_item(request, item_id):
    item = get_object_or_404(Item, id=item_id)
    item.done = not item.done
    item.save()
    return redirect('get_todo_list')
Note: Place below (but separate) to the edit_item function


Note: Run server to view output


7.4. Deleting an Item

In todo / views.py

#
Step
Code
Your Notes
1
Add the delete_item view function
def delete_item(request, item_id):
    item = get_object_or_404(Item, id=item_id)
    item.delete()
    return redirect('get_todo_list')
Note: Place below the toggle_item function



In django_todo / urls.py

#
Step
Code
Your Notes
2
Add a delete path
urlpatterns = [
    ...
    path('delete/<item_id>', views.delete_item, name='delete'),
]
Note: Don’t need to import the view this time.



In todo / templates / todo / todo_list.html:

#
Step
Code
Your Notes
3
Add a delete button to each table row 
    <table>
        {% for item in items %}
            ...
                <td>
                    <a href="/delete/{{ item.id }}">
                        Delete
                    </a>
                </td>
            </tr>
            {% empty %}
            ...
        {% endfor %}
    </table>
Note: Place below the edit button row



_________________________________

Hello Django Instructions Sheet
Part 8: Testing
Note: ​​When you’re writing new code, you should use tests to validate that your code works as expected.

8.1. Introduction to Django Testing

In todo / tests.py

#
Step
Code
Your Notes
1
Create your first test
class TestDjango(TestCase):

    def test_this_thing_works(self):
        self.assertEqual(1, 0)







In the Terminal

#
Step
Code
Your Notes
2
Run tests
python3 manage.py test
Note: Test fails. Try making it pass yourself.



In todo / tests.py

#
Step
Code
Your Notes
3
Replace the current test with 4 more tests
class TestDjango(TestCase):

    def test_this_thing_works(self):
        self.assertEqual(1, 1)

    def test_this_thing_works2(self):
        self.assertEqual(1, 3)

    def test_this_thing_works3(self):
        self.assertEqual(1, )

    def test_this_thing_works4(self):
        self.assertEqual(1, 4)
Note:
pass (.)
fail (F)
error (E)
fail (F)


Note: Run Tests in terminal again.

In todo / tests.py

#
Step
Code
Your Notes
4
Delete all but the first test
class TestDjango(TestCase):

    def test_this_thing_works(self):
        self.assertEqual(1, 1)





In the Terminal

#
Step
Code
Your Notes
5
Rename the test file
e.g. test_views.py


6
Create 2 new files
e.g. test_models.py,
e.g. test_forms.py
Note: you should have 3 test files in total.



8.2. Testing Forms

In todo / test_forms.py

#
Step
Code
Your Notes
1
Add your imports
from django.test import TestCase
from .forms import ItemForm


2
Create your first test
class TestItemForm(TestCase):

    def test_item_name_is_required(self):
        form = ItemForm({'name': ''})
        self.assertFalse(form.is_valid())
        self.assertIn('name', form.errors.keys())
        self.assertEqual(form.errors['name'][0], 'This field is required.')
Note: 
creates a form instance with an empty name field
checks this field is not valid
checks that there is a ‘name’ key in the dictionary of form errors
Check whether the error message on the name key is “This field is required.”
3
Create your second test
    def test_done_field_is_not_required(self):
        form = ItemForm({'name': 'Test Todo Items'})
        self.assertTrue(form.is_valid())
Note:
Create a form instance with a name field of ‘Test Todo Items’
Checks that this instance is valid (even without selecting a ‘done’ status)
4
Create your third test
    def test_fields_are_explicit_in_form_metaclass(self):
        form = ItemForm()
        self.assertEqual(form.Meta.fields, ['name', 'done'])
Note:
Create an empty form instance 
check that the meta fields are equal to ‘name’ and ‘done.


In the Terminal

#
Step
Code
5
Run a specific test e.g. test_forms.py
python3 manage.py test todo.test_forms
6
Run a specific class of tests
python3 manage.py test todo.test_forms.TestItemForm
7
Run an individual test
python3 manage.py test todo.test_forms.TestItemForm.test_fields_are_explicit_in_form_metaclass


8.3. Testing Views

In todo / test_views.py

#
Step
Code
Your Notes
1
Add your imports
from django.test import TestCase
from .models import Item


2
Create your first test
class TestViews(TestCase):

    def test_get_todo_list(self):
        response = self.client.get('/')
        self.assertEqual(response.status_code, 200)
        self.assertTemplateUsed(response, 'todo/todo_list.html')
Note: 
Save the homepage instance (‘/’) as response
check that the response code is 200
check that the template used, ‘todo/todo_list.html’ is the same as ‘response’
3
Create your second test
    def test_get_add_item_page(self):
        response = self.client.get('/add')
        self.assertEqual(response.status_code, 200)
        self.assertTemplateUsed(response, 'todo/add_item.html')
Note: Similar to test_get_todo_list. Don’t forget to adjust the url and template name.
4
Create your third test
    def test_get_edit_item_page(self):
        item = Item.objects.create(name='Test Todo Item')
        response = self.client.get(f'/edit/{item.id}')
        self.assertEqual(response.status_code, 200)
        self.assertTemplateUsed(response, 'todo/edit_item.html')
Note: 
create an Item Object
save the response for that item
assert this item response code is 200
assert the template used is ‘edit_item.html’
5
Create your fourth test
    def test_can_add_item(self):
        response = self.client.post('/add', {'name': 'Test Added Item'})
        self.assertRedirects(response, '/')


Note: 
Create a new item 
check it redirects to the home page
6
Create your fifth test
    def test_can_delete_item(self):
        item = Item.objects.create(name='Test Todo Item')
        response = self.client.get(f'/delete/{item.id}')
        self.assertRedirects(response, '/')
        existing_items = Item.objects.filter(id=item.id)
        self.assertEqual(len(existing_items), 0)
Note: 
Create a new item object instance
delete this item
assert that it redirects to the home page
Try to return the item from the database using filter and the item_id
Check the length of existing_items = 0
7
Create your sixth test
    def test_can_toggle_item(self):
        item = Item.objects.create(name='Test Todo Item', done=True)
        response = self.client.get(f'/toggle/{item.id}')
        self.assertRedirects(response, '/')
        updated_item = Item.objects.get(id=item.id)
        self.assertFalse(updated_item.done)


Note: 
Create a new item object instance with done=True
toggle this item so done=False
assert that it redirects to the home page
Get the item again and save as updated_item
Check the done status is False


Note: You should run each of your tests as you write them to reduce the chances of making an error. 

Note: If you do fail any tests, be sure to read your Error Messages. 
8.4. Testing Models

In todo / test_models.py

#
Step
Code
Your Notes
1
Add your imports
from django.test import TestCase
from .models import Item


2
Create your first test
class TestModels(TestCase):

    def test_done_defaults_to_false(self):
        item = Item.objects.create(name='Test Todo Item')
        self.assertFalse(item.done)


Note:
create a new item instance
check that item.done is False


Note: Run tests


8.5. Coverage

Note: We can use this tool to check what percentage of our code we have actually tested.

In the Terminal:

#
Step
Code
Your Notes
1
Install the Coverage tool
pip3 install coverage


2
Run Coverage
coverage run --source=todo manage.py test


3
View Coverage Report
coverage report
Note: Check Report Results. 
4. 
Create HTML Report
coverage html


5
View HTML Report
python3 -m http.server
Note: Check Report Results. 


Note: Our report shows us we haven’t fully tested our application. We should now complete our tests using the report.

In the Browser:

#
Step
Code
Your Notes
6
Open the .htmlcov folder in the html directory
e.g. .htmlcov


*
Click to view different files
e.g. todo/models.py
Note: Haven’t tested the string method.


In todo / test_models.py:

#
Step
Code
Your Notes
7
Create a test for the string method
    def test_item_string_method_returns_name(self):
        item = Item.objects.create(name='Test Todo Item')
        self.assertEqual(str(item), 'Test Todo Item')
Note:
Create a new item instance
Check it equals to the string returned by the __str__ method i.e. self.name


Note: Rerun coverage, regenerate the report, and check again. 

In todo / test_views.py:
#
Step
Code
Your Notes
8
Create a test for ‘can edit item’
    def test_can_edit_item(self):
        item = Item.objects.create(name='Test Todo Item')
        response = self.client.post(f'/edit/{item.id}', {'name': 'Updated Name'})
        self.assertRedirects(response, '/')
        updated_item = Item.objects.get(id=item.id)
        self.assertEqual(updated_item.name, 'Updated Name')
Note: 
Create an item Instance
Edit the item using Post to “Updated Name”
Check it redirects to home
Save the edited item as updated_item
Check this edited item equals ‘Updated Name”


Note: Rerun coverage, regenerate the report, and check again. We have achieved a 97% coverage score. 

