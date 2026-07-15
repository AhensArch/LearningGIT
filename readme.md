
### version of git
```
git --version
```

### Set username on local so if anything goes wrong we know who to blame
```
git config --global user.name "Ahens"
```

### Set email ID on local
```
git config --global user.email "ahens@mail.com"
```

### Initialize the local working directory
```
git init
```

### setting default branch to main, it was master before
```
git config --global init.defaultBranch main
```

### to check the what is going on currently in git means files are tracked or untracked
```
git status
```

### To add untracked file to tracked
```
git add <filename>
```

### tracking all files
```
git add .
```

### Taking snapshot of project so if you break something you will have the backup
```
git commit -m "message"
```

### To see commit ID, who did it means author and date and time
```
git log
commit 53f34e0bae00c6f7fe24f55e043cd638fe960289 (HEAD -> main)
Author: Sneha <sneha@gmail.com>
Date:   Wed Jul 15 10:44:55 2026 +0400

    added Hello.js and test.js

commit dcf116cc90f685fd7cbf1393ca28237c9d4fe574
Author: Sneha <sneha@gmail.com>
Date:   Wed Jul 15 10:43:29 2026 +0400

    Added readme.md
```

### If you want to go back on previous commit(It will create a new branch, dont worry your changes are safe. It just your HEAD is not on your latest)
```
➜  LearningGit git:(main) git checkout dcf116cc90f685fd7cbf1393ca28237c9d4fe574
Note: switching to 'dcf116cc90f685fd7cbf1393ca28237c9d4fe574'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at dcf116c Added readme.md

➜  LearningGit git:(dcf116c)
```

### To go back to current or latest HEAD
```
➜  LearningGit git:(dcf116c) git checkout main
Previous HEAD position was dcf116c Added readme.md
Switched to branch 'main'
➜  LearningGit git:(main) git log
```
### If you made any changes when you were on other HEAD you can use
```
➜  LearningGit git:(main) git checkout -f main
Already on 'main'
➜  LearningGit git:(main)
```

### Two Types of Directories
```
1. Local Repository - Its on you system where you do your work, you initilize it by "git init". Its private until you push it to remote.

2. Remote Repository - Common system which uses everyone, you work you push changes to this. eg. Github, Gitlab
```
### You can add your remote repo to your local system as remote "origin" (you can name it anything)
```
LearningGit git:(main) ✗ git remote add origin https://github.com/AhensArch/LearningGIT.git
```

### Now push your changes
```
➜  LearningGit git:(main) ✗ git push -u origin main
Enumerating objects: 13, done.
Counting objects: 100% (13/13), done.
Delta compression using up to 10 threads
Compressing objects: 100% (10/10), done.
Writing objects: 100% (13/13), 3.25 KiB | 3.25 MiB/s, done.
Total 13 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/AhensArch/LearningGIT.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```
### To create a new branch
```
LearningGit git:(main) ✗ git branch branch-name
```

### To change the branch
```
➜  LearningGit git:(main) ✗ git checkout branch-name 
M       .idea/workspace.xml
Switched to branch 'branch-name'
```

### To create a branch name and switch to it.
```
➜  LearningGit git:(main) ✗ git checkout -b feature-branch
Switched to a new branch 'feature-branch'
➜  LearningGit git:(feature-branch) ✗ 
```

Note - When you create a new branch it will have code from branch it was created. So you want to take code from another branch use,
```
➜  LearningGit git:(main) ✗ git branch new-branch-name source-branch
```

### When you create a new branch, it will not appear and github will not track changes it in autoamtically. You have to push it.
```
➜  LearningGit git:(feature-branch) git push --set-upstream origin feature-branch 
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote: 
remote: Create a pull request for 'feature-branch' on GitHub by visiting:
remote:      https://github.com/AhensArch/LearningGIT/pull/new/feature-branch
remote: 
To https://github.com/AhensArch/LearningGIT.git
 * [new branch]      feature-branch -> feature-branch
branch 'feature-branch' set up to track 'origin/feature-branch'.

OR

➜  LearningGit git:(feature-branch) git push -u origin feature-branch 
branch 'feature-branch' set up to track 'origin/feature-branch'.
Everything up-to-date
```

### If someone made changes in new then you have to sync those changes with your local working directory
```
➜  LearningGit git:(feature-branch) ✗  git pull
Already up to date.
```

### When you push another branch or change in it, a pull request is created. Pull request lets you share your changes with your team for review and feedback. Once approved your changes will merge into main branch to keep codebase stable and orgnise.
### Once you merge the changes to main branch you can delete the branch.

## Normal Github workflow for you -
1. Clone the repo.
2. Create a new branch from the main or another branch.
3. Make your changes.
4. Push the branch to the remote repo.
5. Open a Pull Request.
6. Merge the changes.
7. Pull the merged changes into your local main branch.
8. Repeat from step 2.

---
# Merge Conflict -
### Sometimes two or more devs added same line of code, GIT gets confuse, this is called merge conflict.
### Git will ask you whose changes you want to keep ?
### This is where you will resolve the Conflict.
---

# Life saving commands, if you broke the production -

### If you want delete/or modify all commits after a specific commit, use "git reset"

1. Soft reset - It will remove the commits from history but those commits will be in staging-working directory. This is tracked commits. (after we do git add)
```
git reset --soft <commit-hash>
```
2. mixed reset - This is default reset. This will remove the commits and keep it in the working directory. (This is before git add)
```
git reset <commit-hash>
```
3. hard reset - It will discard all the commits after the specified commit in the command. It wont be in staging neither in working directory.
```
git reset --hard <commit-hash>
```

### git revert -  This is similar to reset but one twist, This will remove the changes you made but it will not remove the commit history from git log. Also you have to add revert commit message in this.
```
➜  LearningGit git:(main) git revert 37f8ddd72834ba50c14211bb5feac2bb2e11d453
[main 137c98a] Revert "git revert"
 2 files changed, 52 insertions(+), 54 deletions(-)
➜  LearningGit git:(main) git log
 commit 137c98a94bbcf8d5d9003be69cf12f932d751119
Author: ahens <ahens@mail.com>
Date:   Wed Jul 15 13:32:25 2026 +0400

    Revert "git revert"
    
    This reverts commit 37f8ddd72834ba50c14211bb5feac2bb2e11d453.
    
    Demo of revert

commit 37f8ddd72834ba50c14211bb5feac2bb2e11d453
Author: ahens <ahens@mail.com>
Date:   Wed Jul 15 13:31:42 2026 +0400

    git revert

 ```

### git stash - Consider you are working on something but there is an urgent issue and you want to work on that. so you will use git stash on your current work so you can move to the issue. git stash lets you save uncommited changes to staged or unstaged working directory temporarily without actually commiting them.
```
➜  LearningGit git:(main) ✗ git stash
Saved working directory and index state WIP on main: 6f09290 Revert "Demo of revert again"
```
You worked on issue - commit those changes but now you want to work on earlier thing.
```
➜  LearningGit git:(main) git stash list
➜  LearningGit git:(main) git stash apply stash@{0}
Auto-merging Hello.js
CONFLICT (content): Merge conflict in Hello.js
On branch main
Your branch and 'origin/main' have diverged,
and have 6 and 3 different commits each, respectively.
  (use "git pull" if you want to integrate the remote branch with yours)
Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
        both modified:   Hello.js
no changes added to commit (use "git add" and/or "git commit -a")
➜  LearningGit git:(main) ✗ 
```
It will create a conflict but you can resolve it.


