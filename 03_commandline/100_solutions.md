# Solutions on command line

Do the first exercises while being in the Ubuntu Server (no ssh)

## Task 1
Make use of the command `man man` to figure out what the commando `man -f` does and with which other command it can be replaced  

<br/>![man man_1](images/man_man_1.png)  

<br/>![man man_2](images/man_man_2.png)

## Task 2
Make use of the command `man` to figure out what the option is for the command `shutdown` to reboot the machine instead of powering off  

<br/>![man_shutdown.png](images/man_shutdown.png)

## Task 3
Use the command `apropos` and/or the command `man -k` to find the right commando to:
- __reboot__ your vm
- change your __password__ or another __user__'s password
- show the __contents__ of a directory
- __clear__ the terminal screen
- see who is __logged in__/__on__ --> try all the commands
- see how much free __memory__ the server has  --> search in the manpage of this command how you can get the output more human readable (search in the manpage for _human_)
- see how much __disk space__ you have free   

<br/>![apropos1](images/apropos1.png)  

<br/>![apropos2](images/apropos2.png)
  

## Task 4
Use the manpage of `ls` to figure out how you could also see the hidden files. Show the hidden files of your homefolder

<br/>![man_ls](images/man_ls.png)

## Task 5 
Try to only show the short description of the commando `ls`  

<br/>![whatis_ls](images/whatis_ls.png)

## Task 6 
Try to figure out where the command `reboot` and its manpage are stored on the disk  

<br/>![whereis_reboot](images/whereis_reboot.png)

## Task 7 
Run the command `cd`. Run the command to also view the hidden files in this directory. Then run the command `cat .bashrc`. This file contains a script which runs every time you open a new shell (eg. terminal window). We will explain it in a later lesson. Run the command to clear the screen  

<br/>![hidden_files_cat](images/hidden_files_cat.png)  
<br/>![clear](images/clear.png)


## Task 8
Connect from Powershell on your laptop to your server over SSH and stay connected for the duration of the exercises. The benefit is that you can scroll through your screens with the mouse  

<br/>![Connect via Powershell](images/Connect_via_Powershell.png)  

## Task 9 
Use the arrow keys to go to the command `cat .bashrc` and use the arrow keys again to change it to `cat .bash_history`. Hit enter to execute the command. This file holds your history. It receives your history of commands when you close a shell (close terminal window, logout, ...). You do not see the last commands you typed in this shell

<br/>![bash_history](images/bash_history.png)


## Task 10
Run the command to shutdown you server immediately. Restart you server via VMware Workstation.
Connect to your server over SSH and stay connected for the exercises. If it doesn't work you have to check the IP of the server (from VMware Workstation).
Try to use the history to rerun the command `cat .bash_history`. You will now see that the commands are added of the session before you rebooted. Every time you start a new shell the commands from this file are copied into the shell's memory so we can use the history.
`sl` is to prank people who mistype 

<br/>![bash_history](images/bash_history.png)


## Task 11
Run the command ` echo This is the echo command with a space in front`. Mind the space at the beginning of the line, before the echo command.
Run the command `echo This is the echo command with no leading space`. Mind that there is no space in front of the echo command.
Type `history 3` to check your history.
You'll notice that commands started with a space will not be kept in history.
Run the command `ls -a`.
Run the same command `ls -a` again.
Type `history 5` to check your history.
You'll notice that repeating the same command consecutive will only keep the first occurence in history.  

<br/>![not_in_history](images/not_in_history.png)


## Task 12
Run the command `apt install sl`. You'll notice more privileges are needed. We have to rerun this command with root privileges. Run the command `sudo !!` to rerun the last command with sudo in front. `sl` is to prank people that mistype the command `ls`. Type `sl` en push `enter`

<br/>![sl1](images/sl1.png)
<br/>![sl2](images/sl2.png)


## Task 13
Push the key combination `CTRL-R` and type `shu` to search for the last used shutdown command. Use the right arrow key to edit the line and change the command to `sudo shutdown -r now` and press enter to reboot your server. You can follow the boot process in VMware Workstation. Connect to your server over SSH and stay connected for the exercises. If it doesn't work you have to check the IP of the server (from VMware Workstation).  

<br/>![ctrl_r](images/ctrl_r.png)


## Task 14
Push the key combination `CTRL-R` and type `shu` to search for the last used shutdown command. We see the command to `sudo shutdown -r now`. We __don't__ want to reboot the server.  So we push the key combination `CTRL-R` again to go to an older command that has 'shu' in the name. Keep repeating the key combination untill you see the command `sudo shutdown now` and press enter  

<br/>![ctrl_r2](images/ctrl_r2.png)


## Task 15
Try to connect from the Ubuntu Desktop to the Ubuntu Server over ssh.  

<br/>![Connect via Powershell](images/Connect_via_Powershell.png) 

## Task 16
Install `Windows Terminal` on your Windows laptop via the 'Microsoft Store'. Try to connect from the Windows Terminal to the Ubuntu Server over ssh. 

<br/>![windows_terminal1](images/windows_terminal1.png)
<br/>![windows_terminal2](images/windows_terminal2.png)
