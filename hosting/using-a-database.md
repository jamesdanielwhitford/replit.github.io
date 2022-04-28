# Using a database
## Introduction
Replit allows us to make use of databases within our repls to help make programs that can both manage and store data. This reference will walk you through the foundational operations for interacting with the data in these databases. These are the CRUD operations which involve creating, reading, updating and deleting data. This reference also contains information on how to access these databases and many handy methods for managing our data.
## Table of contents
1. [How File Persistence Works](#a)
2. [Choices: The Replit Database and SQLite](#b)
3. [Replit’s Database](#c)
    1. [Introduction](#d)
    2. [Importing the database](#e)
    3. [Creating data](#f)
    4. [Reading data](#g)
    5. [Updating data](#h)
    6. [Delete data](#i)
    7. [Summary](#j)
4. [SQLite database](#k)
    1. [Introduction](#l)
    2. [Importing the database](#m)
    3. [Create and connect to a database](#n)
    4. [Create tables](#o)
    5. [Insert data](#p)
    6. [Read data](#q)
    7. [Update data](#r)
    8. [Delete data](#s)
    9. [Commit changes](#t)
    10. [Closing connection](#u)
    11. [Summary](#v)
    
## How File Persistence Works <a name = "a"></a>
File persistence lets us create programs that store our files and data between runs, so our data is not lost whenever the program ends. This allows for the creation of programs that can create, update, read, and delete data that has not been created from code within that program. The data can also be updated from within our program and those updates will still be accessible after the program ends.

Below is an example of how file persistence works with the Replit database

First we run our application, import the database, add data to our database, and declare some variables. 

#### First run

```python
# Importing the Replit database.
from replit import db

# Adding a key-value pairing to the database.
db[“key1”] = “value1”

# Accessing and printing the value associated wit the key just created.
print(db[“key1”])

# Declaring a variable that stores an integer outside of our database.
my_variable = 100

# Printing the variable.
print(my_variable)
```

#### Output:
```
value1
100
```

We can print both the data from our database and our variables because both were created within the program.

However, if we were to run the program again without the code that adds data to our database and without the declaration of our variable only the data from the database will print, the attempt to print the undefined variable results in an error.

#### Second run:

```python
from replit import db

# Print the value from the key-value pairing created on the previous run.
print(db[“key1”])

# Attempt to print from the variable which was defined in the previous run.
print(my_variable)
```

#### Output:

```python
value1
Traceback (most recent call last):
  File "main.py", line 3, in <module>
    print(my_variable)
NameError: name 'my_variable' is not defined
```

This occurs because the data that was stored in the database persisted between runs and thus did not need to be created again to be accessed. However the variable's data did not persist which leads to the variable name being undefined.


## Choices: The Replit database and SQLite <a name = "b"></a>
Our repls can make use the Replit database and an SQLite database. The Replit database is a user-friendly and handy database that acts, and is structured, much like a Python dictionary and thus does not require a large learning curve. The SQLite database allows for the creation of multiple databases and stores data in a table format. 

## Replit’s Database <a name = "c"></a>


### Introduction <a name = "d"></a>
Every repl can access and interact with its own unique Replit database. This database can be accessed from the library and requires no configuration beyond that import. Interacting with the Replit database follows much of the same syntax and logic as creating and interacting with the key-value pairs of a Python dictionary. This allows the database to be an approachable and user-friendly database with no steep learning curve. This section will introduce the create, read, update, and delete operations associated with the Replit database.

### Importing the database <a name = "e"></a>
To access the Replit database we import db:
```python
from replit import db
```

### Creating data <a name = "f"></a>
The Replit database works a lot like a Python dictionary so we can add data to our database by assigning values to keys using square bracket indexing:
```python
from replit import db

# Adding a key and associated value to the database
db["key1"] = "value1"
```

Replit’s database is able to handle different types of values like lists, dictionaries, Integers, floats, None type, and strings:

```python
from replit import db

db["key1"] = "value1"
db["integer_1"] = 100
db["float_1"] = 9.99
db["my_list"] = [1,2,3]
db["my_dictionary"] = {"key_a": "value_a", "key_b": "value_b"}
db["none_key"] = None
```

Make use of 2D lists as a value to create table-like structures within your database:
```python
from replit import db

db["2D_key"] = [["id","name"],[1,"James"],[2,"Angel"]]

for column in db["2D_key"]:
    print(column)
```
#### Output:
```
ObservedList(value=["id","name"])
ObservedList(value=[1,"James"])
ObservedList(value=[2,"Angel"])
```
The ObservedList object you see in the output is a Replit database object that acts like a Python list and thus can be indexed as such.

### Reading data <a name = "g"></a>
Read from your database by referencing the key of the value:

```python
from replit import db

# Creating data in our database
db["key1"] = "value1"
db["my_list"] = [1,2,3]
db["my_dictionary"] = {"key_a": "value_a", "key_b": "value_b"}

# Accessing and printing data from the database
print(db["key1"])
print(db["my_list"][0])
print(db["my_dictionary"]["key_a"])
```

#### Output:
```
value1
1
value_a	
```

We can use the built-in Python dictionary method .get() to retrieve the value at the key passed in as an argument:

```python
from replit import db

# Creating data for our database
db["float_1"] = 9.99

# Accessing the value of the data created by its key
print(db.get("float_1"))
```

We can loop through the keys stored in the database to get access to the values of those keys:

```python
from replit import db

# Creating data for our database
db["key1"] = "value1"
db["my_list"] = [1,2,3]
db["my_dictionary"] = {"key_a": "value_a", "key_b": "value_b"}

# Accessing the keys from our database and then printing the values associated
for key in db:
  print(db.get(key))
```

The .keys() method returns a list of the keys within our database:

```python
from replit import db

# Creating data for our database
db["key1"] = "value1"
db["my_list"] = [1,2,3]
db["my_dictionary"] = {"key_a": "value_a", "key_b": "value_b"}

# Printing all the keys from our database
print(db.keys())
```
#### Output:
```
{'key1', 'my_list', 'my_dictionary', '2D_keys'}
```

The .prefix() method allows us to get the values of keys with only part of that key. This allows us to return multiple values for keys that share the same prefix:

```python
from replit import db

# Creating data for our database
db["key1"] = "value1"
db["my_list"] = [1,2,3]
db["my_dictionary"] = {"key_a": "value_a", "key_b": "value_b"}

# Printing all the keys from our database that have a prefix of "my"
print(db.prefix("my"))
```
#### Output:
```
('my_dictionary', 'my_list')
```
### Updating data <a name = "h"></a>
We can update values that are stored in our database by assigning new values to their associated key:

```python
from replit import db

# Create data with "float_1" as key and print
db["float_1"] = 9.99
print(db[“float_1”])

# Update data at "float_1" key and print
db[“float_1”] = 3.33
print(db[“float_1”)
```
#### Output:
```
9.99
3.33
```

We can also mutate numbers that are stored in our database:

```python
from replit import db

# Create data with "float_1" as key and print
db["float_1"] = 9.99

# Performing an operation on our data
db["float_1"] += 0.01

# Printing result of operation
print(db["float_1"])
```
#### Output:
```
10.0
```

### Delete data <a name = "i"></a>
We make use of the del keyword and square bracket indexing to delete key-value pairings from out database:

```python
from replit import db

# Creating data for our database
db["float_1"] = 9.99

# Deleting the data we added at the key "float_1"
del db["float_1"]
if "float_1" not in db:
	print("Value deleted successfully.")
```

#### Output:
```
Value deleted successfully.
```

### Summary <a name = "j"></a>
Overall, the Replit database is a simple and useful database that allows us to easily and dynamically update our data. The features resembling the Python dictionary mean we can make use of all the useful built-in Python dictionary functions to interact with our database. 

In order to create more than one database and utilize the creation and merging of data stored in a table format we can look to the SQLite database.


## SQLite database <a name = "k"></a>


### Introduction <a name = "l"></a>
We can make use of SQLite in our repl to allow for the storing, structuring, and managing of data in a relational database that allows for file persistence for our programs. 

SQLite structures our data in a table format. We can set the number of columns, names of those columns, and data types that we expect to store in those columns. However, SQLite allows for dynamic types within each column, meaning we can insert data of a different type than we had set for a particular column. We can create multiple databases and multiple tables within each database. SQLite requires no configuration, install, or login. 

The database allows for complex operations, like joining tables from different databases, all while maintaining a connection to only a single database.


The basic structure of our code when using SQLite is: 
1.	Import SQLite3
2.	Create and connect to a database
3.	Perform CRUD operations
4.	Commit the changes made to the database 
5.	Closing the connection to the database.

Here is a look at what a basic structure of your code should look like when using the SQLite database:
```python
# Import 
import sqlite3

# Create the database and connection
connection = sqlite3.connect("my_database")

# Create a table for storing data
connection.execute("CREATE TABLE IF NOT EXISTS My_library (id INTEGER PRIMARY KEY, author STRING, book STRING);")

# Perform CRUD operations

# Create
connection.execute("INSERT INTO My_library (id,author,book) "
             "VALUES (1, 'Steve Biko','I write what I like.')")

# Read
cursor_object = connection.execute("SELECT * FROM My_library")
print(cursor_object.fetchall())

# Update
connection.execute("UPDATE My_library SET book = 'I WRITE WHAT I LIKE' WHERE id = 1")

# Delete
connection.execute("DELETE from My_library WHERE id = 1;")

# Commit changes
connection.commit()

# Close the connection
connection.close()
```


### Importing the database <a name = "m"></a>
We import SQLite to our program using this line of code:

```python
import sqlite3
```


### Create and Connect to a database <a name = "n"></a>
From there we can create, name, and connect to our database using the sqlite3 module and .connect() method.

```python
connection = sqlite3.connect("my_database")
```


### Create Tables <a name = "o"></a>
SQLite makes use of tables to structure our data. To create a table, we make use of the CREATE TABLE query. To ensure we do not create a table that already exists we may use the CREATE TABLE IF NOT EXISTS query. In this CREATE TABLE query we assign names for our table columns along with what type of data will be stored in that column and whether the data is a primary key:

```python
connection.execute("CREATE TABLE IF NOT EXISTS My_library (id INTEGER PRIMARY KEY, author STRING, book STRING);")
```

### Insert data <a name = "p"></a>
To insert some data into out table we make use of the INSERT query. This query requires the column names we are inserting into along with the values that we will insert into each of those columns:

```python
connection.execute("INSERT INTO My_library (id,author,book) "
             "VALUES (1, 'Steve Biko','I write what I like.')")
```

Alternatively, we may want to insert data into our tables using an input from an external source. To do this we may format our query information as a string and our column names and data we wish to insert as key-value parings in a dictionary:

```python
insert_query = ("INSERT INTO My_library (id,author,book)" 
                "VALUES (:id, :author, :book);")

author_parameters = {
        'id': 2,
        'author': 'Lewis Carrol',
        'book': "Alice's Trip in Wonderland"
    }

connection.execute(insert_query, author_parameters)
```


### Read data <a name = "q"></a>
To read from the database we can make use of a Cursor variable that holds the data we pull from our database connection. We get data from our database using the SELECT query. We then read that data from our Cursor variable.

The SELECT * query returns all the data from our database and the .fetchall() method allows us to retrieve that data from our cursor variable:

```python
cursor_object = connection.execute("SELECT * FROM My_library")

print(cursor_object.fetchall())
```

#### Output:
```
[(1, 'Steve Biko', 'I write what I like.'), (2, 'Lewis Carrol', "Alice's Trip in Wonderland")
```

The WHERE query returns all the data from our database where that data corresponds with our requirements:

```python
cursor_object = connection.execute("SELECT * FROM My_library WHERE id = 1")

print(cursor_object.fetchall())
```

```python
[(1, 'Steve Biko', 'I write what I like.')]
```


### Update data <a name = "r"></a>
To update the data within our table we execute an UPDATE query:

```python
connection.execute("UPDATE My_library SET book = 'Alices Adventures in Wonderland' WHERE id = 2")
```

### Delete data <a name = "s"></a>
To delete data from our table we execute a DELETE query:

```python
connection.execute("DELETE from My_library WHERE id = 1;")
```

### Commit changes <a name = "t"></a>
When we have made our changes to our database, we commit our changes through our connection:

```python
connection.commit()
```

### Closing connection <a name = "u"></a>
Finally, we close our connection to our database:

```python
connection.close()
```

### Summary <a name = "v"></a>

The SQLite database provides an intuitive table format for our data that we can easily interact with by way of queries. The fact we do not need to install or configure our database makes for an easy setup, and the ability to create multiple tables and databases means we can store our data separately all while being able to merge files if needed.
 
