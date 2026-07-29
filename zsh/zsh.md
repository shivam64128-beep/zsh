# load modules
zmodload zsh/complist
autoload -U compinit && compinit
autoload -U colors && colors

# fortune -s | cowthink

eval "$(starship init zsh)"

#bindings
bindkey -v
bindkey -M viins 'jk' vi-cmd-mode
bindkey '^\' autosuggest-toggle

bindkey '^[[A' history-substring-search-up
bindkey '^[[B' history-substring-search-down
bindkey -M vicmd '^k' history-substring-search-up
bindkey -M vicmd '^j' history-substring-search-down

bindkey "^J" history-search-forward
bindkey "^K" history-search-backward
bindkey '^R' fzf-history-widget
bindkey '^H' autosuggest-accept

zstyle :compinstall filename '/home/shivam/.zshrc'
zstyle ':completion:*' menu select
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Za-z}'

# history
HISTFILE=~/.zsh_history
HISTCONTROL=ignoreboth
HISTSIZE=100000
SAVEHIST=100000

setopt APPEND_HISTORY
setopt SHARE_HISTORY
setopt HIST_IGNORE_DUPS
setopt HIST_IGNORE_SPACE
setopt HIST_EXPIRE_DUPS_FIRST
setopt HIST_FIND_NO_DUPS
setopt AUTOCD
setopt NOBEEP
 
source <(fzf --zsh)

function yazi-widget() {
  yazi
  zle reset-prompt
}
zle -N yazi-widget
bindkey '^f' yazi-widget

function open_impala() {
    impala
    zle reset-prompt
}
zle -N open_impala
bindkey '^w' open_impala

function open_bluetui() {
    bluetui
   zle reset-prompt
}
zle -N open_bluetui
bindkey '^b' open_bluetui

function open_wiremix() {
    wiremix
    zle reset-prompt
}
zle -N open_wiremix
bindkey '^a' open_wiremix

export EDITOR="nvim"
export VISUAL="nvim"
export TERM="foot"
export TERMINAL="foot"
export MAN="nvim +MAN!"


# alias
alias claer='clear'
alias date='date +\%F\/\%T'
alias time="tty-clock -S -c -C 4 -b"
alias cat='bat'
alias grep='rg --color=auto'
alias diff='diff --color=auto'
alias df='df -h'
alias ls='eza -lh --icons --git'
alias la='eza -lah --icons --git'
alias tree='eza --tree --icons'
compdef eza=ls

autoload -Uz compinit
compinit

#plugins
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/share/zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/share/zsh/plugins/zsh-history-substring-search/zsh-history-substring-search.zsh
