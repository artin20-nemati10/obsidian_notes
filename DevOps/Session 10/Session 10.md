
# Automate Tasks by Scheduling jobs

## Automate Tasks by Scheduling Jobs
- Some jobs must be scheduled and executed at specific intervals.
- Such as backing up file / database, preparing a report or installing updates, etc.
- two services, Cron and Anacron, are used to schedule jobs:

|                 Cron                  | Anachronistic Cron                   |
|:-------------------------------------:| ------------------------------------ |
|           Good for servers.           | Good for laptops and desktops.       |
| Granularity from 1 minute to 1 year.  | Daily, weekly & monthly granularity. |
| Job runs if system is on at the time. | Job runs in next system power on.    |
|       Usable by regular users.        | Usable just by root.                 |
## Automate Tasks by Scheduling Jobs
- The Cron tool is a service called Cron Daemon (Crond) that pops up at boot-time.
- Cron Table (Crontab) lists scheduled jobs as a table 
- The Crond service checks this list every 1 minute.
- We have two types of Crontabs, one for each user and one system-wide.
###### The crontab file can be edited using the Crontab command and its options.
---
```bash
~ Crontab -e --> To edit or build Crontab for the first time.
~ Crontab -l --> View the contents of the Crontab file.
~ Crontab -r --> To remove the Crontab file.
~ Crontab -u <USER> --> To edit another user's Crontab file.

# cd /var/spool/cron/crontabs
```
---
###### In the Crontab file, each line is a job defined as follows with its Interval:
```
* * * * * <username> command(s)
- - - - -
| | | | |
| | | | ----- Day of week (0 - 7) (Sunday=0/7)
| | | ------- Month (1 - 12)
| | --------- Day of month (1 - 31)
| ----------- Hour (0 - 23)
------------- Minute (0 - 59)
```

| Operator |                   Description                   |
|:--------:|:-----------------------------------------------:|
|    \*    |     Any value can be replaced<br>(always).      |
|    ,     |   Specify a list of values for<br>scheduling.   |
|    -     |   Specify range of values for<br>scheduling.    |
|    /     | Specify values repeated<br>between an interval. |
- 25 18 * * * ~/script
	- Daily @18:25
---
- 20 7 5 * * ~/script
	- 5th of every month @07:20AM
---
- 15 * * 2 1 ~/script
	- Each Monday in FEB, Minute 15 of each hour
---
- 30 12 26 10 * ~/script
	- October 26th @12:30PM
---
- 10,20,30 * * * * ~/script
	- Minutes 10,20,30 of each hour
---
- 0 9 * * 0-3,6 ~/script
	- Working days (SAT to WED) @09:00AM
---
- \*/10 * * * * ~/script
	- Every 10 minutes
---
- 0 10 1,29 * * ~/script
	- 1st & 29th of each month @10:00AM
---
## Crontab Permissions
- to manage access to Cronta, there are two files /etc/cron.allow and /etc/cron.deny.
1. If cron.allow is available, only users within it will access to crontab.
2. if only cron.deny available, everyone except the people in this file would have access.
3. If neither file is available, only Superuser or root will have access.
## One_time Schedule at a Specific Time
- Using at command, you can execute a number of commands once in a specified time.
- By entering at command and the desired date and time, it enters an interactive environment to enter commands.
- Then press Crtl + D to exit the environment and schedule the commands foe desire date.
---
```bash
artin@host:~$ at 8:35 Apr 10
at> touch BlaHBlaH
at> <EOT>
job 2 at Mon Apr 10 08:35:00 2021
```
---
- With the atq commandm, the list of at jobs is displayed, and with the atrm \[job id] command, job can be canceled.
# Git Introduction
## Version control System (VCS)

![[Pasted image 20261001083140.png]]

## "Centralized" VCS
- CVCS is a type of software tool that developers manafe the changes and versions of their code files in a central server.
- In a CVCS, every user commits their changes directly to the main branch of the project.

![[Pasted image 20261001083344.png]]

## Distributed" VCS
- DVCS is a type of s0oftware tool that helps developers manage the changes and versions of their code files in a peer-to-peer manner.
- in a DVCS, every user has a local copy of entire code and its history, and can work on it independently without relying on a central server.

![[Pasted image 20261001083604.png]]

# Source Code Manager (SCM)
- It’s a method to keep a software system that consists of versions/configs, well organized.
- There are many Version Control Systems, such as:
	- Global
	- Information
	- Tracker
	- CVS - Kind of the grandfather of version control
	- PVCS - Commercialized CVS
	- Subversion - inspired by CVS
	- Perforce
	- Microsoft Visual SourceSafe
	- Mercurial
	- TeamSite
	- Vault
	- Bitkeeper - Used to manage the Linux kernel before…
	- Git - Created by our favorite Linux author & creator: Linus!
## Git Installation
### Installing Git on Linux
###### installing git on servers:
```bash
root@host:~# apt install git
root@host:~# git --version
git version 2.30.2
```
---
###### Global username is because to isdentify yourself when making changes on repositories.
```bash
root@host:~# git config --global user.name "Arash Foroughi"
root@host:~# git config --global user.email "arash@localhost"
root@host:~# cat ~/.gitconfig
```
---
## Git Basic Configureations
#### Local Configuration
```bash
$ cat .git/config
```
- local configs are only available for the current project and stored in .git/config in the project's directory.
---
#### Global Configuration
```bash
$ cat ~/.gitconfig
```
- global configs are available for all projects forthe current user and stored in ~/.gitconfig.
---
#### System-level Configuration
```bash
$ cat /etc/gitconfig
```
- System config applies to the entire system for all users & projects and stored in /etc/gitconfig.
---
## git Basic Configurations
```bash
root@host:~# git config --system system.name "git repo server-1"
root@host:~# git config --system user.name "Arash Foroughi"
user@host:~$ git config --global system.name "my repo server-1"
user@host:~$ git config --global core.editor vim
user@host:~$ git config --global core.pager 'less'
user@host:~$ git config --list
user@host:~$ cat ~/.gitconfig
	[user]
		name = Root User
		email = root@localhost
	[system]
		name = git repo server-1
	[core]
		editor = vim
		pager = more
```
## Empty Repository
#### Create Our First local Repo
##### Step-1: use git init command to initializae a location as git repository:
```bash
artin@host:~$ mkdir gittest
artin@host:~$ cd gittest
artin@host:~$ git init
	Initialized empty Git repository in /home/ubuntu/gittest/.git/
artin@host:~$ cd .git
artin@host:~$ ls -l
	total 32
	drwxrwxr-x 2 ubuntu ubuntu 4096 Sep 30 21:25 branches
	-rw-rw-r-- 1 ubuntu ubuntu 92 Sep 30 21:25 config
	-rw-rw-r-- 1 ubuntu ubuntu 73 Sep 30 21:25 description
	-rw-rw-r-- 1 ubuntu ubuntu 23 Sep 30 21:25 HEAD
	drwxrwxr-x 2 ubuntu ubuntu 4096 Sep 30 21:25 hooks
	drwxrwxr-x 2 ubuntu ubuntu 4096 Sep 30 21:25 info
```
---
##### Step-2: Create files in repo needed to be tracked by fit and then use git add:
```bash
artin@host:~$ git status
	On branch master
	No commits yet
	nothing to commit (create/copy files and use "git add" to track)
artin@host:~$ echo "This is my first file" > test.txt
artin@host:~$ git add test.txt
	or git add *
	or
	git add -A
artin@host:~$ git status
	On branch master
	No commits yet
	Changes to be committed:
	(use "git rm --cached <file>..." to unstage)
	new file:
	test.txt
```
---
##### Step-3:use git commit to finalize your changes as the last version:
```bash
artin@host:~$ git commit -m "This is my first git file"
	[master (root-commit) e74c7da] This is my first git file
	1 file changed, 1 insertion(+)
	create mode 100644 test.txt
artin@host:~$ git status
	On branch master
	nothing to commit, working tree clean
```
# Git Basics
## Git basics - Setup, init, Stage & Commit
- initializing repository and working with Git staging area:

|    Git Commits    |                            Description                            |
|:-----------------:|:-----------------------------------------------------------------:|
|     git iniut     |       Initialize an existing directory as a Git Repository.       |
|    git Status     | Show modified files in working directory, staged for next commit. |
|  git add \[FILE]  | Show modified files in working directory, staged for next commit. |
| git reset \[FILE] | Unstage a file while retaining the changes in working directory.  |
|   git diff HEAD   | Show difference between working directory and last commit (HEAD). |
| git diff --staged |           Diff of what is staged but not yet committed.           |
| git diff CM1 CM2  |             Show the differences between two commits.             |
|    git commit     |       Commit your staged content as a new commit snapshot.        |

---
#### Example of adding & removing files to a git repository:
```bash
artin@host:~$ mkdir source; cd source; tar -zxvf source.tar.gz

artin@host:~$ git init; git status

artin@host:~$ git add *

artin@host:~$ git commit -m "Initial source code check"

artin@host:~$ git status

artin@host:~$ rm TODO

artin@host:~$ git status

artin@host:~$ git rm TODO

artin@host:~$ git commit -m "Deleting TODO"

artin@host:~$ git status
```
