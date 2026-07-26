Assignment 1 — CodeTrack: Initial Git Setup (Local Only)

Task 1 — Create the CodeTrack Project and Initialize Git

Screenshot 1—Output of `git init` inside `CodeTrack` showing "Initialized empty Git repository"

<img src="screenshots\Task_1_1.png">

Screenshot 2 — Output of `ls -a` showing the `.git` folder

<img src="screenshots\Task_1_2.png">

Notes

**1. What is the `.git` folder, and why does it matter?**
The .git folder is a hidden directory created by git init that stores your entire repository's history — commits, branches, config, and the staging area. It's what makes a folder an actual Git repository; without it, Git commands won't work at all. Never edit it manually, and deleting it wipes your project's version history (though your actual files remain).

Task 2 — Configure Git Identity Locally (Repository-Only)

Screenshot 3 — Output of `git config --local --list` showing your `user.name` and `user.email`

<img src="screenshots\Task_2_1.png">

# Task 3 — Configure Git Identity Globally

Screenshot 4 — Output of `git config --global --list` showing your `user.name` and `user.email`

