
* **Python web Frameworks :**
  * Django
  * Flask
  * web2py
  * Bottle
  * cherrypy
  * etc.....
### What is a web Framework?
 * A web framework or web application framework is a software framework that is designed to support the development of web applications including web services, web resources, and web APIs. Web frameworks provide a standard way to build and deploy web applications.

## Django Introduction :

### Why django Framework?
 * Django is a Python web framework
 * A Framework provides a structure and common methods to make the life of a web application developer much easier for building    flexible, scalable and maintainable web applications.

### What is Django ?

* A Python web framework is a code library that provide tools and libraties to simplify common web development operations.
* It is based on MVT (Model View Template) design pattern.
* Django is a high-level and has MVC,MVT styled Architecture.
* Django web framework is written on quick and powerful python language.
* Django has a open-source collection of libraries for building afully functioning web application.
* It takes less time to build application after collecting client requirement.

### Features of Django :

 * **very fast  :**
   * It works very fast.
 * **Fully Loaded  :**
   * Django includes various helping task modules and libraries which can be used to handle common Web development tasks. Django takes care of user authentication, content administration, site maps.
 * **Secure  :**
   * Its user authentication system provides a secure way to manage user accounts and passwords.
 * **Scalable  :**
   * Django is scalable in nature and has ability to quickly and flexibly switch from small to large scale application project.
* **OpenSource  :**
  * Django is versatile in nature which allows it to build applications for different-different domains.
  

### MVT Architecture of Django  :

* Every Web applications follows architectures
  * MVC (Model View Controller)
  * MVT (Model View Template)
  * etc..
* Django is a MVT pattern.
* MVC is slightly different from MVT as Django itself takes care of the Controller part.
<img src='https://raw.githubusercontent.com/SatheeshMatampalli/Django_myDocumentation/master/mvt-mvc.PNG' alt='mvc' />


* MVT is a software Design patern
* It is a collection of three important components Model View and Template.
* **Model  :**
  * The Model helps to handle database. It is a data access layer which handles the data.
* **Template  :**
  * The Template is a presentation layer which handles User Interface part completely.
* **View  :**
  * The View is used to execute the business logic and interact with a model to carry data and renders a template.

<img src='https://raw.githubusercontent.com/SatheeshMatampalli/Django_myDocumentation/master/mvt.png' alt='mvt' />
  
* Here, a user requests for a resource to the Django, Django works as a controller and check to the available resource in URL.If URL maps, a view is called that interact with model and template, it renders a template.Django responds back to the user and sends a template as a response.

## **Django Installation :**
  * **download python from website based on your system properties 64/32.** [Download Link](https://www.python.org/downloads/windows/)**
  	* Prefer to python version is 3.7.6
	* if we use below 3.4.3 version we need to give manual path for python and scripts,otherwise pip does'nt work.
  * **Download sublimetext or any other editor tools for editing purpose.**.[Download Link](https://www.sublimetext.com/3)
  * ceck wheather 'pip' is working or not in the 'cmd'
  
  <img src='https://raw.githubusercontent.com/SatheeshMatampalli/Django_myDocumentation/master/pip.PNG' alt='pip' />
  
  * install django # # (latest Version 3.0) wait for installation
  * if you want perticular version then try `pip install Django==3.0.1"` or 
  * By Default version try `pip install django`
  
  <img src='https://raw.githubusercontent.com/SatheeshMatampalli/Django_myDocumentation/master/django.PNG' alt='django' />
  
  * After installing to check the version of Django Framework.
    ```
    
       cmd>django-admin --version
                 (or)
       cmd>python
       >>>import django
       >>>django.get_version()    or    django.VERSION
          '1.11'                   (1,11,0, 'final',1)
<img src='https://raw.githubusercontent.com/SatheeshMatampalli/Django_myDocumentation/master/dversion.PNG' alt='dvers' />
	  
	  
## **Project Creation**
* Now, to create a Project in spcefied folder where to do and now open cmd in same path :
	```
			   path		                   creating project
	    D:\Satheesh\MyPractice>django-admin startproject College(projectname)
	    D:\Satheesh\MyPractice>cd College
	    D:\Satheesh\MyPractice\College
	    
	    
<img src='https://raw.githubusercontent.com/SatheeshMatampalli/Django_myDocumentation/master/project.PNG' alt='project' />
	    
<img src='https://raw.githubusercontent.com/SatheeshMatampalli/Django_myDocumentation/master/folder11.PNG' alt='folder1' />	    
	    
* Present we are in our Django Project(College) path.
* Check in browser wheather its working or not
  	```
	    D:\Satheesh\MyPractice\College>python manage.py runserver
	    localhost:8000/
	    it is localhost address --> http://127.0.0.1:8000/
	    it worked..!
	    
<img src='https://raw.githubusercontent.com/SatheeshMatampalli/Django_myDocumentation/master/view.PNG' alt='view' />
  
## **App Creation in Project**
* Create a new App in Project
	```
	D:\Satheesh\MyPractice\College>python manage.py startapp appname(Students)
	D:\Satheesh\MyPractice\College>python manage.py runserver
	localhost:8000/
	it is localhost address --> http://127.0.0.1:8000/
<img src='https://raw.githubusercontent.com/SatheeshMatampalli/Django_myDocumentation/master/app.PNG' alt='app' />	
<img src='https://raw.githubusercontent.com/SatheeshMatampalli/Django_myDocumentation/master/folder11.PNG' alt='folder11' />
		
## **urls.py :**
* we have defaultly urls.py in  our created project(College) but we dont have urls.py in our own app so we should create new file with name urls.py in our own App(Students).
* Now we find the Students App in our project(College).
* Now goto Students app folder and create "urls.py" file and add like this

  	```
	from django.urls import path
	from Students import views
	urlpatterns=[
		path('index/',views.index,name="index"),

	]

> _NOTE:_ here i am importing views from Students app and mentioned one path because,if we browse localhost:8000/Students/index then it goes to views part index function and gives return template as a output. 

* goto (Students/views.py file) Students folder open views.py file and add like this.
	```
		
	from django.shortcuts import render
	from django.http import HttpResponse
	def index(request):
			return HttpResponse("<h2>Hello World</h2>")
			
* **HttpResponse  :** is a response class with string data. While HttpRequest is created by Django, HttpResponse is created by programmer.
* Create a function index in the views.py file. This function will be mapped from the Students/urls.py file.

> **_NOTE:_** import HttpResponse from http package and defining the function index.

* goto (College/urls.py file) College folder open urls.py file and add like this.
	
* Django already has mentioned a URL here for the admin. The path function takes the first argument as a route of string or regex type.The view argument is a view function which is used to return a response (template) to the user.


	
		from django.contrib import admin
		from django.urls import path,include
		from appname(Students) import views
		urlpatterns = [
	   		path('admin/', admin.site.urls),
			path('Students/',include('Students.urls'))
			]

* here we are importing the include because all the app urls are need to include in project urls.py file,so we are import include and giving path for browser.
* check in browser. localhost:8000/Students/index


	<img src='https://raw.githubusercontent.com/SatheeshMatampalli/Django_myDocumentation/master/output.PNG' width="50%" height="30%" alt='output' />

* In anothe rway to represent url is without creating urls.py file in app Students add path in project urls.py file and import the Students app views in project urls.py file follow like this...
	```
		from django.contrib import admin
		from django.urls import path
		from appname(Students) import views
		urlpatterns = [
	   		path('admin/', admin.site.urls),
			path('index/',views.index,name='index'),
			]
		

* check in browser. localhost:8000/index

<img src='https://raw.githubusercontent.com/SatheeshMatampalli/Django_myDocumentation/master/output.PNG' width="50%" height="30%" alt='output' />


* **You will get Hello World message**
