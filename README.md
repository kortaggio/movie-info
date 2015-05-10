# Movie Info
Find info on movies. [Click here](http://ga-movie-info.herokuapp.com/) for the demo. Built on Flask, Angular.js, Bootstrap, and jQuery.

## Features
- Uses a Python backend to cache results from OMDb so that we don't need to keep fetching data from a third party API. Not only does this improve performance, but the backend also has routes so that the user can hotlink directly to a result once they have seen it. For example, navigating to [http://ga-movie-info.herokuapp.com**/movie/tt0110912/**](http://ga-movie-info.herokuapp.com/movie/tt0110912) takes you directly to a cached results page that doesn't reply on external API calls.
- Connects to S3 to cache movie poster images once they're downloaded. This avoids exposing the OMDb API key to the client.
- Fully responsive on mobile, tablet, and desktop.
- Social sharing of each result page to Facebook, Twitter, and Google+
- Tested to work on Chrome, Firefox, and IE.
- Handles multiple error cases and zero data cases gracefully.

## Installation Instructions

Python Version 3.4.0

Flask Version 0.10.1

### Step 1

	$ git clone git@github.com:Kortaggio/movie-info.git
	$ cd movie-info

### Step 2

Install `virtualenv` and app requirements:

	$ pip install virtualenv
	$ virtualenv -p python3 venv
	$ source venv/bin/activate
	$ pip install -r requirements.txt

### Step 3

Generate a Flask secret key and save it as `/secret.txt` in the root folder. If running on Heroku instead of localhost, set the environment variable:

	$ heroku config:set FLASK_SECRET_KEY=your-secret-key-here

You also need to [get an OMDB Poster API key](http://beforethecode.com/projects/omdb/apikey.aspx) and save it as `/omdb_api_key.txt`. Again, you also need to set the environment varaible if you are running on Heroku:

	$ heroku config:set OMDB_API_KEY=your-api-key-here

### Step 3.5 (Optional)

If you want to wipe the database and create a new one from scratch, first delete the `app.db` file and the `db_repository` folder. You can then create and migrate the database using:

	$ python db_create.py
	$ python db_migrate.py

### Step 4

This app needs [Amazon S3](https://aws.amazon.com/s3/) to store the images of the movie posters. If you don't have an S3 Account or only want to run the app locally, set the config flag `USE_S3 = False` in `config.py` and skip the rest of Step 4.

If you have an S3 account and want to use it in conjunction with deploying on Heroku, run:

	$ heroku config:set S3_ACCESS_KEY=your-access-key-here
	$ heroku config:set S3_SECRET_KEY=your-secret-key-here
	$ heroku config:set S3_BUCKET=your-bucket-id-here

### Step 5

Run with

	$ python run.py

# License

MIT License
