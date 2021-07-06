# django-student_management-project

# views.py

from django.shortcuts import render
from django.shortcuts import redirect 
from django.shortcuts import HttpResponse
from login.models import StudentAdd

# Create your views here.
def home(request):
    if request.method=="POST":
        name=request.POST['sname']
        gender=request.POST['gender']
        dob=request.POST['dob']
        email=request.POST['email']
        phno=request.POST['phno']
        user=StudentAdd(sname=name,gender=gender,dob=dob,email=email,phonenumber=phno)
        user.save()
        return HttpResponse(f"Form Submitted{name,gender,dob,email,phno}")
    return render(request,'add.html')
def display(request):
    data=StudentAdd.objects.all()
    return render(request,'display.html',{"details":data})
def delete(requuest):
    data=StudentAdd.objects.get{id=id}
    user.delete()
    return redirect(display)

def update(request,sid):
    name=request.POST['sname']
        gender=request.POST['gender']
        dob=request.POST['dob']
        email=request.POST['email']
        phno=request.POST['phno']
        user=StudentAdd(sname=name,gender=gender,dob=dob,email=email,phonenumber=phno)
        user.save()
        return redirect(display)
    return render(request,'update.html',{'data':user})
    
  ----------------------------------------------------------------------------------------------------------------------------  
# models.py
    
    from django.db import models

# Create your models here.
class student_managementadd(models,model):
    male_female = (('M','male'),('F','female'))
    sname = models.CharField(max_length=20)
    gender = models.CharField(max_length=1,choices=male_female)
    dob = models.DateField()
    email=models.EmailField()
    phonenumber = models.BigIntegerField()
    
 -------------------------------------------------------------------------------------------------------------------------------   
    
# app....URLS.py
 
 from django.urls import path 
from login import views

urlpatterns = [
    path('',views.home,name="name"),
    path('display',views.display,name="display"),
    path('delete/<sid>', views.delet,name="delete"),
    path('update/<sid>',views.update,name='update'),
        
]

-------------------------------------------------------------------------------------------------------------------------------------

# urls.py
  
  """STUDENT_MANAGEMENT URL Configuration

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/3.0/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
"""
from django.contrib import admin
from django.urls import path
from django.urls import include
from STUDENT_MANAGEMENT import views
import logging

urlpatterns = [
    path('admin/', admin.site.urls),
    path('',include('login.urls')),
    
]

  ---------------------------------------------------------------------------------------------------------------------------------
  
# TEMPLET'S
  
# Add.html
  
  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    <div class="container">
        <div class="row">
            <div class="col">
                <h1>Add student</h1>
    <from action="{% url 'name' %}" method="POST">
        {% csrf_token %}
        <lable for="sname">Student name</lable>
        <input type="text" name="sname">
<br>
        <label for="gender">Gender</label>
        male<input type="radio" name="gender" value="male">
        <br>
        female<input type="radio" name="gender" value="female">
        <br>
        <lable for="dob">Date of birth</lable>
        <input type="date" name="dob">
<br>
        <lable for="emale">EmaileId</lable>
        <input type="email" name="email">
<br>
        <label for="phno">Phone Number</label>
        <input type="number" name="phno">
        <br>
        <input type="submit" value="Add"
        <br>
    </from>
            </div>
            <div class="col">
                <a href="{% url 'display' %">Existing students</a>
            </div>
        </div>
    </div>
    
</body>
</html>
  
 -----------------------------------------------------------------------------------------------------------------------------------
  
  # Update.html
  
  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=
    , initial-scale=1.0">
    <title>Document</title>
    <!--css only-->
</head>
<body>

    <div class="container">
        <div class="row">
            <div class="col">
                <h1>Add student</h1>
    <form action="{% url 'update' date.id %}" method="post">
        {% csrf_tokan %}
        <label for="sname">Student name</label>
        <input type="text" name="sname" value="{{date.sname}}">
<br>
        <label for="gender">Gender</label>
        male<input type="radio" name="gender" value="male" value="{{data.gender}}"
        <br>
        female<input type="radio" name="gender" value="female" value="{{data.gender}}">
        <br>
        <label for="dob">Date of Birth</label>
        <input type="date" name="dob" value="{{ data.dob}}"
<br>
        <label for="email">EmailId</label>
        <input type="email" name="email" value="{{data.email}}">
<br>
        <label for="phone">Phone Number</label>
        <input type="number" name="phno" value="{{data.phonenumber}}">
        <br>
        <input type="submit" value="Update">
        <br>
        
    </form>
            </div>
        </div>
    </div>
    
</body>
</html>
  
  -------------------------------------------------------------------------------------------------------
  
 # display.html
  
  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>student details</h1>
    <table class="table table-hover">
    {% for student in details %}

        <tr>
            <td> {{ student.sname }}</td>
            <td>{{ student.gender }}</td>
            <td>{{ student.dob }}</td>
            <td>{{ student.email }}</td>
            <td>{{ student.phonenumber }}</td>
            <td><a href="{% url 'delete' student.id %}"><button class="button btn-waring">Delete</button></a></td>
            <td><a href="{% url 'update' student.id %}"><button class="button btn-light">update</button></a></td>
        </tr>
    
    {% endfor %}
    </table>
</body>
</html>
