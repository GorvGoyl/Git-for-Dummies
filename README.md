# Git for Dummies
## what means what?
* remote - remote means server like github, bitbucket
* local - your repo stored in PC
* remote repository - your repo available on github, bitbucket
* origin - origin is remote from where you have did `git clone`
* upstream - upstream is their main repo from which you have forked, useful to get latest changes from their repo.releases
* tag - used for software releases
* master - it's a branch named master (default created branch for new repo)
* pull - get latest changes, remote branches and then move HEAD to latest commit (`git pull` = `git fetch` + `git merge`)
* HEAD - head always refers to the latest commit on your current branch.
* fetch - just download latest changes in separate path and do not integrate with your repo. `git merge` is required to integrate these changes
---
# Stage & Commit
```
git add . (stage ALL new,modified files)
```
```
git add -a (stage ALL new,modified,deleted files)
```
```
git add file1.txt file2.txt file3.txt
```
```
git add -i (interactive add/revert)
```
```
git commit -m 'fixed this and that'
```
### Git add & commit in one line (if there's no new file created)
	git commit -a -m 'fixed this and that'
	or
	git commit -am "fixed this and that"
---
# Push/Pull (Get latest changes)
```
git push origin
```
```
git push upstream
```
```
git push upstream/some_branch
```
---
# Branch
* Add Remote branch (origin is your repo on github.com)
	```
	git remote add origin https://github.com/user/repo.git
	```
* Add upstream (upstream is their main repo from which you have forked)
	```
	git remote add upstream https://github.com/their_user/repo.git
	```
* Create Branch "feature_x" and switch to it
	```
	git checkout -b feature_x
	```
* delete the branch
	```
	git branch -d feature_x
	```
* push newly created branch to remote (branch is not available to github.com unless you push it separately)
	```
	git push origin feature_x
	```
* Switch branch

	```
	git checkout branch_name
	```
### Status of remote - local - origin branches tracking
	git remote -v
```
git branch -vv
```

```
git remote show origin
```
```
git status
```
---
## Create Pull Request
* for can-menifest:
	```  
	hub pull-request -b release -r ankit-shukla
	```
	```
	hub pull-request -b pre-release -r ankit-shukla
	```
* for can-cntral:
 
		hub pull-request -b bixby-2 -r ankit-shukla
* https://hub.github.com/hub-pull-request.1.html
---

# Repo Status
	git status
```
git add -i
```
-  show latest commits (to exit type q)

		git log
- Display current branch

		git branch
---
# Git GUI

## Built-in git GUI
	gitk
## Git interactive commands
	git add -i
## use colorful git output
  
	git config color.ui true
---

# I f**ked up

## Resolve Merge Conflicts:
- revert all our changes and pull latest from upstream (their repo):
  
		git reset --hard HEAD
		git pull -s recursive -X theirs upstream branch_remote  

## Revert all local changes and local commits
(fetch the latest history from the server and point your local master branch at it )

	git fetch origin
	git reset --hard origin/master

## Revert everything I did & make repo sync with upstream
	git reset --hard upstream/master
	git pull upstream master

## Git pull without committing local changes
* hide your local uncommitted changes temporarily
  
		git stash

	* show all stashes
  
			git stash list
* get latest changes

		git pull

* now unhide your local uncommitted changes  
  (`pop` will restore only latest stash)

		git stash pop
---	
# git Users
## Set

	git config --local user.name "localuser"
	git config --local user.email "localuser@example.com"
	git config --global user.name "globaluser"
	git config --global user.email "globaluser@example.com"

## Get
	git config --local user.name
	git config --local user.email
	git config --global user.name
	git config --global user.email

	git config --list
---
# Remember Me
## Remember username & password
1) Secured Way  (Store globally)

		git config --global credential.helper manager //secured way for Windows

		git push http://example.com/repo.git
		Username: <type your username once>
		Password: <type your password once>

2) Unsecured way (Store globally)

		git config credential.helper store //username & password stored in plain-text in "%UserProfile%\.git-credentials"
		git push http://example.com/repo.git
		Username: <type your username once>
		Password: <type your password once>

3) Unsecured way (Store locally per repo)

		//saved in file 'cred' inside repo .git folder. Need to manually delete this file.
		git config credential.helper 'store --file=.git/cred'

4) Secured Way (Store in Cache)
   
		git config credential.helper 'cache --timeout=864000' // 10 days expiry
		git credential-cache exit // remove it from cache before timeout


## Remove credentials
	git config --unset credential.helper
	git config --local --unset credential.helper
	git config --global --unset credential.helper
	git config --system --unset credential.helper
	//Windows: delete from Control Panel\User Accounts\Credential Manager

---
## Download big repository on poor bandwidth: 
* https://stackoverflow.com/questions/34389446/how-do-i-download-a-large-git-repository/52090961#52090961

### HTTPS Clone repo vs SSH Clone repo
* HTTPS Clone - easier, works through firewalls & proxies, ask password everytime for push-pull (but password can be saved using `git config credential.helper store`)
* SSH Clone - manually create SSH key & add it to github, password not required for push-pull. Remove key from github to revoke authorization for that PC.

### markdown cheatsheet:
- https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

---
