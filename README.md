# Git and GitHub Cheat Sheet

- [Initialize Git in a Folder](#Initialize-Git-in-a-Folder)

- [How the branches work](#How-the-branches-work)

- [Creating a new branch and moving on it](#Creating-a-new-branch-and-moving-on-it)

- [Create a Commit](#Create-a-Commit)

- [How git works](#How-git-works)

- [Log](#log)
  - [git log](#git-log)
  - [git reflog](#git-reflog)
  - [git blame](#git-blame)
  - [git cherry-pick](#git-cherry-pick)

* [Correct an error](#Correct-an-error)

  - [Created a Branch by error](#Created-a-Branch-by-error)
  - [Added to Master Branch by mistake?](#Added-to-Master-Branch-by-mistake?)
  - [Committed on the master branch by error](#Committed-on-the-master-branch-by-error)
    - [git reset](#git-reset)
  - [Change the commit message](#Change-the-commit-message)
  - [Forgot to add a file to the last commit](#Forgot-to-add-a-file-to-the-last-commit)
  - [Pushed the wrong files to GitHub](#Pushed-the-wrong-files-to-GitHub)
    - [git revert](#git-revert)

* [SSH Key](#SSH-Key)
  - [Creating your SSH Key](#Creating-your-SSH-Key)

---

#### When installing git on the device!

```
$ git config --global user.name "Your Name"
$ git config --global user.email your@email.com
```

_// If you need to change the name for specific project!_

```
$ git config user.name "Your Name"
$ git config user.email your@email.com
```

_// Call the list of Git parameters:_

```
$ git config --list
```

_// To activate the colors in Git Bash:_

```
$ git config --global color.diff auto
$ git config --global color.status auto
$ git config --global color.branch auto
```

_// To change the default editor for Git (NameOfEditor => VSCode = code)._

```
$ git config --global core.editor NameOfEditor
$ git config --global merge.tool vimdiff
```

## Initialize Git in a Folder

_// Create a folder, go in the folder, initialize git in the folder!_

```
$ mkdir folderName
$ cd folderName
$ git init
```

_// To get a Project form other then your repository create a folder go in the folder copy the url of the project and link you local folder to the repository:_

```
$ mkdir gitGitHub
$ cd gitGitHub
$ git remote add GGH https://github.com/danyweis/gitAndGitHub.git
```

_**GGH** is a short name to use to call the repository of the position of the repository **This is not a clone yet!**._

_// Now we will clone the project to our local machine._

```
$ git clone https://github.com/danyweis/gitAndGitHub.git
```

_// you should see in the terminal:_

`Cloning into 'GGH'...`  
`remote: Enumerating objects: 3, done.`  
`remote: Counting objects: 100% (3/3), done.`  
`remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0`

## How the branches work

#### This is the Master Branch --

#### This is an other Branch \_\_

On the Master Branch is the application in production.

```
commit       commit       commit       commit       commit
  [*]----------[*]----------[*]----------[*]----------[*]
                  \                     /
                   \___[*]_______[*]___/
                      commit    commit

* id of the commit
```

On the new branch we can test a new function and if we want we can merge the test branch with the master branch.
Git will merge the branches with no errors.

_// To know the branches of the current project we can call:_

`git branch` and the result on this project will be:

```
$ git branch
* master
```

**The \* shows you on which branch you are at the moment and where you will be making changes!**

## Creating a new branch and moving on it

_// If you you want to make a change to a project and you are not sure about the result or don't know if it can break something it is recommended to create a new branch._

Lets say we want to create a text in color in Markdown and don't know if it is possible and want to start to play around so best we create a branch called colorText

```
git branch colorText
```

_// This will create a branch only on your local machine so lets have a look at our branches now:_

```
$ git branch
* master
  colorText
```

_// OK now we have two branches but we are still on the master (remember the \*) so lets move to the colorText branch._

```
$ git checkout colorText
$ git branch
  master
* colorText
```

_// What Git does behind the scene is that it creates a virtual copy of the folder where the project is in._

## Create a Commit

_Now that we changed the <span style="color:red">color of the text to red</span> we want to save our changes so lets do that:_

```
git commit -m "Changed color of the text to red"
```

_The changes are now committed and the text "Changed color of the text to red" is important to know what was done at that point of the commit._

To see all the commits made we can call `git reflog` and that will show ann the commits with the SHA which is used to come back to an older version of the project.

## How git works

```
         Working
      __ directory
     /
Git Add
     \
      --> Stage  __
                   \
                GitCommit
                   /
    Repository  <--
      |      /\
      |       |
Git push    Git Pull
      |       |
      \/      |

    {   GITHUB   }

```

With `git add` you add files, folders,... to the stage which will be added to your change when you commit

# Log

- [git log](#git-log)
- [git reflog](#git-reflog)
- [git blame](#git-blame)
- [git cherry-pick](#git-cherry-pick)

## git log

We use git log to get information about the commit history of the project. `git log` will show the latest commit on the first place.

```
$ git log

commit 5e1e9194ea2922e88fc0672d7bf24f745dbc0cf7 (HEAD -> testBranch, origin/master, master)
Author: yourname <youremaill@mail.com>
Date:   Sun Jul 5 12:03:20 2020 +0100

    finished the quizapp

commit 3e8ec86bc6d107cd3a7f7faa8c1ed37b36ffeccd
Author: yourname <youremail@mail.com>
Date:   Sat Jul 4 18:51:22 2020 +0100

    init

```

Now if we have a look at this we get a lot of information:

=> commit 5e1e9194ea2922e88fc0672d7bf24f745dbc0cf7  
 this is the SHA of the commit needed to come back to that point

=> (HEAD -> testBranch, origin/master, master)

- HEAD tell us on what branch we are, in this case we are on the testBranch

- origin/master is the master branch on the local machine you are working on

- master is the branch which is there as well next to the test branch.

In case we would be on the master branch we would get this as result:

`(HEAD -> master, origin/master, testBranch)`

=> Author: yourname < youremaill@mail.com>  
Here we get the information about the person who created the commit, there will be you name and you provided email address.

=> Date: Sun Jul 5 12:03:20 2020 +0100  
Then we get the information about when the commit was made.

=> finished the quizapp  
And finally we get the commit message.

## git reflog

`reflog` will keep a history of what you did in that repository:

```
$ git reflog

7eb8f6c (HEAD -> master, origin/master, origin/HEAD) HEAD@{0}: commit: SSH creation

d1affdb HEAD@{1}: commit: Creation of a git github cheat sheet (point errors)

6f3aec3 HEAD@{2}: clone: from https://github.com/danyweis/gitAndGitHub.git

```

We will have as wel the SHA on the beginning which will be useful to go back to that point with:

```
$ git checkout d1affdb
```

## git blame

OK `git blame` will show you the full document with every line and tell you who changed which line and when it was changed and it will give you the SHA of the commit when it was committed! I will not show the full outcome but just a few lines of this document:

_(It will show you the full terminal page and if you look at the bottom you will see **":"** if you press enter it will show you the next line)_

**If you wat to quit you need to type :q**

```
$ git blame nameOfTheFile


d1affdb3 (danyweis 2020-07-21 22:23:28 +0100   1) # Git and GitHub Cheat Sheet
d1affdb3 (danyweis 2020-07-21 22:23:28 +0100   2)
d1affdb3 (danyweis 2020-07-21 22:23:28 +0100   3) - [Initialize Git in a Folder](#Initialize-Git-in-a-Folder)
7eb8f6c9 (danyweis 2020-07-22 17:45:18 +0100   4)
d1affdb3 (danyweis 2020-07-21 22:23:28 +0100   5) - [How the branches work](#How-the-branches-work)
7eb8f6c9 (danyweis 2020-07-22 17:45:18 +0100   6)

......

7eb8f6c9 (danyweis 2020-07-22 17:45:18 +0100 483) Now you **SSH Key** is generated and you will find it in the location you wanted or in the default location. For me it was **/home/yourPcsName/.ssh/id_rsa**
d1affdb3 (danyweis 2020-07-21 22:23:28 +0100 484)
7eb8f6c9 (danyweis 2020-07-22 17:45:18 +0100 485) There you will have a private and a public key in that folder.
7eb8f6c9 (danyweis 2020-07-22 17:45:18 +0100 486) **Do NEVER expose the private key**, what you now want to do is to copy your public key then go to your GitHub account, 'settings', 'SSH and GPG keys' and there click on _New SSH Key_, give it a title (Name of your machine) and past the key below and then click on **Add SSH Key**.
```

## git cherry-pick

If you don't want to merge two branches and only want to take a specific commit of an other branch then you can use `git cherry-pick`

What you want to do is to go on the branch and do a `git log` then copy the SHA of the commit which interests you and go back to the master branch (or other) and then put that commit in front of the last commit _(This will duplicate the chosen commit in you log history)_.

You can even take multiple SHA's

```
$ git cherry-pick 6f3aec3 d1affdb
```

# Correct an error

## Created a Branch by error

If you created a branch which you finally didn't use then the best thing is to delete that branch . You can do that by using this command:

```
$ git branch -d nameOfTheBranch
```

## Added to Master Branch by mistake?

Now we have modified our README.md in our quiz-app repository and we added it to the master branch
Now lets do `git status` to see what happened!

```
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md
```

If the changes where added but not yet committed then NO PANIC we can repair that.

Now we have to `git stash` to record the current state of the working directory and the index, so that we can then go back to a clean working directory (master branch).

```
$ git stash
Saved working directory and index state WIP on master: 5e1e919 finished the quizapp
```

And if we do now `git status` we get:

```
$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

Now lets create a side branch move on it and then bring the record to that branch.

```
$ git branch testBranch
$ git checkout testBranch
Switched to branch 'testBranch'

$ git branch
  master
* testBranch
```

Now there are two ways to get the record now on the branch.

```
$ git stash apply
```

this will add the last record to the current branch but if you made more then one record and don't want to add the last one then you can use `git stash list` to get the list of all the records (In this case we only have one).

```
$ git stash list
stash@{0}: WIP on master: 5e1e919 finished the quizapp
```

Then hen we know which record we want to apply to the branch we then can do:

```
$ git stash apply stash@{0}

On branch testBranch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

```

## Committed on the master branch by error

[All the git reset versions](#git-reset)

Now if you committed on the master branch by mistake and want to delete the last commit and bring that commit to a side branch, then lets see how we can do that:

First we need some information about the last commit we can get that information by using [git log](#git-log). The result will look like this:

Then we have to make sure to copy the SHA and when we have tha done then we can:

```
$ git reset --hard HEAD^
$ git branch newBranch
$ git checkout newBranch
```

`HEAD^` means we want to delete the last commit on the current branch.

When we have created a new branch and we are on that branch or even if it is an existing branch then we can reset the commit on that branch. To do the reset we only need the first 8 characters of the SHA.

```
$ git reset --hard 3e8ec86b
```

## git reset

- [--hard](#hard)
- [--mixed](#mixed)
- [--soft](#soft)

#### --hard

If you want to do a `--hard` reset make sure that you really want to do that and if you are sure then make again sure that you are sure! This command can bring you back to any commit but everything between now and that commit will be **gone**.

OK so we have to do:

```
$ git reset theCommitYouWantToGo --hard
```

Again this command will forget everything between the commit you want to go to and now. Make 5 times sure that you need to do a hard reset before pressing enter!

#### --mixed

Then we have the `--mixed` reset which will come back before the last commit or you can chose what commit you want to go back to without deleting anything. This creates a detached HEAD.

_If you do not specify anything after the reset it will be a --mixed by default._

So we can do:

```
$ git reset HEAD~
```

or

```
$ git reset --mixed HEAD~
```

#### --soft

Lets Talk about the `--soft` reset. The soft reset wont delete anything and wont change the commit, it will only position you on top of the wanted commit and you can see the code from that moment. If wanted you can crete a branch at that point.

```
$ git reset backToTheFuture --soft
```

## Change the commit message

If you did a typo on your last commit or you forgot to describe something in the commit, then there is a way to change the last commit message.

```
$ git commit --amend -m "This will be your new message for the last commit"
```

`--amend` is used to modify the last. commit  
`-m` is used to transmit the message.

## Forgot to add a file to the last commit

If you forgot to add a file to the last commit you first have to add the file and then you can commit again:

```
$ git add forgottenFile.txt
$ git commit --amend --no-edit
```

`--no-edit` is to tell git we don't want to change the message.

## Pushed the wrong files to GitHub

#### git revert

In this case we can create a new commit which will cancel the old one.

```
git revert HEAD^
```

#### Best practice is to use:

`git reset` to make changes locally (changes are not yet committed)

```
RESET                        --<--
                           /      \
-----[ ]-------[ ]-------[ ]-------[ ]
```

`git revert` to make changes publicly (changes were already committed)

```
REVERT                   ---- > ----
                        /           \
-----[ ]-----[ ]-----[ ]-----[ ]-----[ ]
```

_**Before making a `git revert` make sure that the team you are working with knows that you made a mistake so you can do the revert with no problem.**_

Revert does a kind of _undo_ while creating a new commit

# SSH Key

## Creating your SSH Key

The SSH key is used to connect you PC to GitHub so you don't need to type your password anymore when you push to GitHub.

To generate a key we use:

You will be asked first **location for the SSH key** (for me the default is fine) then it will ask if you want to **protect the key with a password** if yes then you will now have to type in you password or just type enter and then a second time type your password or again press enter.

```
$ ssh-keygen

Generating public/private rsa key pair.
Enter file in which to save the key (/home/yourPcsName/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/yourPcsName/.ssh/id_rsa
Your public key has been saved in /home/yourPcsName/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:BPrOHfN6IMyhuwehf89iew3Qh3nPCZxbklLHBNNq+I yourPcsName@thinkcode
The key's randomart image is:
+---[RSA 3072]----+
|      -=       =+|
|     . .      . =|
|.   .  -.    . B.|
| o   . .      B+=|
|. +  o. S  ..ooB+|
| = o o+..+--.o+..|
|o   o +o..oE  . .|
|     +..oE.    . |
|     .+oo.       |
+----[SHA256]-----+
```

Now you **SSH Key** is generated and you will find it in the location you wanted or in the default location. For me it was **/home/yourPcsName/.ssh/id_rsa**

There you will have a private and a public key in that folder.  
**Do NEVER expose the private key**, what you now want to do is to copy your public key then go to your GitHub account, 'settings', 'SSH and GPG keys' and there click on _New SSH Key_, give it a title (Name of your machine) and past the key below and then click on **Add SSH Key**.
