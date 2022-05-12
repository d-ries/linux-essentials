# Lab <!-- {docsify-ignore} -->
In the previous chapter Linus had just downloaded a `server.jar` file but he is confused as to where this file is located now! In this lab we will find out how we can view and navigate through folders and how we can use some basic commands to work with files.

## Finding the server.jar file <!-- {docsify-ignore} -->

Before doing anything else, Linus really wants to find his `server.jar` file that he just downloaded in the previous chapter. Using the `man -k directory` command he finds out that there are all kinds of commands available to work with directories. The first command that Linus checks out is the `pwd` command:
```
pwd - print name of current/working directory
```
After running this command, Linus indeed sees the working directory that he is in:
```bash
student@linux-ess:~$ pwd
/home/student
```
Linu sran the `wget` command his his homefolder (`~` or `/home/student`), so he is certain that this is where the `server.jar` file has to be. Using the manpages he learns about the `ls` command which should list a directories contents:
```bash
student@linux-ess:~$ ls
server.jar
```
His findings are confirmed as we can see in the output above that the `server.jar` file is indeed located in the current working directory `/home/student`. To check if the download was successful he decides that he wants to check the file size. Using the `man ls` command he tries to look for an _option_ that allows him to view file sizes:
```bash
student@linux-ess:~$ ls -lh
-rw-r--r-- 1 student student  45M Feb 28 11:48 server.jar
```
To find out the file size of the file he combines the options `-l` and `-h`.  Now Linus knows the `server.jar` file is 45MB and was last changed on 28 feb at 11:48.

## Create a folder structure <!-- {docsify-ignore} -->
Linus wants a clean folder structure for his _LinusCraft_ project. In his homefolder he would like to create a folder with the name `linuscraft`. To do this he found the `mkdir` command using the manpages.
```bash
mkdir linuscraft
```
After creating the `linuscraft` folder he wants to create a folder `serverfiles` inside that folder. To do this he can use one of the 2 options below:
1. By using the `cd` command:
```bash
student@linux-ess:~$ cd linuscraft
student@linux-ess:~/linuscraft$ mkdir serverfiles
```
2. By using the mkdir command directly using a relative path:
```bash
student@linux-essentials:~$ mkdir linuscraft/serverfiles
```
He checks if the folder is created correctly by navigating to that folder using an absolute path:
```bash
student@linux-essentials:~/linuscraft$ cd /home/student/linuscraft/serverfiles
student@linux-essentials:~/linuscraft/serverfiles$ pwd
/home/student/linuscraft/serverfiles
```
?> Exercise: Can you navigate to the serverfiles folder using a relative path starting from your homefolder?

He would also like a folder `administration` inside the `linuscraft` folder. While using the folder `serverfiles` as the working directory, he creates this folder using a relative path:
```bash
student@linux-ess:~/linuscraft/serverfiles$ mkdir ../administratie
```
To finish up he creates a folder named `backups` and `secrets` using an absolute path:
```bash
mkdir /home/student/backups
```
Linus decides to navigate back to his homefolder by using the `cd` command without any arguments. Afterwards he checks the contents of his created folder `linuscraft`: 
```bash
student@linux-ess:~$ ls -lh linuscraft
total 12K
drwxr-xr-x 2 student student 4.0K May  4 21:45 administration
drwxr-xr-x 2 student student 4.0K May  4 21:48 backups
drwxr-xr-x 2 student student 4.0K May  4 21:44 serverfiles
```

## Create files <!-- {docsify-ignore} -->
Linus would like to create a file to list any outstanding tasks. He creates this file in the folder `linuscraft` using the `touch` command:
```bash
student@linux-ess:~$ touch linuscraft/todo.txt
```
This command creates an empty file. We will find out how to insert data into the file in the next chapter's lab.

Next up he creates some additional files with the following command:
```bash
student@linux-ess:~$  touch linuscraft/contact.txt linuscraft/backuplog.txt
```

He wants to create a hidden file to store important information aswell:
```bash
student@linux-ess:~$ touch /home/dries/linuscraft/.important
```

## Finetune the file and folder structure <!-- {docsify-ignore} -->
There are some problems with the files and folders that we just created. The `server.jar` file for instance is still located in the homefolder of the user `student`. We have to move this file to the `serverfiles` folder:
```bash
student@linux-ess:~$ mv server.jar linuscraft/serverfiles/
```
There are 3 `txt` files present in the `linuscraft` folder. Linus learnt that these do not need file extentions so he wants to remove them only using one command. To achieve this goal, he uses the `rename` command:
```bash
student@linux-ess:~/linuscraft$ ls
administratie  backuplog.txt  backups  contact.txt  serverfiles  todo.txt
student@linux-ess:~/linuscraft$ rename 's/.txt//' *.txt
```

We do not longer need the `secrets` folder so Linus decides to delete it while having `~/linuscraft` as his working directory:
```bash
student@linux-ess:~/linuscraft$ rm -rf secrets
```
