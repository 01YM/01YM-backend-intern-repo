## Reflection

### Why is pushing directly to main problematic?
- Since theres multiple people working on the code pushing to main will create a spaghetti of commits. Its hard to track where bugs and errors came from or how a feature was introduced and who worked on it. 

### How do branches help with reviewing code?
- Branches could represent features or be assigned to different people. This way it becomes easy to track who does what and if there were errors it could be easily found in the specific branch. 

### What happens if two people edit the same file on different branches?
- they will automatically be combined if different parts of the file were edited. If the same lines were changed, a merge conflict will be introduced which would then need to be reviewed manually.