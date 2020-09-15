
[Reference Link](https://dev.to/unseenwizzard/learn-git-concepts-not-commands-4gjc)


## Getting a Remote Repository

**git clone:** Clone the remote repository to your local

    git clone https://github.com/{YOUR_USER_NAME}/git-commands.git

**git status:** it shows the current details like branch-name, state of the branch and untracked files.

    git status


 - If you already staged the files again doing the changes:- `git status --staged`
 - git status will show two status like,
 - the one we already staged where we added text, and the one we just made, which is   still only in the working directory.
   
**git add file-name:** Adds the file to the staging area. In which you collect the all changes you wish to put into repository.

    git add file-name
    
   

**git commit:** Whatever changes made on this branch saved with the some message and it is stored in the local repository.

    git commit -m "commit message"

**git push:** In order to share your commits with the Remote Repository you need to push them.

    git push

**git diff:** 

    git diff

 - See what has changed in your Working Directory
 - git diff operates on the changes in your Working Directory only.
 - `git diff --staged `     it prints the difference in the staging area

**git log:**

 - If we have a look at the git log we'll not only see a list of all the commits with their hash as well as Author and Date, we also see the state of our Local Repository and the latest local information about remote branches. 
 -  `git log`

**git diff <commit>^! :** 

 - To compare the git commits (^!) compare with  one before.
 - **git diff [commit-hash-old ] [commit-hash-new]** to compare any changes between two commits.

**git branch <branch name>**

 - We want to share that change, but not put it on master right away.
 - `git branch branch-name`
 - You can think of branches in git as pointers, pointing to a series of commits.
 - When you commit, you add to whatever you're currently pointing to.
 - In fact the state your Local Repository is currently at, can be viewed as another pointer, called HEAD, which points to what branch and commit you are currently at.

**git checkout :**

 - To switch to our new branch you will have to use git checkout branch-name.
 -  What this does is simply to move the HEAD to the branch you specify.
 - So to create and switch to new branch, we could also just have called `git checkout -b branch-name`.

**upstream branches and remotes :**

 - Git setup the remote of your Local Repository to be the Remote Repository you cloned and gave it the default name origin.
 - Then it copied the remote branches into your Local Repository and finally it checked out master for you.
 -  When you checkout a branch name that has an exact match in the remote branches, you will get a new local branch that is linked to the remote branch. The remote branch is the upstream branch of your local one.

**git branch :**

 - you can see just the local branches you have
 - `git branch -a`  remote branches your Local Repository knows
 - `git push --set-upstream origin new-local--branch`  changes on our branch to a new remote.

**merge :**

 - Note that you always merge some branch into the one you're currently at.

**Fast-Forward merging**

 - from the master run `git merge new-branch ` ,it show fast-forward because there is not conflict, changes made in the new-branch sucessfully merged.
 - master will point to the latest commit once sucessful merge happen.
 
 **Merging divergent branches :**
 

 - Both master and change_alice originated from the same commit, but since then they diverged, each having their own additional commit.
 - Refer the images for better understanding. [Image](https://res.cloudinary.com/practicaldev/image/fetch/s--NKM59jTn--/c_limit,f_auto,fl_progressive,q_auto,w_880/https://raw.githubusercontent.com/UnseenWizzard/git_training/master/img/branches_diverge.png)

 - If you now git merge change_alice a fast-forward merge is not possible.
 -  Instead your favorite text editor will open and allow you to change the message of the merge commit git is about to make in order to get the two branches back together.
 - The new commit introduces the changes that we've made on the change_alice branch into master.

**Resolving conflicts :**

 - The same line has changed on both of the branches, and git can't handle this on it's own.
 - On top you see what has changed in Bob.txt on the current HEAD, below you see what has changed in the branch we're merging in.

**Rebasing :**

 - Git has another clean way to integrate changes between two branches, which is called rebase.
 - merge introduces a merge commit in which the two histories get integrated again.
 - rebasing just changes the point in history (the commit) your branch is based on.
 - Now let's checkout add_patrick again, and get that change that was made on master into the branch we work on!
 - `git rebase master` from the already created branch
 - So HEAD moves from the 0cfc1d2 commit, to the 7639f4b commit that is at the head of master.
 - Then rebase applies every single commit we made on our add_patrick branch to that.
 - After that it does a checkout of the latest commit of the branch you're rebasing on, and then applies each of the stored changed as a new commit on top of that.
 - Using rebase you can make sure that you frequently integrate the changes other people make and push to master, 
 - while keeping a clean linear history that allows you to do a fast-forward merge when it's time to get your work into the shared branch.
 - `git log --graph` cleaner way to display the commits logs.
 - Simply add the changes to the Staging Environment and then `git rebase --continue`. 
 - As when merging, **you can always stop and drop everything you've done** so far when you git rebase --abort.

**Updating the Dev Environment with remote changes: **


**git fetch :**
 - To get changes made to the Remote into your Local Repository you use git fetch.

**Pulling Changes :**

 - `git pull` - Get the remote changes directly into local directory files. It will do git fetch as well as git pull.
 - In case of any local changes , it will not override ask to commit or stash the changes.
 
 **Stashing changes :**
 

 - A git stash is basically a stack of changes on which you store any changes to the Working Directory.
 - `git stash pop` which takes the latest change that was stashed and applies it the to the Working Directory again.
 - `git stash apply`, which doesn't remove them from the stash before applying them.
 - To inspect you current stash you can use `git stash list` to list the individual entries, and `git stash show` to show the changes in the latest entry on the stash.
 - `git stash branch {BRANCH NAME}`, which creates a branch, starting from the HEAD at the moment you've stashed the changes, and applies the stashed changes to that branch.

**Cherry-picking :**

 - Whenever you want to just take a few choice changes from one branch and apply them to another branch, you want to cherry-pick these commits and put them on your branch.
 - `git cherry-pick commit-id`

 - c`herry-pick <from>..<to>` also possible
 - 
**Rewriting history**

 - The 'history' of a branch is made up of all it's commits.
 
 **Amending the last Commit**
 - One way to fix both of these in one go would be to amend the commit we've just made.
 - Amending the latest commit basically works just like making a new one.
 - `git commit --amend`.
 - As you've certainly expected by now, the commit hash is different. The original commit is gone, and in it's place there is a new one, with the combined changes and new commit message.
 
 **Interactive Rebase :**
 

 - Unlike most others, the interactive rebase is something you'll probably be using a lot, as it allows you to change history as much as you want.
 - `git log --oneline`, we'll see our three commits on top of whatever was on your master.
 - As I've highlighted that so suggestively, you're probably ready to try `git push --force` right now. You really shouldn't do that if you want to rewrite public history safely though!
 - You're much better off using --force's more careful sibling `--force-with-lease !`

**Reading history**

 - Luckily git has your back, by having a built in safety feature called the Reference Logs AKA `reflog`.

 - Whenever any reference like the tip of a branch is updated in your
   Local Repository a Reference Log entry is added.

 