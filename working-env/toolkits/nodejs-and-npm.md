# NodeJS & npm

## Documentation

- [nodjs documentation](https://nodejs.org/en/docs/guides/)
- [larn nodejs](https://nodejs.dev/learn/introduction-to-nodejs)
- [npm](https://npmjs.com/)
- [yarn](https://yarnpkg.com/)

## Installation

```bash
# install nodejs and npm
brew install node

# set path for installing global packages
npm config get prefix
# in macOS, it should be /usr/local/
# you can set manually
npm config set prefix /usr/local
```

## Update

```bash
# with homebrew
brew upgrade node
npm install -g npm

node -v
npm -v
```

## Uninstallation

- [https://stackabuse.com/how-to-uninstall-node-js-from-mac-osx](https://stackabuse.com/how-to-uninstall-node-js-from-mac-osx)

```bash
brew uninstall node

# check all these dir, remove *node* and *npm*
cd ~
cd /usr/local/lib
cd /opt/local/lib
cd /usr/local/include
cd /opt/local/include
cd /usr/local/bin
cd /opt/local/bin
cd /usr/local/share/man/man1
cd /usr/local/lib/dtrace
cd /usr/local/share/doc/
cd /usr/local/share/systemtap/tapset
```

## Usage

```bash
# find all global packages
npm list -g --depth=0
```

## Global Packages For Web Dev

### neovim

```bash
# if use neovim as editor
npm install -g neovim
```

### browser-sync

- I need this because I use neovim, no IDE

```bash
# allow web developers use live server
npm install -g browser-sync

# usage
browser-sync start --server --files .
```

### sass

```bash
npm install -g sass
```

### eslint

```bash
# for eslint for some editor plugin, such as coc-eslint coc-vetur
npm i -g eslint -D

# this is just for the global settings you like
# if you want to use specific eslint
# install in local project to cover the global one
```

- You should also create an `eslintrc` file.
- `.eslintrc.json` and `.prettierrc.json` in home dir is the global eslint config, don't change it or add any plugin globally!
- If you are using `vue`, `html`, `react` in your projects and want to lint such files, you should install the eslint plugins in project by using `package.json` or `eslinrc.json`.
- Remember, put `eslint-plugin-*` only in your project, not globally!

```json
// here is a simple example for vue project
// `.eslintrc.json`


// more example: https://gist.github.com/adrianhall/70d63d225e536b4563b2
```

## Commonly Used Local Packages

### yarn

- I use npm in global, while sometimes use yarn in projects

```bash
# install yarn
npm install -g yarn
```

### some eslint plugins

```bash
npm i -g eslint eslint-plugin-vue -D

```
