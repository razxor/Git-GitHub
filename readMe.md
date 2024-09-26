# Initial git setup || Run For the first time.    
git config --global user.name "subrotoice"
git config --global user.email "subroto.iu@gmail.com" // Every space has meaning: git config --global user.email subroto.iu@gmail.com will work
git config --list (Show all config) || git config user.name //(Show User Name)

# Ch-2: Creating Snapshots (do Commit) | https://prnt.sc/zIIkMN39czOk | stage area green , unstated red | https://prnt.sc/9_BUPJ6VX53L
1. Working Directory: Where you work on your files locally || "Project Folder" another name
2. Staging Area: A temporary holding area - Where proposed change for next commit
3. Repository (Store Snapshots Parmanently) | Store what content in the last stage area

# Working Directory -> Stageing Area
- git add a.txt || git add a.txt b.txt || git add .txt(all text file) || git add .
- git ls-files // list of files in Staging area .

# Stageing Area -> Repository 
git commit -m "Short MSG" || -git commit // Opens the default editor to type a long message
git commit -a -m "add & commit" or git commit -am "add & commit" // Skeeping staging area. add+commit

# Removing Files
git rm file1.js // Removes from working directory and staging area
git rm --cached file1.js // Removes from staging area only, but file reamain as untrack file

# .gitignore
node_modules/   //Folder
*.log    // all log file
account_info.js   // file

# Viewing the staged/unstaged changes (--- define old copy, +++ define new modified copy || https://prnt.sc/gfyzlJfoMLZT)
git diff // Working directory vs Last Stage
git diff --staged // Shows staged changes which is gonna to be in next commit

# Creating Snapshots with VSCode | Stated/UnStaged, Commit, Timeline

# Ch-3: Browsing History ------
# Viewing the history
git log // Full history || Up/Down arrow, Space for next page, q for quit
git log --oneline // Summary
git log --reverse // Lists the commits from the oldest to the newest
git log --oneline --stat // What files changes in every commit || git log --stat // full details
git log --oneline --patch // See actual change ie. vscode what we see old vs new copy

# Filter the history (by author, date, commit msg, content so on..)
git log --oneline -3 // last 3 commits
git log --oneline --author="subrotoice" // Filter by author, git log --oneline --author="subr"  and git log --oneline --author="ice" both will rork
git log --oneline --before="2024-09-24" // By date, git log --oneline --before="tomorrow"
git log --oneline --after="2024-09-24" // git log --oneline --after="yesterday" | git log --oneline --after="one week ago" (tow days ago, one month ago) 
git log --oneline --grep="add e" // by commit msg, NB: Case sensetive
git log --oneline -S"content in file" // Search by content: NB: not -S="content in file"
git log --oneline -S"4" --patch // to see what change actually come ie. vscode what we see old vs new copy
git log --oneline 9f4bdb9..cb5dbb6 // in a range, NB: old..new | Also work: git log --oneline 9f4b..cb5 as long as not ambegious
git log --oneline e.txt // those commits that modifyed e.txt file | If not work then use: git log --oneline -- e.txt
git log --oneline --patch e.txt // see actual changes in e.txt file ie. vscode what we see old vs new copy

# Aliases
git config --global alias.l "log --oneline" // 'git l' is equal to 'log --oneline'
git config --global alias.b "branch" // git b is 'git branch'
git config --global alias.lg "log --pretty=format:'%Cgreen%an%Creset committed %h on %cd'"

# Viewing a commit | show command do not change anything in working dir like checkout. It just show what file & content in a certain
git show 86126b1 //Shows the given commit || git show 861 this also works if not ambegious
git show HEAD //Shows the last commit
git show HEAD~2 //Two steps before the last commit
git show HEAD:a.txt //Shows the contains a.txt in the last commit
git show HEAD~2:readme.txt // Show the content of readme.txt 2 step back of last commit
git show HEAD --name-status // Can see which file add, modify or delete of a certain commit | https://prnt.sc/Zf45OTb9jT9o | git show HEAD~2 --name-status
git ls-tree HEAD~3 // list of files 3 steps before last commit || https://prnt.sc/Yn9kkxGd1Mdr (Helpful to see what a file contains in some commit)
git show 98t9 // it link with previous command(git ls-tree HEAD~3) show content of a file after ls tree

# Viewing the Changes Accross Commits (same like staged and unstaged change)
git diff HEAD~5 HEAD // git diff HEAD~5 HEAD~1
git diff HEAD~5 HEAD~1 c.txt  // See on a perticular file
git diff HEAD~5 HEAD --name-status // See what file added, changed or deleted in this range | https://prnt.sc/C9pJyuPfXU7f

# Checking Out a Commit (Should not do another commit when checking out just watch) | going back in time - No change in repo, easily back to Headsection again)# ওই অবস্থায় গিটে কি ফাইল ছিল, কি কনটেন্ট ছিল
git checkout HEAD~2 or git checkout 0f6509e or git checkout 0f6 //use: git log --oneline --all | git checkout master to take back pointer
git checkout master // so it back to master brunch

# Revert, Rebese, Reset ---
# Revert commits (undoing things - Add another history along with keep all previous commit history)
*In a serario where you delete file d.txt and commit. Then you want to get back that file in a new commit but previous delete d.txt also remain*
- git add . (delete d.txt by mouse)
- git commit -m "removed d.txt"
- git revert a440127 (Editor will open change commit msg if you want)
- git log --oneline (Add new commit and not remove previous commit from commit history) https://prnt.sc/2UxIh3rIrC_t
- We can again revert, We can change commit msg completly, But it is good idea to keep - revert "commit msg"
- Revert ke abar revert korle back to previous condition

# Rebase (1. Rename previous commit, 2. merging commits into one)
## Rename Commit || Rename any previous commit
- git rebase -i HEAD~3  => Open Editor pick -> reword  => Open another editor then change msg

## Reset (Remove Commit history parmantely)
- git reset 2135fda (Reset specific commit but files keep in working directory) (You can git add . and commit to back to last commit)
- git reset 40ce348 --hard (Reset completly No file remain in working directory) || or, git reset --hard 40ce348  (Place --hard previous hash code)
          --------      

# Branch Practice--- master(default)
- git branch // show all branch and current branch in green; (for details) git branch -v / git branch -a
- git branch xyz // Create new branch xyz; git checkout -b newBranch // create+Switch to newBranch
- git checkout xyz (switch to xyz branch)
- git branch -d xyz (delete xyz branch but in that time you have to stey another branch otherwise you can not delete) || git branch -D xyz (If problem occured)
- git checkout -b xyz (Create + Checkout)

# Merge 
- git merge xyz (on master branch)(It keep all the commit log from xyz)
- git merge xyz --squash (Bring all changes from xyz branch to master stage area. So you need to run "git add" and It will not added to commmit log)
- git commit -m "Merge msg here" (already added to stage area so just need to commit)

# Addressing Branches with Conflicts (Working on same file from two branches before marge) 
- git marge xyz --squash / git marge xyz (--squash is better idea)
if there is conflict then editor will open then you can keep whatever you want to keep
- git add .
- git commit -m "merge msg here"

# Remote(GitHub)
git remote add <UrlName> <URL-www.>
git remote -v // See URL; git remote aslo work but show only git name
git remote set-url secondURL https://github.com/subrotoice/kst.git // Change URL for second identifier
git push -u third master // you can push without switching branch, ie. from master branch you can push to other branch; https://prnt.sc/QAaFTy0Lt1_s
git push -f second main // Forch Push
git clone -b <branchName> <remote-repo-url> // Clone a Specic Branch from remote repo; ie. git clone -b main9 https://github.com/subrotoice/test9.git // Working, Here brunch name main9
git branch -a // After download you to see all branches || then - git checkout <branch_name>

# Remote(Pull)
git pull origin xyz (Pull a branch)
git pull --rebase origin master // if Error in pushing, that case first do this command then push

# GitHub Push problems
Setting -> Developer Setting -> Personal Access Token -> Token(Classic) -> Create new token and Store it
git config credential.helper store // use before push, to avoid providing credential in every push

# Push using VSCode

# Committed changes to a repository and then made additional changes that you want to include in that same commit
git add <file(s)> // ie. git add README.md
git commit --amend
git push origin master --force // Need to force push to the remote repository if you've already pushed the previous commit.
----------------End--------------

# Basic Windows command like cd
cd\ = back to root directory c drive does not metter where its current postion
cd .. = One step back
cd /d D: = C Drive to D drive
dir or ls(LS) = List all file and folder of current directory. "ls" is more clear to read
mkdir mynewfolder = Create New Folder
echo tailwind-landing >> README.md // Create file and put content Best*  shor: echo > asdfwe.txt (Create file only no content)
cd "folderName" = To enter Folder for doing some task
cls = Clear Screen // "clear" in git bash

# Upload a new project
git init // Basically 3 steps, 1. add, 2. Commit, 3. Push; https://prnt.sc/9_BUPJ6VX53L || https://prnt.sc/EPS4VuRlaJEl
git add . // added to staged area, and ready for commmit; git add -A // same, all files; git add index.html // only index.html file
git commit -m "first commit" // Save as a snapshot what remain in staged area
git remote add origin https://github.com/subrotoice/ccn.git // ("origin Userdifine", origin=url.git, variable e value assign korar moto)
git push -u origin master // push, origin user define name like variable contain url. (master default brunch name, you can create brunch like, https://prnt.sc/26pq9x2

# Work on an existing Project
First you have to download project otherwise it will not work
git clone https://github.com/Tilotiti/jQuery-LightBox-Responsive.git // Pull
cd folder_name // Need to change to inside folder
git add . For all new file and folder (git add file_names.exten it is for single file)
git commit -m "committed message" For asingle file(git commit -m "committed message" file_names.exten)
git push -u origin master // First time pushing the branch or if you've made changes that conflict with the remote repository, you might need to use the '-u'
git pull origin master // Change in github, it take effect in local reprository. 'Synchronization'

# Work on existing Project - Delete Some files and add new files | It is possible to rename reposiotry
1. Delete files manually using mouse keyboard
2. git add .
3. git commit -m "Deleted Files"
4. git push -u origin master
// Another way
1. git rm file1.txt file2.txt file3.txt // remove files and here not need to stage(git add)
2. git commit -m "Remove files: file1.txt, file2.txt, file3.txt"
3. git push -u origin master