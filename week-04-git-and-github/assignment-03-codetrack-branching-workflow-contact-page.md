Assignment 3 — CodeTrack: Branching Workflow (Add & Verify a Contact Page)


Task 1 — Confirm Repository State and Default Branch

Screenshot 1 — Output of `git status` and `git branch` showing a clean status and the default branch checked out

<img src="screenshots\Task_3_1_1.png">

Task 2 — Create and Switch to a Feature Branch

Screenshot 2 — Output of `git checkout -b feature/contact-page` and `git branch` showing `* feature/contact-page`


<img src="screenshots\Task_3_2_2.png">

Task 3 — Add contact.html on the Feature Branch


Screenshot 3 — Output of `ls` showing `contact.html`

<img src="screenshots\Task_3_3_3.png">

Screenshot 4 — Output of `git commit`

<img src="screenshots\Task_3_3_4.png">

Screenshot 5 — Output of `git log --oneline -3` showing the new commit

<img src="screenshots\Task_3_3_5.png">

Task 4 — Add the Contact Link to index.html

Screenshot 6 — Output of `git status` showing `index.html` as modified before staging

<img src="screenshots\Task_3_4_6.png">

Screenshot 7 — Output of `git commit`

<img src="screenshots\Task_3_4_7.png">

Screenshot 8 — Browser showing the Contact Page link on the homepage while on `feature/contact-page`

<img src="screenshots\Task_3_4_8.png">

Task 5 — Verify Isolation (Prove the Default Branch Is Unchanged)

Screenshot 9 — Terminal showing the checkout and `ls` output, proving `contact.html` is absent

<img src="screenshots\Task_3_5_9.png">

Screenshot 10 — Browser showing the homepage on the default branch with no Contact Page link

<img src="screenshots\Task_3_5_10.png">

Task 6 — Merge the Feature Branch into the Default Branch

#### Screenshot 11 — Output of `git merge feature/contact-page`

<img src="screenshots\Task_3_6_11.png">

Screenshot 12 — Output of `ls` showing `contact.html` after the merge

<img src="screenshots\Task_3_6_12.png">

Screenshot 13 — Browser showing the Contact page opened from the homepage link on the default branch

<img src="screenshots\Task_3_6_13.png">

Task 7 — Inspect History (Graph View)

Screenshot 14 — Full output of `git log --oneline --graph --decorate --all`

<img src="screenshots\Task_3_7_14.png">

Task 8 — Optional Cleanup (Delete the Feature Branch)

Screenshot 15 (Optional) — Output showing `feature/contact-page` deleted and no longer listed

<img src="screenshots\Task_3_8_15.png">


