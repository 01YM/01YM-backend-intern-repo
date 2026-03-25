## Reflection

### Which terminal client did you choose? Why?

- I used Powershell since im using windows and its the most convenient one to use at the moment. I also like using it for both git and vs code. Ive been using it previously and so im most familiar with it as well


### What customizations (if any) did you make?

- I didnt customize it, it feels the most familiar and comfortable with its default layout and tab system. 

### What was the most useful command you learned today?

- git reset --soft HEAD~1 : undo last commit 
- findstr "text" <file>   : search text in file 

# Top Used PowerShell Commands

## Navigation
- `pwd` → Show current directory  
- `ls` / `dir` → List files and folders  
- `cd <folder>` → Move into a folder  
- `cd ..` → Go up one directory  
- `cd ~` → Go to home directory  

---

## File & Folder Management
- `mkdir <name>` → Create a new folder  
- `ni <file>` → Create a new file  
- `rm <file>` → Delete a file  
- `rm -r <folder>` → Delete a folder  
- `copy <src> <dest>` → Copy file  
- `move <src> <dest>` → Move or rename file  

---

## Viewing & Editing
- `cat <file>` → View file content  
- `notepad <file>` → Open file in Notepad  
- `code .` → Open current folder in VS Code  
- `echo <text>` → Print text to terminal  

---

## System & Utility
- `clear` / `cls` → Clear terminal screen  
- `Get-Process` → View running processes  
- `Get-Service` → List system services  
- `Get-Location` → Show current path  

---

## Search & Filtering
- `findstr "text" <file>` → Search text in file  
- `Get-ChildItem -Recurse` → List all files recursively  
- `Select-String "text"` → Search text in output  

---

## Git Commands (Commonly Used)
- `git clone <url>` → Clone a repository  
- `git status` → Check changes  
- `git add .` → Stage changes  
- `git commit -m "message"` → Commit changes  
- `git push` → Push to GitHub  
- `git pull` → Pull latest changes  
- `git log --oneline` → View commit history  

---

## Useful Shortcuts / Aliases
- `gcm "message"` → Commit with message (custom function)  
- `gs` → `git status`  
- `gp` → `git push`  
- `ga` → `git add`  

---

## Helpful Developer Commands
- `git rev-parse --show-toplevel` → Show root of repo  
- `npm install` → Install dependencies  
- `npm start` → Run project  
- `dotnet run` → Run .NET project  

---