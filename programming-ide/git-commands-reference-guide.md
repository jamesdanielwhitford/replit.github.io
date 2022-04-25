# Git commands reference guide

You can keep track of changes to your repls using Git. Here are some basic and advanced git commands you might find useful. Note that these are not intended as a replacement for the [git reference docs](https://git-scm.com/docs), but rather a simpler version of the most commonly used commands.

## Basic commands

**Clone a repository**

```
git clone https://github.com/ritza-co/git-demo.git
```

**Add a file that you've created or edited**

```
git add myfile.txt
```

**Add all files that you've created or changed or deleted**

```
git add .
```

**Create a new branch**

```
git switch -c my-cool-feature
```

**Commit your changes with a summary message**

```
git commit -m "fixed the things"
```

**Push your changes to your branch**

```
git push origin my-cool-feature
```

## Advanced commands

If things are going well, you'll probably only need the commands mentioned above. If things go wrong or you make a mistake, you'll probably need some more advanced commands.

### Check what is happening

**Check the status of new and changed files**

```
git status
```

**Check which branch you're currently on**

```
git branch
```

**See the most recent commits**

```
git log
```

**Merge your feature branch into main**

```
git checkout main
git merge my-cool-feature
```

**Rebase your feature branch from main**

```
git checkout my-cool-feature
git rebase main
```

**Copy a specific commit to a new branch**

```
git checkout my-cool-feature
git cherry-pick a5ece7a7893025541e9f819930f3615677a2c1e0
```

**Reset to a specific commit but keep your changes**

```
git reset --soft a5ece7a7893025541e9f819930f3615677a2c1e0
```

**Reset to a specific commit and throw away your changes [DANGER]**

```
git reset --hard a5ece7a7893025541e9f819930f3615677a2c1e0
```
