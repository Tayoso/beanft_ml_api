
# use the python 3.6 image from Docker Hub as our base image
FROM python:3.6

# This installs pipenv on the container
RUN pip3 install pipenv

# The first line sets a environment variable as a path to a directory to store the projects code. \
#   Then the next command sets that directory as the working directory
ENV PROJECT_DIR /usr/src/flaskbookapi
WORKDIR ${PROJECT_DIR}

# We copy over all of our files to the container
COPY Pipfile .
COPY Pipfile.lock .
COPY requirements.txt .
COPY . .

# install dependencies
RUN pipenv run pip install -r requirements.txt

# We expose the 5000 port to be able to use it.
EXPOSE 5000

# we run our program using the CMD command.
CMD ["pipenv", "run", "python", "app.py"]