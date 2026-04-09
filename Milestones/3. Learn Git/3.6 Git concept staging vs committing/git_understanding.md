## Reflection 

### What is the difference between staging and committing?
- staging is selecting the files you want to include in the next commit. Commiting is saving these selected files into the git history. If I finish modifying one file out of the three I changed, I can stage just the one I completed and commit it. 

### Why does Git separate these two steps?
- This way files that arent completed or get accidentaly modified wont break anything. If git saved every single change after it was made, the developeres would have little control over what gets saved. This could create a lot of difficulties while working on projects.

### When would you want to stage changes without committing?
- whenever I want to prepare some files for the next commit while still working on others. If I completed one feature but still testing something else, I can stage the completed feature file and leave the rest unstaged. This also helps to organise everything and keep it clean