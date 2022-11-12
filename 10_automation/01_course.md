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

In the example above we will run 2 `echo` commands. 
  
To run this bash script, we will have to add _execute_ rights:

```bash
student@linux-ess:~$ ls -l helloworld.sh
-rw-rw-r-- 1 student student 371 Nov 11 15:55 helloworld.sh
student@linux-ess:~$ chmod u+x helloworld.sh
student@linux-ess:~$ ls -l helloworld.sh
-rwxrw-r-- 1 student student 371 Nov 11 15:55 helloworld.sh
```
After doing this we can execute the script:
```bash
student@linux-ess:~$ ./helloworld.sh
hello world
this is our first bash script
```
  

?> Although the script is in the working directory, we have to specify it with: ./helloworld.sh  Another way to run it, is to specify the full path: /home/student/helloworld.sh
  
  
?> Only scripts that are executable and saved in a directory which is specified in the $PATH variable can be executed without specifying the full path.
  
  
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
  
You can use the at command to run a process at a specific time. With the cron command it is possible to do this on a regular basis. For the at command we echo an output into the at command as shown by an example below, you can check what is scheduled and remove when necerry with the atrm or at -r command. Cron works different, it uses a file where we put everything we want to happen with the timing, in the example below we echo some text to a file every minute. Remove the line from the crontab to stop this from happening. To check all possibilities check the man at and man cron pages. To see what processes are running in the background use the jobs command.
```bash
tudent@linux-ess:~$ sudo apt-get install at
student@linux-ess:~$ echo "hello" | at -m 2pm
student@linux-ess:~$ echo "reboot" | at now + 2 days
warning: commands will be executed using /bin/sh
job 4 at Sat Sep 17 13:26:00 2022
student@linux-ess:~$ at -l
3	Sat Sep 17 13:25:00 2022 a student
4	Sat Sep 17 13:26:00 2022 a student
1	Thu Sep 15 14:00:00 2022 a student
student@linux-ess:~$ atrm 3
student@linux-ess:~$ at -l
4	Sat Sep 17 13:26:00 2022 a student
1	Thu Sep 15 14:00:00 2022 a student

@linux-ess:~$ crontab -e
no crontab for student - using an empty one

Select an editor.  To change later, run 'select-editor'.
  1. /bin/nano        <---- easiest
  2. /usr/bin/vim.tiny
  3. /bin/ed

Choose 1-3 [1]: 1
crontab: installing new crontab

* * * * * echo 'run this command every minute' >> /tmp/spam.txt

@linux-ess:~$ crontab -l
# Edit this file to introduce tasks to be run by cron.
# 
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
# 
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').
# 
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
# 
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
# 
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
# 
# For more information see the manual pages of crontab(5) and cron(8)
# 
# m h  dom mon dow   command
* * * * * echo 'run this command every minute' >> /tmp/spam.txt
student@linux-ess:~$ cat /tmp/spam.txt 
run this command every minute
run this command every minute
