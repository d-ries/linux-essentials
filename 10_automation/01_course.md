# Automation

## Bash scripts
Scripting is a great way to automate simple tasks or chains of commands. Imagine you want to take a backup. Usually this means creating a `zip` archive of certain files and folders, giving this `zip` file the appropriate name and then move the `zip` file to a certain folder. Running these commands manually is prone to errors and time consuming. A better way would be to bundle these commands in a script, so we can instead run one command that will trigger running all of the steps described above.

In Ubuntu we ofter use _bash_ scripts. _bash_ refers to the default shell that we use as a user in Ubuntu. There are different kinds of _shells_ but this is out of scope for this course. Most syntax seen in this chapter will work in most shell environments.

?> Note that we will focus on the basic syntax of a shell script. You can always learn more about if statements, loops, custom options and arguments, tests, ... in scripts but this is out of scope for this course.

### Hello world
To start of with our first bash script we'll create a new file called `helloworld.sh` and add some contents using `nano`:
```bash
student@linux-ess:~$ nano helloworld.sh
```

We give the file the following contents:
```bash
#!/bin/bash
echo "hello world"
echo "this is our first bash script"
```
The first line in this script is a special line that will make sure the script will be ran in a `bash` shell. After that we can have different lines of all kinds of commands that will be ran in that order.

?> using `#` signs are interpreted as comments. Any code after those signs will not be executed.

In the example above we will run 2 `echo` commands. To run this bash script, we will have to add _execute_ rights:

```bash
student@linux-ess:~$ chmod +x helloworld.sh
```
After doing this we got 2 options to actually execute the script:
```bash
student@linux-ess:~$ ./helloworld.sh
hello world
this is our first bash script
student@linux-ess:~$ bash helloworld.sh
hello world
this is our first bash script
```

### date with shell embedding
Lets extend our script with some nifty logic to use to output of a certain command in another command. We edit the script contents as follows:
```bash
#!/bin/bash
echo "hello world"
echo "this is our first bash script"
echo "the date of today is $(date)"
```
When we run this script, we get the following output:
```bash
student@linux-ess:~$ bash helloworld.sh
hello world
this is our first bash script
the date of today is Tue Jun 28 22:04:09 CEST 2022
```
The concept we've used here is called _shell embedding_. The `$(...)` syntax opens up a new (sub)shell and runs a command. The output of the `date` command is then directly used in the echo command.
### Variables
```bash
#!/bin/bash
CUSTOMDIR=/tmp
echo "customdir is set to $CUSTOMDIR"
touch $CUSTOMDIR/testfile
ls $CUSTOMDIR
```

```bash
student@linux-ess:~$ bash helloworld.sh
customdir is set to /tmp
testfile
```

#### System variables
```bash
#!/bin/bash
echo "hello $USER"
echo "your homefolder is $HOME"
```

```bash
student@linux-ess:~$ bash helloworld.sh
hello student
your homefolder is /home/student
```

Lets combine some of the stuff we learned so far. Lets create a new script called `countfiles.sh`:
```bash
#!/bin/bash
echo "hello $USER"
echo "your homefolder has $(ls ~ | wc -w) files/folders."
```
When we execute it, we get the following result:
```bash
student@linux-ess:~$ bash countfiles.sh
hello student
your homefolder has 12 files/folders.
```

Another example:
```bash
#!/bin/bash
# This will create a variable with the current date as value
createdate=$(date +"%Y-%m-%d")

touch ~/$createdate-superfile
```

#### Reading user input
```bash
#!/bin/bash
echo "enter the absolute path of a folder you want to check:"
read folder
echo "the selected folder is $folder. 
```

Lets extend this script to give it some more functionality and combine some of the concepts we've learned before:
```bash
#!/bin/bash
echo "enter the absolute path of a folder you want to check:"
read folder
echo "the selected folder is $folder. This folder contains $(ls $folder | wc -w) regular files/folders. Showing the first 5:"
ls $folder | tr ' ' '/n' | head -5
```

```bash
student@linux-ess:~$ ./listcontents.sh
enter the absolute path of a folder you want to check:
/home/student
the selected folder is /home/student. This folder contains 16 regular files/folders. Showing the first 5:
2022-06-28-backup
2022-06-28-superfile
auth.log
count1.txt
creafile.sh
```

### Using a parameter
Just one, nothing else!

## adding to PATH

## Crontab
