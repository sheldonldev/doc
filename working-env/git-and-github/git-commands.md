# Git Commands

## Pull & Push

### How to push a local project to github

- init local project as a git repo:

```bash
git init
git add .
git commit -m 'some commentary'
```

- create an empty repo in github, then an insturction will appear, just follow it.

### How to pull from remote

- if remote is more updated than localgit push:

```bash
git pull
```

- if local is more updated than remote

```bash
git stash
git pull
git stash apply    # or follow the error tips if something went wrong
```

## Delete All Commits of a Branch

- It's useful to delete all sensitive information in your commits.

```bash
git checkout --orphan new_branch_name
git add .
git commit -m 'a new branch without history commits'
git push origin HEAD:new_branch_name

# now, delete the old branch on github
# and, delete it in local:
git branch -D old_branch_name 

# now you can create branches based on your new orphan
git branch another_new_branch
```

## How to Merge Orphan Branches

```bash
git checkout orphan_branch_1
git rebase orphan_branch_2
git checkout orphan_branch_2
git merge orphan_branch_1
```

## Deal With Large Files

- [Git Large File Storage](https://git-lfs.github.com/)

## Keeping a Fork Up To Date

- To sync changes you make in a fork with the original repository, you must configure a remote that points to the upstream repository in Git.

```bash
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
```

- You can check if it was succesful with: `git remote -v`;

- Then fetch it to update your project:

```bash
git fetch upstream
```

- Merge the changes from upstream/master into your local master branch:

```bash
git merge upstream/master
```
