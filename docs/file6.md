## Django Templates
<p>A template in Django is basically written in HTML, CSS and Javascript in an .html file. Django framework efficiently handles and generates dynamically HTML web pages that are visible to end-user.Django mainly functions with a backend so, in order to provide frontend and provide a layout to our website, we use templates.</p>
<ul>
<li>Django provides a convenient way to generate dynamic HTML pages by using its template system,creatively called the Django template language (DTL)</li>
<li>A template consists of static parts of the desired HTML output as well as some special syntax describing how dynamic content will be inserted.</li>
</ul>

### Why Django Template ?
<ul>
<li>In HTML file, we can't write python code because the code is only interpreted by python interpreter not the browser. We know that HTML is a static markup language, while Python is a dynamic programming language.</li>
<li>Django template engine is used to separate the design from the python code and allows us to build dynamic web pages.</li>
</ul>

### Django Template Configuration

<p>To Configure the template system we have to provide some entries in settings.py file.</p>
<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/Templates.PNG" alt="Templates"
     width="600"/>
<p>Here, we mentioned that our template directory name is templates. By default, DjangoTemplates looks for a templates subdirectory in each of the INSTALLED_APPS.</p>

<p>we have to install some apps before the starting the project and created app name  must be placed in Installed_Apps.</p>

<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/Installedapps.PNG" alt="Templates" width="600"  />

### Django Templates Creation Procedure

<p> First create a Folder <b>Templates</b> inside the project app i.e firstapp.</p> 

<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/templatefoldercreation.PNG" alt="Templates" width="600" />

<p> Create a folder inside templates i.e <b>firstapp</b> inside firstapp create <b>index.html</b></p>

<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/creating_template(1).PNG" alt="Templates" width="600" />

<p>After creating a template we have to write a code in index.html.</p>

<p>Tempalte <b>index.html</b> contains the code.</p>

```html
<!DOCTYPE html>
<html>
<head>
	<title>My Project</title>
</head>
<body>
	<h2>Welcome to my project.!!!</h2>
</body>
</html>
```

<p>To Load or render our template need a view and url mapped to that view.Let's begin creating urls.py and views.py.</p>

<p>Mapping <b>index.html</b> to <b>urls.py</b><p> 

```python
from django.contrib import admin
from django.urls import path
from firstapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('index/',views.index,name='index'),
]
```

<p> From <b>urls.py</b> mapping to <b>views.py</b>.</p>

```python
from django.shortcuts import render
def index(request):
	return render(request,'firstapp/index.html',{})
```

<p>After mapping all these files we have to run the server,To run server we have to open our project directory and open command promt in that we have to use the command i.e <b>python manage.py runserver.</b></p>

<p>The output will appears like this</p>

<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/output.PNG" alt="Templates" width="600" />

<p> In that ouput we can see that at top of the page we have the title i.e <b>My Project</b> and also body part which we have written in the <b>index.html</b> page.</p>











 






