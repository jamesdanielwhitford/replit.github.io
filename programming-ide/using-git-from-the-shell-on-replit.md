

# Using Git from the shell on Replit


The shell helps us manage our files, allowing us to enter commands to add or remove new files and install or test the code in our files. Let's take a look at how we can use Git from the shell in Replit.


## Getting started


First, create a new repl
![](img1.png)

In the new repl dialog, click on `Import from GitHub` in the top right corner and paste the URL of your GitHub project into the `GitHub URL` field

![](img2.png)

![](img3.png)


Click the blue `Import from GitHub` button at the bottom, and Replit will clone your project and create your repl.
When we `Import from GitHub` replit already clones our repl for us.





### Updating README.md file


We will go ahead and make changes to our ```README.md``` file. 
```
This is my guide tutorial to using Git from the shell on replit

It will include the following commands:
* git clone
* git branch
* git checkout
* git add remote
* git merge
* git rebase
* git push
* git commit
```
I added the above to my `README.md` file. 


Next, we want to add the `README.md` file and then commit the changes we made to the file. 

So we will add the following commands to our shell
```python
git add README.md
git commit -m "Update README.md"
```

![](img5.png)

When we commit the file we save the changes we made to our file to the local repository. The ``` -m``` is for the commits message, which is what we would like to have committed in the file. 

If you want to add a file or multiple files to your repo instead of just editing the `README.md` file then you can add the following command:

```
python
git add -A
```
or 
```
python
git add .
```

## Push README.md file back up to GitHub


For the next step, we might need to use SSH keys so this process might be a little longer than the other steps. 
Before we can ```git push``` the file we need to use the SSH keypairs for Github.

### SSH keypair setup for Github

Now we will generate a SSH key pair in our Shell with the following:

```python
ssh-keygen
```
And you will get the following as a response:

![](img6.png)
At this stage, you should click enter and leave this step to default and it will save it to ```/home/runner/.ssh/id_rsa.pub```  and it will then create a directory for you

![](img7.png)
Press enter to leave passphrase empty. 

 So both times you are asked for a passphrase you would just leave it empty twice and your screen should look like this:


![](img8.png)
Your public key will then be saved.



Next, we can run ```cat``` so we can view the public key that we created. 
```python
cat ~/.ssh/id_rsa.pub
```
After running this command your ssh key will be displayed as follows
![](img10.png)







So now that we have our ssh key we need to add it to our GitHub. In your GitHub profile under your project, you will go to your settings and look for the security section, look for the Deploy Key section and follow the numbering by adding the ssh key and giving it a name 


![](imgscreen.png)



Now we've added the ssh key to our GitHub and we can move on to changing the directory into the local clone of our repository and run it:
```python
git remote set-url origin git@github.com:username/https://github.com/ritza-co/git-demo
```
Next, we want to add the following commands to edit the file and commit the changes before we push it back onto GitHub
```python
git add README.md
git commit -m "Update README.md"
```
This will be the output of this command: 


![](img12.png)

Lastly, we will go ahead and add the command to push the file back onto GitHub with:
```python
git push
```

![](img13.png)

And there we have successfully pushed the file back onto GitHub with all our changes. 

![](img15.png)



You can also add `cp ~/.ssh/id_rsa* ~/` to your shell commands which will copy the key to your home directory. Then after it disappears, you can add `cp ~/id_rsa* ~/.ssh/` to your shell to copy the key back again. This copies the ssh key from the special `.ssh ` directory to your home directory, which is saved persistently and then back again when you need the key.

The passphrase mentioned in the tutorial is hidden for security purposes but if you type something there you’ll have to type the same thing every time you use the key.


