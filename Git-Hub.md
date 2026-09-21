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
  - on Linux: `cat ~/.ssh/id_rsa.pub` (tehn copy manually)
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


