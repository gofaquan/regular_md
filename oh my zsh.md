##### 下载zsh
`sudo yay -Sy zsh`

##### 下载ohmyzsh
`sudo nano /etc/hosts`
````
151.101.76.133 raw.githubusercontent.com
199.232.68.133 user-images.githubusercontent.com
199.232.68.133 avatars2.githubusercontent.com
199.232.68.133 avatars1.githubusercontent.com
140.82.112.4   github.com
````
###### 引入代理
export https_proxy=http://127.0.0.1:8889 http_proxy=http://127.0.0.1:8889

` sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`


##### 切换默认shell为zsh
`chsh -s /bin/zsh`
##### 安装zsh命令自动补全插件
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/plugins/zsh-autosuggestions
##### 安装高亮彩色显示插件
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/plugins/zsh-syntax-highlighting
##### 安装powerlevel9k主题
git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
##### 安装字体图标
yay -Sy awesome-terminal-fonts
##### 将下面的文本复制进~/.zshrc里面
但是在复制之前 需要将第6行中的
export ZSH="/home/womanjaro/.oh-my-zsh" womanjaro
————————————————
````
export TERM="xterm-256color"
# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH

# Path to your oh-my-zsh installation.
export ZSH="/home/archlinux/.oh-my-zsh"

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time oh-my-zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/robbyrussell/oh-my-zsh/wiki/Themes
POWERLEVEL9K_MODE='awesome-fontconfig'
ZSH_THEME="powerlevel9k/powerlevel9k"
#ZSH_THEME="robbyrussell"

# Set list of themes to pick from when loading at random
# Setting this variable when ZSH_THEME=random will cause zsh to load
# a theme from this variable instead of looking in ~/.oh-my-zsh/themes/
# If set to an empty array, this variable will have no effect.
# ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" )

# Uncomment the following line to use case-sensitive completion.
# CASE_SENSITIVE="true"

# Uncomment the following line to use hyphen-insensitive completion.
# Case-sensitive completion must be off. _ and - will be interchangeable.
# HYPHEN_INSENSITIVE="true"

# Uncomment the following line to disable bi-weekly auto-update checks.
# DISABLE_AUTO_UPDATE="true"

# Uncomment the following line to change how often to auto-update (in days).
# export UPDATE_ZSH_DAYS=13

# Uncomment the following line to disable colors in ls.
# DISABLE_LS_COLORS="true"

# Uncomment the following line to disable auto-setting terminal title.
# DISABLE_AUTO_TITLE="true"

# Uncomment the following line to enable command auto-correction.
# ENABLE_CORRECTION="true"

# Uncomment the following line to display red dots whilst waiting for completion.
# COMPLETION_WAITING_DOTS="true"

# Uncomment the following line if you want to disable marking untracked files
# under VCS as dirty. This makes repository status check for large repositories
# much, much faster.
# DISABLE_UNTRACKED_FILES_DIRTY="true"

# Uncomment the following line if you want to change the command execution time
# stamp shown in the history command output.
# You can set one of the optional three formats:
# "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
# or set a custom format using the strftime function format specifications,
# see 'man strftime' for details.
# HIST_STAMPS="mm/dd/yyyy"

# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder

# Which plugins would you like to load?
# Standard plugins can be found in ~/.oh-my-zsh/plugins/*
# Custom plugins may be added to ~/.oh-my-zsh/custom/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
)


source $ZSH/oh-my-zsh.sh
source ~/.oh-my-zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

# User configuration

# export MANPATH="/usr/local/man:$MANPATH"

# You may need to manually set your language environment
# export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='mvim'
# fi

# Compilation flags
# export ARCHFLAGS="-arch x86_64"

# ssh
# export SSH_KEY_PATH="~/.ssh/rsa_id"

# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"

# ==== Theme Settings ====
# PowerLevel9k
#下面这个变量表示最左侧的提示符所显示的内容，默认是 `%n@%m`，也就是你的用户名以及终端名称。 
POWERLEVEL9K_CONTEXT_TEMPLATE="%n@%m"
# 左侧栏目显示的要素（指定的关键字参考官网）
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(os_icon context dir vcs dir_writable)
# 右侧栏目显示的要素
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status root_indicator background_jobs time virtualenv)
#新起一行显示命令 (推荐！极其方便）
POWERLEVEL9K_PROMPT_ON_NEWLINE=true
#右侧状态栏与命令在同一行
POWERLEVEL9K_RPROMPT_ON_NEWLINE=true
#显示是否可读可写权限图标
POWERLEVEL9K_DIR_SHOW_WRITABLE=true
#缩短目录层级
POWERLEVEL9K_SHORTEN_DIR_LENGTH=3
#缩短目录策略：隐藏上层目录中间的字
#POWERLEVEL9K_SHORTEN_STRATEGY="truncate_middle"
#添加连接上下连接箭头更方便查看
POWERLEVEL9K_MULTILINE_FIRST_PROMPT_PREFIX="↱"
POWERLEVEL9K_MULTILINE_LAST_PROMPT_PREFIX="↳ "
# 新的命令与上面的命令隔开一行
#POWERLEVEL9K_PROMPT_ADD_NEWLINE=true
# Git仓库状态的色彩指定
POWERLEVEL9K_VCS_CLEAN_FOREGROUND='orange'
POWERLEVEL9K_VCS_CLEAN_BACKGROUND='red'
POWERLEVEL9K_VCS_UNTRACKED_FOREGROUND='yellow'
POWERLEVEL9K_VCS_UNTRACKED_BACKGROUND='black'
POWERLEVEL9K_VCS_MODIFIED_FOREGROUND='red'
POWERLEVEL9K_VCS_MODIFIED_BACKGROUND='black'

POWERLEVEL9K_TIME_FOREGROUND='red' 
POWERLEVEL9K_TIME_BACKGROUND='green'


#color{{{
autoload colors
colors

for color in RED GREEN YELLOW BLUE MAGENTA CYAN WHITE; do
eval _$color='%{$terminfo[bold]$fg[${(L)color}]%}'
eval $color='%{$fg[${(L)color}]%}'
(( count = $count + 1 ))
done
FINISH="%{$terminfo[sgr0]%}"
#}}}


#命令提示符
#RPROMPT=$(echo "$RED%D %T$FINISH")
#PROMPT=$(echo "$CYAN%n@$YELLOW%M:$GREEN%/$_YELLOW>$FINISH ")


#PROMPT=$(echo "$BLUE%M$GREEN%/
#$CYAN%n@$BLUE%M:$GREEN%/$_YELLOW>>>$FINISH ")
#标题栏、任务栏样式{{{
case $TERM in (*xterm*|*rxvt*|(dt|k|E)term)
precmd () { print -Pn "\e]0;%n@%M//%/\a" }
preexec () { print -Pn "\e]0;%n@%M//%/\ $1\a" }
;;
esac
#}}}

#关于历史纪录的配置 {{{
#历史纪录条目数量
export HISTSIZE=10000
#注销后保存的历史纪录条目数量
export SAVEHIST=10000
#历史纪录文件
export HISTFILE=~/.zhistory
#以附加的方式写入历史纪录
setopt INC_APPEND_HISTORY
#如果连续输入的命令相同，历史纪录中只保留一个
setopt HIST_IGNORE_DUPS
#为历史纪录中的命令添加时间戳
setopt EXTENDED_HISTORY

#启用 cd 命令的历史纪录，cd -[TAB]进入历史路径
setopt AUTO_PUSHD
#相同的历史路径只保留一个
setopt PUSHD_IGNORE_DUPS

#在命令前添加空格，不将此命令添加到纪录文件中
#setopt HIST_IGNORE_SPACE
#}}}

# 补全{{{
#彩色补全菜单
eval $(dircolors -b)
export ZLSCOLORS="${LS_COLORS}"
zmodload zsh/complist
zstyle ':completion:*' list-colors ${(s.:.)LS_COLORS}
zstyle ':completion:*:*:kill:*:processes' list-colors '=(#b) #([0-9]#)*=0=01;31'

#修正大小写
zstyle ':completion:*' matcher-list '' 'm:{a-zA-Z}={A-Za-z}'
#错误校正
zstyle ':completion:*' completer _complete _match _approximate
zstyle ':completion:*:match:*' original only
zstyle ':completion:*:approximate:*' max-errors 1 numeric

#kill 命令补全
compdef pkill=kill
compdef pkill=killall
zstyle ':completion:*:*:kill:*' menu yes select
zstyle ':completion:*:*:*:*:processes' force-list always
zstyle ':completion:*:processes' command 'ps -au$USER'

#补全类型提示分组
#zstyle ':completion:*:matches' group 'yes'
#zstyle ':completion:*' group-name ''
#zstyle ':completion:*:options' description 'yes'
#zstyle ':completion:*:options' auto-description '%d'
#zstyle ':completion:*:descriptions' format $'\e[01;33m -- %d --\e[0m'
#zstyle ':completion:*:messages' format $'\e[01;35m -- %d --\e[0m'
#zstyle ':completion:*:warnings' format $'\e[01;31m -- No Matches Found --\e[0m'
#zstyle ':completion:*:corrections' format $'\e[01;32m -- %d (errors: %e) --\e[0m'

# cd ~ 补全顺序
zstyle ':completion:*:-tilde-:*' group-order 'named-directories' 'path-directories' 'users' 'expand'
#}}}


##行编辑高亮模式 {{{
# Ctrl+@ 设置标记，标记和光标点之间为 region
zle_highlight=(region:bg=magenta #选中区域
special:bold      #特殊字符
isearch:underline)#搜索时使用的关键字
#}}}

##空行(光标在行首)补全 "cd " {{{
user-complete(){
case $BUFFER in
"" )                       # 空行填入 "cd "
BUFFER="cd "
zle end-of-line
zle expand-or-complete
;;
"cd --" )                  # "cd --" 替换为 "cd +"
BUFFER="cd +"
zle end-of-line
zle expand-or-complete
;;
"cd +-" )                  # "cd +-" 替换为 "cd -"
BUFFER="cd -"
zle end-of-line
zle expand-or-complete
;;
* )
zle expand-or-complete
;;
esac
}
zle -N user-complete
bindkey "\t" user-complete
#}}}



#命令别名 {{{
alias cp='cp -i'
alias mv='mv -i'
alias rm='rm -i'
alias ls='ls -F --color=auto'
alias ll='ls -l --color=auto'
alias grep='grep --color=auto'
alias la='ls -a'
alias pacman='pacman --color=auto'
alias yay='yay --color=auto'
#}}}


#漂亮又实用的命令高亮界面
setopt extended_glob
TOKENS_FOLLOWED_BY_COMMANDS=('|' '||' ';' '&' '&&' 'sudo' 'do' 'time' 'strace')

#
#recolor-cmd() {
#region_highlight=()
#colorize=true
#start_pos=0
#for arg in ${(z)BUFFER}; do
#((start_pos+=${#BUFFER[$start_pos+1,-1]}-${#${BUFFER[$start_pos+1,-1]## #}}))
#((end_pos=$start_pos+${#arg}))
#if $colorize; then
#colorize=false
#res=$(LC_ALL=C builtin type $arg 2>/dev/null)
#case $res in
#*'reserved word'*)   style="fg=magenta,bold";;
#*'alias for'*)       style="fg=cyan,bold";;
#*'shell builtin'*)   style="fg=yellow,bold";;
#*'shell function'*)  style='fg=green,bold';;
#*"$arg is"*)
#[[ $arg = 'sudo' ]] && style="fg=red,bold" || style="fg=blue,bold";;
#*)                   style='none,bold';;
#esac
#region_highlight+=("$start_pos $end_pos $style")
#fi
#[[ ${${TOKENS_FOLLOWED_BY_COMMANDS[(r)${arg//|/\|}]}:+yes} = 'yes' ]] && colorize=true
#start_pos=$end_pos
#done
#}
#check-cmd-self-insert() { zle .self-insert && recolor-cmd }
#check-cmd-backward-delete-char() { zle .backward-delete-char && recolor-cmd }
#
#zle -N self-insert check-cmd-self-insert
#zle -N backward-delete-char check-cmd-backward-delete-char

export PATH="/opt/nvim-linux64/bin:$PATH"
export PATH="/root/.gem/ruby/2.6.0/bin:$PATH"

#export http_proxy="127.0.0.1:12333"
#export https_proxy="127.0.0.1:12333"
[ -f ~/.fzf.zsh ] && source ~/.fzf.zsh
