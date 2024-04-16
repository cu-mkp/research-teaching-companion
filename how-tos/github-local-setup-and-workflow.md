# Setting up Github to work locally & general workflow

## Setting up Github
The following three steps only need to be conducted once per machine or repository you are working with.
### 1. Create a local workspace for Github repositories
We recommend creating a dedicated directory for Github in your home user directory. For Windows, it is usually, for example, `C:\Users\naomi\Github`, and for Macs, for example, `/Users/naomi/Github`.

### 2. Creating a private key to access your Github account
SSH is a security protocol that enables computers to talk to each other using public key cryptography. Each user is required to have a private and public key pair to securely access your Github account when working from the command line. 

To check if you already have this:
1. In your home directory, type: `ls -la`
2. Look for a directory called `.ssh`
     a. If you have this directory, you already have a key
     b. If you do NOT have this directory, you will need to make one.


To make a new key, you will need to:
1. Create a private/public key pair: https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/
2. Add it to your Github account: https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

### 3. Clone repository from Github (to make a local version)

Once your key has been set up and linked, all you need to do is clone (which is like downloading) a copy of the repository to your local Githun directory you created in step 1 above. 

You will need to copy the SSH address your repository - see [Cloning a Repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) for a visual guide of where this is on the repo homepage. Make sure to grab the SSH one and not the HTTPS or GitHub CLI addresses. It should look something like `git@github.com:cu-mkp/editioncrafter-data.git`.

In the command line, navigate to your Github directory, then do: `git clone [paste the SSH address here]`.
For example, `git clone git@github.com:cu-mkp/editioncrafter-data.git`

## Main workflow: setting up to work in a branch in a github project

1. Create issue (or find one already created)
2. Assign to someone (or yourself)
3. Open the command line
4. If you are using the Linux Subsystem for Windows, run the command:
     1. `winhome`
5. Navigate to the repository you want to work in, e.g., `m-k-manuscript-data`
     1. For example, if this is where you start: `/mnt/c/Users/naomi/`, run the commands:
     2. /mnt/c/Users/naomi/ `cd Github`
     3. /mnt/c/Users/naomi/Github/ `cd m-k-manuscript-data`
6. Pull the most updated version of the repository
     1. `git fetch`
     2. `git pull`
7. Create new branch titled &quot;issue[##]&quot; (no spaces or special characters)
     1. `git checkout -b [name of branch e.g. issue73]`
8. Make edits to repository files (in text editors such as Sublime, oXygen, or in whatever program suits the files you are working with)
9. Add file in local repository for tracking in github repository
     1. `git add .`
     2. `git commit -m '#[issue##]: [commit message]'` (this will ensure that this commit us linked to the issue you are working on)
10. Push to the remote server (for the first time, MUST BE TRACKED)
     1. `git push -u origin [branchname]`
11. Submit a pull request in github interface (browser) to merge your issue branch with master
     1. Go to the &quot;pull request&quot; tab where a message should appear asking if you would like to open a pull request
     2. Another option: In branch dropdown menu, select the branch you want to merge, then hit the &quot;new pull request&quot;
12. THC or NJR will merge the pull request unless there are conflicts to be resolved
13. Close the issue
14. `git checkout master` (= switch back to master branch)
     1. `git checkout main` (master/main depending on the repository)

## Other helpful commands

- `pwd` &quot;print working directory&quot; -- tells you where you are in the command line
- `ls` &quot;list&quot; -- tells you what files and folders are in the directory you are in
- `cd` &quot;change directory&quot; -- this followed by the name of the directory or a path will move you to that directory
- `cd ..` -- moves you up one directory
- `less` [name of file] script reader
- `q` &quot;quit&quot; -- exit out of a programming that is running

## Check what branch you are in and make sure it is correct

- See also [https://www.git-tower.com/learn/git/faq/checkout-remote-branch](https://www.git-tower.com/learn/git/faq/checkout-remote-branch)
- _Navigate into the desired directory (i.e. m-k-manuscript-data)_
- `git branch` _(tells you which branch you are in)_
- `git fetch` _(tells you what is happening in remote repo)_
- `git status` _(tells you which branch you&#39;re on and how far ahead or behind you are from Origin)_
- If status is behind, pull the most current version
     - `git fetch`
     - `git pull`
