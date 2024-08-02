# issue deploying with heroku

an error message is requesting this middleware

```
MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
    'allauth.account.middleware.AccountMiddleware', # required by heroku
]
```

which then leads to a confusing issue stating allauth needs to be added to INSTALLED_APPS, when in fact it already is

```
remote:     from .views import RegisterView, VerifyEmailView
remote:   File "/app/.heroku/python/lib/python3.9/site-packages/dj_rest_auth/registration/views.py", line 23, in <module>
remote:     from dj_rest_auth.registration.serializers import (
remote:   File "/app/.heroku/python/lib/python3.9/site-packages/dj_rest_auth/registration/serializers.py", line 19, in <module>
remote:     raise ImportError('allauth needs to be added to INSTALLED_APPS.')
remote: ImportError: allauth needs to be added to INSTALLED_APPS.
remote: Waiting for release.... failed.
To https://git.heroku.com/project5-api-lmcrean.git
   2065b43..48138a8  main -> main
```

this issue was also in local, however it was fixed by upgrading django-allauth from 0.44.0 to 0.50.0

the api only runs in dev mode when allauth.account.middleware.AccountMiddleware

my requirements.txt already states that django-allauth is the correct version 0.50.0

dj-rest-auth==2.1.9 perhaps that should be updated to latest?

the conflict seems to lie within the requirements.txt being out of date with the course?