# Assignment on working with files

## Task 1
Navigate to your home directory

```bash
cd
```

## Task 2
?> <i class="fa-solid fa-circle-info"></i> You'll need this structure in a next Task

In your homedirectory, create the following structure:
`
PXL/Courses/S1/SystemsEss
`



```bash
mkdir -p PXL/Courses/S1/SystemsEss
```

## Task 3
Create, without leaving your homedirectory, an empty file named `empty` in each folder created in the previous Task

```bash
touch PXL/Courses/S1/SystemsEss/empty PXL/Courses/S1/empty PXL/Courses/empty PXL/empty
```

## Task 4
Remove, with just one command, the folder `PXL` with all contents created in the previous Task

```bash
rm -rf PXL
```

## Task 5
Create a new folder "My Pictures". Go into this folder and create, with just one command, these following files:
- Picture1.JPG
- picture2.JPG
- Picture3.jpg
- picture4.jpg

```bash
mkdir My\ Pictures
cd My\ Pictures
touch Picture1.JPG picture2.JPG Picture3.jpg picture4.jpg
```

## Task 6
Rename all files to with the command `rename` so no capitals exist anymore in any of the filenames

```bash
rename 's/P/p' *
rename 's/JPG/jpg' *
```

## Task 7 (Additional)
Make sure you are located in your homedirectory (~). <br/>
Copy all 'files' from this directory into a subdirectory named `backup` in your homefolder.

```bash
cd
mkdir backup
cp  ~/* backup

cp ~/.* backup # Also copy hidden files

```

# Assignment on working with directories

?> <i class="fa-solid fa-circle-info"></i> Some Tasks require a second user on your installation. 
Execute `sudo useradd -m piet` to create the new user
Execute `sudo passwd pieter` to set a password for the new user

## Task 8
Install the command `tree` on your ubuntu machine. You can use this command to get an over view of directorystructures on your system.

```bash
sudo apt install tree
```

## Task 9
Why doesn't tab-completion work when executing the following command to open .bashrc?:
`cat /home/student/.bash<tab>`

```
There are multiple files that start with .bash (history rc, logout,...)
```

## Task 10
Create this directorystructure with just 1 command:
`/home/student/school/aca_2018_2019/trimesters/2/vakken/ubuntuserver/exercises/chapter5`

```bash
mkdir -p /home/student/school/aca_2018_2019/trimesters/2/vakken/ubuntuserver/exercises/chapter5
```

## Task 11
Create, in the folder named 'exercises', a folder named 'chapter6'

```bash
mkdir  /home/student/school/aca_2018_2019/trimesters/2/vakken/ubuntuserver/exercises/chapter6
```

## Task 12
Remove the folder named 'chapter5'
```bash
Gooi chapter5 weg
rmdir /home/student/school/aca_2018_2019/trimesters/2/vakken/ubuntuserver/exercises/chapter5
```

## Task 13
Remove all folders starting from the school-directory

```bash
rm -rf /home/student/school
```

## Task 14
Navigate using absolute-path syntax into the home folder of the user named 'piet'

```bash
cd /home/piet
```


## Task 15
Navigate to your own home directory

```bash
cd
```

## Task 16
use cat to print the contents of the .bashrc file that is located in piet's homefolder. Use relative-path syntax.

```bash
cat ../piet/.bashrc
```

## Task 17
Try to navigate to another user's homefolder with a maximum of 7 keystrokes

```
cd -			    → 5 keystrokes
arrow up x 2	    → 3 keystrokes
cd /h<tab>p<tab>  	→ 9 keystrokes
cd ../p<tab>	    → 9 keystrokes
```

## Task 18
Clear the screen

```bash
clear
```

## Task 19
What are the differences between these commands?
- ls /etc/*
```
shows al dirs and files, and also the contents of the dirs
```

- ls /etc/*.*
```
shows all dirs and files with a . in the name, and also the contents of all dirs
```

- ls /etc/*a.*
```
shows all dirs and files with a 'a' in the name, and also the contents of all dirs
```

