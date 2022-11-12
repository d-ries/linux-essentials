# Automation

## Bash scripts
Scripting is a great way to automate simple tasks or chains of commands. Imagine you want to take a backup. Usually this means creating a `zip` archive of certain files and folders, giving this `zip` file the appropriate name and then move the `zip` file to a certain folder. Running these commands manually is prone to errors and time consuming. A better way would be to bundle these commands in a script, so we can instead run one command that will trigger running all of the steps described above.

In Ubuntu we often use _bash_ scripts. _bash_ refers to the default shell that we use as a user in Ubuntu. There are different kinds of _shells_ but this is out of scope for this course. Most syntax seen in this chapter will work in most shell environments.

?> Note that we will focus on the basic syntax of a shell script. You can always learn more about if statements, loops, custom options and arguments, tests, ... in scripts but this is out of scope for this course.

### Hello world
To start of with our first bash script we'll create a new file called `helloworld.sh` and add some contents using `nano`.  

```bash
student@linux-ess:~$ nano helloworld.sh
```

We give the file the following contents:
```bash
#!/bin/bash
echo "hello world"
echo "this is our first bash script"
```
The first line in this script is named in the shebang and is a special line that will make sure the script will be ran in a `bash` shell. After that we can have different lines of all kinds of commands that will be run in sequential order.

?> using `#` signs are interpreted as comments. Any code after those signs will not be executed.

In the example above we will run 2 `echo` commands. To run this bash script, we will have to add _execute_ rights:

```bash
student@linux-ess:~$ chmod +x helloworld.sh
```
After doing this we can execute the script:
```bash
student@linux-ess:~$ ./helloworld.sh
hello world
this is our first bash script
```
  

?> Although the script is in the working directory, we have to specify it with: __./__helloworld.sh  Another way to run it, is to specify the full path: /home/student/helloworld.sh
  
  
?> Only scripts that are saved in a directory which is specified in the $PATH variable can be executed without specifying the full path.
  
  
### date with shell embedding
Lets extend our script with some nifty logic to use to output of a certain command in another command. We edit the script contents as follows:  
_nano helloworld.sh_  
```bash
#!/bin/bash
echo "hello world"
echo "this is our first bash script"
echo "the date of today is $(date)"
```
When we run this script, we get the following output:
```bash
student@linux-ess:~$ ./helloworld.sh
hello world
this is our first bash script
the date of today is Tue Jun 28 22:04:09 CEST 2022
```
The concept we've used here is called _shell embedding_. The `$(...)` syntax opens up a new (sub)shell and runs a command. The output of the `date` command is then directly used in the echo command.
  
  
### Variables
We also can make use of variables to reuse data:  
_nano vars.sh_  
```bash
#!/bin/bash
CUSTOMDIR=testdir
echo "customdir is set to $CUSTOMDIR"
mkdir ~/$CUSTOMDIR
touch ~/$CUSTOMDIR/testfile
ls -l ~/$CUSTOMDIR/*
```

?> We can run the script without setting the execute script (chmod u+x) first, but then we have to specify the interpreter (here bash) to define in which language the sript is written

```bash
student@linux-ess:~$ bash vars.sh
customdir is set to testdir
-rw-r----- 1 student student 0 Nov 11 15:52 /home/student/testdir/testfile
```

#### System variables
We also can make use of variables that are set on the system:  
_nano sysvars.sh_  
```bash
#!/bin/bash
echo "hello $USER"
echo "your homefolder is $HOME"
```
  
_chmod u+x sysvars.sh_    
  
```bash
student@linux-ess:~$ ./sysvars.sh
hello student
your homefolder is /home/student
```
  
Lets combine some of the stuff we learned so far.   
  
Lets create a new script called `countfiles.sh`:
  
_nano countfiles.sh_  
```bash
#!/bin/bash
echo "hello $USER"
echo "your homefolder has $(ls -A1 ~ | wc -l) files/folders."
```
  
When we execute it, we get the following result:
```bash
student@linux-ess:~$ bash countfiles.sh
hello student
your homefolder has 12 files/folders.
```
  
Another example creates a file with the current date in the filename:
  
_nano datefile.sh_  
```bash
#!/bin/bash
# This will create a variable with the current date as value
createdate=$(date +"%Y-%m-%d")
touch ~/${createdate}-superfile && echo "File ${createdate}-superfile created/touched in homedir."
```
When we execute it, we get the following result:
```bash
student@linux-ess:~$ bash datefile.sh
File 2022-11-11-superfile created/touched in homedir.
```
?> Mind that if we ask for the value of a variable by putting a dollar sign in front (eg. `echo $createdate`). But when we put text right after the variable without a space in between, we almost always have to put the variable within boundaries with the curly brackets (eg. `echo ${createdate}superfile` )  
    
#### Reading user input
Sometimes it can be helpful to ask for user input. We place the answer of the user in a variable, so that we can reuse it later on in the script:
  
_nano list5.sh_
```bash
#!/bin/bash
echo "Enter the absolute path of a folder you want to check:"
read folder
echo "The selected folder is $folder." 
```

Let's extend this script to give it some more functionality and combine some of the concepts we've learned before:
```bash
#!/bin/bash
echo "Enter the absolute path of a folder you want to check:"
read folder
echo "The selected folder is $folder. This folder contains $(ls -A1 $folder | wc -l) files/folders." 
echo "Showing the first 5:"
ls -A1 | head -5
```

Let's see what it does:  
```bash
student@linux-ess:~$ ./list5.sh
Enter the absolute path of a folder you want to check:
/home/student
the selected folder is /home/student. This folder contains 23 files/folders.
Showing the first 5:
2022-11-11-superfile
auth.log
.bash_history
.bash_logout
.bashrc
```

### Using a parameter
Just one, nothing else!

## adding to PATH

## Crontab
