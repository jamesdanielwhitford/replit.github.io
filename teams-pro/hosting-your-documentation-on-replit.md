# How to host your technical documentation using replit

In this tutorial, You'll learn how to build a professional technical documentation site. You'll write your docs as simple Markdown files, and use mkdocs-material as a static site generator to create fast-loading HTML pages.

Mkdocs is a popular static site generator, but it doesn't look great and lacks features like search. Material for MKDocs is an extension that looks better and has built-in search.

You can read more about it on the official website at [Material for MKDocs](https://squidfunk.github.io/mkdocs-material/)

![final website](final-website.png)

# Steps to follow

We'll cover how to:

* create an Html repl
* install the mkdocs library
* add pages to our docs
* add our docs under version control
* pull changes made from github
* set up a custom domain

# Creating a repl

To get started, log in to your replit account and head over to your teams' homepage. If you do not have an account on Replit, you can go to [Replit's website](https://replit.com) and sign up, then you can head over to the [team's page](https://replit.com/teams/) to create a new team for your organization.

Once you're logged in, navigate to your team's dashboard and click the 'create team repl button on the dashboard to create a new python repl.

![create repl](create-repl.png) 

on the small window that pops up, choose python as your template language and choose a name for your repl and then click on create repl.

You'll then be directed to the repl workspace where you can edit and work on your project.


# Installing MKDocs 

Next, we need to configure or setup up our environment for our project.

Open up your shell, and run the following command:

`pip install mkdocs-material`

This will install all the mkdocs packages we need for our project.
Once our packages are successfully  installed, we'll bootstrap the app by running the following command:

`mkdocs new .`

you'll notice there's a new mkdocs.yml file which is our configuration file and a docs folder with an index.md file inside, which is the documentation homepage. 

If you open up the mkdocs.yml file you can specify the name of your site and theme to use by adding the following lines to the file:

```
site_name: <name_of_your_site>
theme: material
```

Next, we'll run the build command:

`mkdocs build`

to build the documentation website. The output of this command is placed in the site folder thus we need to copy it to the home directory of our Html project to ensure replit can serve the static content. To do so we need to run the following command:

`rsync -vua site/ .`

this allows us to copy and synchronize files and directories remotely/ locally from a source.
Notice the files in our home directory now correspond with those in the site folder.

Next we're going to use poetry as our dependency management tool to manage our mkdocs packages. 
Run the following comman to initialize the setup:

`python3 -m poetry init --no-interaction`

We need to add our mkdocs library to the configuration file with the following command:
`python3 -m poetry add mkdocs-material`

Next, we'll run the command:

`mkdocs serve -a 0.0.0.0:443`

To serve the static content with live-reload for the docs server as we develop our document site.


Once complete you should be able to see the following output.


![website](doc-website.png)


# Adding pages

If you want to add several pages to your website, you can go to the 'docs' folder in your project and add a new markdown file and give it the name you want your new page to be titled e.g "about.md".

Once you have created the file open the configuration file 'mkdcocs.yml' and add the following lines:

```
nav:
    - Home: index.md
    - About: about.md
```
 
this will add the new page path to your websites navbar.

![new page](new-page.png)

You can repeat this process if you would like to add more pages to your website - create a new file and add the name of the page and file to the configuration file.

# Adding version control

Repit allows us to create add our projects under version control directly from our workspace.
Navigate to the version control tab on the left side of the project workspace and click on create a repository.

![create a repo](create-repo.png)

this will initiate a repository with the current version of your project, you can then click on the connect to Github option to connect to your Github account.

![connect to github](connect-github.png)


on the pop window, you can choose the name of your repository, describe and then create it.

![name repo](create-git-repo.png)


This will automatically upload the contents of the entire site's documentation to your repository on Github.


# Pull changes from github

Once your project has been added to a Github repository, if it is public or accessible to specific people,
the changes they make to the remote repository can be pulled back into our project on replit.

Navigate to the version control tab, and check if your project is up to date with main/master.
If your project is not up to date, it will mean that several commits have been made to the Github repository that you have not yet pulled.

To add those changes, click on the pull button which will update your project by adding those changes.

![pull changes](replit-pr.png)


Once, your changes have been pulled from Github your project will be up to date with the Github repository.

![Up to date repo](up-to-date.png)

To keep your repl on and add a boost so that it can run in production you can click on the repl name and at the bottom of the pop window, you'll see a radio button, slide it right to keep the repl and just below it there's a button to boost the repl. Boosting your repl will allow it to run x2 faster.

![boost repl](boost.png)


# Set up custom domain

 If you are deploying your webite with github, GitHub Pages offers support for using a Custom Domain. However, you need to take an additional step so that MkDocs will work with your custom domain. You can follow the lin for more on
 [how to add custom domain to your site](https://www.mkdocs.org/user-guide/deploying-your-docs/).

# Things to try

Some things you can try out to improve your documentation site:

* [Change the color palette of your theme](https://www.mkdocs.org/getting-started/#theming-our-documentation)
* [Change the favicon icon on your site](https://www.mkdocs.org/getting-started/#changing-the-favicon-icon)
