# VCS

## .gitconfig

```bash
cat ~/.gitconfig
```

## .gitignore

```bash
touch ~/.gitignore_global
```

```bash
# my ~/.gitignore_global
.git
.DS_Store
node_modules
/dist


# local env files
.env
.env.local
.env.*.local

# Log files
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*

# Editor directories and files
.idea
.vscode
```

```bash
git config --global core.excludesfile ~/.gitignore_global
```
