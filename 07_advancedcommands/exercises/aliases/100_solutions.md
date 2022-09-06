# Aliases

## Task 1
Install the package lolcat and create an alias to run `lolcat` instead of `cat`
sudo apt install lolcat
alias cat='lolcat'

## Task 2
Once tested make sure that your alias will be remembered in the future (after reboot, etc)
nano ~/.bash_aliases
cat='lolcat'

## Task 3
Create an aliases to clear you screen when you give the command `c`
alias c='clear'

## Task 4
Remove the alias `c` to clear your screen
unalias c
