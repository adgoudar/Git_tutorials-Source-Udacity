# Git cheatsheet

##Source : Udacity : Version control with Git

### First Time Git Configuration
Before you can start using Git, you need to configure it. Run each of the following lines on the command line to make sure everything is set up.


#### sets up Git with your name
```
git config --global user.name "<Your-Full-Name>"
```

#### sets up Git with your email
```
git config --global user.email "<your-email-address>"
```

#### makes sure that Git output is colored
```
git config --global color.ui auto
```

#### displays the original state in a conflict
```
git config --global merge.conflictstyle diff3
```

```
git config --list
```

### Git code editor setup

#### Sublime Text Setup
```
git config --global core.editor "'C:/Program Files/Sublime Text 2/sublime_text.exe' -n -w"
```

### To create a repo from scratch

#### Create a directory 
```
mkdir -p udacity-git-course/new-git-project && cd $_
```

#### Git init
The init subcommand is short for "initialize" - does the initial setup of a repository.
Here's a brief synopsis on each of the items in the .git directory:
1. config file - where all project specific configuration settings are stored.

From the Git Book:
Git looks for configuration values in the configuration file in the Git directory (.git/config) of whatever repository you’re currently using. These values are specific to that single repository.
For example, let's say you set that the global configuration for Git uses your personal email address. If you want your work email to be used for a specific project rather than your personal email, that change would be added to this file.

2. description file - this file is only used by the GitWeb program, so we can ignore it
3. hooks directory - this is where we could place client-side or server-side scripts that we can use to hook into Git's different lifecycle events
4. info directory - contains the global excludes file
5. objects directory - this directory will store all of the commits we make
6. refs directory - this directory holds pointers to commits (basically the "branches" and "tags")

#### Git clone - to create an identical copy
```
$ git clone https://github.com/udacity/course-git-blog-project
```

#### Git status
The git status command will display the current status of the repository.
```
$ git status
```

#### Git log
The git log command is used to display all of the commits of a repository.
```
$ git log
```
By default, this command displays:
* the SHA
* the author
* the date
* the message

#### git log --oneline 
The --oneline flag is used to alter how git log displays information:
```
$ git log --oneline
```

This command:
* lists one commit per line
* shows the first 7 characters of the commit's SHA
* shows the commit's message

#### git log --stat 
The --stat flag is used to alter how git log displays information:
```
$ git log --stat
```

This command:
* displays the file(s) that have been modified
* displays the number of lines that have been added/removed
* displays a summary line with the total number of modified files and lines that have been added/removed

#### git log -p
The -p flag (which is the same as the --patch flag) is used to alter how git log displays information:
```
$ git log -p
```
This command adds the following to the default output:
* displays the files that have been modified
* displays the location of the lines that have been added/removed
* displays the actual changes that have been made

#### Git add
The git add command is used to move files from the Working Directory to the Staging Index.
```
$ git add <file1> <file2> … <fileN>
```
This command:
* takes a space-separated list of file names
* alternatively, the period . can be used in place of a list of files to tell Git to add the current directory (and all nested files)

#### Git commit

Make sure you configure your editor before performing the commit
```
$ git config --global core.editor <your-editor's-config-went-here>

git commit
```

Enter the commit message, save the file and close the editor

Bypass The Editor With The -m Flag
TIP: If the commit message you're writing is short and you don't want to wait for your code editor to open up to type it out, you can pass your message directly on the command line with the -m flag:
```
$ git commit -m "Initial commit"
```
#### Important things to think about when crafting a good commit message:

##### Do

* do keep the message short (less than 60-ish characters)
* do explain what the commit does (not how or why!)

##### Do not

* do not explain why the changes are made (more on this below)
* do not explain how the changes are made (that's what git log -p is for!)
* do not use the word "and"
* if you have to use "and", your commit message is probably doing too many changes - break the changes into separate commits
e.g. "make the background color pink and increase the size of the sidebar"

#### Git diff

The git diff command is used to see changes that have been made but haven't been committed, yet:
```
$ git diff
```
This command displays:

* the files that have been modified
* the location of the lines that have been added/removed
* the actual changes that have been made

#### Git Ignore

The .gitignore file is used to tell Git about the files that Git should not track. This file should be placed in the same directory that the .git directory is in.

### Tagging, Merging and Branching

#### Git Tag
The git tag command is used to add a marker on a specific commit. The tag does not move around as new commits are added.

To interact with the repository's tags is the git tag command:
```
$ git tag -a v1.0
```

In the command above (git tag -a v1.0) the -a flag is used. This flag tells Git to create an annotated flag. If you don't provide the flag (i.e. git tag v1.0) then it'll create what's called a lightweight tag.

Annotated tags are recommended because they include a lot of extra information such as:
* the person who made the tag
* the date the tag was made
* a message for the tag

##### Verify Tag
The following command displays all the tags in the repository:
```
git tag
```

##### --decorate
In the 2.13 update to Git, the log command has changed to automatically enable the --decorate flag.

```
git log --decorate
git log
```

##### Deleting a Tag
A Git tag can be deleted with the -d flag (for delete!) and the name of the tag:
```
git tag -d v1.0
```

##### Adding tag to a Past commit
provide the SHA of the commit you want to tag
```
git tag -a v1.0 a87984
```

### Branching

The git branch command is used to interact with Git's branches:
```
$ git branch
```

It can be used to:
* list all branch names in the repository
* create new branches
* delete branches

#### Create a branch
```
$ git branch branchname
```
There are a number of branches in the repository, but that the command prompt displays the current branch.


#### Git checkout command
Even though we created the new branch say sidebar, no new commits will be added to it since we haven't switched to it, yet. If we made a commit right now, that commit would be added to the master branch, not the sidebar branch. 

```
git checkout sidebar
```

Running this command will:
* Remove all files and directories from the Working Directory that Git is tracking
(files that Git tracks are stored in the repository, so nothing is lost)
* Go into the repository and pull out all of the files and directories of the commit that the branch points to

#### Branches  in the log
The clearest way to see the branch information is by looking at the output of git log. To display the branches:
```
$ git log --oneline --decorate
```
#### Active branch
The fastest way to determine the active branch is to look at the output of the git branch command. An asterisk will appear next to the name of the active branch.

#### Delete A Branch
A branch is used to do development or make a fix to the project that won't affect the project (since the changes are made on a branch). Once you make the change on the branch, you can combine that branch into the master branch (this "combining of branches" is called "merging").

After a branch's changes have been merged, you probably won't need the branch anymore. If you want to delete the branch, you'd use the -d flag. The command below includes the -d flag which tells Git to delete the provided branch (in this case, the "sidebar" branch).
```
$ git branch -d sidebar
```
NOTE : you can't delete a branch that you're currently on. So to delete the sidebar branch, you'd have to switch to either the master branch or create and switch to a new branch.

Git wouldn't let you delete a branch if it has commits on it that aren't on any other branch. To force delete, you need to use a capital D flas 
```
$ git branch -D sidebar
```

####  Switch and Create Branch In One Command

If you provide the -b flag in the git checkout, you can create a branch and switch to it all in one command.
```
$ git checkout -b branch-for-awesome-changes
```

To create our new footer branch and have this footer branch start at the same location as the master branch:
```
$ git checkout -b footer master
```

#### See All Branches At Once

 We can't see other branches unless in the git log output unless we switch to a branch. Wouldn't it be nice if we could see all branches at once in the git log output. 
 ```
 $ git log --oneline --decorate --graph --all
 ```
 The --graph flag adds the bullets and lines to the leftmost part of the output. This shows the actual branching that's happening. The --all flag is what displays all of the branches in the repository.













