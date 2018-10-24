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

