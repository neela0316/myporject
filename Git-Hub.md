# Git GitHub

1. Sign up for GitHub
2. Create a Repository
3. What is a remote Repository?

## Git Security SSH

- **SSH** (Secure Shell) is a way to connect securely to remote computers and services, like Git repositories.
- `sudo apt install ssh` - Install in Ubuntu OS
- **SSH key Pair** - A public and private key for secure access
- `ssh-keygen` - generate a new SSH key pair
- `ssh-add` - Add your private key to the SSH agent
- `ssh -T git@github.com` - Test SSH connection
- `ssh-add -l` - List loaded SSH keys
- `ssh-add -d` - Remove a key from agent

## How SSH Keys Work

- **SSH** keys come in pairs: a public key (like a lock) and a private key (like your own key).
- You share the public key with the server (like GitHub or Bitbucket), but keep the private key safe on your computer.
- Only someone with the private key can access what's locked by the public key.
- `eval $(ssh-agent -s)` - Enable SSH Agent
- `ssh-keygen -t rsa -b 4096 -C "mlsankar@saimail.com` - Generate SSH Key
- `ssh-add ~/.ssh/id_rsa` - Adding Your Key to the SSH Agent
- Copying Your Public Key
  - on macOS: `pbcopy < ~/.ssh/id_rsa.pub`
  - On Windows (Git Bah): `clip < ~/.ssh/id_rsa.pub`
  - on Linux: `cat ~/.ssh/id_rsa.pub` (then copy manually)
- `ssh-add -l` - List Loaded SSH Keys
- `ssh-add -d ~/.ssh/id_rsa` - Remove SSH Key from Agent

### Troubleshooting SSH

- If you get "Permission denied", make sure your public key is added to your Git host and your private key is loaded in the agent.
- Check file permissions: private keys should be readable only by you (`chmod 600 ~/.ssh/id_rsa`).
- Use `ssh -v` for verbose output to debug problems.
- Make sure you're using the correct SSH URL for your remote (starts with `git@`).

## Git GitHub Add SSH

### Add SSH to GitHub

- Now that you have generated your SSH key, you need to add your **public Key** to your GitHub account.

### Add the key to GitHub

Avatar Icon -> Settings -> SSH and GPG Keys -> New SSH Key -> Add SSH Key

### Pull from Remote

- Fetch
- Merge
- Pull
- `pull` is combination of 2 different commands:
  - `fetch`
  - `merge`

## Git Push to GitHub

Key Push Commands

- Basic Push -`git push origin`
- Force Push - `git push --force origin feature-branch` or `git push --force-with-lease origin feature-branch`
- Push Tags
  - All Tags - `git push --tags`
  - Specific Tag - `git push origin v1.0`
- Troubleshooting
  - **Non-fast-forward error**: Happens if someone else pushed to the branch. Run `git pull --rebase` before pushing again.
  - **Authentication failed**: Make sure you have access to the repository and your credentials are correct.

## Git Pull Brach from gitHub

### Pulling a Branch from GitHub

- Now continue working on our new `branch` in our local Git.
- Lets `pull` from our GitHub repository again so that our code is up-to-date:
- Now our main `branch` is up to date. And we can see that there is a new `brach` available on GitHub.
- Do a quick `status` check:

## Git Push Branch to GitHub

### Push Branch to GitHub

- `gti checkout -b update-readme`
- `git push origin update-readme`

### Push and Set Upstream

- `git push --set-upstream origin update-readme`
- `git push --force origin update-readme` (Force Push)
- `git push origin --delete update-readme` (Delete Remote Branch)
- `git push --all origin` (Push All Branches)
- `git push --tags` (Push Tags)

### Troubleshooting

- **Rejected push (non-fast-forward):** Someone else pushed changes before you. Run `git pull --rebase` first, then try again.
- **Authentication failed:** Make sure you are logged in and have permission to push to the repository.
- **Remote branch not found:** Double-check the branch name and spelling.

## Git GitHub Flow

### GitHub Flow works, step by step:

- **Create a Branch**: Start new work without affecting the main code.
- **Make Commits**: Save progress as you make changes.
- **Open a Pull Request**: Ask other to review your work.
- **Review**: Discuss and improve the changes together.
- **Deploy**: Test your changes before merging.
- **Merge**: Add your finished work to the main branch.

### Summary of Git Revert Commands and Options

- `git revert HEAD` - Revert the latest commit
- `git revert <commit>` - Revert a specific commit
- `git revert HEAD~2` - Revert commit future back in history
- `git revert --no-edit` -
  Skip commit message editor
- `git log --online` - Show commit history

### Tips & Troubleshooting

- Use `git revert` instead of `git reset` when you want to undo a previous commit, but still keep the commit history intact.
- Use `git log --oneline` to find the commit you want to undo.
- Use `git revert HEAD --no-edit` to create a new commit that reverses the changes.
- If you get an error message saying "error: could not revert...", try using `git revert --abort` to abort the revert process.
- If you get an error message saying "error: could not apply...", try using `git revert --continue` to continue the revert process.

## Git Reset

The `git reset` command moves your current branch (HEAD) to a different commit.
<br>
Use it to undo commits, unstage files, or clean up your history.

### Reset Commands and Options

- `git reset --soft <commit>` - Move HEAD to commit, keep changes staged
- `git reset --mixed <commit>` - Move HEAD to commit, unstage changes (default)
- `git reset --hard <commit>` - Move HEAD to commit, discard all changes
  `git reset <file>` - Unstage a file
- `git log --oneline` - Show commit history

#### Git Reset `--soft`

`git reset --soft <commit>` moves HEAD to the specified commit, but keeps all your changes staged (in the index).

#### Git Reset `--mixed` (default)

- `git reset --mixed <commit>` (or just `git reset <commit>`) moves HEAD to the specified commit and unstage any changes, but keeps them in your working directory.

## Git Amend

- Git Amend is a command that allows you to modify the most recent commit.
- You cna use it to fix typos, add or remove files, or change the commit message.

### Fix Last Commit Message

1. Open your terminal and navigate to your repository.
2. Type `git commit --amend -m "New message"` to change the commit message.
3. Press Enter to save the changes.

### Add Files to Last Commit

1. Open your terminal and navigate to your repository.
2. Type `git add <file>` to add the file to the staging area.
3. Type `git commit --amend` to add the file to the last commit.
4. Press Enter to save the changes.

### Remove Files from Last Commit

1. Open your terminal and navigate to your repository.
2. Type `git reset HEAD^ -- <file>` to remove the file from the staging area.
3. Type `git commit --amend` to remove the file from the last commit.
4. Press Enter to save the changes.

## Git Rebase

- **Rebasing** moves or combines a sequence of commits to a new base commit.
  - Keep a clean, linear project history
  - Avoid unnecessary merge commits
  - Combine multiple commits into one
    Edit or reorder commits

### Basic Rebase

`git checkout feature- branch` <br>
`git rebase main`

### Interactive Rebase

`git rebase -i <base>` let you edit, reorder, squash or fix up commits before a certain point.
`git rebase -i HEAD~3`

### Continue, Abort, or Skip

If you hit a conflict or need to finish editing a commit, use `git rebase --continue` after resolving the issue.
`git add fixed_file.txt` <br>
`git rebase --continue`
<br>
If something goes wrong or you want to stop the rebase, use `git rebase --abort`.
<br>

If you can't fix a commit during a rebase (for example, if a conflict can't be resolved), you can skip it with `git rebase --skip`.

### Tips & Troubleshooting

- Use `git rebase -i` to edit, reorder, squash, or fix up commits before a certain point.
- Use `git rebase --continue` to continue a rebase after resolving conflicts.
- Use `git rebase --abort` to cancel a rebase in progress.
- If you encounter conflicts during a rebase, resolve them and then use `git rebase --continue` to continue the rebase process.
- If you can't fix a commit during a rebase, use `git rebase --skip` to skip it.

### What is Git Reflog?

- `git reflog` records updates to the tip of branches and HEAD.

- It lets you see where your branch and HEAD have been, even changes you made by mistake.

- This is useful for recovering lost commits or undoing a reset.

- Use `git reflog` when you need to:

- Recover lost commits or changes
- Undo a reset or a merge
  See the history of your branch and HEAD

### Tips & Best Practices

- Use `git reflog` regularly to keep track of your changes
- Use `git reflog` to recover lost commits or changes
- Use `git reflog` expire to clean up old entries

### Troubleshooting

If you encounter issues with git reflog, try:

- Checking the Git documentation for more information
- Searching online for solutions to specific issues
- Seeking help from a Git expert or community

## Git Recovery

### Recover Lost Commits with `git reflog`

### Restore a Deleted Branch `git checkout -b branch-name <commit-hash>`

### Recover a Deleted or Changed File `git restore filename.txt`

### Recover from a Hard Reset `git reset --hard`

### Tips & Best Practices

- Regularly commit your changes to avoid losing work
- Use `git reflog` to find lost commits
- Use `git restore` to recover deleted or changed files

## Git Ignore and `.gitignore`

- The `.gitignore` file tells Git which files and folders to ignore (not track).
- The `.gitignore` file itself is tracked by Git, so everyone using the repository ignores the same files.

### Wildcards & Patterns

- `*` matches any number of characters
- `?` matches a single character
- `[abc]` matches any character in the set
- `[!abc]` matches any character not in the set

### Negation (!)

- Use `!` to not ignore something that would otherwise be ignored. This is called an exception:

```
*.log
!important.log
```

This ignores all `.log` files except `important.log`.

### Comments and Blank Lines

Lines starting with `#` are comments and are ignored by Git. Blank lines are also ignored. Use comments to explain your rules:

```
# Ignore log files
*.log

# Ignore temp folders
temp/
```

### Local & Personal Ignore Rules

If you want to ignore files only for yourself (not for everyone who uses the repository), add them to `.git/info/exclude`. This works just like `.gitignore` but is not shared.

`git config --global core.excludesfile ~/.gitignore_global`

### How to Stop Tracking a File

If you add a file to `.gitignore` but Git is still tracking it, you need to tell Git to stop:
`git rm --cached filename.txt`

### Tips & Troubleshooting

- Check for typos-`.gitignore` is case-sensitive!
- If a file is already tracked, use `git rm --cached` to stop tracking it.
- Use comments (`#`) to explain tricky rules for your teammates.
- Use `git status` to see if your ignored files are being tracked.
- **Remember**: `.gitignore` only affects files that are not already tracked by Git.

## Git `.gitattributes`

The `.gitattributes` file is a special file that tells Git how to handle specific files in your repository.

- Force Unix Line Endings for All Text Files - `*.txt text eol=lf`
- Set LF for Shell Scripts - `*.sh text eol=lf`
- Mark PNG Files as Binary - `*.png binary`

- Track PSD Files with LFS - `*.psd filter=lfs diff=lfs merge=lfs -text`
- Custom Diff for Markdown - `*.md diff=markdown`
- Check Attributes of a File - `git check-attr --all README.md`
- Ignore Files on Export `docs/* export-ignore`

### Tips & Best Practices

- Patterns work like `.gitignore` (wildcards, etc).
- Put `.gitattributes` in subfolders for rules that only apply there.
- Changing `.gitattributes` won't retroactively fix files already committed-re-add files to update them.
- Use `git check-attr` to debug attribute issues.

## Git LFS

**Git LFS (Large File Storage)** is an extension for Git that helps you manage large files (like videos, images, or datasets) efficiently.

- Install Git LFS - `git lfs install`
- Track `.psd` Files - `git lfs track "*.psd"`

```
git lfs track "*.zip"
git lfs track "data/*.csv"
git lfs track "images/*.{png,jpg}"
```

- `.gitattributes` Entry - `*.psd filter=lfs diff=lfs merge=lfs -text`

### Add, Commit, and Push LFS Files

- **Add** files as usual: `git add largefile.psd`
- **Commit:** `git commit -m "Add large file"`
- **Push:** `git push origin main`

### Check LFS Status

- List LFS Files `git lfs ls-files`

- Untrack/Remove Files from LFS
  <br>
  `git lfs untrack "*.psd"`
  <br>
  `git add .gitattributes`

  ## Git CI/CD

  **CI/CD** stands for **Continuous Integration** and ** Continuous Deployment/Delivery**.
  <br>
  It means your code is automatically test and deployed every time you push.
  <br>
  This helps you catch bugs early and deliver features faster, with less manual work.

  ### Use of CI/CD

  CI/CD automates the process of testing and deploying your code. This means:
  - Find bugs before they reach users
  - Deploy changes faster and more safely
  - Reduce manual steps and mistakes
  - Get quick feedback on every push

### Popular CI/CD Services

- GitHub Actions: Built into GitHub, uses YAML files in `.github/workflows/`
- **GitLab CI/CD:** Built into GitLab, uses `.gitlab-ci.yml`
- **CircleCI:** Works with GitHub/GitLab, easy setup for many languages
- **Travis CI:** Popular for open-source, uses `.travis.yml`
- **Azure Pipelines:** Works with Azure DevOps and GitHub, supports many platforms

### Key CI/CD Concepts

Here are some important terms:

- **Workflow:** A series of jobs that run together
- **Job:** A group of steps that run together
- **Step:** A single task, like checking out code or running tests
- **Runner:** The computer/server that runs your jobs
- **Trigger:** Decides when your workflow runs
- **Environment Variables:** Settings for your workflow
- **Secrets:** Passwords or API keys

## Git Hooks

**Git hooks** are scripts that run automatically when certain Git events happen, like making a commit or pushing code.

### List Available Hooks

`ls .git/hooks`

### Enable a Hook

`mv .git/hook/pre-commit.sample .git/hooks/pre-commit`

`chmod +x .git/hooks/pre-commit`

### Types of Hooks

There are many types of hooks, but the most common are:

- `pre-commit`
- `commit-msg`
- `pre-push`
- `pre-receive`
- `post-receive`

## Git Submodules

**Git submodules** let you include one Git repository inside another as a subdirectory.

### Add a Submodule

`git submodule add https://github.com/example/library.git libs/library`

### Clone a Repo with Submodules

`git submodule init` <br>
`git submodule update`

### Clone with Submodules

`git clone --recurse-submodules https://github.com/user/repo.git`

### Submodule Status

`git submodule status`

### Run commands in All Submodules

`git submodule foreach git status`

### Update submodules

`git submodule update --remote`

### Remove a Submodule

- To remove a submodule:
  - Delete the relevant section from `.gitmodules`
  - Remove the submodule directory from your working tree
  - Run `git rm --cached path/to/submodule`

## Git Advanced Remote

**Remotes** are references to remote repositories.

They let you collaborate, fetch, and push code to shared projects on services like GitHub, GitLab, or Bitbucket.

### Add a Remote

`git remote add upstream https://github.com/other/repo.git`

### Remove a Remote

`git remote remove upstream`

### Rename a Remote

`git remote rename origin main-origin`

### List Remotes

`git remote -v`

### Show Remote Details

`git remote show upstream`

### Fetch from a Remote

`git fetch upstream`

### Push to a Remote

`git push upstream main`

### Track a Remote Branch

`git checkout -b new-feature upstream/new-feature`
