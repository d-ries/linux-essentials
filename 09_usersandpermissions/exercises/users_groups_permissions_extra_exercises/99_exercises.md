# Assignment on Users, Groups, Permissions - Extra Exercises

## Task 1
Create a group named pxl and a user itstudent. This user's primary group is pxl. Set the password for the user to test123. The home directory for this user is /home/itstudent and for the shell the user uses /bin/bash.

## Task 2
Make sure the user itstudent becomes a sudoer. Test if this works. 

## Task 3
Copy the file /etc/hosts to your home directory (do not do this as root!). Set the permissions with the chmod command as follows: 
r-x for others, rw- for group and no permissions (---) for the file owner. Check with the ls -l command if everything is changed. 
- Can the file owner check the file contents? Why / Why not?
- Can he change permissions?
- Can he delete the file? 

## Task 4
Create the directory sturcture with the necessary users, groups and ACLs as shown in the image below.
![foldersecurity](../../../images/09/folderSecurity.PNG)
  
Test where the users Ava and Oliver have read and write permissions.

## Task 5
Find out how to copy the ACL-configurations of one folder to another one. 

## Task 6
Find out how to create a backup of the ACL-configurations set on a directory.
  
## Task 7

Suppose you work in a company where devices are designed, created, repaired and sold. Engineers are appointed to design the devices. Technicians are appointed to create and repair these devices and for selling them, sellers are appointed. Alle employees of this company work on a central Linux system. The users of this system should be defined so the __engineers have their own home directory and have a shared directory /home/shared/design (where they have all permissions)__. All __technicians share one home directory /home/technicians__ and all __Sales personnel have their own home directory but share a directory /home/shared/info (where they have all permissions)__ where all technical/marketing data is stored about the devices. The __engineers also need access to the directory /home/shared/info (all permissions)__. <br />
  
  
The groups for the different employments are:

| Employment | Linux group | User | Password |
| --- | --- | --- | --- |
| Engineers | engineers | George | summer1 |
| | | Isla | summer2 |
| Technicians | technicians (primary group) | Leo | winter1 |
| | | Amelia | winter2 |
| Sales | sales | Jack | spring1 |
| | | Grace | spring2 |


The special groups for the shared directories: <br />

| Directory | Linux group with all permissions | 
| --- | --- |
| /home/shared/design | engineers | 
| /home/shared/info | sales, engineers | 

The userowner of the shared directories is the ‘root’ user


### Task 7.1
Create the folders, groups and users as mentioned in the situation above. 

### Task 7.2
Give all users the correct groups as mentioned in the situation above.

### Task 7.3
Set all the permissions and ACL's for the scenario mentioned above.
  
    
    
## Task 8
Create 7 users named: <br />
Walter, Michael, Ben, James, Mia, Emma and Charlotte<br />
<br />
Emma, Charlotte and Mia have users as their primary group, their secondary group should be Sales.<br />
Walter and Michael are member of the group planning <br />
Ben and James are part of both the departments and are because of this member of both groups<br />
<br />
Alle users have their home directory in /home/username.<br />
There are 3 extra directories, which can be found in /home:<br />
/home/planning: contains the planning, customizable for all members of planning. <br />
/home/sales: contains information about sales, customizable for all members of sales<br />
/home/general: contains general information for everyone? (James is responsible for this folder and therefore only James has writing permissions on this directory and its content. 

All users (members of the group users) have reading permissions for these directories.   
Test the scenario!
