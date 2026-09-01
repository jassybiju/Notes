`git add --all` : Stages all the files in workdir
`git add -A` : Minized form of --all
`git add *` : Stages all visible changes ( not deleted )
`git add .` : Stages all in that folder

`git status` : View status of al files

Moving changes from stage to Local Repo is called **Commit**. (We're confirming the changes)

`git rm <file_path>` : It remove the file and stage the deletion file

`git rm -f <file_path>` : If there are modifications which aren't staged. It won't remove it so force it.
`git rm --cached <file_path>` : Same scenario as above but keep the file only removes from staging area to workingdir
`git rm -r <folder_path>` : Recursive remove all the files in the folder

## `git reset`

### Flags (what gets reset)

| Flag | HEAD | Index | Working Dir |
|------|------|-------|-------------|
| `--soft` | ✅ moved | ❌ untouched | ❌ untouched |
| `--mixed` *(default)* | ✅ moved | ✅ reset to target | ❌ untouched |
| `--hard` | ✅ moved | ✅ reset to target | ✅ reset to target |

### Target (where to move to)

| Syntax | Meaning |
|--------|---------|
| `HEAD~1` | 1 commit back |
| `HEAD~2` | 2 commits back |
| `HEAD` | current commit (no move) |
| `a1b2c3d` | specific commit hash |
| `main` | specific branch |

### Quick reference

| Command | Effect |
|---------|--------|
| `git reset` | Unstage everything. Files stay on disk. |
| `git reset --soft HEAD~1` | Undo last commit. Changes stay **staged**. |
| `git reset HEAD~1` | Undo last commit. Changes become **unstaged**. |
| `git reset --hard HEAD~1` | Undo last commit. Changes are **gone**. |

### Rule of thumb

- **`--soft`** → "I want to re-commit differently"
- **`--mixed`** → "I want to unstage and rethink"
- **`--hard`** → "I want to throw it all away"   

---

`git log` : View Commit History
`git log --oneline` : View history in one-line

**Git Branching** : Branching in git allow secure, organized intermediate step to review, test, and amnge feature

**Merging** : Combining the changes froim two branches into one

`git branch <branch_name>` : Creates new branch. with the state of the current branch

`git merge <brach-1> -m <message>` : Merge branch-1 to current branch with message 

`GIT CONFLICT` : It occurs when same part of same file

`git diff <comit-1> <comit-2>` : To see the difference between 2 commits

`PUSH` : Moves the local changes to remote
`FETCH` : Bringing the changes from remote to local, but not merging them yet
`PULL` : Fetching + Merging. so your working directlory immediately reflect the remote changes

`git restore --staged <path>` : Remove changes from staged area to previous commit keeps the working dir
`git restore <path>` : Remove the chnges from both staged area and working_dir

`git stash` : Temporarily set aside your unfinished work, switch to another branch to do something
`git stash pop` : Restores the most recent stash and removes from the list
`git stash apply` : Restores the most recent stash but won't remove form the list
`git stash list` : List all the stash
`git stash drop` : Removes the stash

`git revert <commit>` : Used to undo the changes made in a previous commit, but instead of deleting that old commit, it creates a new one that reverses those changes
OR
Create a new commit that inverse that the <commit>

### why dont use git reset instead of revert
If others already used the reverting commit. It will cause issure. since they need to reset it and redo all the features they are already doing. so if reverted they only need have a merge conflict

“Rebase takes my branch's commits that were based on an older commit and replays them on top of the latest commit of the base branch.”

PULL REQUEST : 