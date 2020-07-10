## Django topics we will learn
* ORM
* Models
* Using models
* Migrations
* Model Queries using django shell
* Superuser and Role of superuser


### Prefaces

* You should create project(simpleproject) and app(simpleapp) for understanding.

* Here i am refering **YOUR_APP_NAME** means you should replace with your created django app name

* and **YOUR_PROJECT_NAME** means you should replace with your created django project name

* greater-than signs (>>>) signify a Python prompt.


###  ORM(Object Relational Mapper)     
Object Relational Mapper presents a method of associating user-defined Python classes with database tables, and instances of those classes (objects) with rows in their corresponding tables. 

It includes a system that transparently synchronizes all changes in state between objects and their related rows, called a unit of work, as well as a system for expressing database queries in terms of the user defined classes and their defined relationships between each other.


ORM provides many tools to express queries without writing raw SQL

#### Fields
The most important part of a model – and the only required part of a model – is the list of database fields it defines.
Fields are specified by class attributes. Be careful not to choose field names that conflict with the **models API** like clean, save, or delete.

#### Field types

Each field in your model should be an instance of the appropriate Field class. Django uses the field class types to
determine a few things:
* The column type, which tells the database what kind of data to store (e.g. INTEGER, VARCHAR, TEXT).
* The default HTML widget to use when rendering a form field (e.g. ```<input type="text">, <select>```).

* The minimal validation requirements, used in Django’s admin and in automatically-generated forms.



#### Field options
Each field takes a certain set of field-specific arguments For example,
```CharField``` (and its subclasses) require a ```max_length``` argument which specifies the size of the **VARCHAR** database
field used to store the data.

Here’s a quick summary of the most often-used ones:

```null``` If True, Django will store empty values as **NULL in the database**. Default is False.

```blank``` If True, the field is allowed to be blank. Default is False.

> **_Note:_** 
  that **this is different than null**. **null is purely database-related, whereas blank is validation-related**. 
  If a field has blank=True, form validation will allow entry of an empty value. If a field has blank=False,the field will be required.


```choices``` A sequence of 2-tuples to use as choices for this field. If this is given, the default form widget will be a
select box instead of the standard text field and will limit choices to the choices given.


A choices list looks like this:

```gender_vals = [('Male','Male'),('FeMale','FeMale')]```

The first element in each tuple is the value that will be stored in the database. The second element is displayed
by the field’s form widget.



```default``` The default value for the field. This can be a value or a callable object. If callable it will be called every
time a new object is created.

```help_text``` Extra “help” text to be displayed with the form widget. It’s useful for documentation even if your field
isn’t used on a form.

```primary_key``` If True, this field is the primary key for the model.

If you don’t specify ```primary_key=True``` for any fields in your model, Django will automatically add an
```IntegerField``` to hold the primary key, so you don’t need to set primary_key=True on any of your
fields unless you want to override the default primary-key behavior.

### Relationships

Clearly, the power of relational databases lies in relating tables to each other. Django offers ways to define the three
most common types of database relationships: **many-to-one**, **many-to-many** and **one-to-one**.

#### Many-to-one relationships
To define a many-to-one relationship, use ```django.db.models.ForeignKey```. You use it just like any other
```Field``` type: by including it as a class attribute of your model.

```ForeignKey``` requires a positional argument: the class to which the model is related.


For example, if a Car model has a Manufacturer – that is, a Manufacturer makes multiple cars but each Car
only has one Manufacturer – use the following definitions:


```
from django.db import models
class Manufacturer(models.Model):
    name = models.CharField(max_length=100)
class Car(models.Model):
    manufacturer = models.ForeignKey(Manufacturer, on_delete=models.CASCADE)
```

If you delete a manufacturer, his cars will be deleted (assuming that the ForeignKey was defined with django.db.
models.ForeignKey.on_delete set to CASCADE, which is the default):


#### Many-to-many relationships
To define a many-to-many relationship, use ```ManyToManyField```. You use it just like any other Field type: by including it as a class attribute of your model

```ManyToManyField``` requires a positional argument: the class to which the model is related.

For example, if a Pizza has multiple Topping objects – that is, a Topping can be on multiple pizzas and each
Pizza has multiple toppings – here’s how you’d represent that:

```
from django.db import models
class Topping(models.Model):
    # ...
    pass
class Pizza(models.Model):
    # ...
    toppings = models.ManyToManyField(Topping)
```

It doesn’t matter which model has the ManyToManyField, but you should only put it in one of the models – not
both.

#### One-to-one relationships
To define a one-to-one relationship, use ```OneToOneField```.You use it just like any other Field type: by including it as a class attribute of your model.

This is most useful on the primary key of an object when that object “extends” another object in some way.

```OneToOneField``` requires a positional argument: the class to which the model is related.


Once you’ve created your data models, Django automatically gives you a database-abstraction API that lets you create, retrieve, update and delete objects. 




###  Models
A model is the single, definitive source of information about your data. It contains the essential fields and behaviors
of the data you’re storing. Generally, each model maps to a single database table.

The basics:
* Each model is a Python class that subclasses **django.db.models.Model**.
* Each attribute of the model represents a database field.
* With all of this, Django gives you an automatically-generated database-access API.

#### Quick Example
This example model defines a **Register**, which has a **firstName**,**lastName**,**emailId**,**phoneNo**,**age**,**gender**,**date_of_birth** are the **fields** of the model.Each field is specified as a class attribute, and each attribute
maps to a database column.

> **_Note:_** for learning practically please do the steps which i am provided and indicated by <b>step- number</b>

**step-1** do in **YOUR_PROJECT_NAME/YOUR_APP_NAME/models.py**

```
from django.db import models

class Register(models.Model):
    gender_vals = [('Male','Male'),('FeMale','FeMale')]
    firstName = models.CharField(max_length=100)
    lastName = models.CharField(max_length=100)
    emailId = models.MailField(null = True)
    phoneNo = models.CharField(max_length=10)
    age = models.IntegerField(null=True)
    gender = models.CharField(max_length=10,choices=gender_vals )
    date_of_birth = models.DateField(null=True)

  def __str__(self):
    return str(firstName)

```

**end-step-1**

The above **Register**  model would create a database table like this:
```


CREATE TABLE "YOUR_APP_NAME_register" (
    "id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, 
    "firstName" varchar(100) NOT NULL, 
    "lastName" varchar(100) NOT NULL, 
    "emailId" varchar(254) NULL, 
    "phoneNo" varchar(10) NOT NULL, 
    "age" integer NULL, 
    "gender" varchar(10) NOT NULL, 
    "date_of_birth" date NULL, 
);

```

> **_Some technical notes:_**
  * The name of the table, **YOUR_APP_NAME_register**, here appName is your django app name related to your model.
  * An id field is added automatically, but this behavior can be overridden.
  * The CREATE TABLE SQL in this example is formatted using PostgreSQL syntax, but it’s worth noting Django uses SQL tailored to the database backend specified in your **settings** file

### Using models
Once you have defined your models, you need to tell Django you’re going to use those models. Do this by editing your **settings.py** file and changing the **INSTALLED_APPS** setting to add the name of the module that contains your
models.py.



For example, if the models for your application live in the module myapp.models (the package structure that is
created for an application by the manage.py startapp script), INSTALLED_APPS should read, in part:


**step-2** do in **settings.py**

```
INSTALLED_APPS = [
    #...
    'YOUR_APP_NAME',
    #...
]
```

**end-step-2**

> **_Note:_** for above code **#...** means you don't need to modify existing code.You just need to add **YOUR_APP_NAME**.

When you add new apps to INSTALLED_APPS, be sure to run manage.py migrate, optionally making migrations for them first with manage.py makemigrations.


### Migrations
It is the Django’s way of propagating changes you make to your models (adding a field, deleting a model,
etc.)

There are several commands which you will use to interact with migrations and Django’s handling of database schema:
*  ```migrate```, which is responsible for applying and unapplying migrations.
* ```makemigrations```, which is responsible for creating new migrations based on the changes you have made to your models.
* ```sqlmigrate```, which displays the SQL statements for a migration.
* ```showmigrations```, which lists a project’s migrations and their status

**step-3** Now we can apply migrations to our model

open the **command prompt** from the location of project's **manage.py**

in cmd run below commands

```python manage.py makemigrations```

```python manage.py sqlmigrate YOUR_APP_NAME 0001```

```python manage.py migrate```

> **_Note_** Here 0001 is the latest migrations number generated by makemigrations command
you have to replace 0001 by your latest number



**end-step-3**



### Model Queries using django shell

Now we will practice **CRUD** operations from **command prompt**

**step-4**

open the **command prompt** from the location of project's **manage.py**

run the command ``` python manage.py shell ``` to get interactive shell to work

**end-step-4**

#### Creating objects

To represent database-table data in Python objects, Django uses an intuitive system: A model class represents a database table, and an instance of that class represents a particular record in the database table.

To create an object, instantiate it using keyword arguments to the model class, then call **save()** to save it to the
database.

Assuming models live in a file **YOUR_PROJECT_NAME/YOUR_APP_NAME/models.py**

**step-5** do from current  shell(already we done in step-4)

```
>>> from YOUR_APP_NAME.models import Register
>>> from datetime import date
>>> obj = Register(
              firstName='haritha',
              lastName='h',
              emailId='haritha.h@example.com',
              phoneNo = '9895051914',
              age = 20,
              gender = 'FeMale',
              date_of_birth = date.today()              
           )
>>> obj.save()
```

This performs an INSERT SQL statement behind the scenes. Django doesn’t hit the database until you explicitly call
save().

#### Retrieving objects
To retrieve objects from your database, construct a QuerySet

#### Retrieving all objects
The all() method returns a QuerySet of all the objects in the database.

```
>>> all_rows=Register.objects.all()
```

#### Retrieving specific objects with filters
example to get a QuerySet of date_of_birth  from the year 2020

```
>>> register_set = Register.objects.filter(date_of_birth__year=2020)
>>> for row in register_set:
...    print(row.name)
...

```

#### Retrieving a single object with get()

filter() will always give you a QuerySet, even if only a single object matches the query - in this case, it will be
a QuerySet containing a single element.

If you know there is **only one object** that matches your query, you can use the **get()** method

```
>>> register_row = Register.objects.get(emailId='haritha.h@example.com')
   
```

#### Saving changes to objects in 3 simple steps
1. get the existing object
2. do the modification
3. save the object

```
>>> register_row = Register.objects.get(emailId='haritha.h@example.com')
>>> register_row.age = 21
>>> register_row.save()
```

#### Deleting objects in 2 simple steps
1. get the existing object
2. delete the object

```
>>> register_row = Register.objects.get(emailId='haritha.h@example.com')
>>> register_row.delete()
```

if we want to exit from shell use below command 

```
>>> exit()
```

**end-step-5**

### Superuser and Role of superuser

Giving all permissions to particular user(admin).

Generating admin sites for your staff or clients to add, change, and delete content is tedious work that doesn’t require
much creativity. For that reason, Django entirely automates creation of admin interfaces for models

> **_Note:_**
  * The admin isn’t intended to be used by site visitors. It’s for site managers.


**step-6**

open the command prompt from the location of project's **manage.py**

First we’ll need to create a user who can login to the admin site. Run the following command:

```
python manage.py createsuperuser
```

Enter your desired username and press enter

```
Username: admin
```

You will then be prompted for your desired email address:

```
Email address: admin@example.com
```

The final step is to enter your password. You will be asked to enter your password twice, the second time as a
confirmation of the first

```
Password: **********
Password (again): *********
```

**end-step-6**

finally you will get **Superuser created successfully** message.

**Start the development server**

```
python manage.py runserver
```

Now, open a Web browser and go to “/admin/” on your local domain – e.g., http://127.0.0.1:8000/admin/


#### If you want to manage app from admin do step-7

**step-7** do this in YOUR_PROJECT_NAME/YOUR_APP_NAME/admin.py

```
from django.contrib import admin

# Register your models here.

from YOUR_APP_NAME.models import Register


admin.site.register(Register)
```

**end-step-7**

