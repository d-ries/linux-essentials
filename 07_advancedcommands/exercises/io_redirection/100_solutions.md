# Solutions on I/O redirection

## Task 1
Create a new file names "userinfo" in your homefoler. Do this by redirecting the output of the echo command of the variable $USER to this file. 

<br/>![](images/2022-08-15-15-32-42.png)

## Task 2
Add the output of the echo command of the variable $UID to this file.

<br/>![](images/2022-08-15-15-32-56.png)

## Task 3
Copy, without using sudo, the directory /etc to the directory /tmp recursively

<br/>![](images/2022-08-15-15-33-06.png)

## Task 4
Do the last exercise again, but send the error messages to the black hole

<br/>![](images/2022-08-15-15-33-31.png)

## Task 5
Do the penultimate exercise again, but send the error messages to ~/backup.errors

<br/>![](images/2022-08-15-15-33-44.png)

## Task 6
Execute ls /tmp/* while sending the result and error messages to the file ~/contentslashtmp.full

<br/>![](images/2022-08-15-15-33-58.png)

## Task 7
Empty out the file userinfo by adding only one character before the filename in the command line 

<br/>![](images/2022-08-15-15-34-12.png)

## Task 8
Execute the command "ls /*", from the result and any error messages only keep the lines with the word "root". For example there should not be a line "lost+found"

<br/>![](images/2022-08-15-15-34-26.png)


## Task 9
Extra challenge: 
From the last command, only send the error messages with the text "root" to the file ~/root-errors.log

<br/>![](images/2022-08-15-15-34-46.png)
