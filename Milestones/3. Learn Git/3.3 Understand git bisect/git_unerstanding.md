## Reflection 

### What does git bisect do?

- git bisect helps find which commit introduced a bug by checking the commits between good and broken versions. 

### When would you use it in real world debugging situation?

- when a project was working before and after several commits you realise some  feature or method is crashing or not working anymore. Or when multiple people commit at the same time and youre unsure when the bug came 

### How does it compare to manually reviewing commits?

- its faster when there are many new commits, when its a big project 

### Testing the git bisect 

- I created a simple snake game inside the milestone 3.3 folder to test git bisect. First, I committed a working version of the game, then I made a few small changes in later commits. After that, I introduced a bug into the food collision logic and made another commit after the broken version. I used git bisect to compare a working commit and a broken commit. Git automatically searched through the commits and found the first bad commit