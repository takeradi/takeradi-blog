title: Git Submodules
date: 2015-12-04 08:26:41
tags: ['Git']
categories: ['Version Control']
---
This post aims to ease the pain that one might feel while trying to understand [Git Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules). It is an advanced Git topic but it really isn't that difficult to understand.

I will try to demonstrate Git Submodules through an example. Imagine that you have to create a project and use a third party library inside that project. You also want to customize the 3rd party library according to your needs. How do you approach this problem? Using Git Submodules! Let's look at the example:

<!--more-->
<hr/>
# Initialize your Git Repository:<p/>
```
✝  ~/takeradi/blog > git init
Initialized empty Git repository in /Users/adityab/takeradi/blog/.git/
```
<p/>
<hr/>
# Fork the 3rd party repo to your GitHub account:<p/>

The reason why I chose to fork the 3rd party repo to my own Github account is because I didn't have permission to push to the 3rd party vendor's repo. Who in their right state of mind would give me or you the permission to do that! And I wanted to customize the library according to my needs. Many stackoverflow users have faced this [issue](http://stackoverflow.com/questions/12309884/make-changes-to-a-git-submodule-and-then-add-those-into-my-main-project) and I have found this to be the best way to customize the library to my needs. If in the future, I want to sync the updates from the 3rd party vendor into my fork, I will just have to perform these [steps](https://help.github.com/articles/syncing-a-fork/) mentioned on GitHub.


<hr/>
# Add the forked module as a submodule into my main project:<p/>
```
✝  ~/takeradi/blog -- master± > git submodule add https://github.com/takeradi/hexo-theme-next.git themes/next
Cloning into 'themes/next'...
remote: Counting objects: 4802, done.
remote: Total 4802 (delta 3), reused 3 (delta 3), pack-reused 4798
Receiving objects: 100% (4802/4802), 9.69 MiB | 1.77 MiB/s, done.
Resolving deltas: 100% (2496/2496), done.
Checking connectivity... done.
```
<p/>

<hr/>
# Customize the submodule:<p/>

## _- Make the changes and check git status:_


```
✝  ~/takeradi/blog/themes/next -- master± > git status
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

## _- Stage, Commit, and Push the submodule to its master:_


```
✝  ~/takeradi/blog/themes/next -- master± > git add .
✝  ~/takeradi/blog/themes/next -- master± > git commit -m "Removed language support"
[master 32ca4fa] Removed language support
7 files changed, 493 deletions(-)
delete mode 100644 languages/de.yml
delete mode 100644 languages/fr-FR.yml
delete mode 100644 languages/pt.yml
delete mode 100644 languages/ru.yml
delete mode 100644 languages/zh-Hans.yml
delete mode 100644 languages/zh-hk.yml
delete mode 100644 languages/zh-tw.yml
✝  ~/takeradi/blog/themes/next -- master > git push origin master
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
<p/>

<hr/>
# Check the status of the main project:<p/>


```
✝  ~/takeradi/blog -- master± > git status
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

If you notice carefully, you will see two things:
1. a new file named `.gitmodules` has been created. This gets created when you add a submodule to your main project. If you view that file, you will see the references to the submodule:

    ```
    ✝  ~/takeradi/blog -- master± > cat .gitmodules
    [submodule "themes/next"]
       path = themes/next
       url = https://github.com/takeradi/hexo-theme-next.git
    ```
2. The `new commits` message which indicates that a submodule has been created and needs to be committed.


<hr/>
# Stage, Commit, and Push the main project to master:<p/>
```
✝  ~/takeradi/blog -- master± > git add .
 ✝  ~/takeradi/blog -- master± > git commit -m "Initial commit of the blog"
[master (root-commit) c17cc19] Initial commit of the blog
 10 files changed, 257 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 .gitmodules
 create mode 100644 _config.yml
 create mode 100644 package.json
 create mode 100644 scaffolds/draft.md
 create mode 100644 scaffolds/page.md
 create mode 100644 scaffolds/post.md
 create mode 100644 source/_posts/Git-Submodules.md
 create mode 100644 source/_posts/hello-world.md
 create mode 160000 themes/next
 ✝  ~/takeradi/blog -- master > git remote add origin https://github.com/takeradi/takeradi-blog.git
 ✝  ~/takeradi/blog -- master > git push -u origin master
Username for 'https://github.com': takeradi
Password for 'https://takeradi@github.com':
Counting objects: 15, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (10/10), done.
Writing objects: 100% (15/15), 3.77 KiB | 0 bytes/s, done.
Total 15 (delta 0), reused 0 (delta 0)
To https://github.com/takeradi/takeradi-blog.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

If you look at the GitHub repository you will see the hash of the commit linking to the commit of the forked repo that the submodule links to. Something like this:

The above screenshot shows `32ca4fa` as the hash of the commit which is referenced in the forked repo. Clicking on it will take you to that commit.

![Submodule hash link](/images/04122015/Git_Submodule_Hash.png)

In fact, if you dig deeper, you will notice that the commit that was pushed from the main project was in fact the complete hash of the commit in the forked repo as shown below:

![Complete hash of the forked repo](/images/04122015/Git_Hash_Link.png)
<hr/>
# Customizing the library further:<p/>
If you want to continue customizing the 3rd party library, you just have to follow the same steps again:
1. Stage, commit and push changes in the library
2. Change directory to the main project and check git status. You will see something like this:

    ```
    ✝  ~/takeradi/blog -- master± > git status
    On branch master
    Your branch is up-to-date with 'origin/master'.
    Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git checkout -- <file>..." to discard changes in working directory)

       modified:   source/_posts/hello-world.md
       modified:   themes/next (new commits)

    no changes added to commit (use "git add" and/or "git commit -a")
    ```

    The `new commits` message now indicates that the submodule was updated. This updates the hash linking the submodule in your main project to point to the commit which is referenced on the forked module as shown below:

    ![Git Hash Update](/images/04122015/Git_Hash_Update.png)

3. Stage, commit and push these changes in the main project.

Simple!
<hr/>
# Closing Thoughts:<p/>


Thats it! It sucks that you have to jump through so many hoops to do this but IMHO, this is the best way (atleast that I know of). Forking enables you to sync and consume the upstream changes at a later stage of your development. Forking also enables you to customize and keep those changes on your repo for use into other projects.

Also, I have heard that there is a better way to this but its currently in the works. Its called [git-subtree](https://github.com/apenwarr/git-subtree) and it has been merged to the main [Git](https://github.com/git/git/tree/master/contrib/subtree) repo. As soon as I get a hang of git-subtree, I will post an alternative way complete this whole process. Let me know what you guys think!
