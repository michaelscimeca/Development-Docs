# Git Commands

### Handle Vim Message

```sh
Press a
Press esc
Press :x --> Note x must be Lowercase
Press Enter
```

Please enter a commit message to explain why this merge is necessary, especially if it merges an updated upstream into a topic branch.
```
Press i
Write your merge message
Press esc
Write :wq --> Not working add ! at the end
Then Press Enter
```

Actually it's not an error! It means you should enter some message to mark this merge. My OS is Ubuntu 14.04. If you use the same OS, you just need to do this as follows:

Type some message
```
'Ctrl + C + O'
Type the file name(such as "Merge_feature01") and Press Enter
'Ctrl + X' to exit
```
Now if you go to .git and you will find the file "Merge_feature01", that's the merge log actually.


### Git Version
```sh
git —version
```
### Start Git
```sh
git Init
```
### Add file to Git
Few things we need to do for good practice. Is add a `gitignore` file and a `readme.md` file. Another thing to note is to prevent tracking large files like `node_modules` & videos, so set up your `gitignore` file to prevent from tracking such large folders/files.

It's also recommend that we use git add filename at all times unless you are adding a folder containing images or something of that nature.
```sh
# Adding a file
git add filename

# Adding all files
git add -A
git add -all

# Add all of the same file type
git add *.txt or *.jpg etc

# Adding all files changes in a directory
git add .

# Choosing what changes to add (this will got through all your changes and you can 'Y' or 'N' the changes)
$ git add -p
```
### Git Commit
When you're about to commit your message, it's best to try to be as clear as possible. This way people can read the git logs better which in turn makes the code more maintainable.

For example, if you're doing QA Sifters. It's good practice to add in the Sifter Id.
```sh
git commit -m “ ”
```


### Git Commit All shortcut
Using `-a` means you want to get all.
```sh
git commit -a -m “ ”
```

### Shows You All Commits
Once you used git log. You can leave the log by pressing q
For more ways to view logs checkout this site. https://githowto.com/history
```sh
# Detailed log
git log
# Simple Log
git log --pretty=oneline
```

### Current Version Control
```sh
git status
```
### Show Git Repository Your Currently On
```sh
git remote -v
```
### Add a Git Repository
```sh
git remote add [alias] [https://name].git
```
### Remove Git
```sh
rm -r .git
```
### Show me list of Git Branches
```sh
git branch
```
### Move to the Previous Commit
```sh
git checkout HEAD~1
```
### Move to The Latest Commit
```sh
git checkout HEAD
```
### Start A Branch
```sh
git branch [ name ]
```
### Creates Branch
```sh
git checkout -b branchname
```
### Push commit to Branch (Allows Github to track commits)
```sh
git push -u origin [ branch name ]
```
### Checkout remote Branch
```sh
git fetch
git checkout [ branch name ]
```
### Push Branch to Remote Repository
```sh
git push [ remote repository ] [ branch name ]:master
```

### Return to Master Branch
```sh
git checkout master
```

### Merge Branch
```sh
git merge [ branch name ]
```

### Delete Branch
( Note: You can’t delete a branch that your in. )
```sh
git branch -D [ branch name ]
```
###  Should you ever need to update a remote's URL
```sh
git remote set-url origin [ git://name ].git
```
### Reset
On the commit-level, resetting is a way to move the tip of a branch to a different commit. This can be used to remove commits from the current branch. For example, the following command moves the hotfix branch backwards by two commits.

```sh
git checkout hotfix
git reset HEAD~2
```

### Remove Git Commits

Checkout
```sh
git checkout --orphan latest_branch
```
Add all the files
```sh
git add -A
Commit the changes
git push -f origin master
```
```sh
git commit -am "commit message"
git push -f origin master
```
Delete the branch
```sh
git branch -D master
git push -f origin master
```
Rename the current branch to master
```sh
git branch -m master
git push -f origin master
```
Finally, force update your repository
```sh
git push -f origin master
```

### Some Git Rules
There are a set of rules to keep in mind:
* Perform work in a feature branch.

    _Why:_
    >Because this way all work is done in isolation on a dedicated branch rather than the main branch. It allows you to submit multiple pull requests without confusion. You can iterate without polluting the master branch with potentially unstable, unfinished code.
* Branch out from `develop`

    _Why:_
    >This way, you can make sure that code in master will almost always build without problems, and can be mostly used directly for releases (this might be overkill for some projects).

* Never push into `develop` or `master` branch. Make a Pull Request.

    _Why:_
    > It notifies team members that they have completed a feature. It also enables easy peer-review of the code and dedicates forum for discussing the proposed feature.

* Update your local `develop` branch and do an interactive rebase before pushing your feature and making a Pull Request.

    _Why:_
    > Rebasing will merge in the requested branch (`master` or `develop`) and apply the commits that you have made locally to the top of the history without creating a merge commit (assuming there were no conflicts). Resulting in a nice and clean history.

* Resolve potential conflicts while rebasing and before making a Pull Request.
* Delete local and remote feature branches after merging.

    _Why:_
    > It will clutter up your list of branches with dead branches.It insures you only ever merge the branch back into (`master` or `develop`) once. Feature branches should only exist while the work is still in progress.

* Before making a Pull Request, make sure your feature branch builds successfully and passes all tests (including code style checks).

    _Why:_
    > You are about to add your code to a stable branch. If your feature-branch tests fail, there is a high chance that your destination branch build will fail too. Additionally, you need to apply code style check before making a Pull Request. It aids readability and reduces the chance of formatting fixes being mingled in with actual changes.

* Use `.gitignore` file.

    _Why:_
    > It already has a list of system files that should not be sent with your code into a remote repository. In addition, it excludes setting folders and files for most used editors, as well as most common dependency folders.

* Protect your `develop` and `master` branch.

    _Why:_
    > It protects your production-ready branches from receiving unexpected and irreversible changes. read more.


### Writing Good Commit Messages
- Having a good guideline for creating commits and sticking to it makes working with Git and collaborating with others a lot easier. Here are some rules of thumb ([source](https://chris.beams.io/posts/git-commit/#seven-rules)):

* Separate the subject from the body with a newline between the two.

  _Why:_
  > Git is smart enough to distinguish the first line of your commit message as your summary. In fact, if you try git shortlog, instead of git log, you will see a long list of commit messages, consisting of the id of the commit, and the summary only.

  * Limit the subject line to 50 characters and Wrap the body at 72 characters.

  _why_
  > Commits should be as fine-grained and focused as possible, it is not the place to be verbose. [read more...](https://medium.com/@preslavrachev/what-s-with-the-50-72-rule-8a906f61f09c)

  * Capitalize the subject line.
  * Do not end the subject line with a period.
  * Use [imperative mood](https://en.wikipedia.org/wiki/Imperative_mood) in the subject line.

  _Why:_
  > Rather than writing messages that say what a committer has done. It's better to consider these messages as the instructions for what is going to be done after the commit is applied on the repository. [read more...](https://news.ycombinator.com/item?id=2079612)


  * Use the body to explain **what** and **why** as opposed to **how**.
