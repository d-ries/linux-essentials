# Assignment on working with files and folders

`Connect over ssh to you server to do the exercises'

## Task 1
Navigate to your home directory


## Task 2
?> <i class="fa-solid fa-circle-info"></i> You'll need this structure in a next Task

In your homedirectory, create the following structure:
`
PXL/Courses/S1/LinuxEss
`

## Task 3
Create, without leaving your homedirectory, an empty file named `empty` in each folder created in the previous Task

## Task 4
Install the command `tree` on your ubuntu machine. You can use this command to get an overview of directorystructures on your system. Search the manpage of tree to show the contents of the root directory and one extra level.

## Task 5
Why doesn't tab-completion work when executing the following command to open .bashrc?:
`cat /home/student/.bash<tab>`


## Task 6
Create a new folder "My Pictures" in you homefolder. Go into this folder and create, with just one command, these following files (notice the capitalization):
- Picture1.JPG
- picture2.JPG
- Picture3.jpg
- picture4.jpg


## Task 7
Rename all files to with the command `rename` so no capitals exist anymore in any of the filenames


## Task 8
Make sure you are located in your homedirectory (~). <br/>
Copy all 'files' from this directory into a subdirectory named `backup` in your homefolder.

## Task 9
Remove, with just one command, the folder `PXL` with all contents created in the previous Task


## Task 10
Create this directorystructure with just 1 command:
`/home/student/school/semester/1/courses/ubuntuserver/exercises/chapter5`


## Task 11
Create, in the folder named 'exercises', a folder named 'chapter6'


## Task 12
Remove the folder named 'chapter5'


## Task 13
Remove all folders starting from the school-directory  


?> <i class="fa-solid fa-circle-info"></i> Some Tasks require a second user on your installation. 
Execute `sudo useradd -m johndoe` to create the new user
Execute `sudo passwd johndoe` to set a password for the new user

## Task 14
Navigate using absolute-path syntax into the home folder of the user named 'johndoe'


## Task 15
Navigate to your own home directory


## Task 16
use cat to print the contents of the .bashrc file that is located in johndoe's homefolder. Use a relative-path syntax.


## Task 17
Try to navigate to the other user's homefolder with a maximum of 7 keystrokes


## Task 18
Clear the screen


## Task 19
Multiple people can have a ssh connection to the same server and meanwhile a person can be working on the server itself. Each person will have it's own screen (terminal window). 
Make sure you are logged in on the server itself and are also logged in over ssh. Make sure you see both screens at the same time.  

Search for commands that have the text "logged on" in their short description of the manpage

  
## Task 20
In the shell of your ssh session type one of the two commands you found in the previous task.
You will see two screens, tty1 and .
  
Everything is a file in linux. This is also true for the screen/window you're working in. When you are connected over _ssh_, your screen name is _pts/2_. When you are working _on the server_ itself, your screen name is _tty1_.  
  
In the shell of your ssh session type `echo hello there > /dev/tty1`. The greater than sign will redirect the output of the text _hello there_ to the tty1 device. The text appears on the screen on the server.
  
Try the following command in the shell of you ssh connection: `sl > /dev/tty1`.
  
If you want to see your prompt again on the server itself, you just have to press _enter_
