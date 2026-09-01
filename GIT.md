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