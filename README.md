# $ dev-productivity

![dev-productivity](./dev-productivity-notes.png)

<br/>

# Table of Contents

1. [Softwares I Use](#softwares-i-use)
1. [Setup a Quick Postgres DB with Docker](#setup-a-quick-postgres-db-with-docker)
1. [Set SSH for Multiple Accounts](#set-ssh-for-multiple-accounts)
    1. [Generate SSH](#generate-ssh)
    1. [Copy SSH To Hosting Services](#copy-ssh-to-hosting-services)
    1. [Create SSH Config File](#create-ssh-config-file)
    1. [Add SSH](#add-ssh)
    1. [Remove SSH](#remove-ssh)
    1. [Git Config and Workflow](#git-config-and-workflow)
    1. [Clone Repository](#clone-repository)
    1. [Check the Git User Email Inside the Repository](#check-the-git-user-email-inside-the-repository)
1. [For More Dev Notes](#for-more-dev-notes)

<br/>

# Softwares I Use

- Postman
- iTerm2 with ZSH
- Simplenote
- pgAdmin
- Docker
- VSCode
  - Font - FiraCode
  - Theme - Retreon Color Theme
  - Prettier
  - Rainbow Brackets
  - Material Icon Theme
  - Indent Rainbow
  - ESLint
  - Live share
  - Git Lens

<br/>

# Setup a Quick Postgres DB with Docker

```bash
docker run --name <db-name> -e POSTGRES_PASSWORD=admin -p 5432:5432 -d postgres
```

<br/>

# Set SSH for Multiple Accounts

## Generate SSH

```bash
$ ssh-keygen -t ed25519 -C "your.work@email.com"
```

```bash
$ ssh-keygen -t ed25519 -C "your.personal@email.com"
```

You should check if ***ed25519*** is still the most recommended algorithm.

## Copy SSH to Hosting Services

Copy output from each key using:

```bash
$ cat ~/.ssh/<your_geenrated_ssh_key>.pub
```

## Create SSH Config File

Create file:
```bash
$ touch ~/.ssh/config
```

Open file with VSCode:
```bash
$ code ~/.ssh/config
```

Paste configuration

**~/.ssh/config**
```
Host work
  AddKeysToAgent yes
  HostName <work_host_name>
  User <work_user_name>
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/<work_key>
  Port <port_number>

Host personal
  AddKeysToAgent yes
  HostName <personal_host_name>
  User <personal_user_name>
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/<personal_key>
  Port <port_number>
```
### Or

```bash
$ echo "Host work
  AddKeysToAgent yes
  HostName <work_host_name>
  User <work_user_name>
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/<work_key>
  Port <port_number>

Host personal
  AddKeysToAgent yes
  HostName <personal_host_name>
  User <personal_user_name>
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/<personal_key>
  Port <port_number>" > ~/.ssh/config
```

### Add SSH

```bash
$ ssh-add <ssh_key_name>
```

### Remove SSH

In case you need to remove it, you can do:

```bash
$ ssh-add -D
```

```bash
$ rm -rf ~/.ssh/*
```

## Git Config and Workflow

You should create a root folder called `repos`, and inside of it, create two new folders.

- `work` - This folder you'll have all your work repositories
- `personal` - This folder you'll have all your personal repositories

Edit your git config file, and create two new ones for each of the folders above.

**~/.gitconfig**
```bash
[includeIf "gitdir:~/repos/work/"]
    path = ~/repos/work/.gitconfig
[includeIf "gitdir:~/repos/personal/"]
    path = ~/repos/personal/.gitconfig
```

**~/repos/work/.gitconfig**
```bash
[user]
	email = professional@email.com
	name = Your Name
```

**~/repos/personal/.gitconfig**
```bash
[user]
	email = personal@email.com
	name = Your Name
```

## Clone Repository

To clone any repository now, public or private, use this command:

```bash
git clone git@<your_host_name>:<remote_repository_name>
```

### Example

If the git repository tells you to clone like this: `git@github.com:nodejs/node.git`

You should use this command instead:

```bash
git clone git@work:nodejs/node.git
```

or

```bash
git clone git@personal:nodejs/node.git
```

## Check the Git User Email Inside the Repository

```bash
$ git config --show-origin --get user.email
```

<br/>

# For More Dev Notes

This is just one piece of my open personal notes collection, where I'm mapping out all my knowledge. If you're keen on checking out other topics, give this a click: ***[official dev-notes](https://github.com/gabrielvsantana/dev-notes)***
