# Global Settings

## Global .gitconfig

```bash
cat ~/.gitconfig
```

## Global .gitignore

```bash
touch ~/.gitignore_global
```

```bash
**/.git
**/.DS_Store
**/node_modules
**//dist

**/.env
**/.env.local
**/.env.*.local

**/npm-debug.log*
**/yarn-debug.log*
**/yarn-error.log*
**/pnpm-debug.log*

**/.idea
**/.vscode
```

```bash
git config --global core.excludesfile ~/.gitignore_global
```
