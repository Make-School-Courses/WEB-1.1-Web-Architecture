# Deploy to Heroku

Congratulations - you have now completed (several) Flask applications, and you're ready to deploy!!

To do this, we'll use a service called [Heroku](https://heroku.com) that is free, but it does require a credit card to be on file.

Make sure to read the following instructions carefully. If you get an error message that is not mentioned, reach out to your isntructor or try using Stack Overflow for help!

## Before you Start

Before starting, let's go over some terminology we'll use in the instructions:

- `databaseName` - The name of the database used in your application.
- `uniqueprojectname` - A unique name for your project that you'll use for the Heroku URL. This is the one that your "beta" users will see in the URL! If your chosen name is taken, Heroku will instruct you to choose a new one.

Be sure to replace these with your _actual_ database & project names! Otherwise, your code may not work properly.

## Step 1: Sign up for & Install Heroku

First you need to create a Heroku account at [heroku.com](https://heroku.com). The service is free, but will require you to have a credit card on file.

Then you will need to add the Heroku Command Line Interface (CLI) to your bash terminal so we can interact with the Heroku service via the terminal and git. Follow [these instructions](https://devcenter.heroku.com/articles/heroku-cli) to install the Heroku CLI.

## Step 2: Install Gunicorn

Heroku does not provide a web server, and the Flask web server is not well-suited for production use because it is single-threaded. If we want our server to perform well when multiple users make requests simultaneously, then we should use a multi-threaded web server. We will be using **gunicorn**.

### If you are using a Virtual Environment

If you're using a virtual environment, make sure to **activate** it, then run the following commands in your project folder to install gunicorn and update your `requirements.txt` file:

```bash
pip3 install gunicorn

pip3 freeze > requirements.txt
```

### If you are not using a Virtual Environment

If you're not using a virtual environment, simply update your `requirements.txt` file so that it has the following contents:

```
click
Flask
Flask-PyMongo
gunicorn
itsdangerous
Jinja2
MarkupSafe
pymongo
Werkzeug
```

Make sure to also add any other Python libraries you are using!

## Add your Procfile

Before we push to Heroku, we'll have to create a special file, called `Procfile`, that lets Heroku know how to run your website.

Create a new file called `Procfile` (no file extension) and give it the following contents:

```
web: gunicorn app:app
```

Great! When we push to Heroku, it'll know how to run our application.

## Push to Heroku using GitHub

Let's start by committing what we have so far so that we have that `Procfile`. Commit your code change using the following commands:

```bash
git add .
git commit -m 'add Procfile'
```

Now, let's use the `heroku` command to create a heroku app and name it with `uniqueprojectname`. This `heroku create` command will also add our heroku app as a git remote repository that we will be able to push to using the git command `git push`.

```bash
heroku create uniqueprojectname
```

We can see our remote repos by using the command `git remote -v`. Once you run this command, you should now see that you have **two** remotes: one for GitHub, and one for Heroku:

```bash
git remote -v
```

Great, now we can push our code to heroku and open our new website!

```
git push heroku master
heroku open
```

You are probably seeing an error screen right now! Bit of a let down maybe. But also a good lesson - **Things never work the first time**. Let's debug our issues.

## Read the Logs

Whenever you have an error or problem with Heroku, you can see the logs by running `heroku logs`.

```bash
heroku logs
```

If you want to see the logs to continually you can add --tail to this command.

```bash
heroku logs --tail
```

What error are we seeing in heroku now? What do we need to do?

## Adding a Production Database

It looks like the error is that we cannot connect to our mongodb database. That's because it is looking at the `'mongodb://localhost:27017'` URI, but that is running on our local computer and Heroku, which is remote, doesn't have access to that. So we have to add a mongodb heroku add-on called mLabs.

Add `mLabs`:

```bash
heroku addons:create mongolab:sandbox
```

Then, we have to point to this production mongodb database URI in our `app.py` file. We'll use `os.environ.get` to get the `MONGODB_URI` environment variable.

Update `app.py` to point to the mongodb URI if it exists:

```py
# Add the following import
import os

# Update your setup code
host = os.environ.get('MONGODB_URI', 'mongodb://localhost:27017/databaseName') + "?retryWrites=false"
app.config["MONGO_URI"] = host
mongo = PyMongo(app)
```

Make sure to update the `databaseName` to your own database name!!!

Next, follow the steps again to `git add`, `git commit`, and `git push heroku master` to ensure that our changes are reflected in Heroku.

```bash
git add .
git commit -m 'Update deployment settings'
git push heroku master
```

Now if we try to open our heroku app via the terminal using heroku open, what happens?

## If you ran into other issues...

If your application still doesn't load, you may have other issues to fix! Read over the logs file with `heroku logs --tail` and try doing a Google search for the specific error message you see. If you get a Python or Jinja error, make sure to debug locally first! 

## If your deployment was successful...

Awwww yeah - you did it! You made your first RESTful and Resourceful app using Flask, Jinja2, and MongoDB!

Make sure to push your changes to GitHub (which DOES NOT happen automatically if you push to Heroku):

```bash
git push origin master
```

If you're interested in taking your deployment skills to the next level, check out the [BEW 2.2 - Docker, DevOps, & Deployments](https://make.sc/bew2.2) course.