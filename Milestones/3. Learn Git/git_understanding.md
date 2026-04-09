# Milestone 3 summary 

## 3.2 Reflection

### What makes a good commit message?
- its short, clear, explains what changed 
- easy to understand without opening code 
- focus on one change only

### How does a clear commit message help in team collaboration?
- quickly understand what changed
- reviewing code becomes easy 
- helps find bugs or chnages
- project history stays organized

### How can poor commit messages cause issues later?
- hard to find bugs 
- hard to understand new methods, variables and functions
- wasting time to understand what changes were madee

## 3.3 Reflection 

### What does git bisect do?

- git bisect helps find which commit introduced a bug by checking the commits between good and broken versions. 

### When would you use it in real world debugging situation?

- when a project was working before and after several commits you realise some  feature or method is crashing or not working anymore. Or when multiple people commit at the same time and youre unsure when the bug came 

### How does it compare to manually reviewing commits?

- its faster when there are many new commits, when its a big project 

### Testing the git bisect 

- I created a simple snake game inside the milestone 3.3 folder to test git bisect. First, I committed a working version of the game, then I made a few small changes in later commits. After that, I introduced a bug into the food collision logic and made another commit after the broken version. I used git bisect to compare a working commit and a broken commit. Git automatically searched through the commits and found the first bad commit

## 3.4 Reflection 

### What does each command do?
- git checkout main -- <git_understanding>: this command restores the file, in this scenario the git_understanding file from main. Its useful if one file was messed up, you just take the working copy from main.  

- git cherry-pick <commit>: brings a commit from another branch into yours. Its useful if you want a feature thats been updated on a different branch or if you need the latest update on your branch as well.

- git log : just shows the commit history, you can check the list of commits and navigate through if you need to pull anything, a reference or see where changes were made.

- git blame <file> : this will reveal who did what work on the file. If you need an explanation of anything you can check who made the changes and ask them.

### When would I use it in a real project?

- while working in a team I used a lot of git log and git checkout main. Those two were the most useful to me and since I worked in small teams I didnt need git blame or git cherry pick. I used git log to check the commit history and see which one introduced a specific funciton or feature. Git checkout main was for resetting files I messed up. In bigger teams I would imagine using git blame a lot, to figure out who introduced the latest changes. And cherry pick the most recent features from latest updates into the branch im currently working on.

### what surprised me

- I was most surprised with git blame since I never used it before. Its cool that I can see who wrote or changed every single line of the code in a file. I can see why it would be very useful in the future. 


## 3.5 Reflection

### Why is pushing directly to main problematic?
- Since theres multiple people working on the code pushing to main will create a spaghetti of commits. Its hard to track where bugs and errors came from or how a feature was introduced and who worked on it. 

### How do branches help with reviewing code?
- Branches could represent features or be assigned to different people. This way it becomes easy to track who does what and if there were errors it could be easily found in the specific branch. 

### What happens if two people edit the same file on different branches?
- they will automatically be combined if different parts of the file were edited. If the same lines were changed, a merge conflict will be introduced which would then need to be reviewed manually.

## 3.6 Reflection 

### What is the difference between staging and committing?
- staging is selecting the files you want to include in the next commit. Commiting is saving these selected files into the git history. If I finish modifying one file out of the three I changed, I can stage just the one I completed and commit it. 

### Why does Git separate these two steps?
- This way files that arent completed or get accidentaly modified wont break anything. If git saved every single change after it was made, the developeres would have little control over what gets saved. This could create a lot of difficulties while working on projects.

### When would you want to stage changes without committing?
- whenever I want to prepare some files for the next commit while still working on others. If I completed one feature but still testing something else, I can stage the completed feature file and leave the rest unstaged. This also helps to organise everything and keep it clean