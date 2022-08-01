# Step 1: python scripts
Make FastAPI files. Get pickle file from
orig [repo](https://github.com/AssemblyAI-Examples/ml-fastapi-docker-heroku)
or, from the actual google [colab file](https://colab.research.google.com/drive/1uaALcaatvxOu42IhQA4r0bahfdpw-Z7v?usp=sharing)

# Step 1: more prep
create a Dockerfile and .dockerignore (last one is by convention).
Dockerfile contains some lines from the FastAPI in containers wesbite
(actual image from tiangolo/uvicorn-gunicorn-fastapi)
Put in requirements.txt which libraries you are using.
Because fastAPI image, no need to specify guvicorn, FastAPI, etc.
<br>
<br>

# Step 2: create docker container
Run the following in the terminal
```bash
docker build -t app-name .

docker run -p 80:80 app-name
```

When doing docker run (which is optional), can then in a browser check the /docs,
and get a swagger api GUI where you can test it out


# Step 2.5: Setup heroku account

After making free account, get the CLI from [here](https://devcenter.heroku.com/articles/heroku-cli)


# Step 3: deploy to heroku

Create a heroku.yml (look up official doc for details)
Login with heroku credentials 
Note: the heroku project name must be "unique"
and is the basis for your url

```bash
heroku login
heroku create your-app-name
heroku git:remote your-app-name
heroku stack:set container
git push heroku <your-main-branch>
```

# Step 4: Test ML model with postman

My test ML app is on
https://language-detection-app-luigi.herokuapp.com/
Use Postman to test it
In "Collections", add URL to the GET request field to
get some sanity check results.

First,  click on POST, and add the endpoint to the URL (in this case, we called
it "/predict" in the main.py).
Then, click on  Body -> raw, and make sure it is JSON and not text in the dropdown.
Finally,  input valid JSON text, and hit send (note. make sure that /predict is at end of POST request-URL)

