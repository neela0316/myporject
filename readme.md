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
It records a snapshot of your files at certain time, with a message describing what chaged.
<br>
You can always go back to pervious commit if you need to.
<br>
Here are some key commands for commits:

- `git commit -m "message"` - Commit staged changes with a message
- `git commit -a -m "message"` - commit all tracked chages (skip staging)
- `git log` - See commit history

```
git commit -m "First release of Hello World!"
git commit -a -m "Quick update to README"
git commit -a -m "Try to commit new file"
```

### view Coit History (`git log`)

```
git log
git log --online
git log --stat
```

## Git Tagging

- `git tag <tagname>` - Create a lightweight tag
- `git tag -a <tagname> -m "message"` - Create an annotated tag
- `git tag -a <tagname> <commit-hash)>` - Tag a specific commit
- `git tag` - List tags
- `git show <tagname>` - Show tag details
- A **tag** in git like lable or bookmark for a specific commit.
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

```
git stash
git stash -u
git stash --include-untracked
git stash push -m "WIP: homepage redesign"
git stash list
git stash show
```
