# README

## Git for Dummies

### what means what?

- remote - remote means server like github, bitbucket
- local - your repo stored in PC
- remote repository - your repo available on github, bitbucket
- origin - origin is remote from where you have did `git clone`
- upstream - upstream is their main repo from which you have forked, useful to get latest changes from their repo.releases
- tag - used for software releases
- master - it's a branch named master \(default created branch for new repo\)
- pull - get latest changes, remote branches and then move HEAD to latest commit \(`git pull` = `git fetch` + `git merge`\)
- HEAD - head always refers to the latest commit on your current branch.
- fetch - just download latest changes in separate path and do not integrate with your repo. `git merge` is required to integrate these changes

## Stage & Commit

```text
git add . (stage ALL new,modified files)
```

```text
git add -A (stage ALL new,modified,deleted files)
```

```text
git add file1.txt file2.txt file3.txt
```

```text
git add -i (interactive add/revert)
```

```text
git commit -m 'fixed this and that'
```

#### Git append \(commit using last commit msg\)

```text
git commit --reuse-message=HEAD
_(make shortcut: add,append,push; run once in terminal)_
git config --global alias.append '!f() { git add -A && git commit --reuse-message=HEAD && git push; }; f' (run once)
git append (use it like this)
```

#### Git add+commit \(1 line, if there's no new file created\)

```text
git commit -am "fixed this and that"
```

#### Git add+commit \(1 line, add newly created files also\)

```text
git add -A ; git commit -m "Your Message" (powershell)
git add -A && git commit -m "Your Message" (bash)
```

#### Git add+commit+push \(1 line, stage newly created files also, run it once to create alias in .gitconfig\)

```text
git config --global alias.lazy '!f() { git add -A && git commit -m "$@" && git push; }; f' (run once)
git lazy "fixed bugs" (use it like this)
```

## Push/Pull \(Get latest changes\)

```text
git push origin
```

```text
git push upstream
```

```text
git push upstream/some_branch
```

```text
git push origin HEAD (push local changes to remote branch with same name)
```

```text
git pull origin master (pull latest changes from remote master branch into local dev branch)
```

## untrack & remove pushed files

1. add those to .gitignore
2. git rm -r --cached .
3. git add .
4. git commit -am "Remove ignored files"
5. git push

## remove untracked files from local and server

(which persist even after adding to .gitignore)

```text
git rm -r --cached . && git add . && git commit -am "Remove ignored files" && git push
```

## Branch

- create local branch \(code will be copied from current branch ~master\)

  ```text
    git checkout -b feature_x
  ```

- push newly created branch to remote \(branch is not available to github.com unless you push it separately\)

  ```text
    git push --set-upstream origin feature_x
  ```

- Add Remote branch \(origin is your repo on github.com\)

  ```text
    git remote add origin https://github.com/user/repo.git
  ```

- Add upstream \(upstream is their main repo from which you have forked\)

  ```text
    git remote add upstream https://github.com/their_user/repo.git
  ```

- Create new local version branch of an upstream branch

  ```text
    git checkout -b feature_x upstream/master (master is the branch name)
  ```

- Switch branch

  ```text
    git checkout feature_x
  ```

- delete the branch

  ```
  git branch -d feature_x

  ```

- show origin (repo/branch URL on github)
  ```
  git remote show origin
  ```
- change origin (link to different repo URL on github)
  ```
  git remote set-url origin new.git.url
  ```
  
 - Clone uncommited changes to new branch
 make copy of changes in current A branch stack
 ```
 git stash -u
 git stash apply
 ```
 carry these changes to new branch and do your work
 ```
 git checkout -b new_branch
 ```
 To see uncommited changes on previous A branch
 ```
 git checkout A
 git stash apply // or if you've made stash in some other branch: `git stash list` and then use correct number: `git stash apply 2`
 ```
 

### Status of remote - local - origin branches tracking

    git remote -v

```text
  git branch -d feature_x
```

**Status of remote - local - origin branches tracking**

    git remote -v

```text
git remote show origin
```

```text
git status
```

### Create Pull Request

- for can-menifest:

  ```text
    hub pull-request -b release -r ankit-shukla
  ```

  ```text
    hub pull-request -b pre-release -r ankit-shukla
  ```

- for can-cntral:

  ```text
    hub pull-request -b bixby-2 -r ankit-shukla
  ```

- [https://hub.github.com/hub-pull-request.1.html](https://hub.github.com/hub-pull-request.1.html)

## Repo Status

```text
git status
```

```text
git add -i
```

- show latest commits \(to exit type q\)

  ```text
   git log
  ```

- Display current branch

  ```text
    git branch
  ```

## Git GUI

use fork app on windows

### Built-in git GUI

```text
gitk
```

### Git interactive commands

```text
git add -i
```

### use colorful git output

```text
git config color.ui true
```

## I f\*\*ked up

### Resolve Merge Conflicts:

revert all our changes and pull latest from upstream \(their repo\):

```text
  git reset --hard HEAD
  git pull -s recursive -X theirs upstream branch_remote
```

**Revert last commit and keep the changes \(local\)**

```text
git reset HEAD^
```

**Revert last remote commit \(from remote, untracable\)**

```text
git pull #to get that commit to local
git reset HEAD^ #remove commit locally
git push origin +HEAD #force-push the last HEAD commit to remote
```

**Revert all local changes and local commits \(local\)**

\(fetch the latest history from the server and point your local master branch at it \)

```text
git fetch origin git reset --hard origin/master (master is the branch name)
```

### Revert everything I did & make repo sync with upstream

```text
git reset --hard upstream/master (master is the branch name)
git pull upstream master
```

### Clean up a fork and restart it from the upstream

```text
git reset --hard upstream/master (master is the branch name of original repo)
git push origin my_branch --force (or git push origin HEAD --force)
```

### Git pull without committing local changes

- hide your local uncommitted changes temporarily

  ```text
    git stash --include-untracked // shorthand git stash -u
  ```

  - show all stashes

    ```text
      git stash list
    ```

- get latest changes

  ```text
    git pull
  ```

- now unhide your local uncommitted changes  
  \(`pop` will restore only latest stash\)

  ```text
    git stash pop
  ```
  or 
  ```text
  git stash apply
  ```
  `git stash pop` restore changes and also removes it from stack, `git stash apply` restores it but still keeps it on stack for possible later reuse (or you can then `git stash drop` it). So `git stash pop` is `git stash apply` && `git stash drop`

## git Users

### Set

```text
git config --local user.name "localuser"
git config --local user.email "localuser@example.com"
git config --global user.name "globaluser"
git config --global user.email "globaluser@example.com"
```

### Get

```text
git config --local user.name
git config --local user.email
git config --global user.name
git config --global user.email

git config --list
```

## Remember Me

### Remember username & password

1\) Secured Way \(Store globally\)

```text
    git config --global credential.helper manager //secured way for Windows

    git push http://example.com/repo.git
    Username: <type your username once>
    Password: <type your password once>
```

2\) Unsecured way \(Store globally\)

```text
    git config credential.helper store //username & password stored in plain-text in "%UserProfile%\.git-credentials"
    git push http://example.com/repo.git
    Username: <type your username once>
    Password: <type your password once>
```

3\) Unsecured way \(Store locally per repo\)

```text
    //saved in file 'cred' inside repo .git folder. Need to manually delete this file.
    git config credential.helper 'store --file=.git/cred'
```

4\) Secured Way \(Store in Cache\)

```text
    git config credential.helper 'cache --timeout=864000' // 10 days expiry
    git credential-cache exit // remove it from cache before timeout
```

### Remove credentials

```text
git config --unset credential.helper
git config --local --unset credential.helper
git config --global --unset credential.helper
git config --system --unset credential.helper
//Windows: delete from Control Panel\User Accounts\Credential Manager
```

### Download big repository on poor bandwidth:

- [https://stackoverflow.com/questions/34389446/how-do-i-download-a-large-git-repository/52090961\#52090961](https://stackoverflow.com/questions/34389446/how-do-i-download-a-large-git-repository/52090961#52090961)

#### HTTPS Clone repo vs SSH Clone repo

- HTTPS Clone - easier, works through firewalls & proxies, ask password everytime for push-pull \(but password can be saved using `git config credential.helper store`\)
- SSH Clone - manually create SSH key & add it to github, password not required for push-pull. Remove key from github to revoke authorization for that PC.

#### markdown cheatsheet:

- [https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
