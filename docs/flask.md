# Flask

## What is Flask
Micro-frameworks are the opposite of full-stack frameworks, which also offer additional modules for features such as authentication, database ORM, input validation and sanitization, etc.

Flask is known as a micro-framework because it is lightweight and only provides components that are essential.
- routing
- request handling
- sessions

## Client vs. Server
The client and server are the main entities between which all communication of data over the Internet takes place.
The request and response cycle is the core of all communication that takes place between a client and a server!

The client and server communicate with each other through http protocol(can be varied)
- Think of the protocols as a language that they both understand. 
- GET, POST, PUT, DELETE


## WSGI(Web Server Gateway Interface)
- a standard that describes the specifications concerning the communication between a web server and a client application.
- Flaks handles it for you

```
from flask import Flask
app = Flask(__name__)
@app.route("/")
def hello():
    return "Hello World!";

if __name__ == "__main__":
    app.run(debug = True, host = "0.0.0.0", port = 3000)
```
- Flask allows us to use the route() decorator to bind a meaningful URL to each view function we create.

route decorator (case sensitive, static routing)
- rule: The rule represents the URL rule which is passed as a string to the decorator.
- endpoint (not needed): The endpoint is the name of the view function which is bound to the URL route. Flask assumes this parameter itself, and the developer does not need to specify it.
- options


## dynamic routing
In static routing, the rule parameter of the route decorator was a simple string. However, in dynamic routing, the rule parameter is not a constant string. Instead, a variable rule is passed to the route(). 
- In Flask we can add variable rules inside the URL route by using the following syntax: <variable_name>. The variable called variable_name will then be passed to the view function to be used.

```
"""An example application to demonstrate Variable Rules in Routing"""
from flask import Flask
app = Flask(__name__)


@app.route("/")
def home():
    """View for the Home page of the website."""
    return "Welcome to the HomePage!"


@app.route("/<my_name>")
def greatings(my_name):
    """View function to greet the user by name."""
    return "Welcome "+ my_name +"!"


if __name__ == "__main__":
    app.run(debug=True, host="0.0.0.0", port=3000)
```

## Static Templates

render_template() which is used to render the desired HTML templates. This method has the following parameters:
- template_name_or_list: the name of a template or an iterable list of templates (the method will render the first template in the list)
- context (optional): variables that should be available inside the template.

### Module file structures


./templates folder
- .html

./
- app.py

### Package file structures
- If the application logic is divided into separate modules (i.e., separate .py files), then these files are present in the same package.

./application
- __init__.py
  - ./templates
  - home.html




```
from flask import Flask, render_template
app = Flask(__name__)

@app.route("/")
def home():
    return render_template("home.html")


if __name__ == "__main__":
    app.run(debug=True, host="0.0.0.0", port=3000)
```


## Static Files

./statics
- url_for() function
  - The url_for() function is used to build a URL for a certain endpoint. We can use it to build URLs for view functions as well. It takes the name of the endpoint and any associated variables as arguments.
```
<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="{{url_for('static', filename='borders.css')}}" />
    </head>
    <body>
        <h1>Home Page!</h1>
        <p>Welcome to the homepage for "How to Server Static Files" Demo!</p>
    </body>
</html>
```

## Dynamic Templates
