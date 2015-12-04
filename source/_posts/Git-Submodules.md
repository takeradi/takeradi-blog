title: Git Submodules
date: 2015-12-04 08:26:41
tags:
---

# Initialize your Git Repository

```
✝  ~/takeradi/blog  git init
Initialized empty Git repository in /Users/adityab/takeradi/blog/.git/
```

# Fork the 3rd party repo to your GitHub account
The reasons why I chose to for the 3rd party repo to my own Github account is because I didn't have permission to push to the 3rd party vendor's repo. Of course! Who would give you the permission to do that! And I wanted to customize the library according to my needs. Many Stackoverflow users have faced this [issue](http://stackoverflow.com/questions/12309884/make-changes-to-a-git-submodule-and-then-add-those-into-my-main-project) and I have found this to be the best way to customize the library to my needs. If in the future, I want to sync the updates from the 3rd party vendor into my fork, I will just have to perform these [steps](https://help.github.com/articles/syncing-a-fork/) mentioned on GitHub

# Add the forked module as a submodule into my main project
```
✝  ~/takeradi/blog   master±  git submodule add https://github.com/takeradi/hexo-theme-next.git themes/next
Cloning into 'themes/next'...
remote: Counting objects: 4802, done.
remote: Total 4802 (delta 3), reused 3 (delta 3), pack-reused 4798
Receiving objects: 100% (4802/4802), 9.69 MiB | 1.77 MiB/s, done.
Resolving deltas: 100% (2496/2496), done.
Checking connectivity... done.
```

# Customize the submodule

## Make the changes and check git status
```
✝  ~/takeradi/blog/themes/next   master±  git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
 (use "git add/rm <file>..." to update what will be committed)
 (use "git checkout -- <file>..." to discard changes in working directory)

   deleted:    languages/de.yml
   deleted:    languages/fr-FR.yml
   deleted:    languages/pt.yml
   deleted:    languages/ru.yml
   deleted:    languages/zh-Hans.yml
   deleted:    languages/zh-hk.yml
   deleted:    languages/zh-tw.yml
```

## Stage, Commit, and Push the submodule to its master
```
✝  ~/takeradi/blog/themes/next   master±  git add .
✝  ~/takeradi/blog/themes/next   master±  git commit -m "Removed language support"
[master 32ca4fa] Removed language support
7 files changed, 493 deletions(-)
delete mode 100644 languages/de.yml
delete mode 100644 languages/fr-FR.yml
delete mode 100644 languages/pt.yml
delete mode 100644 languages/ru.yml
delete mode 100644 languages/zh-Hans.yml
delete mode 100644 languages/zh-hk.yml
delete mode 100644 languages/zh-tw.yml
✝  ~/takeradi/blog/themes/next   master  git push origin master
Username for 'https://github.com': takeradi
Password for 'https://takeradi@github.com':
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 318 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
To https://github.com/takeradi/hexo-theme-next.git
  0881139..32ca4fa  master -> master
```

# Check the status of the main project
```
✝  ~/takeradi/blog   master±  git status
On branch master

Initial commit

Changes to be committed:
 (use "git rm --cached <file>..." to unstage)

   new file:   .gitmodules
   new file:   themes/next

Changes not staged for commit:
 (use "git add <file>..." to update what will be committed)
 (use "git checkout -- <file>..." to discard changes in working directory)

   modified:   themes/next (new commits)

Untracked files:
 (use "git add <file>..." to include in what will be committed)

   .gitignore
   _config.yml
   package.json
   scaffolds/
   source/
```

If you notice carefully, a new file named `.gitmodules` has been created. This gets created when you add a submodule to your main project. If you view that file, you will see the references to the submodule:
```
✝  ~/takeradi/blog   master±  cat .gitmodules
[submodule "themes/next"]
   path = themes/next
   url = https://github.com/takeradi/hexo-theme-next.git
```

# Stage, Commit, and Push the main project to master
