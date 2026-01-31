[![Joknarf Tools](https://img.shields.io/badge/Joknarf%20Tools-Visit-darkgreen?logo=github)](https://joknarf.github.io/joknarf-tools)
[![Shell](https://img.shields.io/badge/shell-bash%20|%20zsh%20|%20ksh%20-blue.svg)]()
[![Licence](https://img.shields.io/badge/licence-MIT-blue.svg)](https://shields.io/)

# nerdp
Nerd prompt for bash/ksh/zsh (mksh/ash)  

## demo
<img width="900" alt="image" src="https://github.com/joknarf/nerdps1/assets/10117818/ebc3f680-69b1-45d2-b1ce-b09b09b545f2">

## features

The following information is displayed:

* exit code if command returns code is not 0
* elapse time during command if command lasts more than 1s (bash / zsh / ksh >2012)
* user@hostname
* current working directory
* git branch if in git directory (colorized according to git status)
* python VIRTUAL_ENV and other variables values with name in `ps1_info` variable
* filesystem usage check of `ps1_fslist` (default "/ /tmp") according to `ps1_fslimits` (default "95 100")
* 1min cpu load (colorized default `ps1_loadlimits` "10 20")
* Available memory (colorized default `ps1_memlimits` "300 100" MB)
* Time

## Install

* You can install using a plugin manager like sheldon / zgenom or the best [thefly](https://github.com/joknarf/thefly) : plugin joknarf/nerdp
```
fly add joknarf/nerdp
```
* Or you can get your local copy and source in your rc file:  
```
curl -sL -o ~/nerdp https://raw.githubusercontent.com/joknarf/nerdp/main/nerdp
. ~/nerdp
```
* To test it you can activate the nerdp prompt directly using:  
```
. <(curl -s https://raw.githubusercontent.com/joknarf/nerdp/main/nerdp)
```

## Font for prompt

For better experience, install a Nerd font on your system/console (Windows console / Windows terminal / putty / git-bash / CmdEr / iTerm2 / Terminator / MobaXterm / VScode terminal / Pycharm terminal...):  
[Nerd Fonts](https://www.nerdfonts.com/)

on Unix, copy to `~/.fonts` and run `fc-cache -fv` then relaunch your terminal and set the font

  
## choose your style
set `ps1_style` variable to available styles in your .nerdrc  
You can test using `ps1_style` function:

![image](https://github.com/joknarf/nerdps1/assets/10117818/f8d32297-73f4-4827-9802-b635c9d9a481)


## Font rendering

If your terminal does not manage correctly nerd font symbols, you may switch to more commonly supported powerline font symbols, or even disable the segment separator symbols.  
You can use : `ps1_display` function/var to switch prompt display symbol characters:
```
$ ps1_display -h
usage: ps1_display <option>
    <option>: nerdicons, nerd, powerline, nofont, ascii
```

## Customizing prompt

You can add informations on the prompt using ps1_info variable:  

* `ps1_info="MYVAR MYVAR2..."` : will display content of variables
* `ps1_info="(myfunc) (myfunc2)"` : will display output of functions myfunc myfunc2

You can add custom colorized segment defining `ps1_addon()` function:

* `ps1_addon() { pgrep rsyslogd >/dev/null || echo 'red:syslog'; }`
output format of function:
  `<bgcolor>[/<fgcolor>/<sepcolor>]:<message>[|message]`
empty output discards the segment.

Changing prompt powerline, ps1_powerline variable represents the prompt:

*  segment setting : `symbol/bgcolor/fgcolor/sepcolor:function`
    * function called is `ps1_function` (ps1_ prefixed)
    * colors : `black red green yellow blue magenta cyan white`, prefix `l` for light color
    * symbols : `< > ( )`
    * when color is set to auto, the function output must be `<color>:<text>` else only `<text>`
* right alignment separator : `|`
* `ps1_powerline="(/auto:exit_status (/blue:userhost )/auto:git_branch )/lblack:cwd > | (/lblue/black/blue:info (/auto:freemem (/blue:time )"`
![image](https://github.com/joknarf/nerdps1/assets/10117818/54fa6b66-03b5-4b04-8920-a461efcd9ca4)
* `ps1_powerline="auto:exit_status blue:userhost >/auto:git_branch >/lblack:cwd > | </lblue/black/blue:info </auto:freemem </blue:time"`
![image](https://github.com/joknarf/nerdps1/assets/10117818/f5d3bc4e-cf65-4889-af5b-817445575ef7)

## Customizing colors

colors are defined with `$ps1_col` / `$ps1_lcol` variables, and can be overridden, if `$ps1_col` is empty will use 16 default terminal colors.

* `ps1_col` : 8 RGB colors codes corresponding to names: black red green yellow blue magenta cyan white
  * default: `"20;25;25 160;0;0 36;114;67 175;138;27 30;90;180 55;35;126 41;98;114 204;204;204"`
* `ps1_lcol` : 8 RGB colors cores corresponding to name: lblack lred lgreen lyellow lblue lmagenta lcyan lwhite
  * default: `"32;64;64 252;78;110 24;237;147 222;220;18 118;141;255 255;126;128 142;221;244 238;238;238"`
