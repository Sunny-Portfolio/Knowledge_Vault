### Create a new repo
---
Create a new repo on github, get the repo link
```sh
git init	// create initial setup of new repo
git add -A
git commit -m 'Added my project'
git remote add origin git@github.com:sammy/my-new-project.git
```

`push -u (--set-upstream)` flag sets the remote origin as upstream reference
`push -f (--force)` flag force overwrite everything in the remote dir
if didn't create README file when creating repo, then not needed
in other words, it replace any file inside the repo. 
```sh
git push -u -f origin main
```
---
### <u>The Basics</u>

// set local default git :branch to main
git config --global init.defaultBranch main

// Clone a dir already created on github, if you didn't git init the project folder
git clone git@github.com:Sunny-Portfolio/notes.git

// Add all files in current dir to be commited
git add .

git commit -m "Type your msg here"

// default for git push origin main
git push

git --version

// display the URL of the repo
git remote -v

git status
git log

