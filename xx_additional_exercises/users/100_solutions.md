# Assignment Users

## Task 1
The definition of users is kept in the file /etc/passwd. This file have 1 line for each user. Each of these lines is divided into 7 fields, separated by a “:”. Give a description of each of these fields:

Field 1:	Login name
Field 2:	X to show there is a password for this user in /etc/shadow
Field 3:	Numerical user ID
Field 4:	Numerical group ID
Field 5:	Username and/or comment field
Field 6:	User home directory 
Field 7:	Login shell 

<br/>![](images/2022-08-15-16-13-12.png)
<br/>![](images/2022-08-15-16-13-19.png)

## Task 2
Back in the early days of Unix, the file /etc/passwd didn’t only keep user-information, it also contained a coded version of the password. This was a weak point in the security of the Unix system of course, because everyone can read the /etc/passwd file and thus could see the coded passwords. For a hacker the next step would be to create a tool to decode these passwords, for example: cracker. After this problem was recognized, it was decided that the passwords were to be kept in a different file. This file would only be accessible by the user root, who’s ID is used to run the passwd and login programs. 
What is the name of the file with the coded passwords? 

```
/etc/shadow, note that only the user student currently has a password, all the other users show a * where the encrypted password would be.
```


## Task 3
Create a user with following characteristics:
User-name:	jan
User-ID:	1111
Group-ID:	100 (=users)
Description:	Testuser jan
Home-dir:	/home/jan
Shell:		/bin/bash


<br/>![](images/2022-08-15-16-14-00.png)
<br/>![](images/2022-08-15-16-14-05.png)

?> <i class="fa-solid fa-circle-info"></i> After a user is created, its password is set to “!”, which means that this name cannot be used to log in. To make this possible you need to give Jan a password. Set Jan’s password to “January”. 

<br/>![](images/2022-08-15-16-14-34.png)


## Task 4
Check the changed files:
Wat is changed in the file /etc/passwd?

```
One line has been added for the user jan
```
<br/>![](images/2022-08-15-16-15-02.png)


## Task 5
What is changed in the file /etc/shadow?

```
One line has been added for the password of jan 
```
<br/>![](images/2022-08-15-16-15-24.png)


## Task 6
Wat is changed in the file /etc/group?

```
jan has been added behind the group users (100)
```

## Task 7
Wat is changed in the directory /home? 

```
a directory has been added for jan's home folder 
```
<br/>![](images/2022-08-15-16-16-03.png)


## Task 8
The user Jan is now created on your system. Now Jan should be able to ask information about himself. 
Log in as Jan and execute the following command: 
```bash
id
```

<br/>![](images/2022-08-15-16-16-46.png)


## Task 9
Remove the user Jan from your system using the command:  userdel –r jan
What is changed in the file /etc/passwd?

<br/>![](images/2022-08-15-16-16-59.png)

?> <i class="fa-solid fa-circle-info"></i> The line with user Jan is deleted.

## Task 10
What is changed in the file /etc/shadow?

```
The line with user jan is deleted. 
```
<br/>![](images/2022-08-15-16-17-28.png)


## Task 11
What is changed in the file /etc/group?

```
Jan is not shown in the group users anymore  
```
<br/>![](images/2022-08-15-16-17-50.png)

## Task 12
Does the directory /home/jan still exist? YES / NO

```
NO
```

<br/>![](images/2022-08-15-16-18-15.png)


## Task 13
Create a user Piet, by only specifying its username and that he must have a home folder. 

<br/>![](images/2022-08-15-16-18-27.png)


## Task 14
Examine the files that have been modified
What is changed in the file /etc/passwd?

```
One line has been added for the user piet. 
```

<br/>![](images/2022-08-15-16-18-40.png)


## Task 15
What is changed in the file /etc/shadow?

```
One line has been added for the user piet, but no password as set yet. 
```
<br/>![](images/2022-08-15-16-19-06.png)


## Task 16
What is changed in the file /etc/group?

```
One line has been added for the new group piet, the primary group for the user piet.
```

<br/>![](images/2022-08-15-16-19-27.png)

## Task 17
What is changed in the directory /home?

```
One directory has been added for the home folder of the user piet.
```

<br/>![](images/2022-08-15-16-19-46.png)


## Task 18
Give the user Piet a password

<br/>![](images/2022-08-15-16-20-09.png)


## Task 19
Try to log in as Piet

<br/>![](images/2022-08-15-16-20-18.png)

## Task 20
Remove the user Piet, but keep his home folder

<br/>![](images/2022-08-15-16-20-30.png)


## Task 21
Delete Piet’s home folder

<br/>![](images/2022-08-15-16-20-40.png)