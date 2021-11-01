---
title:  "SQLAlchemy"
layout: blog
order: 5
topic: Flask
topic_path: /docs/flask/index.html
---

Most web applications use a database to store and maintain application data. It's possible to build a Flask app using a collection of files saving application data in the background (this could be a quick way to prototype); however, using a database on the backend is usually a more sustainable solution.

The prevailing way to interact with a database, in a web application, is using object-relational-mappers. ORMs empower you to write database queries in a language other than SQL. [SQLAlchemy](https://docs.sqlalchemy.org/en/14/) is a popular ORM tool for Python. [Flask-SQLAlchemy](https://pypi.org/project/Flask-SQLAlchemy/) is a Flask extension which add support for SQLAlchemy to the application. To install:
```bash
pip install Flask-SQLAlchemy
```

# SQLAlchemy Sessions
The primary interface for database operations is the [`SQLAlchemy session`](https://docs.sqlalchemy.org/en/13/orm/session.html). Within the `Session`, you can perform the basic CRUD operations : create, read, update and delete.

To add this model to the database, we need to use a Session which is connected to our SQLite database. One way of accomplishing this is to initialize the database outside of the initialization function, and then associate the app with the database afterwards. Flask offers [great instructions](https://flask-sqlalchemy.palletsprojects.com/en/2.x/api/) for this approach.

The database object might be created in `__init__.py`, so how do we access the database session in external files? Since we defined the `db` object outside of the initialization function in `__init__.py`, we can actually import this object into other files. We will do this in `person.py` below, by importing the file into `person.py` (implicit is that Python uses `__init__.py` to figure out how to import a module).


```python
# __init__.py
db = SQLAlchemy()

def init_app():
    db.init_app(app)

# routes/person.py
from .. import db
```

Now in `person.py` we can use the database session.

# Models
SQLAlchemy represents database tables as [models](https://flask-sqlalchemy.palletsprojects.com/en/2.x/models/), which are Python classes. Let's define a model for a Person, which contains a single attribute, a name.

We can define a Python class for our Person model. Notice that the class definition relies on a `db` object, which is created in `__init__.py`. We will need to import `db` into this file.

```python
# models.py
from .. import db

class Person(db.Model):
    __tablename__ = 'person'

    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(80), unique=True, nullable=False)

    def __repr__(self):
        return '<Name %r>' % self.name
```
We want want SQLAlchemy to use this Python class to create a table, `person`, in our database. To do this, we need to import the Python class back into the initialization function `init_app`. Notice why concurrency is an issue here - `models.py` imports a `db` object from `__init__.py` - if this object is not created, our application won't run.

After we import the Python classes, we can run `db.create_all()` to generate the required tables on the connnected database. The following code completes database initialization, using SQLAlchemy.

```python
# __init__.py
db = SQLAlchemy()

def init_app():
    db.init_app(app)

    with app.app_context():
        from models import Person
        db.create_all()

# routes/person.py
from .. import db
```
