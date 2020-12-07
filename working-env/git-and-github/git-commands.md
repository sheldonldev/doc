# Git Commands

## Pull & Push

- How to push a local project to github

  - init local project as a git repo:

  ```bash
  git init
  git add .
  git commit -m 'some commentary'
  ```

  - create an empty repo in github, then an insturction will appear, just follow it.

- How to pull from remote

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
