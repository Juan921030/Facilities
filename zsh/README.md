1. Realizamos la instalacion de las siguiente librerias:
```
sudo apt install -y zsh konsole git 
```
luego le indicamos cual es la terminal con la que queremos trabajar con el comando:
```
chsh
/bin/zsh
```

2. creamos un fichero con el siguiente nombre y le ingresamos el siguiente contenido: 
```
cd ~/
touch .zshrc
vim .zshrc
```

```
# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
# Initialization code that may require console input (password prompts, [y/n]
# confirmations, etc.) must go above this block; everything else may go below.
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

ZINIT_HOME="${XDG_DATA_HOME:-${HOME}/.local/share}/zinit/zinit.git"
if [ ! -d "$ZINIT_HOME" ]; then
        mkdir -p "$(dirname $ZINIT_HOME)"
        git clone https://github.com/zdharma-continuum/zinit.git "$ZINIT_HOME"
fi

source "${ZINIT_HOME}/zinit.zsh"

zinit ice depth=1; zinit light romkatv/powerlevel10k

zinit light zsh-users/zsh-syntax-highlighting
zinit light zsh-users/zsh-completions
zinit light zsh-users/zsh-autosuggestions
zinit light Aloxaf/fzf-tab

zinit snippet OMZP::qrcode
zinit snippet OMZP::git
zinit snippet OMZP::aws
zinit snippet OMZP::sudo
zinit snippet OMZP::command-not-found
zinit snippet OMZP::python

autoload -U compinit && compinit

zinit cdreplay -q


# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh

bindkey '^p' history-search-backward
bindkey '^n' history-search-forward

HISTSIZE=5000
HISTFILE=~/.zsh_history
SAVEHIST=$HISTSIZE
HISTDUP=erase
setopt appendhistory
setopt sharehistory
setopt hist_ignore_space
setopt hist_ignore_all_dups
setopt hist_save_no_dups
setopt hist_ignore_dups
setopt hist_find_no_dups

zstyle ':completion:*' matcher-list 'm:{a-z}={A-Za-z}'
zstyle ':completion:*' list-colors "${(s.:.)LS_COLORS}"
zstyle ':completion:*' menu no
zstyle ':fzf-tab:complete:cd:*' fzf-preview 'ls --color $realpath'

eval "$(fzf --zsh)"
alias ll="ls -lha --color"
```
y reiniciamos el equipo.

3. luego descargamos el fzf de la fuente y lo movemos a la siguiente ruta:
```
cd ~/
wget https://github.com/junegunn/fzf/releases/download/0.52.1/fzf-0.52.1-linux_amd64.tar.gz
tar -xf fzf-0.52.1-linux_amd64.tar.gz
sudo mv fzf /usr/bin
```
y procedemos a configurar nuestra terminal.

4. para agregarle mas iconos realizamos el siguiente procedimiento:
```
cd ~/
mkdir .fonts
cd .fonts
git clone https://github.com/Juan921030/fonts.tar.git
tar -xf fonts.tar
rm fonts.tar
fc-cache -fv
```

5. si no sale la  opcion de configurar realizamos la configuracion con el siguiente comando:
```
p10k configure
```

para poner la terminal como preterminada ejecutamos el siguiente comando y elegimos la zsh
```
sudo update-alternatives --config x-terminal-emulator
```
