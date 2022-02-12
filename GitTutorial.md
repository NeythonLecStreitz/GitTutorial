<h1> 'Git' Good at Git: <br> A Beginner's Guide to Git </h1>

### By Neython Lec Streitz

---
### Table of Contents
 1. [What is Git?](#what-is-git)
 2. [Installing Git](#installing-git)
 3. [Git Essentials](#git-essentials)
	 - Creating a Project | `git init`
	 - Adding Files to a Project | `git status`
	 - Staging Files | `git add`
	 - Committing Files | `git commit`, `git log`
	 - Branching | `git branch`, `git checkout`
	 - Stashing | `git stash`
     - Merging | `git merge`
4. [Collaborating with Others](#collaborating-with-others)
5. [Cheat Sheet](#cheat-sheet)
6. [Works Cited and Additional Resources](#additional-resources)

---
##  What is Git?
Originally created by Linus Torvalds in 2019, **Git** is an open source **Distributed Version Control System (DVCS)**.
What this means is that the full history of changes of a project is copied to every developer working on their copy of the project, instead of only residing in one place.
As a version control system, Git lets you track changes to files, go back to old versions of files, and work collaboratively with others on the same files.

Compared to old version control systems and even modern alternatives, Git excels in security, performance, and flexibility.
It is now the standard version control tool.
It is important to note that Git is not the same as GitHub.
Git runs locally on your computer as a piece of software.
GitHub is a cloud-based service to host and manage Git repositories.

Now that we have a basic understanding, let's get into using Git!

---
## Installing Git
A more comprehensive explanation of installing Git can be found [here](https://git-scm.com/downloads).
For the sake of this tutorial, we will only cover installation via the stand-alone installers for Mac and Windows.
To verify whether or not Git is already installed, open a terminal and type:
```
$ git --version
```

### For Mac OS
1. The latest [Git installer for Mac](https://sourceforge.net/projects/git-osx-installer/) can be found [here](https://sourceforge.net/projects/git-osx-installer/).
2. Using the Git setup wizard, follow the prompts to complete installation.
3. Open a terminal to verify installation by typing:
	```
	$ git --version
	```
	```
	git version 2.33.0
	```
	Your version may be different.
4. To configure your Git username and email type:
	```
	$ git config --global user.name "Moe Schmoe"
	```
	```
	$ git config --global user.email "moeschmoe123@gmail.com"
	```
	These will be used when committing changes.

Alternatively, Git can be downloaded using [Homebrew](https://brew.sh/) and [MacPorts](https://www.macports.org/install.php).

### For Windows
1. The latest [Git Installer for Windows](https://gitforwindows.org/) can be found [here](https://gitforwindows.org/).
2. Using the Git Setup wizard, follow the prompts to complete installation.
3. Open a command prompt or Git Bash to verify installation by typing:
	```
	[user@localhost] $ | git --version
	                   | git version 2.28.0.windows.1
	```
4. 4. To configure your Git username and email type:
	```
	[user@localhost] $ | git config --global user.name "Moe Schmoe"
	[user@localhost] $ | git config --global user.email "moeschmoe123@gmail.com"
	```
---
## Git Essentials

As a motivated Computer Science student, lets say you've decided to start practicing common Python whiteboard questions in your spare time.
We begin by creating a folder for our new Git project, containing files with all of our practice solutions.

### Creating a Project | `git init`
Open a new terminal/command prompt and change to the directory you'd like to create a folder in.
For this example, we'll create the folder on our desktop.
```
[user@localhost] $ | cd Desktop
[user@localhost] $ | mkdir practice-problems
[user@localhost] $ | cd practice-problems
```
Now we have to initialize Git! Use the `git init` command:
```
[user@localhost] $ | git init
                   | Initialized empty Git repository in /Users/user/Desktop/practice-problems/.git/
```
You've just created your first **repository/repo**!

### Adding Files To A Project | `git status`

Our repo is empty, so let's add our first file, a simple README.txt text file.
Using your favorite text editor, create a new file and save it into your repo as `README.txt`.
There's not much to write here but it can look something like this:
```
- PRACTICE PROBLEMS -

This repository holds Python files for my whiteboard practice problems.
This is also the first file in my new Git repo!

```
Don't forget to save it.
To verify your file has saved and is in your folder, use `ls` in the command line while in your project directory.

Next, check the status of our repository using `git status`:
```
[user@localhost] $ | git status
                   |On branch master
                   |
                   | No commits yet
                   |
                   | Untracked files:
                   |   (use "git add ..." to include in what will be committed)
                   |		 README.txt
                   |
                   | nothing added to commit but untracked files present (use "git add" to track)
```
As you can see, Git is aware of the `README.txt` file in our practice-problems folder, but it has not been added to our repository yet.
In Git, there are essentially three different "trees" in your local repository.
The *Working Directory* holds your actual files and is where changes are initially saved, the *Staging Environment/Index* holds changes ready to be committed, and the *Head* points to the most recent commit.
We'll further explain these three sections soon!
> **Note:** <br>
> `git status` lets you see which files have been staged, which haven't, and which files aren't being tracked by Git.

### Staging Files | `git add`
So, let's make sure Git tracks our new file.
Whenever you're done working on a part of a project (editing a file, adding a new file, deleting an old file), its important to add the files to your Staging Environment.

> **Note:** <br>
> To **stage** a file in Git is to prepare it for a **commit**. That is, the **staging environment** allows you to choose what you'd like to package together into one cohesive commit. Imagine moving to a new house using a moving service. Likely, you'll selectively pack up items that logically go together before allowing the movers to take them to your new house. This is the benefit to staging! You can decide exactly what you want moving together (to the repository)!

We add files to the staging environment via the `git add` command:
```
[user@locahost] $ | git add README.txt
```
To make sure the add was successful, use `git status` once more:
```
[user@localhost] $ | git status
                   | On branch master
                   |
                   | No commits yet
                   |
                   | Changes to be committed:
                   |   (use "git rm --cached ..." to unstage)
                   |		 new file: README.md
```
Nice work!
Now, let's try it once more with a new file, `two-sum.py`.
Using your favorite IDE, create a new Python file named `two-sum.py`.
Two Sum is a classic whiteboard problem.
If you're unfamiliar with it and want to solve it yourself, find a description [here](https://leetcode.com/problems/two-sum/).
For our purposes, I present a possible Python brute-force solution:
 ```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
```
Go ahead and copy the code into your file.
Don't forget to save the file in your `practice-problems` directory.
Following the steps we used for our `README.txt` file, `add` the file to our staging area.

> **Note:** <br>
> When you want to **add** multiple files to the staging environment at once, use `git add -A` or `git add --all`.

Done adding our new file? Running the `git status` command should output:
```
[user@localhost] $ | git status
                   | On branch master
                   |
                   | No commits yet
                   |
                   | Changes to be committed:
                   |   (use "git rm --cached ..." to unstage)
                   |		 new file: README.md
                   |		 new file: two-sum.py
```
### Committing Files | `git commit`, `git log`
Now that we've finished adding our two new files, its time for us to save our changes as a snapshot of our repository.
That is, we're happy with the state of our project so we need to save it as a "version" of our project!
We do this using the `git commit` command.
It is important to always include a descriptive message with any commit so you (and any collaborators) know exactly what was changed:
```
[user@localhost] $ | git commit -m "Added README and two-sum solution."
                   | [master (root-commit) 09f4acd] Added README and first practice problem file
                   | 2 files changed, 11 insertions(+)
                   | create mode 100644 README.txt
                   | create mode 100644 two-sum.py
```
To view a complete history of commits for your repository, use the `git log` command:
```
[user@localhost] $ | git log
                   | commit 09f4acd3f8836b7f6fc44ad9e012f82faf861803 (HEAD -> master)
                   | Author: Joe Schmoe <joeschmoe@gmail.com>
                   | Date: Mon Feb 7 10:43:03 2022 -0800
                   |
                   | Added README and first practice problem file
```
Curious as to the long string of characters after `commit` in your output?
That's the **commit hash**.
It uniquely identifies every commit and is generated by Git using the complete status of your repository, including the files in your repo, the hash of your previous commit, the current date/time, and any other metadata.
Commit hashes are a big security feature for Git, as they maintain the integrity of your repo's history.
Changes to previous commits result in a cascade of changes for all the commits coming after.

### Branching | `git branch`, `git checkout`
**Branching** in Git is essentially creating a separate version of your main repository.
It allows you to work on features in isolation from the rest of your project.
The **master** branch serves as your default branch and is where completed changes are merged.

 As it turns out, our Two Sum solution is not efficient.
 It runs in O(n<sup>2</sup>)!
 Let's say we want to test out a more efficient solution, but we don't want to lose our current solution.
 That's where branching comes in to play.

To create a new branch, use the `git branch` command:
```
[user@localhost] $ | git branch two-sum-linear
```
This creates a new branch named `two-sum-linear`.
To see all the branches in our repository, once again type `git branch`:
```
[user@localhost] $ | git branch
                   | *master
                   |  two-sum-linear
```
Notice the branch we are currently in, the master branch, is identified by an asterisk.
To switch to our newly created branch, we use the `git checkout` command:
```
[user@localhost] $ | git checkout two-sum-linear
                   | Switched to branch 'two-sum-linear'
```
Using your favorite IDE, let's attempt to code a new solution that runs in O(n) time.
Go ahead and copy our new solution into your `two-sum.py` file:
```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        d = {}
        for i, v in enumerate(nums):
            if v in d:
                return d[v], i
            d[target - v] = i
```
Don't forget to save your file!
Type `git status` if you'd like to see what we've modified!

Now that we've written our new solution, lets stage and commit them to our `two-sum-linear` branch:
```
[user@localhost] $ | git add twoSum.py
[user@localhost] $ | git commit -m "Changed twoSum to run in linear time"
```

Good work!
We've now successfully committed our new solution to our `two-sum-linear` branch.

### Stashing changes to Commit Later | `git stash`
Now,  let's say we're feeling especially motivated today and want to start on a new practice problem.
Let's first return to the main branch:
```
[user@localhost] $ | git checkout master
                   | Switched to branch 'master'
```
Open an IDE and write up a new Python file for our new problem, **Palindrome Number** ([description here](https://leetcode.com/problems/palindrome-number/solution/)):
```
class Solution:
    def isPalindrome(self, x: int) -> bool:


	     return True

```
Oh!
We realized we never merged our `two-sum-linear` branch back to our master branch.
Since we have to leave soon, maybe its best we wait on working on this problem and make sure we finish up with `two-sum`.
We've written up the basic outline for our code, but our code is far from done.
Save your file as `palindrome-number.py`.

Because we haven't quite finished working on our solution, it doesn't make sense to commit our new file.
Instead, we can temporarily store our file to work on it later.
To do this, we use the `git stash` command.
Importantly, `git stash` will not work on files that are not currently being tracked without a special flag.
Thus, lets add our file and then stash it:
```
[user@localhost] $ | git add palindrome-number.py
[user@localhost] $ | git stash
                   | Saved working directory and index state WIP on master: f75470e Added README and first practice problem file
```
Go ahead and type `ls`.
As you can see, `palindrome-number.py` doesn't show up in our directory:
```
[user@localhost] $ | ls
                   | README.txt  two-sum.py```
```
With our file stashed away, we can now create new commits, switch to different branches, and make any other changes to our repository that we wanted to.
In general, stashing is most useful when you need to stop working on something to immediately work on a different part of your project.
We'll bring back our stashed change later.

> **Note:** <br>
> To stash away files that are tracked AND untracked use `git stash -u`. <br>
> To see a list of all your different current stashes, use `git stash list`. <br>
> To retrieve a specific stash, use `git stash pop stash@{num}`. <br>


### Merging Branches | `git merge`
Now that we've stashed our file away, lets merge our finished `two-sum-linear` branch into our `master` branch before we stop working on our project.
To do this, we use the `git merge` command.
From our `master` branch:
```
[user@localhost] $ | git merge two-sum-linear
                   | Updating f75470e..e0d722d
                   | Fast-forward
                   |  two-sum.py | 8 +++-----
                   |  1 file changed, 3 insertions(+), 3 deletions(-)
```
What we've done is take the changes we made in our `two-sum-linear` and apply them to our `master` branch.
Because no changes were made to our `two-sum.py` file while we worked on it in our other branch, Git simply sees our change as a continuation of `master`.
This is known as a *Fast-forward*.
If we were to run into a conflict between our master version and branch version, Git gives you the opportunity to see the differences and correct them manually.
Theoretically, it would look something like this:
```
[user@localhost] $ | git merge two-sum-linear
                   | Auto-merging two-sum.py
                   | CONFLICT (content): Merge conflict in two-sum.py
                   | Automatic merge failed; fix conflicts and then commit results
```
Using `git status` will confirm the conflict and then opening the file in an editor allows you to see the differences and correct them.

At any rate, now that our `master` branch and `two-sum-linear` branch are essentially the same, we can safely delete our `two-sum-linear` branch:
```
[user@localhost] $ | git branch -d two-sum-linear
                   | Deleted branch two-sum-linear (was e0d722d)
```
Notice the use of a `-d` flag to specify the deletion.
With everything in order, we can close our project to work on it another time.

If we felt up for it, we could bring back our `palindrome-number` stashed changes using the `git stash pop` command:
```
[user@localhost] $ | git stash pop
                   | On branch master
                   | Changes to be committed:
                   |   (use "git restore --staged <file>..." to unstage)
                   |         new file:   palindrome-number.py
                   | Dropped refs/stash@{0} (d7fd9dad1c856a5369e0f0ad261e51f509ff1f60)
```

And with that, we've covered all the basic features of Git.
Great job!

## Collaborating with Others

One last thing!
A major advantage of using Git is the ease of collaboration it gives you.
We'll briefly touch on a few of the commands that facilitate collaboration with remote repositories.

Instead of creating your own repo, lets say you're interested in downloading a local version of someone else's repo, perhaps a teammate's.
Their repo is likely hosted by GitHub or a similar cloud-based Git host.
For the purpose of this tutorial we will use a fake remote repo, but go ahead and find a GitHub repo yourself to download for practice!

To begin, use **cd** to change to the directory you'd like the new repo to reside in.
To download the repo, use the `git clone` command:
```
[user@localhost] $ | git clone https://github.com/NotARealUser1234/GitTutorial.git
                   | Cloning into 'GitTutorial'...
                   | remote: Enumerating objects: 3, done.
                   | remote: Counting objects: 100% (3/3), done.
                   | remote: Compressing objects: 100% (2/2), done.
                   | remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
                   | Unpacking objects: 100% (3/3), 751 bytes | 93.00 KiB/s, done.
```
With the repo now cloned, **cd** into it and you are now working in a local copy of the repository.
Make changes as if it were your own repository, because technically it is!

Once changes are finished, you can `commit` them like usual.
Now, if we want to send those changes to the remote repository, say for instance your friend is working on the project alongside you, we use the `git push [alias]` command:
```
[user@localhost] $ | git commit -a -m "Added collaboration section to GitTutorial.md"
                   | [master e7de78f] Updated GitTutorial.md.
                   | 1 file changed, 40 insertion(+), 3 deletion(-)
                   |
[user@localhost] $ | git status
                   | On branch master
                   | Your branch is ahead of 'origin/master' by 1 commit.
                   | (use "git push" to publish your local commits)
                   |
                   | nothing to commit, working tree clean
                   |
[user@localhost] $ | git push origin
                   | Enumerating objects: 9, done.
                   | Counting objects: 100% (8/8), done.
                   | Delta compression using up to 16 threads
                   | Compressing objects: 100% (5/5), done.
                   | Writing objects: 100% (5/5), 578 bytes | 578.00 KiB/s, done.
                   | Total 5 (delta 3), reused 0 (delta 0), pack-reused 0
                   | remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
                   | To https://github.com/AFakeUser1234/GitTutorial.git 5a04b6f..facaeae master -> master
```
As you can see, after committing the changes made to `GitTutorial.md`, our branch was 1 commit ahead of origin (the remote repository).
Thus, to sync the two, we used the `git push origin` command to send our changes to the remote repository.

What if your friend made changes to the remote repository as well?
That's where the `git pull` command comes in.
Technically, `git pull` is a combination of two separate commands: `git fetch` and `git merge`.
To begin, `git fetch [alias]` retrieves and displays all of the changes and branches of a remote repository.
Then, `git merge` integrates those new changes with your own local version of the repository:
```
[user@localhost] $ | git pull origin
                   |remote: Enumerating objects: 5, done.
                   |remote: Counting objects: 100% (5/5), done.
                   |remote: Compressing objects: 100% (3/3), done.
                   |remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
                   |Unpacking objects: 100% (3/3), 794 bytes | 1024 bytes/s, done.
                   |From https://github.com/AFakeUser1234/GitTutorial
                   |  a7cdd4b..ab6b4ed master -> origin/master
                   |Updating a7cdd4b..ab6b4ed
                   |Fast-forward
                   |  README.md | 2 ++
                   |  1 file changed, 2 insertions(+)
```
Thus, the `git push` and `git pull` commands allow you to collaborate easily with other people by letting you send changes and retrieve them.
For a more in depth explanation of collaborating using Git, see the [**Additional Resources**](#additional-resources) section.


## Cheat Sheet
#### Setup and Init
- `git init`: initialize an existing directory as a Git repo
- `git clone`: download a local repo of a remotely hosted repo

### Staging
- `git status`: displays files in your working directory and staging environment
- `git add [file]`: stages a file ready to be committed
- `git reset [ file]`: unstages a file without affecting anything else
- `git diff`: displays changes made but not staged
- `git commit -m "message"`: commits a file with a custom message and creates a new snapshot of your repository

### Branch and Merge
- `git branch`: displays a list of all your current branches (active branch has a *)
- `git branch [name]`: creates a new branch
- `git checkout [name]`: switch to a specific branch
- `git merge [branch]`: merges the specified branch into your current one
- `git log`: displays a history of all the commits in the branch history

### Stashing
- `git stash`: stash the current changes and return to a clean working directory
- `git stash list`: display list of stashed changes chronologically
- `git stash pop`: retrieve stashed changes from oldest stash
- `git stash pop [stash-name]`: retrieve specified stashed changes

### Collaborating and Updating
- `git fetch [alias]`: downloads and displays branches from Git remote repository
- `git pull`: fetch and merge commits from remote branch
- `git push [alias][branch]`: send local commits to remote repository

---
## Additional Resources
For more information on using Git, including more technical explanations or advanced use, check out these sources: <br>

- [Atlassian Learn Git with Bitbucket-cloud](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud)
- [GitHub Training Cheat Sheet](https://training.github.com/downloads/github-git-cheat-sheet/)
- [git - the simple guide](https://rogerdudler.github.io/git-guide/)
- [Git Tutorial/Documentation](https://git-scm.com/docs/gittutorial)
- [W3schools Git Tutorial](https://www.w3schools.com/git/default.asp?remote=github)



