# How to write and host your technical documentation using Replit

In this guide, You'll learn how to build a professional technical documentation site. You'll write your docs as simple Markdown files, and use mkdocs-material as a static site generator to create fast-loading HTML pages.

By using Replit as an IDE and web server, you can keep your documentation publishing process very agile, having your changes reflect in production as you make them if you want. We'll also look at how to scale this better, by using multiple repls for a staging and production version of your docs and tracking everything in using version control with git and GitHub.

By the end of this guide, you'll have a bare-bones docs page set up and you can simply start adding content.

![final website](/images/teamsPro/hosting-docs/final-website.png)

## Steps to follow

We'll cover how to:

* create the repl
* install the MkDocs library
* add pages to our docs
* view the HTML version of our docs
* add our docs under version control
* pull changes made from GitHub
* set up a custom domain
* scale the docs site using multiple repls and Cloudflare

## Creating a repl

MkDocs is a Python library so we'll use a Python repl. We're going to be using [Teams Pro](https://replit.com/site/teams-pro) so sign up for that if you haven't already. You can also follow along most of the steps using the free version of Replit if you want, but some of the functionality will be more limited.

Visit [https://repl.new/python](https://repl.new/python) to create a new repl and choose your Team account as the owner.

![create repl](/images/teamsPro/hosting-docs/create-repl.png) 

You'll then be directed to the Replit workspace where you can edit and work on your project.

## Installing MKDocs 

Next, we need to configure or setup up our environment for our project.

Open up your shell, and run the following command:

```bash
python3 -m poetry init --no-interaction
```

This will create a Poetry file to track our Python dependencies. Now install Material for MKDocs by running the following:

```bash
python3 -m poetry add mkdocs-material
```

This installs `mkdocs-material` and `mkdocs`. Run the following command to bootstrap your new docs site.


```bash
mkdocs new
```

Notice that this creates a `mkdocs.yml` file which is our configuration file and a `docs` folder with an `index.md` file inside. This `index.md` file will have the content for our new homepage.

Open the `mkdocs.yml` file and replace the contents with the following.

```yaml
site_name: My Docs
theme:
  name: material
```

This will set up the name for your docs site (feel free to change it) and the theme.

Take a look at what things look like so far by running the following command in the shell.

```
mkdocs serve -a 0.0.0.0:443
```

This will start the MKDocs development server and Replit will pop open a browser preview window. It should look as follows.

![website](/images/teamsPro/hosting-docs/doc-website.png)

You can also see the URL of your docs that is visible to the world. It should look similar to `https://mkdocs.ritza.repl.co`, but with your team and project name.

## Adding pages

You probably want more than a single page of docs. Add a new file in `docs` folder named `about.md`. 

Now add the following to the `mkdocs.yml` file.

```yaml
nav:
    - Home: index.md
    - About: about.md
```
 
This will add the new page to the website's navigation bar.

![new page](/images/teamsPro/hosting-docs/new-page.png)

You can repeat this process if you would like to add more pages to your website - create a new file and add the name of the page and file to the configuration file.

## Keeping your repl alive and adding a boost

Normal repls turn off after some period of inactivity. To make it easier to run and to ensure it stays alive, create a file called `.replit` in the root of the project and add the following line to it.

```
run = ["mkdocs", "serve", "-a", "0.0.0.0:443"]
```

Now the docs will be served whenever you hit the big green "Run" button. 

Next, click on the name of your repl and turn on "Always On" and "Add Boost". This will mean users can always visit your site and it won't get turned off. The boost will give you some extra processing power which will make it faster to build your site once you have a lot of markdown files.

![boost repl](/images/teamsPro/hosting-docs/boost.png)


## Adding version control

You'll want to track changes and updates to your documentation with version control. Replit integrates with GitHub and you can set this up directly from within your repl.

Navigate to the version control tab on the left side of the project workspace and click on create a repository.

![create a repo](/images/teamsPro/hosting-docs/create-repo.png)

This will initiate a repository with the current version of your project, you can then click on the connect to GitHub option to connect to your Github account.

![connect to GitHub](/images/teamsPro/hosting-docs/connect-github.png)

From the pop window, choose the name of your repository and create it.

![name repo](/images/teamsPro/hosting-docs/create-git-repo.png)

This will automatically upload the contents of the entire site's documentation to your repository on GitHub. Any time you make a change from Replit, you can commit and push up the changes to GitHub to ensure that nothing gets lost and you have a log of all changes made to the docs.

## Pull changes from GitHub

People may also contribute to your docs by making pull requests to your GitHub repository. If it is public or accessible to specific people, the changes they make to the repository can be pulled back into our project on Replit.

Navigate to the version control tab, and check if your project is up to date with main/master.
If your project is not up to date, it will mean that several commits have been made to the Github repository that you have not yet pulled.

To add those changes, click on the pull button which will update your project by adding those changes.

![pull changes](/images/teamsPro/hosting-docs/replit-pr.png)

Once, your changes have been pulled from GitHub your project will be up to date with the Github repository. You may have to stop and start the repl to see the changes reflect live.

![Up to date repo](/images/teamsPro/hosting-docs/up-to-date.png)

## Set up a custom domain

For a more professional docs site, you'll probably want to run it on your own doman, such as `docs.example.com`. You can add a custom domain by pressing the Pencil icon on the right of the domain that Replit assigned to you and setting up your DNS settings as prompted. You can find more detailed instructions on this [here](https://docs.replit.com/hosting/hosting-web-pages#custom-domains)

## Scaling your docs platform

We've shown you how to get started with hosting your docs on Replit, but you'll likely have to tweak this to meet your own needs. We're still using the development server that is built into MKDocs, but this is not suitable for production use. 

The easiest way to handle more traffic is to add Cloudflare (The [free version](https://www.cloudflare.com/en-gb/plans/free/) should be fine for most use cases). This means Cloudflare will cache a version of your website and serve most of your users directly, taking the pressure off the repl.

You could also set up two separate repls: a Python repl, as we did in this guide, for the development version of your docs. You can use the command `mkdocs build` to create an optimized, static version. You can then transfer the `site` folder generated by this command to an [HTML repl](https://docs.replit.com/hosting/hosting-web-pages) which you can use as the production version of your docs site.

## Where next?

MKDocs Material has many customizations. You can add tags, add-ons, integrate with analytics, and [much more](https://squidfunk.github.io/mkdocs-material/reference/).

The [Replit docs](https://docs.replit.com) are built and hosted completely on Replit itself, so if you want help with anything or have any feedback, just email us at pro@replit.com.




