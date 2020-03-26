# git_workshop
Small repo to test/practice git workflow

### Set up a user

`git config --global user.name "Your Name"`
`git config --global user.email "your@email.email"`
`git config --list` - to see if values have been set up 

### Useful git commands

- `git help <command>` || `git <command> --help` - show documentation for command

- `git init` - initialise an empty git repo
- `git clone <url>` - clone repository to folder
- `git status` - displays the state of the working directory and the staging area. It lets you see which changes have been staged, which haven’t, and which files aren’t being tracked by Git.
- `git checkout -b <branch name>` - creates a new branch from your current one and checks it out
- `git add <filepath>` - stage file, with `-A` or `.` stage all changed files, with `-p` can decide on each change to include it or not
- `git push -u origin <branch name>` - push branch and track remote branch
- `git push origin HEAD` - pushes all your current commits to the corresponding remote branch

Extra commands: 
- `git log --pretty=oneline` - show a list of your previous commits
- `git log --oneline --decorate --all --graph` - shows all commits and branches in a pretty graphical way
- `git remote -v` - shows information of the remote repo
- `git branch -a` - list all branches (local and remote)
- `git clean -df` - deletes all untracked files

### Set VSCode as default git editor

- Make sure you can run code --help from the command line and you get help. if you do not see help, please follow these steps:
  - **macOS**: Open the Command Palette (F1) and type 'shell command' to find the Shell Command: Install 'code' command in PATH command.
  - **Windows**: Make sure you selected Add to PATH during the installation.
- From the command line, run git config --global core.editor "code --wait"
- Now you can run git config --global -e and use VS Code as editor for configuring Git.

### Interactive rebasing

It rebases the branch against a previous commit and gives you options to alter the outcome.

`git rebase -i HEAD~<number of commits you'd like to include>`
`git rebase -i <last commit's hash before the commit you would like to include>`

The command list on the interactive rebase file:

```
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

**Fixup** is used commonly to unite commits to ease the pain of rebasing against other branches or to not have that many commits in the PR.
With **drop** you can remove unnecessary commits if there's any.
**Reword** can edit the commit message if it's not descriptive enough.

### Rebasing against master

1. `git checkout master` and `git pull`
2. `git checkout <your branch name>`
3. `git rebase master`
4. Fix conflicts (always save the files)
5. `git add .`
6. `git rebase --continue`
7. If there's no changes introduced in the next commit, then `git rebase --skip`
8. Do steps 4-7, until your branch is cleaned and the rebase is done (you'll see that your branch name is visible in the terminal again)
9. Run the application and check if everything works as expected and there are no styling issues
10. Force push your branch `git push -f`

### Picking commits from other branches

You can use `git cherry-pick <commitSha>` to integrate a commit from an other branch into yours.
Only use it when you really need it. When you're merging your branch into master, this can create duplicate commits.

