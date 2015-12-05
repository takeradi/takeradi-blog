title: Multiple Git accounts on one PC
date: 2015-12-04 12:41:19
tags: ['Git']
categories: ['Version Control']
---

What do you when you have to manage multiple Git accounts on the same PC? I face the same situation for managing my work and personal Git accounts. Github recommends [merging both the accounts](https://help.github.com/articles/merging-multiple-user-accounts/) and managing all your repos from one account.

What if you still want to manage them seperately?
<!--more-->
You could follow these steps:

1. Set up one of the accounts (the more frequently used one) with the global config. Refer to this [Github documentation](https://help.github.com/articles/set-up-git/). This will save you the pain of authenticating every time you want to commit something.

2. For your second account, override the global config by a local one everytime you create a repo. While this might be a bit longer (2 extra commands for god's sake!), it saves you from merging both the accounts and helps you manage both the accounts in a cleaner fashion. Following are the steps to override the global config by a local one:

    ```
    ✝  ~/takeradi/blog -- master± > git config user.name takeradi
    ✝  ~/takeradi/blog -- master± > git config user.email sampleemail@sampleemail.com
    ```
    _Note: The above steps should be performed inside the newly created repo before committing/pushing anything to your Git remote repo._

Hope this helps!
