## Start django project

django-admin startproject mysite

cd mysite

## Manage enviroment

conda create --name mysite python=3.7.4

conda activate mysite (conda deactivate)

## Install Django

pip3 install django

pip3 freeze (see dependencies)

## Run server

python3 manage.py runserver

## Create app

python3 manage.py startapp polls (create app)

## Create tables

python3 manage.py migrate (create tables & permissions)

## Create migrations

python3 manage.py makemigrations polls

## Commit migrations

python3 manage.py sqlmigrate polls 0001

## Interact with Python shell

> python3 manage.py shell
>> from polls.models import Choice, Question
>
>> Question.objects.all()
>
>> from django.utils import timezone
>
>> q = Question(question_text="What's new?", pub_date=timezone.now())
>
>> q.save()
>
>> q.id
>
>> q.question_text
>
>> q.pub_date
>
>> q.question_text = "What's up?"
>
>> q.save()
>
>> Question.objects.all()
>
>> q = Question.objects.filter(id=1) || q = Question.objects.get(pk=1)
>
>> q.was_published_recently()
>
>> Question.objects.filter(question_text__startswith='What')
>> q = Question.objects.get(pk=1)
>
>> q.choice_set.all()
>
>> q.choice_set.create(choice_text='Not much', votes=0)
>
>> q.choice_set.create(choice_text='The sky', votes=0)
>
>> c = q.choice_set.create(choice_text='Just hacking again', votes=0)
>
>> c.question
>
>> q.choice_set.all()
>
>> q.choice_set.count()
>
>> Choice.objects.filter(question__pub_date__year=current_year)
>
>> c = q.choice_set.filter(choice_text__startswith='Just hacking')
>
>> c.delete()

## Creating an admin user

python manage.py createsuperuser

http://127.0.0.1:8000/admin/login/?next=/admin/

## Make the poll app modifiable in the admin

go to => polls/admin.py

## Running tests

wrote test in => polls/tests.py

python manage.py test polls

## Testing views

>python manage.py shell
>> from django.test.utils import setup_test_environment
>
>> setup_test_environment()
>
>> from django.test import Client
>
>> client = Client()
>
>> response = client.get('/') => not found
>
>> response.status_code => 404
>
>> from django.urls import reverse
>
>> response = client.get(reverse('polls:index'))
>
>> response.status_code => 200
>
>> response.content
>
>> response.context['latest_question_list']
