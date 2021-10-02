---
title:  "SQLite and config variables"
layout: blog
order: 6
topic: Python
topic_path: /docs/python/index.html
---

To connect a SQLite database to Flask, and SQLAlchemy, we only need set a few configuration variables in the Flask app. I usually define my configuration variables in a separate file, `config.py`. I then import this file into `__init__.py`. I have noticed that I need a secret key defined to use some features of SQLAlchemy. Best practice is to set this to a secure value.

```python
# config.py
class Config:
    SQLALCHEMY_DATABASE_URI = 'sqlite:///{}'.format(db_path)
    SQLALCHEMY_TRACK_MODIFICATIONS = False

# __init__.py
def init_app():
    app = Flask(__name__, instance_relative_config=False)
    app.config.from_object("App.config.Config")
    app.secret_key = 'abc'
```