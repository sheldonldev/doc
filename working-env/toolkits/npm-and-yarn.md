# npm & yarn

## Documentation

- [nodjs documentation](https://nodejs.org/en/docs/guides/)
- [learn nodejs](https://nodejs.dev/learn/introduction-to-nodejs)
- [npm](https://npmjs.com/)
- [yarn](https://yarnpkg.com/)
- [nvm](https://github.com/nvm-sh/nvm)

## Install node

```zsh
brew install node

# set path for installing global packages
npm config get prefix
# in macOS, it should be /usr/local/
# you can set manually
npm config set prefix /usr/local
```

## Install multi-version node with nvm

- Install `nvm`

```zsh
cd ~ && git clone https://github.com/nvm-sh/nvm.git .nvm
git checkout v0.37.2  # check out latest version
```

```zsh
# ~/.zshrc
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

# restart zsh and check
nvm -v
```

- Install and run `node.js`

```zsh
# list all versions
nvm ls-remote

# install LTS version
nvm install --lts  # the first version you install will become the default

nvm use node  # use default, or use specific version:
nvm exec 14.5.3 node --version  # or:
# if you also use node installed with prefix configured in /usr/local
nvm use --delete-prefix v14.15.3
```


## Update

```zsh
# with homebrew
brew upgrade node
npm install -g npm
```

## Uninstallation

- [https://stackabuse.com/how-to-uninstall-node-js-from-mac-osx](https://stackabuse.com/how-to-uninstall-node-js-from-mac-osx)

```zsh
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

```zsh
# find all global packages
npm list -g --depth=0

# analyze outdated packages
npm outdated -g --depth=3
```

## yarn

> I feel that yarn is much better for managing npm packages globally.

- It is recommended to install an independent yarn with `homebrew`;

```zsh
brew install yarn
```

- Usage

```zsh
yarn [global] add <packageName>

yarn [global] list --depth=0
```

- Path: `~/.config/yarn`, I init as a git repo:

{% embed url="https://github.com/sheldonldev/yarn_config" caption="My Global Yarnpkg" %}

## SemVer

- Semantic Versioning

```zsh
"dependencies": {
  "packageName": "prefixMAJOR.MINOR.PATCH"
  "express": "^4.4.14"
}

# MAJOR: increment when make incompatible API changes
# MINOR: increment when add a backwards-compatible functionality
# PATCH: increment when fix a backwards-compatible bug

# prefix (optional)
  # ~ : till the latest PATCH release
  # ^ : till the latest MINOR release
```

## Global Packages For Web Dev

### live-server

- I need this because I use neovim, no IDE

```zsh
# allow web developers use live server
yarn global add live-server

# usage
live-server file-name.html
live-server some-directory/
```

### sass

```zsh
yarn global add sass
```

### vue

```zsh
yarn global add @vue/cli
```


### intelephense

```zsh
yarn global add intelephense
```

## Commonly Used Local Packages

### Linters and Prettier

- Some project builder such as @vue/cli has its own lint, see its README:

```zsh
yarn lint
```

- In a JS project, Prettier and Eslint is commonly used.

#### Prettier
- [Prettier](https://prettier.io/docs/en/install.html)

```zsh
# Note: It’s important to install Prettier locally in every project, so each project gets the correct Prettier version.
yarn add --dev --exact prettier
echo {} > .prettierrc.json
cp .gitignore .prettierignore
yarn prettier --check .
yarn prettier --write .
```

#### Eslint

```zsh
yarn add --dev eslint   # and some other eslint plugins
yarn run eslint --init
yarn run eslint FileName.js
yarn eslint --fix
```

### tailwindcss

```zsh
yarn add tailwindcss
```

