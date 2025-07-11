# git notları

source → [[https://www.freecodecamp.org/news/git-cheat-sheet/](https://www.freecodecamp.org/news/git-cheat-sheet/)] 

---

- `learn and setup your git username and mail`

```markdown
git config -l (learn your credentials)
git config --global user.name "bugra"
git config --global user.email "bugrakara@hotmail.com"
git config --global credential.helper cache (store your git credentials in cache so you don’t have to type each time)
```

- `initialize a git repo in a folder`

```markdown
git init
```

- `add a file to the stage area (ready to commit)`

```markdown
git add whatever
git add .
git add my*
```

- `check status`

```markdown
git status
```

- `commit changes`

```markdown
git commit 
git commit -m "your message"
git commit -a -m "your message" (git add + git commit in one command)
```

- `see commit history`

```markdown
git log
git log -p (see also the changes)
git log --graph
```

- `see a spesific commit by commit_id`

```markdown
git show <commit-id>
```

- `see the differences between local changes and staged files (those git added)`

```markdown
git diff 

git diff --staged (shows the diff b/w the last commit)

git diff commit1 commit2 (shows the difference b/w two commits)  
for instance: git diff master master2
```

- `to link a folder with a repository`

```markdown
git init (in an empty folder) 
git remote add origin your_repo_link
git remote -v (verify)
git add && commit
git push -u origin master
```

- `remove a file`

```markdown
git rm file_name (removes both from folder/repo)
git rm *.o
git rm -rf myCppExercises

git rm --cached file_name (removes from repo but keeps in local)
```

- `rename or move a file`

```markdown
git mv <old_file_name> <new_file_name>
git mv file.sh ../
```

- `ignores files (does not upload them to the repo)`

```markdown
touch .gitignore
vim .gitignore [things you want to exclude like *.out *.o *.exe myFile etc. ]
```

- `reset your commit to a previous one`

```markdown
git reset --soft <commit> (moves back to the commit's log BUT keeps the later 
changes intact, in staged area)

git reset --mixed <commit> (moves back to the commit's log BUT removes the files
from staged area)

git reset --hard <commit> (moves back to the commit's log AND removes the files
from both staged area and the local)

git reset --soft/mixed/hard HEAD~1 (undoes the last 1 commit)
```

- `switch between branches`

```markdown
git checkout <branch_name> (switch to a branch)
git checkout -b <new_branch> (create & switch to a new branch)

git checkout <file_name> (discards local changes & reverts a file 
to the state it has in the latest commit)
```

- `amend your latest commit`

```markdown
git commit -amend -m "new commit message"
```

- `create a new commit with the undoing`

```markdown
unlike git reset, git revert creates a whole new commit that does 
not have the latest changes

git revert <commit> && git push

git revert HEAD (revert the latest commit)
```

- `create a new branch`

```markdown
git branch <branch_name> (create it)
git checkout <branch_name> (switch to it)
git switch <branch_name> (2nd way to switch to it)
git branch (see all branches)
git branch -d <branch_name> (delete it)
```

- `merge two branches`

```markdown
git merge <branch_name> (merges the branch_name with the current branch)
git merge --abort (abandons a merge)
```

- `pull from repo`

```markdown
git pull = git fetch + git merge
git pull
```

- `kullanıcı adı vs. ekleme`

```markdown
git config --global user.name "bugrahan karamollaoglu"
git config user.name # diyerek kontrol edebilirsin

git config --global user.email "bugrahankaramollaoglu@gmail.com"
```

- `grafikte görme`

```kotlin
git log --oneline --graph --all
```

- `git stash nerede kullanılır?` git stash henüz commitlemedigin degisiklikleri gecici olarak saklamana yarar. bu sakladıgın seyi baska bir branchte kolayca uygulayabilirsin.

```kotlin
git stash
```

stashlerine mesaj vermek için 

```kotlin
git stash save "my stash message"
```

stashlerini görmek için 

```kotlin
git stash list
```

bir stashi stackten alip uygulamak için 

```kotlin
git stash pop
```

eğer silinmesin istiyosan 

```kotlin
git stash apply
```

stashlerini silmek için

```kotlin
git stash clear
```

- `eski commitlere dönmek için` git reset kullanıyoruz.

```kotlin
git reset f7e633deb7cbb
```

değişiklikleri de silmek istiyosan 

```kotlin
git reset --hard f7e633deb7cbb
```

- `git rebase:`