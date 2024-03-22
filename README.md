# **Summary on Git**
---
## Git - what is it? Main commands.

* Git is a version control system that helps you track changes to a project. This tool can be used for both individual and team work. <br>
---
### Repository creation.

* In order for Git to start tracking changes in a project, the folder with the files of this project must be made a Git repository (storage). To do this, go to it and enter the command **git init** (initialize). <br>
```bash
$ git init
```
* In the message there will be 'Using 'master' as the name…'. Master is a main branch (trunk) of commits. <br>
---
### Repository deletion.
* If you accidentally set the wrong folder as a Git repository, you can “ungit” it. To do this, you need to delete the hidden .git subfolder. <br>

```bash

$ cd <folder with repository> 

$ rm -rf .git # deleted .git 
```
---
### Repository state.
```bash

$ git status

```
---
### Adding files to index before commiting

* After creation any files in your project, before commiting you need to add it into index (like trensition zone) <br>

```bash

$ git add filename # first option 

$ git add . # another option - add into repository all folder

$ git add --all # another option - add into repository all files

```
* Without add files will be untracked <br>

---
### Commiting.

* You can make a commit using the git commit command with the -m switch (“message”), which assigns a message to the commit. <br>

```bash
$ git commit -m 'Commit name - short description'
```
---
## Commiting history.

* To see all commits done, enter the command git log (records). <br>

```bash
$ git log
```
---
## GitHub - What is it? How to use?

* GitHub is a platform for storing IT projects and collaborating on them using Git. Basically, it's a site where you can upload your project files to share with other people. <br>
* Whereas Git is a console tool for working with local and remote repositories. It is not directly associated with any of the platforms and is developed separately from them. <br>
---
### GitHub connection.

* First, register on GitHub. <br>

* Next, create a remote repository: <br>
    1. Go to your profile.
    2. Go to the Repositories tab, and then click on the green New button on the right.
    3. Set the name of repository. Better nake it matching with one on your PC.
    4. Click "Create repository".
<br>

### SSH - what is it?

* Before synchronizing repositories, it is required to generate SSH-key - this is networ protocol. It provides secure data exchange on the network.
* SSH uses a key pair for security - public and private.
* Only you can decrypt the data using the private key, but anyone with the public key can encrypt it for you. <br>

* Checking for SSH key availability:

```bash
$ cd ~
$ ls -la .ssh/ # list the created keys
```

* If the folder is empty or doesn't exist, everything is fine. 
* Key generation:
```bash
$ ssh-keygen -t ed25519 -C "your email, assigned to GitHub"
```
* After entering, the following message will be displayed: > Generating public/private rsa key pair. # public and private keys are generated
* Specify the location where the keys are stored. A simple option is to make the user's home directory the default path. To do this, press Enter.
* The program will ask for a passphrase to access the SSH key. You can leave the field blank. To do this, press Enter and then Enter again to confirm.
* To check that the keys were actually generated:
```bash
$ ls -a ~/.ssh 
```
![Keys](https://pictures.s3.yandex.net/resources/M2_T4_01_1684937563.png "Keys")

<br>
---

### Assign SSH-key to your GitHub
* First, copy keys to bufer:
```bash
# copy the contents of the key to the clipboard:
$ pbcopy < ~/.ssh/id_rsa.pub
# for ed25519:
$ pbcopy < ~/.ssh/id_ed25519.pub

#Alternatively copy the text from:

$ cat ~/.ssh/id_rsa.pub
```
* Next, go to GitHub and select Settings from the account menu:

![Account menu](https://pictures.s3.yandex.net/resources/M2_T4_03_01_1685016747.png "Account menu")

* In the menu on the left, click on SSH and GPG keys:

![SSH and GPG keys](https://pictures.s3.yandex.net/resources/M2_T4_03_02_1685016772.png "SSH and GPG keys")

* In the tab that opens, select New SSH key:
![New SSH keys](https://pictures.s3.yandex.net/resources/M2_T4_03_02_1685016772.png "New SSH keys")

* In the Title field, write the name of the key. For example, Personal key.
The Key type field must contain Authentication Key.
In the Key field, copy your key from the clipboard:

![Key from bufer](https://pictures.s3.yandex.net/resources/M2_T4_03_04_1685016816.png "Key from bufer")

* Click on the Add SSH key button.
* Verify that the key is correct using the following command:
```bash
$ ssh -T git@github.com
```
* To verify authenticity, the server generates and publishes SHA256 keys. You can check the GitHub keys at this [link](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints '"ink check"). If the key in the alert matches what you see on the site, then the server is valid. Enter yes to continue. You will see a greeting on the screen.

---

### Link local and remote repositories

* Go to the remote repository page, select the SSH type and copy the URL. The button on the right will allow you to do this instantly:

![URL](https://pictures.s3.yandex.net/resources/M2_T4_02_1685021914.png "URL")

* Link a remote repository to a local one - git remote add. The command must be passed two parameters: the name of the remote repository and its URL. Use origin as the name. And you copied the URL from the remote repository page. <br>

```bash
$ git remote add origin git@github.com:%Accout_Name/first-project.git 
```
* To make sure the repositories are linked:

```bash
$ git remote -v

#Message will appear:
# origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
#origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push) 
```
---

#### Synchronizing local and remote repositories:

* In order to push changes to a remote repository use git push. 
* The first time this command must be called with the -u flag and the parameters origin (the name of the remote repository) and main or master (the name of the current branch). The -u flag will link the local branch to the remote branch of the same name.

```bash
$ git push -u origin main
```
*  Go to the project repository on GitHub. You will see that files with changes have appeared in the repository.

* In the future, when working with a remote repository, the -u flag can be omitted and simply write git push. <br>

## READ.me file.

* In order for other users to understand what the project is, it needs to be described. Such a description is usually indicated in the README.md file. It can include:
    1. The name of the project and its brief description: who created it, why, what problems it solves and what problems it solves.
    2. Technologies used in the project. How does it differ from similar ones?
    3. Project documentation - detailed instructions about what the project is.
    4. Project plans, if any.
---

# Navigation through the commits.
---

## Hash - what is it?

* If you run 'git log' and look on the history of the committing, you will see on the first line of the message commits' hashes, or in other words their IDs. They include 40 letters and number unique combination.
* These hashes can be used further to run commands on a particular commit.
* So, has is the main identifier of the commit. It includes encoded data about the commit:
    - when the commit was made, 
    - the contents of the files in the repository at the time of the commit
    - a link to the previous, or parent, commit.
* Git hashes (converts) commit information using the SHA-1 algorithm (Secure Hash Algorithm). 
* If a hash is obtained twice for the same set of input data, the result is guaranteed to be the same. <br>
---