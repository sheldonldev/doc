# Set Up MacOS

## Basic Tools for Programming

### Git

* See my posts.

### Homebrew

* Install [homebrew](https://brew.sh);

```bash
# no auto-update
export HOMEBREW_NO_AUTO_UPDATE=true
```

* In China, you have to change to the mirror

```bash
# 中科大镜像源
cd "$(brew --repo)" && git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" && git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-cask" && git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.zshrc
brew update

# reset
cd "$(brew --repo)" && git remote set-url origin https://github.com/Homebrew/brew.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" && git remote set-url origin https://github.com/Homebrew/homebrew-core.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-cask" && git remote set-url origin https://github.com/Homebrew/homebrew-cask.git
# export HOMEBREW_BOTTLE_DOMAIN=xxxxxxxxx // comment this line in .zshrc
brew update
```

### VSCode

* Install [VSCode](https://code.visualstudio.com/);
* Add it to `$PATH`;
* Settings:
  * Turn on `Settings Sync` extension, here is

    [my sync settings on gist](https://gist.github.com/sheldonldev/755e01f398a95ce339b302ad9a77ea19);

  * To open the settings page: `D-,`;
  * To open the shortcut page: `D-k D-s`;

### XCode

* Install `XCode` from AppleStore;
* Add it to `$PATH`;

### Optimize Terminal

* Install `zsh` and `iTerm`, set `zsh` as the default shell for both system and VSCode;
* Install font `Inconsolate for Powerline` and set it as text font for iTerm;
* Theme for zsh:

```bash
vim ~/.zshrc

ZSH_THEME='agnoster'
#comes from https://github.com/ohmyzsh/ohmyzsh/wiki/themes
```

* Syntax highlight for zsh:

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting

vim ~/.zshrc
# add 'source path/to/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh'
```

* Syntax autosuggestions for zsh:

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions

vim ~/.zshrc
# add 'source path/to/zsh-autosuggestions/zsh-autosuggestions.zsh'
```

* Open `Profile` section in settings, open `keys` tag, set `Left Option (Alt) Key` to `Esc+`;

