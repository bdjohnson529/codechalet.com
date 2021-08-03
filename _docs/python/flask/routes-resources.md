---
title:  "Routes and Resources"
layout: blog
topic: flask
order: 2
parent: Python
parent_path: python/
---

Routing is the mechanism by which HTTP requests are routed to the code which handles them. When a user visits the page `/home`, their computer makes an HTTP request to the server. Routing will determine what happens from there.

When building an app, a good first step is to map out all of the possible HTTP requests. The most common kind of request is a `GET` request - for example, accessing a homepage might be a `GET` request. Likely you will have some combination of `GET` and `PUT` requests. Each of these requests needs to be mapped to a Python function  using the Flask `route` decorator.
```
GET 	/home
GET 	/people
PUT 	/people
GET 	/people/<:id>
```

Requests can be organized by *resource*. In theory, each resource would have four routes for each of the [CRUD operations](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) for persistent storage. In practice, you might not need an *update* operation for one of your resources. In the example above, *people* is one resource. All of the routes associcated with this resource could be grouped into one file, `people.py`.

As your project grows, so will your resources. One way to keep track of your routes is to separate the routes by resource, creating a different file with the routes for each resource.
```
├── routes
|	├── home.py
|	├── people.py
|	├── pets.py
```

# Routes
In Flask, routes are defined using decorators. Flask routes the HTTP request to a Python function. For example, the following route would return the string `hello world` to the client computer. 

```python
@app.route("/")
def homepage():
    return "hello world"
```