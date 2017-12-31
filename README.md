# Django Oauth Example

## About
This is a small app for an example of how to configure together Django, Django REST Framework and Django Oauth Toolkit.

## Requirements
* Python 3.6.3

## Install
1. Clone project.  
`git clone git@github.com:ryanrodemoyer/DjangoOauthExample.git`
1. Switch directory  
`cd DjangoOauthExample`
1. Install requirements.  
`pip install -r requirements.txt`
1. Migrate database.  
`python manage.py migrate`
1. Create user.  
`python manage.py createsuperuser`
1. Run!  
`python manage.py runserver`

## Usage

### Views
1. Admin Login @ http://localhost:8000/admin.
1. Register/View applications @ http://localhost:8000/o/applications.
1. Token endpoint @ http://localhost:8000/o/token

### Getting A Token

#### Authorization Code
1. Register new application.
    * Name: \<your choice\>.
    * Client type: confidential.
    * Authorization grant type: Authorization code.
    * Redirect urls: http://django-oauth-toolkit.herokuapp.com/consumer/exchange/
1. Follow the steps @ http://django-oauth-toolkit.herokuapp.com/consumer/ to get a token.
1. Verify /api/users/ route is protected.  
`curl http://localhost:8000/api/users/`.
1. Request /api/users/ to see data.  
`curl -H "Authorization: Bearer <your_access_token>" http://localhost:8000/api/users/`

#### Resource Owner Password
1. Register new application
    * Name: \<your choice\>.
    * Client type: confidential.
    * Authorization grant type: Resource owner password-based.
    * Redirect urls: \<blank\>
1. Verify /api/users/ route is protected.  
`curl http://localhost:8000/api/users/`
1. Get a token. Use the super user credentials from above in Install or create a new user via Django Admin and use those credentials.  
`curl -X POST -d "grant_type=password&username=<user_name>&password=<password>" -u "<client_id>:<client_secret>" http://localhost:8000/o/token/`
1. Request /api/users/ to see data.  
`curl -H "Authorization: Bearer <your_access_token>" http://localhost:8000/api/users/`

## Credits
Based mostly on the documentation at https://django-oauth-toolkit.readthedocs.io.

#### Projects
* https://github.com/django/django
* https://github.com/encode/django-rest-framework
* https://github.com/evonove/django-oauth-toolkit