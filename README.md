
## What is Beanft?
**Beanft**, short for Bean Forecast Tool is a basic Machine Learning Tool which consists of Classification, Regression type algorithms to view best model fit on training data and predict on unseen datasets. This tool can also be used to visualise datasets, albeit in the raw form.



## Author

Temitayo Ososanya: ososanyatayo@gmail.com



## Usage

```powershell
# IMPORTANT: App works best in python 3.6
# Test data is in .\bean_ft\beanftsite\static\data_upload

# Launch App -------------------------
# navigate the wd to the location of app.py
cd location/of/app_py

# Run the below to install the requirements and create a virtual env
pipenv run pip install -r requirements.txt

# launch the subshell in virtual environment 
pipenv shell

# Check your installed dependencies for security vulnerabilities
pipenv check

# if the env passess the PEP requirements, set FLASK_APP environment variable (no space around "=")
set FLASK_APP=app.py

# run the app
python app.py

## N:B: If app fails to launch, check the error. Its probably a python version compatibility issue, anaconda related issue, etc.
```



## License

Free to use.



## For more on Flask

If you are new to flask and want to find out more, read ***Intro_to_Flask.md***

[Intro to Flask]: ./Intro_to_Flask.md



