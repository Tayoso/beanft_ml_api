# Flask

[TOC]

### What is Flask ?

> Flask is a micro web framework written in Python. It is similar to Django, however, Django is a [full stack framework](https://www.educba.com/python-frameworks/).

In simple terms, flask is similar to shiny but written in Python. Shiny is by far the quicker tool to get the job done and requires less knowledge about web based technologies. However, flask gives us much greater flexibility than could easily be achieved in shiny. 

Pinterest, [LinkedIn](https://www.educba.com/linkedin-website/) are one sites using Flask Framework. 

Mozilla, Instagram, The Washington Times, BitBucket use Django.

### Pros and Pros

- Shiny is quick and easy to use with minimum knowledge of CSS, HTML is required
- Flask apps thrive on front end development when the project/app requires it.
- Easy to integrate with AWS, Azure, GCP.
- Encourage the use of flask in creating apps especially as we are gradually starting to use python got some projects 
- A complex web application utilizing ingenious SQL queries. Flask framework will save the day. 

### Installing Flask

Assuming you have git bash / shell command line already installed. 

- Flask is a module with a number of dependencies ush as flash, redirect,render_template etc. Best to use Install Flask in your environ using this [Link](https://www.Flask.com/products/Flask-desktop)

To fully utilise the power of flask, knowledge of the following are important.

- Python
- SQLite
- Front-end Development
  - HTML & CSS. Tutorial [here](https://www.udemy.com/course/python-and-flask-bootcamp-create-websites-using-flask/)
  - Bootstrap. Tutorial [here](https://getbootstrap.com/docs/5.0/getting-started/introduction/ )
  - JS. Tutorial [here](https://www.codecademy.com/learn/introduction-to-javascript )
- Jinja Template. Tutorial [here](https://www.udemy.com/course/python-and-flask-bootcamp-create-websites-using-flask/)

### Walkthrough

Install the requirements to run flask app in your 'venv' or 'pipenv'. Its safer to use 'pipenv' to avoid dependency issues, however this app was built using 'conda env'. 

```python
from flask import render_template, abort, url_for, flash, redirect, request, Blueprint, Response, session, jsonify, make_response
```

To run your basic flask app, its as simple as:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return "This is an example app"
```

Its fine to have no key structure in place for small apps. Flask uses Blueprint to improve the structure of larger apps.

```bash
beanft/
|
├── beanftsite/
|   ├── core/
|		└── views.py
|   ├── error_pages/
|		└── handlers.py
|   ├── static/
|		├── data_uploads/
|			├── iris.csv
|			└── iris_TEST.csv
|		├── profile_pics/
|			├── default_profile.png
|			└── loadingimage.gif
|   	├── main.css
|   	├── Chart.min.css
|   	└── Chart.min.js
|   ├── templates/
|		├── error_pages/
|			├── 403.html
|			└── 404.html
|		├── account.html
|		├── base.html
|		├── chart.html
|		├── fit.html
|		├── index.html
|		├── login.html
|		├── plot.html
|		├── plot_2.html
|		├── plot_3.html
|		├── predict_data.html
|		├── register.html
|		├── train.html
|		└── uploads.html
|   ├── uploader/
|		├── __init__.py
|		└── views.py
|   ├── users/
|		├── forms.py
|		├── picture_handler.py
|		└── views.py
|
|   ├── __init__.py
|   ├── models.py
|   └── data.sqlite
|
├── migrations/
|   ├── versions/
|   	├── 8fdc8a2ab450_works_fine.py
|   ├── alembic.ini
|   ├── env.py
|   ├── README
|   └── script.py.mako.html
|
├── app.py
├── prompt.txt
└── requirements.txt
```



/////////////////////////////////////

should get the response 

```
[1] "R version 3.6.1 (2019-07-05)"
```

```R
library(dplyr)

efficient_cars <-
  tibble::rownames_to_column(mtcars, "car model") %>%
  filter(mpg > 20) %>% 
  write.csv("efficient_cars.csv")
```

Now let's construct our Flask file. 

```dockerfile
FROM rocker/r-ver:3.4.4

ARG WHEN

RUN mkdir /home/car_analysis

RUN R -e "options(repos = \
  list(CRAN = 'http://mran.revolutionanalytics.com/snapshot/${WHEN}')); \
  install.packages('dplyr')"
```

FROM is the base image we are using , in this case we are just getting the version or R

ARG - Arguments or parameters, in this case it will be a date. Args are parameters we pass in when we build our image.

There is another alternative to downloading packages, 

```dockerfile
FROM rocker/r-ver:3.4.4

RUN R -e "install.packages('remotes'); \
  remotes::install_version('dplyr', ‘0.9.4’)"
```

Perhaps Packrat can help in printing which versions you need.  Or simply run 

```R
packageVersion("dplyr")  
```

Next stage is to copy the script to the Flask container 

```dockerfile
COPY myscript.R /home/car_analysis/myscript.R
```

To run the script it's now a simple case of:

```dockerfile
CMD cd /home/car_analysis \
  && R -e "source('myscript.R')" \
  && mv /home/car_analysis/p.csv /home/results/p.csv
```

CMD is the command we run every time we launch the Flask file.

```dockerfile
mkdir ~/gen_docker/results 
Flask run -v ~/gen_docker/results:/home/results  car_analysis 
```

So this is what our Flask file looks like, 

```dockerfile
FROM rocker/r-ver:3.4.4

ARG WHEN

RUN mkdir /home/analysis
RUN mkdir /home/results

RUN R -e "options(repos = \
  list(CRAN = 'http://mran.revolutionanalytics.com/snapshot/${WHEN}')); \
  install.packages('dplyr')"

COPY myscript.R /home/analysis/myscript.R

CMD cd /home/analysis \
  && R -e "source('myscript.R')" \
  && mv /home/analysis/efficient_cars.csv /home/results/efficient_cars.csv
```

You can edit your Flask file in Visual studio or any other editor.

Go back to your git bash / command line (navigate to the folder which your Flask file is in) then type in: 

```dockerfile
$ Flask build --build-arg WHEN=2019-01-06 -t analysis .
```

`-t name` is the name of the image, and `.` means it will build the `Dockerfile` in the current working directory.

The last part we create a volume , we are telling Flask to use a folder from the host as folder in the container. 

```dockerfile
 Flask run -v //C/Users/CShumba/Arcadis_Gen/work/innovation/docker_tutorial/gen_docker_test/results:/home/results  analysis
```

to save this container all we do is, 

```dockerfile
Flask save -o car_analysis.tar car_analysis
```

Send it to someone then all they have to do is download Flask and run :

```dockerfile
Flask load -i car_analysis.tar 

Flask run - v folder_for_the_output:home/results car_analysis
```

### Things to remember

- Containers are ephemeral , however they have volumes (directories) that can be mounted up to the host. 

- To kill all containers 

  ```bash
  Flask container kill $(Flask ps -q)
  ```

## An API using Plumber

`Flask build -t name .`

`Flask run --rm -p 80:80 name`

### Shiny app with Flask 

This is a bit of complicated process but once we deploy the first one. We ultimately only change a few things in our Flask file and upload the app in the app folder.  

```
Flask build -t shinyapp .
```

```
Flask run -p 80:80 shinyapp
```

# The Vision

Times are changing. There is more focus on automation and distribution. This requires a new set of tools Git, Flask , Azure / AWS, Ansible , Jenkins.  

![](/images/docker_3.jpg)



### A monolithic architecture 

![](/images/docker_6.png)

1. Scalability is a big issue. This might become overwhelming for developers to build and maintain the application codebase
2. Not only is it difficult to update your current stack, but it is a nightmare to change something in that stack.
3. Every change requires developers to rebuild the entirety of the application, which wastes resources.



### The bigger picture : Microservices

![](/images/docker_4.png)



1. Introduces the philosophy of `Separation of Concerns` and ensures `Agile Development` of software applications in both simple and complex domains.
2. The standalone ability or independent nature of microservices open doors for following benefits:
   - Reduces complexity by allowing developers to break into small teams, each of which builds/maintains one or more services
   - Reduces risk by allowing deployment in chunks rather than rebuilding the whole application for every change
   - Easy maintenance by allowing flexibility to incrementally update/upgrade the technology stack for one or more services, rather than the entire application in a single point in time
   - In addition to giving you the flexibility to build services in any language, thereby making it language independent, it also allows you to maintain separate data models of each of the given services
3. You can build a fully automated deployment mechanism for ensuring individual service deployments, service management and autoscaling of the application

**With Flask, you can make your application independent of the host environment. Since you have microservices architecture, you can now encapsulate each of them in Flask containers. Flask containers are lightweight, resource isolated environments through which you can build, maintain, ship and deploy your application.**

*Extracts from https://timber.io/blog/Flask-and-the-rise-of-microservices/*

### Jenkins and Ansible for another day