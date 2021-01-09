# Webapp
This is the instruction step by step of deploying a django app on heruro using python and pycharm.

1.	Terminal: pip install Django, Django-heroku, gunicorn, whitenoise, whitenoise[Brotli]

2.	Install Heroku CLI: https://devcenter.heroku.com/articles/heroku-cli

3.	Terminal: Django-admin startproject projectname

4.	Terminal: cd projectname

5.	Terminal: manage.py startapp appname

6.	Make Procfile in root directory: web: gunicorn projectname.wsgi

7.	Make runtime.txt file in root directory: python-version

8.	Terminal: pip freeze > requirements.txt

9.	Make “templates” directory in the root directory

10.	Project/settings: 

          Import os

          Import Django_heroku

          INSTALLED_APPS =[

                                  .....

                                ‘app_name’
                             ]

          MIDDLEWARE: [

                          'django.middleware.security.SecurityMiddleware',

                          'whitenoise.middleware.WhiteNoiseMiddleware',

                           …..

            ] 

            (make sure whitenosie under security and above all)

          TEMPLATES: ‘DIRS’ : [BASE_DIR/ ’templates’]

    •	Add the following at the end of settings file: 

           STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

           STATIC_URL = '/static/'

           STATICFILES_STORAGE = 'whitenoise.storage.CompressedStaticFilesStorage'

           django_heroku.settings(locals())

11.	Make home.html file in templates directory:
  
        <!--<title>Home Page</title>-->
        <!--<body>
            <p>Home Page is running successful!</p>
            </body>-->
        (remove comment tag in HTML file)
        
12.	Project/urls:

          From Django.urls import include

          urlpatterns = [

                       path('admin/', admin.site.urls),

                       path('', include('appname.urls')),

                         ]

13.	app/views:

          from django.views.generic import TemplateView

          class HomeView(TemplateView):

              template_name = 'home.html'
    
14.	Make urls.py in app directory:

          from django.urls import path

          from .views import HomeView

          urlpatterns = [

              path('', HomeView.as_view(), name='Home'),

          ]

15.	Test: 

    a.	Terminal: manage.py runserver

    b.	Exit server

16.	Terminal: 

    a.	Manage.py collectstatic

    b.	Share project on GitHub

    c.	Git add -A

    d.	Heroku login

    e.	Heroku create appname


17.	Project/setting:

          DEBUG = False   

          ALLOWED_HOSTS = ['appname.herokuapp.com']

18.	Terminal: 

    a.	Heroku git:remote -a appname

    b.	Git push Heroku master (or main, or origin/master)

    c.	Heroku ps:scale web=1

    d.	Heroku open

19.	DONE! https://weapps.herokuapp.com/
