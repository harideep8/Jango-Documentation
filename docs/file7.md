## Django Static Files Handling

### Why Static Files?

<p>In a web application, apart from business logic and data handling, we also need to handle and manage static resources like CSS, JavaScript, images etc.</p>

<p>It is important to manage these resources so that it does not affect our application performance.</p>

<p>Django deals with it very efficiently and provides a convenient manner to use resources.</p>

<p>Today, websites have become much more interactive than ever. They contain tons of CSS and JavaScript Code to make our experience smoother.</p>

<p>There are lots of graphics involved on websites too. Our Python Tutorials Home Page is the best example. There are outputs and screenshots and these images are important for the blog. So, from this, we can state that there are multiple files on a webpage.</p>

<p>Important point is that <i>none of these files can be modified by the server</i>. It means these files are transmitted as it is, without any modification.</p>

### What are Static files?

<i>Static files are those files which can not be processed, generated or modified by the server.</i>

<p>There is a catch here. Images, JavaScript files, etc are types of content or static files. Static files contain all kinds of file types – from .mpeg, .jpeg to .pdf, etc.There is a simple concept of working with static files. When a user requests for a webpage, the server will generate the HTML. Then the server will collect all the corresponding static files related to that page. Lastly, this whole data is served.</p>

<p>You can see that process in this flow-diagram. Also, we can say that static websites are much faster than dynamic websites.</p>

<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/staticex.PNG" alt="Templates" width="600"  />

#### Benefits of Static Files
<ul>
<li><b>They are static:</b> These files don’t change until the developer replace them with a new one. Thus, the server just fetches them from the disk, taking a minimum amount of time.</li>
<li><b>Static files are easier to cache:</b> They don’t change and are not modified by the server. That makes the performance faster.</li>
  <li><b>Static files are energy efficient:</b> Static files are fetched from the disk when required. They require no processing which saves the processing overhead and website response becomes fast.</li>
</ul>

## Django Static (CSS, JavaScript, images) Configuration
<ul>
<li>Include the <b>django.contrib.staticfiles</b> in <b>INSTALLED_APPS</b>.</li>
</ul>
<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/Installedapps.PNG" alt="Templates" width="600"  />
<ul>
<li>Define STATIC_URL in settings.py file as given below.</li>
</ul>

```python
STATIC_URL = '/static/'  
```

<ul>
<li>Load static files in the templates by using the below expression.</li>
</ul>

```html
{% load static %}  
```

<ul>
<li>Store all images, JavaScript, CSS files in a static folder of the application. First create a directory static, store the files inside it. The static Folder is created inside our app i.e <b>firstapp</b></li>
</ul>

<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/creatingstaticfolder.PNG" alt="Templates" width="600"  />

### Django Image Loading Example

<ul>
<li>we have to create Folder or directory inside static Folder i.e <b>images</b>,in that <b>images</b> folder upload some pictures from your local system.</li>
</ul>

<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/imagefolder.PNG" alt="Templates" width="600"  />

<ul>
<li><b>index.html</b> code</li>
</ul>

```html
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <title>Loading Images</title>  
     {% load static %}  
</head>  
<body>  
<img src="{% static 'images1/django.png' %}" alt="django" height="300px" width="700px"/>  
</body>  
</html>     
```
<ul>
<li><b>urls.py</b> code</li>
</ul>

```python
from django.contrib import admin
from django.urls import path
from firstapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('index/',views.index,name='index'),
]
```
<ul>
<li><b>views.py</b> code</li>
</ul>

```python
def index(request):  
    return render(request,'firstapp/index.html',{})
```
<ul>
<li>Run the server by using <b>python manage.py runserver</b> command,then output look like this.</li>
</ul>

<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/imageoutput.PNG" alt="Templates" width="600"  />

### Django Loading JavaScript

<ul>
<li>we have to create Folder or directory inside static Folder i.e <b>js</b>,in that <b>js</b> folder create a file and name it as <b>mystyle.js</b></li>
</ul>

<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/mystyle.PNG" alt="mystyle" width="600"  />

<ul>
<li><b>mystyle.js</b> code</li>
</ul>

```javascript
alert("now your are using java script alert")
```
<ul>
  <li>To load JavaScript file, just add the following line of code in <b>index.html</b> file.</li>
</ul>

```html
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <title>JavaScript</title>  
     {% load static %}  
    <script src="{% static 'js/mystyle.js' %}" type="text/javascript"></script>  
</head>  
<body>  
</body>  
</html> 
```
<ul>
<li>Run the server by using <b>python manage.py runserver</b> command.Then,output look like this.</li>
</ul>


<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/jsoutput.PNG" alt="Templates" width="600" />


> **_NOTE:_** It is not necessary to run the server everytime,because the server is running in background.untill unless you stop the server. 

### Django Loading CSS Example

<ul>
<li>we have to create Folder or directory inside static Folder i.e <b>css</b>,in that <b>js</b> folder create a file and name it as <b>mystyle.css</b> folder looks like this.</li>
</ul>

<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/cssimage.PNG" alt="cssimage" width="600" />

<ul>
<li><b>mystyle.css</b> code</li>
</ul>

```css
h2{  
color:pink;  
} 
```

<ul>
  <li>To load css file, just add the following line of code in <b>index.html</b> file.</li>
</ul>

```html
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <title>Styles</title>  
     {% load static %}  
    <link href="{% static 'css/mystyle.css' %}" rel="stylesheet">  
</head>  
<body>  
<h2>Welcome to MyProject</h2>  
</body>  
</html>  
```

<ul>
<li>Run the server by using <b>python manage.py runserver</b> command.Then,output look like this.</li>
</ul>

<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/Images1/cssoutput.PNG" alt="Templates" width="600" />

<p>In this topic, we have learned the process of managing static files efficiently.</p>

