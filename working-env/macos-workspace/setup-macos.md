# Setup MacOS

## Basic Tools for Programming

### Homebrew

- Install [homebrew](https://brew.sh);

### VSCode

- Install [VSCode](https://code.visualstudio.com/);
- Add it to `$PATH`;
- Settings:
  - Turn on `Settings Sync` extension, here is
    [my sync settings on gist](https://gist.github.com/sheldonldev/755e01f398a95ce339b302ad9a77ea19);
  - To open the settings page: `D-,`;
  - To open the shortcut page: `D-k D-s`;

### XCode

- Install `XCode` from AppleStore;
- Add it to `$PATH`;

### Git

{% embed url="https://doc.sheldonl.dev/working-env/git-and-github/install-and-set-up-git" caption="First-Time Git Setup" %}

### Optimize Terminal

- Install `zsh` and `iTerm`, set `zsh` as the default shell for both system and VSCode;
- Install font `Inconsolate for Powerline` and set it as text font for iTerm;
- Theme for zsh:

```bash
vim ~/.zshrc

ZSH_THEME='agnoster'
#comes from https://github.com/ohmyzsh/ohmyzsh/wiki/themes
```

- Syntax highlight for zsh:

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting

vim ~/.zshrc
# add 'source path/to/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh'
```

- Syntax autosuggestions for zsh:

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions

vim ~/.zshrc
# add 'source path/to/zsh-autosuggestions/zsh-autosuggestions.zsh'
```
