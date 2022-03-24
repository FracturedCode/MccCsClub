# Git Meeting Notes

## Introduction

Hi my name is Austin, I am the new VP of the club. I am really excited to be able to participate and hopefully we can all have some fun and learn fun things about tech related topics together. 

Before I get started with the demo on git I was hoping to talk some about bi-weekly meetings on off weeks for the club. We are hoping to get members more engaged by doing coding problems together on CodeWars or LeetCode. Maybe we will even meet in person on campus and pitch in to order pizza if everyone is up for it. 

I put a survey in the general chat on the discord to see what the best times were for everyone. Right now it looks like Fridays from 3 - 5 are the best times. If you are interested and didn’t see the survey before, I’ll go ahead and put the link for the survey in the chat here so you can still take it. I will finalize the times by the end of the week and hopefully we can have our first meeting next week if everything lines up.


## Git is a version control system

### What is a VCS (Version Control System)

- How code changes are tracked and shared between developers
- Two types: Central Version Control and Distributed Version Control
	- Central is located in one place
		- Check out, make changes, then check in
		- If server is offline or you are working somewhere without a connection then you can only see what you have ‘checked out’ so there is limited access
		- If something happens to the central repository then you have to hope there is a backup of that code somewhere
	- Distributed (GIT)
		- Everyone working on the code has their own local repository
		- There is the option to have a remote repository
		- Local has the same information as remote based on the last sync
		- You can see all of the changes that happened since the last backup
		- It is “Distributed” because there are multiple repositories distributed across developers

### Difference between Git and GitHub

- Git
	- Distributed VCS
	- Git is a version control tool used for developers to share code
	- Git is singularly focused - all it does is version control
- GitHub
	- Cloud based platform built around the git tool
	- Hosts code
	- Provides numerous other features
		- Forking (create a copy of code that you manage)
		- SSH (secure shell) connection
			- SSH is a network protocol that gives users a secure way to access a computer over an unsecured network
		- Branch Protection
		- Project Insights
		- Online editing of files

#### Why to use the command line
	
- GUIs can only do so much and there are circumstances where you can get stuck without understanding the command line prompts

#### How to download GIT - (Walkthrough)
- Go to: https://git-scm.com/ 
- Click Downloads
- Select OS
- Select Version

#### BASH(Bourne-Again Shell) commands - Cheat Sheet: https://www.educative.io/blog/bash-shell-command-cheat-sheet
- ls - list directory contents
- cd - change directory
- pwd - print working directory

#### Git commands
- Check version
	- git --version
- First time setup
	- git config --global user.name “YourName”
	- git config --global user.email “yourName@gmail.com”
- List config
	- git config --list
- Need Help?
	- git (command) --help
	- git help (command)
- Initialize a repository - (demo with /eclipse-workspace/DemoProject)
	- git init
	- ls -la (see all files in directory using long format)
- Check the status of the repository
	- git status
- Creating .gitignore
	- touch .gitignore
	- open .gitignore in text editor
	- Add files or directories you want git not to track
		- bin
		- .settings
		- .project
	- git status again
- Add files to staging area
	- git add (file / files)
	- git add .gitignore
	- git add -A or git add .
- Remove files from staging area
	- git reset (file / files)
	- git reset 
- Committing files to the repository
	- git add -A
	- git commit -m “Initial Commit”
- Seeing Changes
	- git diff
- Checking the repository log
	- git log
	- Returns a log of commits with their comments

### Interacting with GitHub

#### Setting up SSH on GitHub: https://www.geeksforgeeks.org/using-github-with-ssh-secure-shell/
- Creating SSH Key
	- ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
	- Enter to use default
	- Type passphrase
	- ls -al ~/.ssh (verify rsa creation)
- Adding SSH Key to agent
	- eval "$(ssh-agent -s)"
	- ssh-add ~/.ssh/id_rsa
- Add SSH key to github
	- clip < ~/.ssh/id_rsa.pub (copy to clipboard)
	- Add to github using settings under profile
- Test SSH connection
	- ssh -T git@github.com

#### Creating a remote repository on GitHub
- Click new use name “DemoProject” on GitHub
	- echo "# DemoProject" >> README.md
	- git init
	- git add README.md
	- git commit -m "first commit"
	- git branch -M main
	- git remote add origin git@github.com:AustinFinell/DemoProject.git
	- git push -u origin main
 
- Pushing to a repository (push your changes to the master branch)
	- git push <url> 

- Pulling from a repository (pull other changes before pushing in order to normalize changes made by other devs)
	- git pull <url>

- Cloning a remote repository
	- git clone <url> <where to clone>
	- git clone https://github.com/AustinFinell/TicTacToe/ .

- Branching (more common workflow) Image: https://www.nobledesktop.com/image/blog/git-branches-merge.png
	- git branch “name” (creates a new branch)
	- git branch (returns all branch names)
	- git checkout “name” (change to that branch)
	- Commit changes to local new branch
	- git push -u <url> <branch name> (push to remote before merging)

- Merging to master branch
	- git checkout main (could also be master)
	- git pull <url> master(any changes from master branch)
	- git branch --merged (see which branches have been merged)
	- git merge “feature-branch”
	- git push <url> master (push changes to master branch)

- Deleting used branches
	- git branch --merged
	- git branch -d “name”
	- git branch -a (check branches)
	- git push <url> --delete “name”

- Pull Requests
	- Finished your commits in a new branch in local repository
	- Your code needs to be checked by someone else in the remote repository before merging
	- Push new branch up to the remote repository (GitHub)
	- Create a pull request on that repository (GitHub)
	- The idea is you are pulling the new branch into the master branch.
	- This allows the merge to be checked off by whoever controls the repository. If they do, they will accept the pull request.
