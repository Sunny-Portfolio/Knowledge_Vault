### <u>Create a new repo</u>

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

set local default git :branch to main
```sh
git config --global init.defaultBranch main
```

Clone a dir already created on github, if you didn't git init the project folder
```sh
git clone git@github.com:Sunny-Portfolio/notes.git
```

Add all files in current dir to be commited
```sh
git add .
```

```sh
git commit -m "Type your msg here"
```

Default for git push origin main
```sh
git push
```

```sh
git --version
```

Display the URL of the repo
```sh
git remote -v
```

```sh
git status
git log
```

