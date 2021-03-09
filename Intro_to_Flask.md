# Flask

[TOC]

## What is Flask ?

> Flask is a micro web framework written in Python. It is similar to Django, however, Django is a [full stack framework](https://www.educba.com/python-frameworks/).

In simple terms, flask is similar to shiny but written in Python. Shiny is by far the quicker tool to get the job done and requires less knowledge about web based technologies. 

Netflix, Airbnb, Uber, LinkedIn use Flask Framework.[1]

Pinterest, Spotify, Instagram use Django.

### Pros and Pros

- Shiny is quick and easy to use with minimum knowledge of CSS, HTML required.[2]
- Flask apps thrive on front end development when the project/app requires it.
- Flask is easy to integrate with AWS, Azure, GCP.
- Flask supports payment functionality using 'stripe'.
- A complex web application utilizing ingenious SQL queries. Flask framework will save the day. 

Encourage the use of flask in creating apps especially as we are gradually starting to use python got some projects.

### Installing Flask

Assuming you have git bash / shell command line already installed. 

- Flask is a package with a number of modules such as flash, redirect,render_template etc. Best to use Install Flask in your environ using this [Link](https://www.Flask.com/products/Flask-desktop). Some of the modules which support a flask app include

  ```python
  from flask import render_template, abort, url_for, flash, redirect, request, Blueprint, Response, session, jsonify, make_response
  ```


To fully utilise the power of flask, knowledge of the following are important.

- Python
- SQLite
- Front-end Development
  - HTML & CSS. Tutorial [here](https://www.udemy.com/course/python-and-flask-bootcamp-create-websites-using-flask/)
  - Bootstrap. Tutorial [here](https://getbootstrap.com/docs/5.0/getting-started/introduction/ )
  - JS. Tutorial [here](https://www.codecademy.com/learn/introduction-to-javascript )
- Jinja Template - Tutorial [here](https://www.udemy.com/course/python-and-flask-bootcamp-create-websites-using-flask/)
- Celery
- etc.

## Flask app on AWS

Install the requirements to run flask app in your 'env'. Its safer to use 'pipenv' to avoid dependency issues, however this app was built locally using 'conda env' and is currently hosted on a small EC2 instance (virtual computer) in AWS.

To run your basic flask app, its as simple as:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return "This is a flask app"

if __name__=='__main__':
    app.run(debug=True)
```

To debug the app, copy the pin when the debug prompt comes up. Importantly, the below is an example of the temporary pin provided and will be displayed in the terminal. When the app is ready for production, its important to set *debug* back to '`False`'.

```
* Serving Flask app "app" (lazy loading)
* Environment: production
  WARNING: This is a development server. Do not use it in a production deployment.
  Use a production WSGI server instead.
* Debug mode: on
* Restarting with stat
* Debugger is active!
* Debugger PIN: 930-225-787
```



> To run the app in AWS, 

```bash
# change directory to location of app.py needed to initiate the flask app
cd flask-apps-demo/beanft

# set the default app to app.py
set FLASK_APP=app.py

# run the flask app
python app.py
```

This app serves as a tool for regression and classification type machine learning.

Its fine to have no key structure in place for small apps. However, its very important to have a structure in place for larger apps. Flask uses Blueprint to organise the scripts within the app.

```text
└── beanft
    ├── app.py
    ├── beanftsite
    │   ├── __init__.py
    │   ├── core
    │   │   └── views.py
    │   ├── data.sqlite
    │   ├── error_pages
    │   │   └── handlers.py
    │   ├── models.py
    │   ├── static
    │   │   ├── Chart.min.css
    │   │   ├── Chart.min.js
    │   │   ├── data_uploads
    │   │   │   ├── crimes-2017-18_SAS.csv
    │   │   │   ├── example_workorders_Sep18.csv
    │   │   │   ├── example_workorders_Sep18_TEST.csv
    │   │   │   ├── final_model.sav
    │   │   │   ├── iris.csv
    │   │   │   ├── iris_TEST.csv
    │   │   │   ├── mtcars.csv
    │   │   │   ├── pima-indians-diabetes.csv
    │   │   │   └── pima-indians-diabetes_TEST.csv
    │   │   ├── main.css
    │   │   └── profile_pics
    │   │       ├── default_profile.png
    │   │       └── loadingimage.gif
    │   ├── templates
    │   │   ├── account.html
    │   │   ├── base.html
    │   │   ├── chart.html
    │   │   ├── error_pages
    │   │   │   ├── 403.html
    │   │   │   └── 404.html
    │   │   ├── fit.html
    │   │   ├── index.html
    │   │   ├── login.html
    │   │   ├── plot.html
    │   │   ├── plot_2.html
    │   │   ├── plot_3.html
    │   │   ├── predict_data.html
    │   │   ├── register.html
    │   │   ├── train.html
    │   │   └── uploads.html
    │   ├── uploader
    │   │   ├── __init__.py
    │   │   └── views.py
    │   └── users
    │       ├── forms.py
    │       ├── picture_handler.py
    │       └── views.py
    ├── migrations
    │   ├── README
    │   ├── alembic.ini
    │   ├── env
    │   ├── script.py.mako
    │   └── versions
    │       └── 8fdc8a2ab450_works_fine.py
    ├── prompt.txt
    └── requirements.txt
```



### Serving ML APIs on Cloud

**Heroku** is another cloud platform which can host an app on cloud - [https://ml-beanft.herokuapp.com](https://ml-beanft.herokuapp.com/). Hosting an app on Heroku is easy, you can do this via the CLI, GitHub etc. The necessary files include:

- Procfile - This is a process type for the app
- runtime.txt (python version)
- requirements.txt

Free tier is available for apps under 512mb which is sufficient for simple apps. 



> Next: Invoke api using Heroku.



## References

1. https://www.codingninjas.com/blog/2020/11/10/flask-vs-django-lets-take-a-preview/
2. https://www.jumpingrivers.com/blog/r-shiny-python-flask