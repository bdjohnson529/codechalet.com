---
title:  "Dash pages"
layout: blog
order: 4
topic: Python
topic_path: /docs/python/index.html
---

Dash is actually built on Flask. Each Dash app is actually an instance of a Flask application. This is great news for anyone who is familiar with one of the technologies because it means, in theory, the other will be similar.

Dash and Flask do have their similarities, one of which is how they handle events. In Flask, client requests are handled by `route` methods, which route the request to a Python function. For example, a simple page can be created with the following code:

```python
@app.route('/test', methods=['POST'])
def test():
	return "Hello world"
```

Flask will route a post request at the URL `/test` to the function `test()`, which returns a value of `"Hello world"` to the user. tldr: The user will see `Hello world` on their screen.

In a similar style,  Dash offers callback decorators for functions. A callback function is a function which is passed as an argument to a parent function - when the parent function finishes executing, it calls the callback function. Using callbacks in Dash, you can update variables in response to user behavior. For example, if a user changes the value of a dropdown menu, you can set the figures on the page to refresh.

```python
@app.callback(
		Input('dropdown', 'value'),
		Output('barchart', 'figure')
	)
def update_figure():
	return newbarchart
```

When the input variable changes, the callback is invoked. The function sets `barchart` equal to the output of the function. Note that you can use callbacks with multiple outputs, you just need to identify each output within the callback decorator `@app.callback` and also return the output from the function.


## Multiple Dash Pages?
If each Dash app is a Flask application, how can you create a Flask app with multiple Dash pages? For example, what if you wanted to build the following app, where `barchart` and `linechart` are two different pages within the same webapp?

```bash
mysite.com/
mysite.com/barchart
mysite.com/linechart
```

Following in the steps of [Todd Birchard](https://hackersandslackers.com/plotly-dash-with-flask/), we found we were able to solve this problem if we approached it from a functional perspective. What if each page was constructed by a function?

We could pass the server to the function, and then instantiate the Dash app on the same server. We could also return the same server at the end of the function, with our newly added Dash page.
```python
def construct_page(server):
	dash_app = dash.Dash(server=server, routes_pathname_prefix="/barchart")

	return dash_app.server
```

Constructing the Flask app would look something like this:
```python
def init_app():
	app = Flask(__name__, instance_relative_config=False)

	with app.app_context:
		app = init_homepage(app)
		app = init_linechart(app)
		app = init_barchart(app)

		return app
```

Voila! We can build a Flask app with as many Dash pages as we want! Think of the possibilites...