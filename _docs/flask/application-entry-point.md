---
title:  "App Entry Point"
layout: blog
order: 1
topic: Flask
topic_path: /docs/flask/index.html
---

Flask leaves it up to us to stitch all of our code together. I have found it helpful to define a single file which the web server interacts with when hosting the app. In this file, you define the [Flask object](https://flask.palletsprojects.com/en/1.1.x/api/). Everything needs to get routed back to this object at some point - this is the object which is used to run the server.

We need to import certain files after the `app` object has been instantiated. The routes, for example, are attached to a Flask object. If we try to import the routes before creating `app`, our computer will throw an error. 

One way to enforce that files are imported in the correct places is to define an initialization function which executes, and returns an instance of the [Flask object](https://flask.palletsprojects.com/en/1.1.x/api/). Functions are executed in a stepwise manner, whereas the order of imports within an unstructured Python file might be inconsistent.

To accomplish deferred imports, we can import Python files *within* this initialization function, rather than at the top of the Python file. This disagrees with several PEP8 standards, and is definitely not the most visually attractive solution. However, we have limited this sort of import to one file, the application entry point. Don't worry Mom, we will take off our muddy boots before we come back in the house.

Here is one place Flask really starts to shine. Flask has created an [Application Context](https://flask.palletsprojects.com/en/1.1.x/appcontext/) to keep track of application level data. Using the App Context we can access the `current_app`, and make modifications to the `app` object. We will import the app context into the separate files used to define, for example, routes for different resources.

```python
# routes/people.py
from flask import current_app as app

@app.route("/people")
def homepage():
    return "People page"

# __init__.py
def init_app():
    app = Flask(__name__, instance_relative_config=False)
    with app.app_context():
        from .routes import people
```

# WSGI File
I define a file `wsgi.py`, which is the file which the Python interpreter will execute when it serves the app. This file imports the initialization function from the app entry point, and uses the Flask run function to serve the app.

```python
# wsgi.py
from App import init_app

app = init_app()
if __name__ == "__main__":
    app.run(host="0.0.0.0", port=9000)

# App/__init__.py
def init_app():
    app = Flask(__name__, instance_relative_config=False)
    ...
    return app
```

To serve the app locally, execute the `wsgi` file using the Python interpreter.
```
python wsgi.py
```


## Structure
All in all, the backbone of my Flask project resembles the following:
```
| wsgi.py
├── App
| ├── __init__.py
|    ├── routes
|      ├── people.py
```