crud-app-tutorial

# Building internal tools with Replit

In this tutorial, we'll use Flask, SQLite for data storage, and SQlalchemy to create a task management app for a team, that allows team members to perform CRUD operations on the SQLite database and persist the data even if our application is shutdown. 

At the end of the tutorial, you should have an idea of:

* What is persistent data?
* How to create app authentication
* How to set up a database
* How to read data from a CSV file
* How to perform CRUD operations on the app

You can find the code for this tutorial at https://replit.com/@ritza/task-manager-app or check out the embedded repl below.


## Persistent Data

We will create an application  that uses a perisitent storage system to persist data even when our application is no longer running.

## Getting started with the code

Start a new team repl and Choose python as the template language.

![create-repl image](create_repl.png)


## Creating a flask application

Add the following few imports to the "main.py" to begin implementing the app:

```Python
import os
from replit import web
from flask import Flask
```

The "web" module is used for authentication so that only users with a replit account can get access to the application, "Flask" is used to send data through HTTP requests to our code, and "SQLAlchemy" to map our Python objects to the database.

Initialize a flask application, with the following code:

```Python
app = Flask(__name__)

@app.route("/")
@web.authenticated
def index():
    return "My task management app"
  
if __name__ == "__main__":
    web(app.run(host='0.0.0.0', debug=True))
```

This basic flask application will ask users to login into their Replit account before accessing the application. You can run the application to see the login request page before accessing the app. 

Next, create a list of users or team members that will be allowed access to manage the tasks. Add the following line below `app = Flask(__name__)` to initialize a secret key:

```python
app.config["SECRET_KEY"] = os.environ['SECRET_KEY']
```

Open up the console and type `import random, string`, then type `''.join(random.SystemRandom().choice(string.ascii_uppercase + string.digits) for _ in range(20))
` to generate string of random numbers.

This will be the secret key for the application. Save the secret key as an environment variable in the "Secrets(environment variables)" tab on the left panel. 

![secret key](secret_key.png)

Then create a list of Replit usernames belonging to the team member's who should have access to the application:

```python
USERS = ["your_usernames_here"]
```
Import the following modules:

```python
from functools import wraps
from flask import flash, url_for, render_template
```
Then add a helper and a decorator function to check whether the user is in the users list and enable access if it is.

```Python
def is_admin(username):
    return username in USERS

def admin_only(f):
    @wraps(f)
    def decorated_function(*args, **kwargs):
        if not is_admin(web.auth.name):
            flash("Permission denied.", "warning")
            return render_template(url_for("index"))
        return f(*args, **kwargs)
    return decorated_function

```
Add the annotation `@admin_only` just above the `index()` function in the `main.py` file.

In the root directory of the project, add a new folder and save it as "templates", inside it create a new File and save it as "index.html".

This "index.html" file will be the homepage of our application. Add the following code to it:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <h1>Replit Team Tasks</h1>
  </head>
  <body>
    <h1>Add an Task</h1>
    <form method="POST" action="/">
      <input type="text" name="title" placeholder="Title">
      <div>
      <input class="text-box" type="text" name="note" placeholder="Write text...">
      </div>
      <input type="submit" value="Add">
    </form>
  </body>
</html>
```

Change the return statement of the `index()` function to:
  ```Python
  return render_template('index.html')
  ``` 

Run the application to see the task form on our admin page.

![basic form](basic_form.png)

With this, we've created a basic Html template, which allows us to submit new tasks through a form. 

## Connecting to a database

Let's configure a database for storing tasks. Add two more imports to the "main.py" file:

```Python
import sqlite3
from flask_sqlalchemy import *
```

Add the following code below the import statements:

```Python
project_dir = os.path.dirname(os.path.abspath(__file__))
database_file = "sqlite:///{}".format(os.path.join(project_dir, "Tasks.db"))
```

In these two lines, we've stored a path to our projects directory and used it as the location for our SQLite database, `"Tasks.db"`.

Pass the SQLAlchemy URI to the app to create a  connection to the database by adding the following line of code below the secret key:

```Python
app.config["SQLALCHEMY_DATABASE_URI"] = database_file
db = SQLAlchemy(app)
```

For the database table to store the tasks, we'll create a class for the database model and then use SQLAlchemy to create the table.

Add the following block of code, below `'db = SQLAlchemy(app)'`:

```Python
class Task(db.Model):
    task_id = db.Column(db.Integer, primary_key=True)
    team_member = db.Column(db.String(40))
    task_name = db.Column(db.String(40))
    description = db.Column(db.String)
    due_date = db.Column(db.String)

db.create_all()
```
This code declares the 5 fields for the database table with the "task_id" field as the primary key field. If we run the application, a new database will be created as a file "Tasks.db" in the root directory of our project.

## Mapping our data

Let's create some GET and POST methods for the application, to add and display data from the database. Add the following import to the import statements:

```Python
from flask import request
```

Modify the `index()`function to look like this:

```Python
@app.route("/", methods=["GET", "POST"])
@web.authenticated
@admin_only
def index():
 
    if request.form:
        task = Task(task_id=request.form.get("task_id"),team_member=request.form.get("team_member"),task_name=request.form.get("task_name"),due_date=str(request.form.get("due_date")),description=request.form.get("description"))
        db.session.add(task)
        db.session.commit()
        print(task_id)
    tasks = Task.query.all()

    return render_template("index.html", tasks=tasks)
```

Also modify the "index.html" form to request all fields for the tasks:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <div>
    <h1>Replit Team Tasks</h1>
    </div>
  </head>
  <body>

<div >
  
  <form method="POST" action="/">
    <h2>Add a task</h2>
    <div >
      <label>Assign to</label>
      <input type="text" name="team_member">
    </div>
    <div>
       <label>Task Name</label>
       <input type="text" name="task_name">
    </div>
    <div>
       <label>Description</label>
      <input type="text" name="description">
    </div>
    <div>
       <label>Due Date</label>
       <input type="text" name="due_date" placeholder="yyyy-mm-dd">
    </div>
     <input type="submit" value="Add">
  </form>
</div>
 
<div>
<h1>Tasks</h1>
  {% for task in tasks %}
    
  <p>{{task.task_id}}, {{task.team_member}}, {{task.task_name}}, {{task.due_date}}, {{task.description}}</p>
    {% endfor %}

</div>
    
  </body>
</html>
```


The `query.all()` call for our GET method returns all tasks from our database and "tasks=tasks" defines the variable in our template.

If we run the application now, we'll see our tasks form.

![task_form](task_form.png)

## Reading File Data

We'll use a CSV file to load a mass of data into our database rather than using the Html form.

Create a new file in the root directory of the project and name it "team_tasks.csv". This is a template of how our CSV file should look:

```markdown
team_member,task_name,description,due_date
Azula,Update UI,Create avatar feature,2020-04-27
Yuni Gasai,Security,Add two-step authentication to web app,2020-05-22
Twice,Cloning,Clone the task management app,2020-03-22
Ken Takatsuki,Tutorial,Create a a javascript tutorials book,2020-08-11	
```

Using a CSV file is a much faster way of populating the database and it is easy to access too. We'll create a method to read and insert all the data into our database from the file. Add the following imports to the "index.html file".

```Python
import csv
from flask import redirect
```
Below the `db.create_all()` call, add the following function:

``` Python
def addTasks(task_file):
  with open(task_file,'r') as file:
    csv_reader = csv.DictReader(file, delimiter=',')
    counter = 0
    for line in csv_reader:
      if counter == 0:
        counter +=1
        pass
      else:
        print( line['team_member'],line['task_name'],line['description'],line['due_date'])
        
        task= Task(team_member=line['team_member'],task_name=line['task_name'],description=line['description'],due_date=line['due_date'])
        db.session.add(task)
        db.session.commit()
        counter+=1
  return redirect("/")

addTasks("team_tasks.csv")
```
Calling the `addTasks()` method inserts the data into the database, immediately after running the program you should delete this line. If you run it with this line every time it will keep adding the same data into the database.

After running the application, we should now be able to see all this data from our file in the Tasks table.

## Updating and Deleting Data

Now let's add a method for deleting and updating the data. Start with modifying the "index.html file" to add a form for updating and deleting data and a table to display the tasks in a better format.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <div >
    <h1>Replit Team Tasks</h1>
    </div>
  </head>
  <body>

<div>  
  <form class="task-form" method="POST" action="/">
    <h2>Add a task</h2>
      <div>
        <label>Assign to</label>
        <input type="text" name="team_member">
      </div>
      <div>
         <label>Task Name</label>
         <input type="text" name="task_name">
      </div>
      <div >
         <label>Description</label>
        <input type="text" name="description">
      </div>
      <div>
         <label>Due Date</label>
         <input type="text" name="due_date" placeholder="yyyy-mm-dd">
      </div>
      <input type="submit" value="Add">
  </form>
</div>
 
<div>
  <table>
    <caption><h1>Tasks</h1></caption>
    <thead>
      <tr>
        <th>Task ID</th>
        <th>Assigned Member</th>
        <th>Task Name</th>
        <th>Date Due</th>
        <th>Task Description</th>
         <th>Manage Task</th>
      </tr>
    </thead>
    <tbody>
    {% for task in tasks %}     
    <tr>
      <td>{{task.task_id}}</td>
      <td>{{task.team_member}}</td>
      <td>{{task.task_name}}</td>
      <td>{{task.due_date}}</td>
      <td>{{task.description}}</td>
      <td>
        <form method="POST" action="./update">
          <input type="hidden" value="{{task.team_member}}" name="oldTeamMember">
          <input type="text" value="{{task.team_member}}"  name="newTeamMember">
          <input type="submit" value="Update Team Member">
        </form>
        <form method="POST" action="./delete">
          <input type="hidden" value="{{task.task_id}}" name="task_id">
          <input type="submit" value="Delete Task">
      </td>
    </tr>
    {% endfor %}
    </tbody>
</table>
</div>
    
  </body>
</html>
```

We added the update and delete forms to the "index.html" file. Next, add their functions below the `index()` function in the "main.py" file.

```Python
@app.route("/update", methods=["POST"])
@web.authenticated
@admin_only
def update():
    oldTeamMember = request.form.get("oldTeamMember")
    newTeamMember = request.form.get("newTeamMember")
    task = Task.query.filter_by(team_member=oldTeamMember).first()
    task.team_member = newTeamMember
    db.session.commit()
    return redirect("/")

@app.route("/delete", methods=["POST"])
@web.authenticated
@admin_only
def delete():
    task_id = request.form.get("task_id")
    task = Task.query.filter_by(task_id=task_id).first()
    db.session.delete(task)
    db.session.commit()
    return redirect("/")
```
The two functions are both very similar. The update function can edit team members assigned the tasks. The delete function removes the tasks from the database by the task id.

## Styling your application

To add some CSS styling to our application, create another folder in the root directory and name it "static" to place the CSS file in. Then add the path to the flask app so it could read the directory to get those styles.

Change `app = Flask(__name__)` to:

```Python
app = Flask(__name__, static_folder='static', static_url_path='')
```

Let's start with styling the body of our "index.html". In the "static" folder, create a new file and name it "style.css".

Add the following code to it:

```css
body {
	height: 100%;
  jusitfy-content: center;
  margin: 0;
	background: linear-gradient(45deg, #49a09d, #5f2c82);
	font-family: sans-serif;
	font-weight: 100;
}
```
This creates a background with a blue to purple color gradient.
Next, we'll style our tasks table.

```CSS

input{
  text-align: center
}
table {
  color: white;
	width: 800px;
	border-collapse: collapse;
	overflow: hidden;
	box-shadow: 0 0 20px rgba(0,0,0,0.1);
}

th,
td {
	padding: 15px;
	background-color: rgba(255,255,255,0.2);
	color: #fff;
}

th {
	text-align: left;
}

thead {
	th {
    color: #fff;
		background-color: #55608f;
	}
}

tbody {
	tr {
		&:hover {
			background-color: rgba(255,255,255,0.3);
		}
	}
	td {
		position: relative;
		&:hover {
			&:before {
				content: "";
				position: absolute;
				left: 0;
				right: 0;
				top: -9999px;
				bottom: -9999px;
				background-color: rgba(255,255,255,0.2);
				z-index: -1;
			}
		}
	}
}

```
This creates a table with a transparent background and a white-highlighter effect when you hover above a cell.

For the header and forms in our application, we'll use the following 3 classes.

```css
.header{
  color: white;
  font-size: 50px;
  font-family: ''
  
}

.task-form{
  color: white;
  text-align: center;
  margin: auto;
  width: 220px;
  background-color: rgba(255,255,255,0.3)
  box-sizing: border-box;
  box-shadow: 0 15px 25px rgba(0,0,0,.6);
  border-radius: 10px;
}

.container {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, 10%);
}

```
The "container" class is for the div tags in the task form.

Modify the "index.html form" to look the code below, to apply the CSS styles:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <div class="header">
    <h1 class="header">Replit Team Tasks</h1>
    </div>
    <link rel="stylesheet" type="text/css" href="{{ url_for('static',filename='style.css')}}"/>
  </head>
  <body>

<div>
  
  <form class="task-form" method="POST" action="/">
    <h2>Add a task</h2>
    <div>
      <label>Assign to</label>
      <input type="text" name="team_member">
    </div>
    <div>
       <label>Task Name</label>
       <input type="text" name="task_name">
    </div>
    <div>
       <label>Description</label>
      <input type="text" name="description">
    </div>
    <div >
       <label>Due Date</label>
       <input type="text" name="due_date" placeholder="yyyy-mm-dd">
    </div>
     <input type="submit" value="Add">
  </form>
</div>
 
<div class="container">
  <table>
    <caption><h1>Tasks</h1></caption>
  <thead>
  <tr>
    <th>Task ID</th>
    <th>Assign Member</th>
    <th>Task Name</th>
    <th>Date Due</th>
    <th>Task Description</th>
     <th>Manage Task</th>
  </tr>
    </thead>
    <tbody>
  {% for task in tasks %}
    
  <tr>
    <td>{{task.id}}</td>
    <td>{{task.team_member}}</td>
    <td>{{task.task_name}}</td>
    <td>{{task.due_date}}</td>
    <td>{{task.description}}</td>
    <td><form method="POST" action="./update">
    <input type="hidden" value="{{task.team_member}}" name="oldTeamMember">
    <input type="text" value="{{task.team_member}}"  name="newTeamMember">
    <input type="submit" value="Update Team Member" style="background-color: rgba(255,255,255,0.3)">
  </form>
  <form method="POST" action="./delete">
  <input type="hidden" value="{{task.task_id}}" name="task_id">
  <input type="submit" value="Delete Task" style="background-color: rgba(255,255,255,0.3)"></td>
  </tr>
    {% endfor %}

    </tbody>
</table>
</div>
    
  </body>
</html>
```

The application should look like the following image:

![app](task_manager.png)

Check out the embedded repl below to see the code.


### Here are some things you can try to improve your skills:

* Create a login page that stores visitor usernames and passwords
* E-commerce web app and store product info in a database

<iframe frameborder="0" width="100%" height="500px" src="https://replit.com/@ritza/task-manager-app?embed=true"></iframe>



