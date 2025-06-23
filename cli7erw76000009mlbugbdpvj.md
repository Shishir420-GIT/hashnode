---
title: "GIT in simple terms"
seoTitle: "GIT, BIGINNERS"
seoDescription: "GIT explanation for biginners:
What is GIT or Global Information Tracker?

Git is a version control system. Plain and simple, you don't need to make it comp"
datePublished: Sun May 28 2023 12:40:07 GMT+0000 (Coordinated Universal Time)
cuid: cli7erw76000009mlbugbdpvj
slug: git-in-simple-terms
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/UT8LMo-wlyk/upload/9f47c251ed1aed09a022d580e4140262.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1685277542567/57af81c3-f3eb-4e73-864c-76c27453d864.png
tags: repository, github, git, commands

---

### What is GIT or Global Information Tracker?

Git is a version control system. Plain and simple, you don't need to make it complex. I have talked about the version control system in this article- [version control system.](https://shishirslearningjourney.hashnode.dev/version-control-system)

A few points you can add to it would be:

* Git is a distributed version control system.
    
* Git is the most widely used and accepted VCS. That's it for now.
    

### How does GIT work?

GIT basically works in 4 steps,

* First, you put your files in one folder/place.
    
* Second, you stage(add) the files to be committed(to be added to your local system repository).
    
* Third, you commit the files/changes in the file to your local repository.
    
* Fourth, you push your local repository into your main repository (main server).
    

### How exactly to perform the above four steps?

The first thing to perform this is a GIT application, you can install GIT on your system by [clicking here](https://git-scm.com/download).

There is both a GUI and a CLI interface available for you to use If you are using a Windows machine, you can go ahead with either of those, depending on your convenience, on how you wish to use it. However, in this article, we will be focusing on the CLI interface only.

You can check if GIT is already installed in your system or not `'git --version'.`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685276130353/886e6b5d-3bc5-4f6d-ab7b-d438a3475dd0.png align="center")

Now, you choose the folder you wish to put your files in,

Then, initialise git inside it using the command - `'git init'`This will create an empty repository in your system in the '.git' folder along with the necessary folder structure.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685274834212/978c7166-0744-4ed0-bcaa-eb3057a25c0e.png align="center")

From there, everything is a game between you and your commands.

For example, we take a scenario where you now have to upload a complete project to your repository.

Let's say you have your files open in your git, and give the command `'cd /d/projects'` #*Do mind the case of the letters here, 'A' is not the same as 'a.*

Once you are inside the folder you wish to upload the files from, do a `'git add . '` A command to add all the files to the staging area.

What this means is that your work is done on the current files, and now you wish to move it to the local repository on your system. (It has not yet been moved yet, we need to commit it first.)

*Note: If you wish to add one file at a time into the staging area, then you can use the command* `'git add <filename>'.`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685274953188/fc67b189-dcb7-4d93-a284-f3fbcb85c1e6.png align="center")

*<mark>if you have accidentally staged a file and now wish to remove it, you can use the command </mark>* `'git rm --cached <filename>'.`

To check whether the files you have added have been added or not, use the `'git status'` command.

In its output, you'll be able to see the modified files (tracked file) in green color, those are the files that have successfully been staged(added), and if there is any file in that same folder that is not stagged(added) yet, then it will be shown in red color as an untracked file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685275023532/9169c7b5-ac8b-44a7-89d1-a8900907f96c.png align="center")

Now that you have your files staged, the next step is to move them to your local repository.

Use the command `'git commit -m "Meaningful message" '`In this command, the value in quotes, you should use a message which helps others or you in later stages understand what this change is about.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685275109966/582fb913-72f0-434f-ab7b-233282e7429c.png align="center")

*Note: Post executing the above command, if you run* `'git status'`*You will get a result that says, 'Work tree clean', which means that your changes have now moved from your staging area to your local repository.*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685275156456/44e06fd9-f38e-4ad8-9f6c-6fda119e1c33.png align="center")

So, even if you now lose the main files stored in your system, you still have a copy of it in your local repository.

As for the last step here, now you need to upload the files to your main remote repository so that your peers/teammates can work on it.

In order to do that, use the command `'git push origin <BranchName>'.` Typically, it is the main branch.

Please keep this in mind, though, as a best practice, you should not commit anything directly to the main branch; you should always create a new branch, work on it, and create a pull request to merge it into the main branch post the review of your code.

### How to create a new branch?

You can manually create a new branch in your repository by clicking the new branch button (see the green button below the screenshot).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685274197311/18cc8050-b3b7-49b1-a4cb-c9a3ab3596d2.png align="center")

Or you can create it from your CLI by issuing the command `'git checkout -b <BranchName>'.`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685275361367/25075cc2-6b50-43ff-b665-13b6218313ac.png align="center")

Note: To switch to another existing branch ,you can use `'git switch AnotherBranch'.`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685275450768/9cbeee07-6c54-49d7-b00e-a684f38186d6.png align="center")

### Authentication:

When you commit the changes to your repository, your server should be able to identify that it is you only who is making those changes, hence you need to authenticate yourself.

You need to do the below setup before being able to do any push or pull on your remote repository.

* Add your username and email using the `git --config` command.
    
* Set Username: `git config --global` [`user.name`](http://user.name) `"shishir"`
    
* Set an email address: `git config --global` `user.email` `"`[`Shishir.workemail@gmail.com`](mailto:Shishir.workemail@gmail.com)`”`
    
* You can also generate SSH Keys and add them to your system. Read about it in detail on their official page - [click here to read](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).
    

*In my personal opinion, it is better to use a credential manager; you only need to log in the first time, post that the authentication is taken care of by the credential manager. Password-based authentication is prone to a lot of errors (GitHub doesn't support it as well post-2021), and it is easier than generating the SSH keys and using them.‍*

---

---

Hope I was able to explain the process well. If in any case you still face any issues, please feel free to reach out to me, I'd be happy to help.

*You can always connect with me over LinkedIn to share feedback or queries by* [clicking here](https://www.linkedin.com/in/shishir-srivastav/)*.*

---

---

Thanks for coming this far in the article. I hope I was able to explain the concept well enough. If you face any issues, please feel free to reach out to me; I'd be happy to help.

## 🔗 Let’s stay connected!

[**🌐 Linktree**](https://linktr.ee/shishirsrivastav)| [**🐦 X**](https://x.com/shishir_who)| [**📸 Instagram**](https://www.instagram.com/programmatic.ly)| [**▶️ YouTube**](https://www.youtube.com/channel/UCCZiCzPtg9pmDwChJ4ROIpA) [**✍️ Hashnode**](https://hashnode.com/@ShishirSrivastav)| [**💻 GitHub**](https://github.com/Shishir420-GIT)| [**🔗 LinkedIn**](https://www.linkedin.com/in/shishir-srivastav)| [**🤝 Topmate**](https://topmate.io/shishir_srivastav) [**🏅 Credly**](https://www.credly.com/users/shishir-srivastav-who)

© 2024 Shishir Srivastav. All rights reserved.