Full documentation: https://githowto.com/

- Install and setting [1.]

```bash
Windows
    https://git-scm.com/
Mac
    brew install git
Linux
    apt-get install git

Setting up name and e-mail address
    git config --global user.name "Your Name"
    git config --global user.email "Your_Email@whatever.com"

Setting up line endings
    Windows
        git config --global core.autocrlf false
        git config --global core.safecrlf false
    Mac
        git config --global core.autocrlf input
        git config --global core.safecrlf true
```

- Work flow [3.-9.]

```bash
Create a “Hello, World” page
    mkdir hello
    cd hello
    
    //create index.html
    
    //index.html
    Hello, World

Create a repository
    git init
    git status
    git add .
    git status
    git commit -m "initial commit"
    git log

First Change: Adding default page tags
    //index.html
    <html>
    <body>
        <h1>Hello, World!</h1>
    </body>
    </html>
    
    git add .

Second change: Add the HTML headers
    //index.html
    <html>
    <head>
    </head>
    <body>
        <h1>Hello, World!</h1>
    </body>
    </html>

    git status
    git commit -m "HTML > Hello, World!"
    git status
    git add .
    git status
    git commit -m "HTML > <header>"
```

- History [10.]

```bash
git log

One line history
    git log --pretty=oneline
    
Controlling the display of entries
    git log --pretty=oneline --max-count=2
    git log --pretty=oneline --author=<your name>
    git log --pretty=oneline --all
```

- Aliases [11.]

```bash
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.br branch
git config --global alias.hist "log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short"
```

- Getting older versions [12.]

```bash
Getting hashes for the previous versions
    git hist
    git checkout <hash> // initial commit

    //see index.html

Returning to the latest version in the master branch
    git checkout master

    //see index.html
```

- Tagging versions [13.]

```bash
Creating a tag of the first
    git tag v1

Tags for previous versions
    git checkout v1

    //index.html
    <html>
    <body>
        <h1>Hello, World!</h1>
    </body>
    </html>

    git tag v1-beta
    
Check out by the tag name
    git checkout v1
    git checkout v1-beta
    
Viewing tags with the tag command
    git tag
    git hist --all // viewing tags in logs
```

- Discarding local changes (before adding) [14.]

```bash
git checkout master

Change index.html
    //index.html
    <html>
    <head>
    </head>
    <body>
        <h1>Hello, World!</h1>
        <!-- This is a bad comment.  We want to revert it. -->
    </body>
    </html>

    git status
    
Undoing the changes in the working directory
    git checkout index.html
    git status

    //see index.html
```

- Cancel staged changes (after adding) [15.]

```bash
Edit file and stage changes
    //index.html
    <html>
    <head>
        <!-- This is an unwanted but staged comment -->
    </head>
    <body>
        <h1>Hello, World!</h1>
    </body>
    </html>

    git add .
    git status    

Reset the buffer zone
    git reset HEAD index.html
    git status

Switch to commit version
    git checkout index.html
    git status
```

- Cancelling commits [16.]

```bash
Edit the file and make a commit
    //index.html
    <html>
    <head>
    </head>
    <body>
        <h1>Hello, World!</h1>
        <!-- This is an unwanted but committed change -->
    </body>
    </html>

    git add .
    git commit -m "oops, we didn't want this commit"
    
Make a commit with new changes that discard previous changes
    git revert HEAD --no-edit
    git hist
```

- Removing a commit from a branch [17.]

```bash
Mark this branch first
    git hist
    
Reset commit to previous Oops
    git tag oops
    git reset --hard v1
    git hist
    git hist --all
```

- Removing the oops tag [18.]

```bash
git tag -d oops
git hist --all
```

- Changing commits [19.]

```bash
//index.html
Change the page and commit
    <!-- Author: hope horizon -->
    <html>
    <head>
    </head>
    <body>
        <h1>Hello, World!</h1>
    </body>
    </html>

    git add .
    git commit -m "add an author comment"
    
Oops... email required
    //index.html
    <!-- Author: Alexander Shvets (hope@horizon.com) -->
    <html>
    <head>
    </head>
    <body>
        <h1>Hello, World!</h1>
    </body>
    </html>

    git add .
    git commit --amend -m "add an author/email comment"
    git hist
```

- Creating a Branch [24.-25.]

```bash
Create a branch
    git branch style
    git checkout
    git status

    //create style.css

    //style.css
    h1 {
    color: red;
    }

    git add .
    git commit -m "add style.css"
    
Change the main page
    //index.html
    <!-- Author: hope horizon (hope@horizon.com) -->
    <html>
    <head>
        <link type="text/css" rel="stylesheet" media="all" href="style.css" />
    </head>
    <body>
        <h1>Hello, World!</h1>
    </body>
    </html>

    git add .
    git commit -m "index.html uses style.css"

Change index.html
    //index.html
    <html>
    <head>
        <link type="text/css" rel="stylesheet" media="all" href="style.css" />
    </head>
    <body>
        <iframe src="lib/hello.html" width="200" height="200" />
    </body>
    </html>

    git add .
    git commit -m "updated index.html"
    
Switching to the Master branch
    git hist --all
    git checkout master

    //see index.html
    
Let us return to the style branch.
    git checkout style

    //see index.html
```

- Changes to master branch [26.-27.]

```bash
git checkout master

//create README.md

git add .
git commit -m "create README.md"
git hist --all
```

- Merging to a single branch [28.]

```bash
git checkout style
git merge master
git hist --all
```

- Creating a conflict [29.]

```bash
git checkout master

//index.html
<!-- Author: hope horizon (hope@horizon.com) -->
<html>
<head>
    <!-- no style -->
</head>
<body>
    <h1>Hello, World! Life is great!</h1>
</body>
</html>

git add .
git commit -m "life is great!"
git hist --all
```

- Resolving Conflicts [30.]

```bash
Merge the master branch with style
    git checkout style
    git merge master

Resolution of the conflict
    //index.html
    <!-- Author: hope horizon (hope@horizon.com) -->
    <html>
    <head>
        <link type="text/css" rel="stylesheet" media="all" href="style.css" />
    </head>
    <body>
        <h1>Hello, World! Life is great!</h1>
    </body>
    </html>
    
    git add .
    git commit -m "Merged master fixed conflict."
```

- Resetting the style branch [32.]

```bash
git checkout style
git hist
git reset --hard <hash> // commit -m "updated index.html"
git hist --all
```

- Reset of the Master branch [33.]

```bash
git checkout master
git hist
git reset --hard <hash> // commit -m "create README.md"
git hist --all
```

- Rebase [34.]

```bash
git checkout style
git rebase master
git hist
```

- Merging style into master [35.]

```bash
git checkout master
git merge style
git hist
```

- Multiple repositories [36.-45.]

```bash
cd..

Create a clone of the hello repository
    git clone hello cloned_hello
    cd cloned_hello
    git hist --all

Remote branches
    git remote
    git remote show origin
    git branch
    git branch -a
    
Make a change in the original hello repository
    cd ../hello
    
    //README.md
    This is the Hello World example from the git tutorial.
    (changed in original)
    
    git add .
    git commit -m "Changed README in original repo"
    
Fetching changes
    cd ../cloned_hello
    git fetch
    git hist --all
    
    //see README.md
    
Merging pulled changes
    git merge origin/master
    
    //see README.md
    
Pulling and merging changes
    We are not going to run through the entire process of making and pulling a new change, but we want you to know that
        git pull
    is actually equivalent to the following two steps
        git fetch
        git merge origin/master

Adding a tracking branch
    git branch --track style origin/style
    git branch -a
    git hist --max-count=2
```



















