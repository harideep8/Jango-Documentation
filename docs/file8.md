## Data Rendering From Views to Html
-----
### What is a render?

Render Combines a given template with a given context dictionary and returns an HttpResponse object with that rendered text.

### How to import render?

In views.py we should have to import render as follows **from django.shortcuts import render**

### How many arguments does render takes?

Render takes upto 6 argumnets i.e, Required arugumnets are 2 Optional arguments are 4

***Required Argumnets***:
  - **request**: Used to generate the response
  - **template name**: It will call the HTML Page which it is existed in the template folder

***Optional Arguments***:
  - **context**: A dictionary of values to add to the template context. By default, this is an empty dictionary. If a value in the                        dictionary is callable, the view will call it just before rendering the template.
  - **content_type**: The MIME type to use for the resulting document. Defaults to 'text/html'.
  - **status**: The status code for the response. Defaults to 200.
  - **using**: The name of a template engine to use for loading the template.

> How ever we will use upto 3 argumnets maximum(request,template name,context(dictionary)

**Structure of a Render**
- First HTTP Request(user request) will forward to urls.py
- From urls.py if request found then the request is carried to view.py i.e it call's the function
- Now the function will render to template (html file)
- Finally the result in the form of html response



<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/d1.png"/>

***Steps to implement render from views to html and html to views***

- In views.py first we should have to import a render
- Create a view(Function) in views.py
- Create a template file(HTML File) which is to be rendered and link it to the view.
- Create a URL to map to that view

Let us create a simple template that shows the current date and time as discussed earlier we will follow those steps to get desired result.

For this project i created one application i.e, testapp is my application name and i created one function show inside the views.py, to display output i created one templated called display.html

**urls.py**

```
from django.urls import path
from testapp import views

urlpatterns = [
    path('test/', views.show),
]
```

**Views.py**

- Import datetime module is a mandatory to display the current server time
-  We are passing dictionary to display.html, data as a key and date as a value
```python
from django.shortcuts import render
import datetime


def show(request):
    date=datetime.datetime.now()
    return render(request,'testapp/display.html',{'data':date})
```


**display.html**

- Inside the template tag we are calling data(key) which is coming from the function show in views.py
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <h2>The server date and time is : {{data}}</h2>
  </body>
</html>

```



**Result**


<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/d5.JPG"/>

----

## Data rendering from html to views without using forms and models


***Steps as follows***

- Created one application i.e, apssdc is my application name
- In this we will create a simple template(html file) which includes some fields like name,Mobile Number,Mail Id
- Here total we consired 3 fields in our application so that we require 3 input fields and one submit button
- To display the output create another template

**urls.py**

```
from django.urls import path
from apssdc import views
urlpatterns = [
    path('register/',views.register,name="register")
]
```

**Views.py**

- We are collecting data with request.POST after passing collected data to result.html
```python
from django.shortcuts import render

def register(request):
    if request.method=="POST":
        name=request.POST['Name']
        phonenumber=request.POST['Mobile']
        mailid=request.POST['Mail']
        age=request.POST['age']
        branch=request.POST['branch']
        return render(request,'apssdc/result.html',{'name':name,'phonenumber':phonenumber,'mailid':mailid,'age':age,'branch':branch})
    return render(request,'apssdc/index.html')
```


**index.html**


```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <form action="{% url 'register' %}" method="post">
      {%csrf_token%}
      Name:<input type="text" name="Name"><br>
      Mobile Number:<input type="text" name="Mobile"><br>
      Mail Id:<input type="text" name="Mail"><br>
      Age :<input type="text" name="age"><br>
      Branch:<input type="text" name="branch"><br>
      <input type="submit" name="submit" value="Submit">
    </form>
  </body>
</html>

```


**result.html**

- Inside the template tag calling keys to display the data which came from register function in views.py
```html

<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <table border=2>
      <tr>
        <th>Name</th>
        <th>Mobile Number</th>
        <th>Mail ID</th>
        <th>Age</th>
        <th>Branch</th>
      </tr>
      <tr>
        <td>{{name}}</td>
        <td>{{phonenumber}}</td>
        <td>{{mailid}}</td>
        <td>{{age}}</td>
        <td>{{branch}}</td>
      </tr>
    </table>
  </body>
</html>

```


**Result**


<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/d10.JPG"/>

**After click on submit result shown as follows**

<img src="https://raw.githubusercontent.com/avinash516/Documentation-web-development/master/d11.JPG"/>

