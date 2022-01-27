# How to write and host your technical documentation using Replit

In this guide, you'll learn how to build a professional technical documentation site. You'll write your docs as simple Markdown files, and use mkdocs-material as a static site generator to create fast-loading HTML pages.

By using Replit as an IDE and web server, you can keep your documentation publishing process very agile, having your changes reflect in production as you make them if you want. We'll also look at how to scale this better, by using multiple repls for a staging and production version of your docs and tracking everything using version control with git and GitHub.

By the end of this guide, you'll have a bare-bones documentation site set up, and you can simply start adding content.

![final website](/images/teamsPro/hosting-docs/final-website.png)

## Steps to follow

We'll cover how to:

* create the repl
* install the MkDocs library
* add pages to our documentation site
* view the HTML version of our docs
* add our docs under version control
* pull changes made from GitHub
* set up a custom domain
* scale the docs site using multiple repls and Cloudflare

## Creating a repl

MkDocs is a Python library so we'll use a Python repl. We're going to be using [Teams Pro](https://replit.com/site/teams-pro) so sign up for that if you haven't already. You can also follow along most of the steps using the free Replit starter plan if you want, but some functionality will be more limited.

Visit [https://repl.new/python](https://repl.new/python) to create a new repl and choose your Team account as the owner of the repl.

![create repl](/images/teamsPro/hosting-docs/create-repl.png) 

You'll then be directed to the Replit workspace where you can edit and work on your project.

## Installing MKDocs 

Next, we need to configure or setup up the environment for our project.

Open up your shell, and run the following command:

```bash
python3 -m poetry init --no-interaction
```

This will create a Poetry file to track our Python dependencies. Now install Material for MKDocs by running the following:

```bash
python3 -m poetry add mkdocs-material
```

To bootstrap the creation of a new docs site, run the following command:


```bash
mkdocs new .
```

This creates a `mkdocs.yml` file which is our configuration file and a `docs` folder with an `index.md` file inside. This `index.md` file will have the content for our new homepage.

Open the `mkdocs.yml` file and replace the contents with the following.

```yaml
site_name: My Docs
theme:
  name: material
```

This will set up the name for your docs site (feel free to change it) and the theme.

To preview the new documentation site, run the following command in the shell.

```bash
mkdocs serve -a 0.0.0.0:443
```

This will start the MKDocs development server and Replit will pop open a browser preview window. It should look as follows.

![website](/images/teamsPro/hosting-docs/doc-website.png)

The URL of your docs that is visible to the world is displayed just above the preview. It should look similar to `https://docs-site.ritza.repl.co`, but with your team and project name.

## Adding pages

You probably want more than a single page for your docs. To add new pages to your documentation, you will need to add new markdown files in the `docs` folder and then reference them in `mkdocs.yml` file. 

As an example create a new file in docs folder named `about.md`. 

Now add the following to the `mkdocs.yml` file.

```yaml
nav:
    - Home: index.md
    - About: about.md
```
 
This will add the new page to the website's navigation bar.

<img src="/images/teamsPro/hosting-docs/new-page.gif"
alt="new page"
style="Width: 60% !important;"/>


You can repeat this process if you would like to add more pages to your website - create a new markdown file in the `docs` folder and reference it in the `mkdocs.yml` configuration file.

## Keeping your repl alive and adding a boost

Normal repls turn off after some period of inactivity. To make it easier to run and to ensure it stays alive, create a file called `.replit` in the root of the project and add the following line to it.

```
run="mkdocs serve -a 0.0.0.0:443"
```

Now the docs will be served whenever you hit the big green "Run" button. 

Next, click on the name of your repl and turn on "Always On" and "Add Boost". This will mean users can always visit your site and it won't get turned off. The boost will give you some extra processing power which will make it faster to build your site once you have a lot of markdown files.

<img src="/images/teamsPro/hosting-docs/boost.png"
alt="boost repl"
style="Width: 60% !important;"/>


## Adding version control

You'll want to track changes and updates to your documentation with version control. Replit integrates with GitHub and you can set this up directly from within your repl.

Navigate to the version control tab on the left side of the project workspace and click on "Create a Git Repo".

<img src="/images/teamsPro/hosting-docs/create-repo.png"
alt="create a repo"
style="Width: 50% !important;"/>


This will initiate a repository with the current version of your project. You can then click on the connect to GitHub option to connect to your GitHub account. If you haven't already linked your GitHub account, you will be prompted to authorize Replit to access your GitHub account. 

<img src="/images/teamsPro/hosting-docs/connect-github.png"
alt="connect to GitHub"
style="Width: 50% !important;"/>

From the popup window, choose the name of your repository and create it.

<img src="/images/teamsPro/hosting-docs/create-git-repo.png"
alt="create git repo"
style="Width: 70% !important;"/>


This will automatically upload the contents of the entire site's documentation to your repository on GitHub. Any time you make a change from Replit, you can commit and push up the changes to GitHub to ensure that nothing gets lost and you have a log of all changes made to the docs.

## Pull changes from GitHub

People may also contribute to your docs by making pull requests to your GitHub repository. If it is public or accessible to specific people, the changes they make to the repository can be pulled back into our project on Replit.

Navigate to the version control tab, and check if your project is up to date with your working branch.
If your project is not up to date, it will mean that several commits have been made to the GitHub repository that you have not yet pulled.

To add those changes, click on the pull button which will update your project.

<img src="/images/teamsPro/hosting-docs/replit-pr.png"
alt="pull changes"
style="Width: 60% !important;"/>


Once, your changes have been pulled from GitHub your project will be up to date with the Github repository. You may have to stop and start the repl to see the changes reflect live.


## Set up a custom domain

For a more professional docs site, you'll probably want to run it on your own domain, such as `docs.example.com`. You can add a custom domain by pressing the pencil icon on the right of the domain that Replit assigned to your site and set up your DNS settings as prompted. You can find more detailed instructions on this [here](https://docs.replit.com/hosting/hosting-web-pages#custom-domains)

<img src="/images/teamsPro/hosting-docs/domain.png"
alt="custom domain"
style="Width: 70% !important;"/>

## Scaling your docs platform

We've shown you how to get started with hosting your docs on Replit, but you'll likely have to tweak this to meet your own needs. We're still using the development server that is built into MKDocs, but this is not suitable for production use. 

The easiest way to handle more traffic is to add Cloudflare (The [free version](https://www.cloudflare.com/en-gb/plans/free/) should be fine for most use cases). Cloudflare will cache a version of your website and serve most of your users directly, taking the pressure off the repl.

You could also set up two separate repls: a Python repl, as we did in this guide, for the development version of your docs. You can use the command `mkdocs build` to build an optimized, static version. You can then transfer the `site` folder generated by this command to an [HTML repl](https://docs.replit.com/hosting/hosting-web-pages) which you can use as the production version of your docs site.

## Where next?

MKDocs Material has many customizations. You can add tags, add-ons, integrate with analytics, and [much more](https://squidfunk.github.io/mkdocs-material/reference/).

The [Replit docs](https://docs.replit.com) are built and hosted completely on Replit itself, so if you want help with anything or have any feedback, just email us at pro@replit.com.

<iframe height="400px" width="100%" src="https://replit.com/@ritza/docs-site?embed=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>



