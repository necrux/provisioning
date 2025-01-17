# E11y Provisioning POC 
This is a basic first swing at a POC for e11y account using skeema for schema creation 
We still need to add a global call (if needed) and a call to the PDDB endpoint on the proxy, but there is prior art for all of that

## Setup

1. Install pyenv and pyenv-virtualenv from Homebrew. (You will need to modify your .bash_profile after doing it, see the brew install output)
2. Install python 3.8.0: ```pyenv install 3.8.0```
3. Install mysql8 in whatever way you prefer, and create a user named skeema with the password Pardot07
4. Install Skeema from Homebrew
5. Create a virtualenv for e11y:  ```pyenv virtualenv 3.8.0 e11y2```
6. git clone this repo 
7. ```cd top/level/of/this/project; pyenv local e11y2``` (This will make the e11y virtual environment activated whenever you enter this directory)
8. ```cd provisioning; sudo pip install -r requirements.txt [--ignore-installed]```
9. ```cd ../skeema_files;   skeema init -u skeema -pPardot07 -h localhost```

## Running the app

In a separate terminal window, cd to the provisioning folder (where this file is)

```python app.py```

## Testing the API
In a separate terminal window, make a post to the endpoint, and check to see if a new schema was created in the database

```curl -i -H "Content-Type: application/json" -X POST -d '{"sName":"54552"}' http://localhost:5000/e11y/api/createSchema```

Then drop all the tables with the deprovisioning call

```curl -i -H "Content-Type: application/json" -X POST -d '{"sName":"54552"}' http://localhost:5000/e11y/api/deleteSchema```

