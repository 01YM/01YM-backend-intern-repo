## Reflection 

### What does each command do?
- git checkout main -- <git_understanding>: this command restores the file, in this scenario the git_understanding file from main. Its useful if one file was messed up, you just take the working copy from main.  

- git cherry-pick <commit>: brings a commit from another branch into yours. Its useful if you want a feature thats been updated on a different branch or if you need the latest update on your branch as well.

- git log : just shows the commit history, you can check the list of commits and navigate through if you need to pull anything, a reference or see where changes were made.

- git blame <file> : this will reveal who did what work on the file. If you need an explanation of anything you can check who made the changes and ask them.

### When would I use it in a real project?

- while working in a team I used a lot of git log and git checkout main. Those two were the most useful to me and since I worked in small teams I didnt need git blame or git cherry pick. I used git log to check the commit history and see which one introduced a specific funciton or feature. Git checkout main was for resetting files I messed up. In bigger teams I would imagine using git blame a lot, to figure out who introduced the latest changes. And cherry pick the most recent features from latest updates into the branch im currently working on.

### what surprised me

- I was most surprised with git blame since I never used it before. Its cool that I can see who wrote or changed every single line of the code in a file. I can see why it would be very useful in the future. 