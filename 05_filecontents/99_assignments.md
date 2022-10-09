# Assignment on file contents

## Task 1
Find out why you should use ‘less’ instead of ‘more’

## Task 2
Show the first line of the file /proc/meminfo to find out how much memory you’ve given to your Ubuntu Virtual machine.

## Task 3
Show the last line of the file passwd located in the folder etc of the root folder

## Task 4
Show the first 4 characters (=bytes) of the file /etc/passwd. What do you see? 

## Task 5
Use cat to put the following text in a new file "mytextfile" in your home folder:  
This is my text  
spaced over multiple lines
inserted by cat.

## Task 6
Use echo to put the following text in a new file "myechotextfile" in your home folder:  
This is my text  
spaced over multiple lines
inserted by echo.

## Task 7
Use cat to copy the file .bashrc in your home folder to a new file named .bashrc.backup

## Task 8
When you add a new user, a new line is added to the file /etc/passwd. Show the contents of the file but in order from newest user to oldest user (other way around than normal) 

## Task 9
Use the tail command to keep the file /var/log/auth.log open, so that you see all new log entries appear when they happen. (You can press enter a few times to seperate the new coming lines) In a new Powershell window start a new ssh session and log in. Then log out again. Wat did you see in the logs?

## Task 10
Open the configuration file of ssh, _/etc/ssh/sshd_config_, with the _less_ command and try the search function to search for X11. This is something we'll use later on to enable screens to open over SSH.

## Task 11
Use nano to edit the text in the file "myechotextfile" you created earlier in your home folder:  
This is my text, edited,  
still spaced over multiple lines  
inserted by echo and edited by nano.  

## Task 12
Use cat with the end marker "LinuxIsFun" to overwrite the text in the file "myechotextfile" you created earlier in your home folder:  
This text is way more interesting.  
I still use multiple lines d'oh,  
just because I can.  

## Task 13
Print the full contents of the previously made files "mytextfile" and "myechotextfile" with only one command.

## Task 14
Get the last 10 created users and put them in the file "newestUsers" with only one command.

## Task 15
Change the password part of the student user to the know password "pxl" in the file "newestUsers".

## Optional Task
use the command `vimtutor` to learn how to use vim. What is so different with this editor? 
