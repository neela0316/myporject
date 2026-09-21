# Git

## What is git?

#### Git is popular version control system.

#### It was created by Linus Torvalds in 2005, and has been maintained by Junio Hamano since then.

#### It is used for

- Tracking code
- tracking who made changes
- Coding collaboration

## Key Git Concepts

- **Repository:** A folder where Git tracks your project and its history.
- **Clone:** Make a copy of a remote repository on your computer.
- **Stage:** Tell Git which changes you want to save next. Commit: Save a snapshot of your staged changes.
- **Branch:** Work on different versions or features at the same time.
- **Merge:** Combine changes from different branches.
- **Pull:** Get the latest changes from a remote repository. Push: Send your changes to a remote repository.

## Working with Git

- Initialize Git on a folder, making it a Repository
- Git now creates a hidden folder to keep track of changes in that folder
- When a file is changed, added or deleted, it is considered modified
- You select the modified files you want to **Stage**
- The **Staged** files are **Committed**, which prompts Git to store a **permanent** snapshot of the files
- Git allows you to see the full history of every commit.
- You can revert back to any previous commit.
  -Git does not store a separate copy of every file in every commit, but keeps track of changes made in each commit!

```
sudo apt install git
git --version
git config --global core.editor "code --wait"
git config --global core.editor "notepad"
ls
pwd
git config --global user.name "Your Name"
git config --global user.email "you@example.com"


```

Use `--global` to set the value for every repository on your computer.

Use `--local` (the default) to set it only for the current repository.

### List All Settings and View a Specific Setting

```
git config --list
git config user.name
```

### Unset an Alias

```
git config --global -unset code.editor
```

### Set Default Branch Name

```
git config --global init.defaultBranch main
```

### Configuration Levels

- **System** (all users): `git config --system`
- **Global** (Current User)
  : `git config --global`
- **Local** (Current repo): `git config --local`

```
git config user.name "Project Name"
git config --global user.name "Global Name"
git config --system user.name "System Name"
```

### Initialize Git

```
git init
```

```
ls
ls -a
pwd
git status
touch index.html
ls

```

## Git Staging Environment

- `git add <file>` - Stage a file
- `git add -all` or `git add -A` - Stage all changes
- `git status` - See what is staged
- `git restore --staged <file>` - Unstage a file

```
git status
git add index.html
git status
```

### Troubleshooting

- **Staged the wrong file?** Use `git restore --staged <file>` to unstage it.
- **Forgot to stage a file?** Just run `git  add <file>` again before you commit.
- **Not sure what's staged?** Run `git status` to see what will be committed.

## Git Commit

A **Commit** is like a save point in your project.
<br>
It records a snapshot of your files at certain time, with a message describing what changed.
<br>
You can always go back to pervious commit if you need to.
<br>
Here are some key commands for commits:

- `git commit -m "message"` - Commit staged changes with a message
  - `git commit -m "first release of Hello World!"`
- `git commit -a -m "message"` - commit all tracked changes (skip staging)
- `git log` - See commit history

<br>

**Warning:** Skipping the staging step can make you include unwanted changes. Use with care.
<br>

**Note:** `git commit -a` does <u>not</u> work for new/untracked files. You must use `git add <file>`first for new files

- If you ust type `git commit` (no `-m`), your default editor will open so you can write a detailed, multi-line message:
- **Create an empty commit:** `git commit --allow-empty -m "Start project"`
- **Use previous commit message (no editor):** `git commit --no-edit`
- **Quickly add staged changes to last commit, keep message:** `git commit --amend --no-edit`

#### Troubleshooting common commit Mistakes

- **Forgot to stage a file?**
  <br>
  If you run `git commit -m "message"` but forgot to `git add` a file, just add it and commit again. Or use `git commit --amend` to add it to our last commit.
- **Typo in your commit message?**
  <br>
  Use `git commit --amend -m "Corrected message"` to fix the last commit message.
- **Accidentally committed the wrong files?**
  <br>
  You can use `git reset --soft HEAD-1` to undo the last commit and keep your changes staged.

```
git commit -m "First release of Hello World!"
git commit -a -m "Quick update to README"
git commit -a -m "Try to commit new file"
```

### view commit History (`git log`)

```
git log
git log --online
git log --stat
```

## Git Tagging

- `git tag <tag-name>` - Create a lightweight tag
- `git tag -a <tag-name> -m "message"` - Create an annotated tag
- `git tag -a <tag-name> <commit-hash)>` - Tag a specific commit
- `git tag` - List tags
- `git show <tag-name>` - Show tag details
- A **tag** in git like label or bookmark for a specific commit.
- Tags are most often used to mark important points in your project history, like releases (`v1.0` or `v2.0`).
- Tags are a simple and reliable way to keep track of versions and share them with your team or users.

Some common tag types include:

- **Releases:** Tags let you mark when your project is ready for release, so you (and others) can always find that exact version later.
- **Milestones:** Use tags to highlight major milestones, like when a big feature is finished or a bug is fixed.
- **Deployment:** Many deployment tools use tags to know which version of your code to deploy.
- **Hot fixes:** If you need to fix an old version, tags make it easy to check out and patch the right code.

### Annotated Vs Lightweight Tags

- **Annotated Tag:** Store author, date, and message. Recommended for releases and sharing with others.
- **Lightweight Tag:** Just a siple name for a commit (no extra info, like a bookmark).

```
echo `Lightweight Tag`
git tag v1.0

echo `Annotated Tag`
git tag -a v10 -m "Version 1.0 release"
git log
9ce84bdfef415cf3b9b354a9dd8debd899409d (HEAD -> master)
git tag v1.1 9ce84bdfef415cf3b9b354a9dd8debd899409d
git tag
```

## Git Stash

- `git stash` - Stash your changes
- `git stash push -m "message"` - Stash with a message
- `git stash list` - List all stashes
- `git stash branch <branchname>` - Create a branch from a stash

common use cases:

- **Switch braanches safely**: Save your work before changing branches.
- **Handle emergencies**: Stash your work to fix something urgent, then restore it.
- **Keep your work-in-progress safe**: Avoid messy commits or losing changes.

`git stash`
<br>
`git stash -u`
<br>
`git stash --include-untracked`
<br>
`git stash push -m "WIP: homepage redesign"`
<br>
`git stash list`
<br>
`git stash show`
<br>

### What is stash stack?

<br><br>
Each time you run `git stash`. your changes are saved on top of a "stack".
<br><br>
The most recent stash is on top, and you can apply or drop stashes from the top down, or pick a specific one from the list.

### Stash with a Message (`git stash push -m`)

Add a message to remember what you stashed:
`git stash push -m "WIP: homepage redesign"`

### List stashes (`git stash list`)

See all your saved stashes:
<br>
`git stash list`

### Show stash Details (`git stash show`)

See what was changed in the latest stash:
<br>
`git stash sow`
<br>

#### Show Full Diff

` git stash show -p`

#### Apply the Latest Stash (`git stash apply`)

Restore your most recent stashed changes (keeps the stash in the stack):

#### Apply a Specific Stash (`git stash apply stash@{n}`)

Restore a specific stash from the list:

`git stash apply stash@{1}`

#### Pop the Stash (`git stash pop)`

Apply the latest **and remove it from the stack**:

#### Drop a Stash (`git stash drop`)

Delete a specific stash when you no longer need it:
<br>

`git stash drop stash@{0}`

#### Clear All Stashes (`git stash clear`)

Delete all your stashes at once:
<br>

`git stash clear`

#### Branch from a Stash (`git stash branch`)

Create a new branch and apply a stash to it.
<br>
Useful if your stashed work should become its own feature branch:
<br>

`git stash branch new-feature stash@{0}`

#### Troubleshooting

- **Did you lose your changes?** Try `git stash list` and `git stash apply` to recover stashed work.
- **Stash didn't apply cleanly?** You may need to resolve conflicts, just like a merge.
- Git will mark the conflicts in your files for you to resolve.
- **Untracked files missing?** By default, untracked files are not stashed. If you need to stash them, use `git stash -u` next time.
- **Accidentally cleared all stashes?** Unfortunately, git stash clear is permanent. Always double-check before running it!

## Git History

Git keeps a detailed record of every change made to your project.
<br>
You can use history commands to see what changed, when, and who made the change.
<br>
This is useful for tracking progress, finding bugs, and understanding your project's evolution.

### Key Commands for Viewing History

- `git log` - Show full commit history
- `git log --online` - show a summary of commits
- `git show <commit>` - Show details of specific commit
- `git diff` - See unstaged changes
- `git diff --staged` - See staged changes
- `git diff <commit1> <commit2>` - Compare Tow Commits
- `git log --author="neela0316"` - Show Commits by Author
- `git log --since="2 weeks ago"` - Show Recent Commits
- `git log --stat` - Show files changes per commit
- `git log --graph` - Show a branch graph

### Troubleshooting

- **Can't see your changes?** Make sure you have committed your work. Uncommitted changes won't appear in the history.
- **Log is too long?** Use `git log --oneline` or `git log --since` to make it easier to read.
- **How do I quit the log view?** Press q to exit the log or diff view.

## Why and When to Use Git Help?

<br>
Git has many commands and options.
<br>
If you forget how a command works or want to learn about its options, you can use Git's built-in help.
<br>
This is the fastest way to get answers without leaving your terminal.

- `git help <command>` - See the manual page for a command
- `git <command> --help` - See help for a command (same as above)
- `git <command> -h` - See a quick summary of options
- `git help --all` - List all possible Git commands
- `git help -g` - List guides and concepts

## Git Branch

In Git, a `branch` is like a separate workspace where you can make changes and try new ideas without effecting the main project. Think of it as a "parallel universe" for your code.

- Developing a new feature
- Fixing a bug
- Experimenting with ideas
- `git branch hello-world-images` - Creating a New Branch
- `git branch` - Listing all branches
- `git checkout hello-world-images` - Switching Between Branches

- **Rename a branch:** `git branch -m old-name new-name`
- **List all branches:** `git branch`
- **Switch branches:** `git checkout branch-name` or `git switch branch-name`
- **Delete a branch (not merged):** `git branch -D branch-name`
- **See which branch you're on:** `git status`

## Git Branch Merge

Merging in Git means combining the changes from one branch into another.
<br>
This is how you bring your work together after working separately on different features or bug fixes.

#### Common `git merge` Options

- `git merge` - Merge a branch into your current branch
- `git merge --no-ff` - Always create a merge commit
- `git -squash` - Combine changes into a single commit
- `git merge --abort` - Abort a merge in progress

#### Practical Examples

- **Abort a merge:** `git merge --abort`
- **Check status during a merge:** `git status`
- **Resolve a conflict and complete the merge:** Edit the conflicted file(s), then `git add file` and `git commit`
- **Fast-forward merge:** Happens when no new commits diverged-Git just moves the branch pointer forward.
- **No-fast-forward merge:** Use `git merge --no-ff branch` to always create a merge commit, preserving branch history.
- If you want to combine all the changes from a branch into a single commit (instead of keeping every commit), use `git merge --squash branch-name`. This is useful for cleaning up commit history before merging.
