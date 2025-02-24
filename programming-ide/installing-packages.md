# Installing packages

With Replit, you can use most packages available in Python and JavaScript. Replit will install many packages on the fly just by importing them in code. You can read more about how we do this using [a universal package manager](https://blog.replit.com/upm).

## Searching For and Adding Packages

On a Python or JavaScript repl, you can search for a package to install by clicking on the
<img
  src="https://replit.github.io/media/misc/libraries_hover.png"
  style="height: 24px; vertical-align:text-bottom; width: 21px; margin: 0 3px; display: inline-block;"
/>
icon on the sidebar in the workspace. Simply search for the package you want, and select it to install the package or to view its documentation. Clicking on the "Add Package" icon will put it in a spec file and a lock file. If no such file exists, it will be created for you.

Unless otherwise specified, the repl will always attempt to install the latest version of each package.

## Direct Imports

The easiest way to add a package is to directly import it:

Python:

```python
import flask
```

JavaScript:

```javascript
const express = require('express');
```

Doing so will install the latest version of the package into your repl. A spec file and lock file will be created so the versions won't change. Wherever possible, we recommend using a file to manage dependencies.

### Guessing Failures

When you add a package by importing, we attempt to guess what package you want based on the modules you are importing. In most languages, this is a direct correspondence. However, in Python we can sometimes get it wrong. You can directly request a package by specifying the package directly on the import line.

```python
import twitter #upm package(python-twitter)
```

You can configure additional options for package guessing by reading about the [.replit](https://docs.replit.com/repls/dot-replit) file.

## Spec Files

Each language has a file that is used to describe the project's required packages:

* Python: `pyproject.toml`
* JavaScript (Node.js): `package.json`

### Python

In a `pyproject.toml` file, you list your packages along with other details about your project. For example, consider the following snippet from `pyproject.toml`:

```
...
[tool.poetry.dependencies]
python = "^3.8"
flask = "^1.1"
...
```

This will tell the packager that your project requires at least Python version 3.8, and to install the flask package at version 1.1.

### JavaScript

Note that `package.json` files are only for Nodejs/Express repls (they do not work in HTML/CSS/JS repls). A `package.json` file contains more information about the project, but also lists the dependencies. As an example, here is the `package.json` file you can include in a
[Nodejs/Express template](https://replit.com/languages/nodejs):

```json
{
  "name": "app",
  "version": "0.0.1",
  "description": "",
  "main": "index.js",
  "scripts": {
  },
  "author": "",
  "license": "MIT",
  "dependencies": {
    "express": "latest",
    "body-parser": "latest",
    "sqlite3": "latest"
  }
}
```

Note that all the packages are being installed with their latest version. Alternatively, you can replace "latest" with a specific version number to install that version, or precede it with a carat `^` to indicate "this version or newer". For example:

```json
  "dependencies": {
    "express": "^4.16.3",
    "body-parser": "latest",
    "sqlite3": "3.1.12"
  }
```

This will install `express` at version 4.16.3 or newer, `body-parser` at the latest version, and `sqlite3` at exactly version 3.1.12.
