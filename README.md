# Git and GitHub Cheat Sheet

- [Initialize Git in a Folder](#Initialize-Git-in-a-Folder)
- [How the branches work](#How-the-branches-work)
- [Creating a new branch and moving on it](#Creating-a-new-branch-and-moving-on-it)
- [Create a Commit](#Create-a-Commit)
- [Correct an error](#Correct-an-error)
- [How git works](#How-git-works)
- [Created a Branch by error](#Created-a-Branch-by-error)

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

## Correct an error

### Created a Branch by error
