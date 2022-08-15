# Assignment Users

## Task 1
The definition of users is kept in the file /etc/passwd. This file have 1 line for each user. Each of these lines is divided into 7 fields, separated by a “:”. Give a description of each of these fields:

Field 1: ________
Field 2: ________
Field 3: ________
Field 4: ________
Field 5: ________
Field 6: ________
Field 7: ________


## Task 2
Back in the early days of Unix, the file /etc/passwd didn’t only keep user-information, it also contained a coded version of the password. This was a weak point in the security of the Unix system of course, because everyone can read the /etc/passwd file and thus could see the coded passwords. For a hacker the next step would be to create a tool to decode these passwords, for example: cracker. After this problem was recognized, it was decided that the passwords were to be kept in a different file. This file would only be accessible by the user root, who’s ID is used to run the passwd and login programs. 
What is the name of the file with the coded passwords? 



## Task 3
Create a user with following characteristics:
User-name:	    jan
User-ID:	    1111
Group-ID:	    100 (=users)
Description:	Testuser jan
Home-dir:	    /home/jan
Shell:		    /bin/bash


## Task 4
Check the changed files:
Wat is changed in the file /etc/passwd?

## Task 5
What is changed in the file /etc/shadow?


## Task 6
Wat is changed in the file /etc/group?

## Task 7
Wat is changed in the directory /home? 

## Task 8
The user Jan is now created on your system. Now Jan should be able to ask information about himself. 
Log in as Jan and execute the following command: 
```bash
id
```

## Task 9
Remove the user Jan from your system using the command:  userdel –r jan
What is changed in the file /etc/passwd?

## Task 10
What is changed in the file /etc/shadow?


## Task 11
What is changed in the file /etc/group?

## Task 12
Does the directory /home/jan still exist? YES / NO


## Task 13
Create a user Piet, by only specifying its username and that he must have a home folder. 

## Task 14
Examine the files that have been modified
What is changed in the file /etc/passwd?

## Task 15
What is changed in the file /etc/shadow?

## Task 16
What is changed in the file /etc/group?


## Task 17
What is changed in the directory /home?

## Task 18
Give the user Piet a password

## Task 19
Try to log in as Piet

## Task 20
Remove the user Piet, but keep his home folder

## Task 21
Delete Piet’s home folder
