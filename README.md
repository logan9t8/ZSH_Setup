# ZSH Ricing on Arch Linux

## Preview
![image](https://github.com/user-attachments/assets/2070efa6-022a-4d68-b82f-d3163a68a075)

![image](https://github.com/user-attachments/assets/d81293c8-9470-4a0f-b05f-8b64d8408e3d)

![image](https://github.com/user-attachments/assets/0ab8fdac-0adf-4a42-bc68-8e456860cec1)



## Packages Installation
```shell
sudo pacman -S cmake fzf powerline powerline-vim python-pygments shfmt shellcheck \
ttf-fira-code zsh-completions zsh-history-substring-search zsh-syntax-highlighting
yay -S autojump ttf-meslo-nerd-font-powerlevel10k zsh-theme-powerlevel10k-git
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## Configuration
```shell
mv .zshrc .zshrc.omz
mv .zshrc.pre-oh-my-zsh .zshrc
ln -sf /usr/share/zsh-theme-powerlevel10k $HOME/.oh-my-zsh/themes/powerlevel10k
source /usr/share/zsh-theme-powerlevel10k/powerlevel10k.zsh-theme
mkdir -p $HOME/.config/powerline
cp -r /usr/lib/python$(python -V | awk '{print $2}' | cut -d. -f1,2)/site-packages/powerline/config_files/* $HOME/.config/powerline
cp ./backup/default.json ~/.config/powerline/themes/tmux/default.json
```

Add the below to `.vimrc`
```shell
set rtp+=/usr/share/powerline/bindings/vim
if exists('+termguicolors')
    let &t_8f="\<Esc>[38;2;%lu;%lu;%lum"
    let &t_8b="\<Esc>[48;2;%lu;%lu;%lum"
    set termguicolors "Enable 24-bit colors
else
set t_Co=256 "Fallback to 8-bit colors
endif
```

Add the below to `.zshrc` 

```bash
# Tmux autostart
if [[ $(ps -o args= $PPID | awk -F' ' '{print $1}') =~ '<YourTerminalEmualtorName>|init' ]]; then
    ZSH_TMUX_AUTOSTART=true
    #ZSH_TMUX_AUTOQUIT=false
fi

# Theme
if [[ -f $HOME/.p10k.zsh ]]; then
    source $HOME/.p10k.zsh && ZSH_THEME=powerlevel10k/powerlevel10k
elif [[ -f /usr/share/powerline/bindings/zsh/powerline.zsh ]]; then
    source /usr/share/powerline/bindings/zsh/powerline.zsh
elif [[ -f $HOME/.oh-my-zsh/oh-my-zsh.sh ]]; then
    ZSH_THEME=agnoster
else
    autoload -Uz promptinit && promptinit && prompt adam2
fi

# 3rd party settings

# Per your needs https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins
plugins=(
    aliases
    autojump
    colored-man-pages
    colorize
    fzf
    history-substring-search
    tmux
    zsh-interactive-cd
)

source $HOME/.oh-my-zsh/oh-my-zsh.sh
source $HOME/.arrows.sh
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/share/zsh/plugins/zsh-history-substring-search/zsh-history-substring-search.zsh
bindkey "$terminfo[kcuu1]" history-substring-search-up
bindkey "$terminfo[kcud1]" history-substring-search-down
```

Add ```arrows.sh```, ```tmux_bindings.sh``` and ```tmux.conf``` to home dir and rename them by prefixing with a ```.```

## Credits
1. https://sourceforge.net/projects/zsh/
1. https://github.com/wting/autojump
1. https://github.com/tonsky/FiraCode
1. https://github.com/junegunn/fzf
1. https://github.com/ryanoasis/nerd-fonts
1. https://github.com/ohmyzsh/ohmyzsh
1. https://github.com/romkatv/powerlevel10k
1. https://github.com/powerline/powerline
1. https://github.com/pygments/pygments
1. https://github.com/mvdan/sh
1. https://github.com/koalaman/shellcheck
1. https://github.com/tmux/tmux/wiki
1. https://github.com/zsh-users/zsh-completions
1. https://github.com/zsh-users/zsh-history-substring-search
1. https://github.com/zsh-users/zsh-syntax-highlighting
