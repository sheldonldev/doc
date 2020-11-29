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

- [Large File Storage](https://packagecloud.io/github/git-lfs/install)
