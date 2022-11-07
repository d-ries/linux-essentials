# Users and permissions
As with any operating system we will be working with different users on the system. We've been using the user `student`. We can confirm this by running the command `whoami`. Other commands we can run are `who` or `w`. These will show us all of the users that are logged in on the system (mind that both commands have a different output!).

## User management
### /etc/passwd
As we've seen before all system configuration is done using config files. The same is true for user management. User configuration is stored in the file `/etc/passwd`. It contains a list of user accounts together with some metadata seperated by colons:
```bash
student@linux-ess:~$ tail /etc/passwd
pollinate:x:105:1::/var/cache/pollinate:/bin/false
sshd:x:106:65534::/run/sshd:/usr/sbin/nologin
syslog:x:107:113::/home/syslog:/usr/sbin/nologin
uuidd:x:108:114::/run/uuidd:/usr/sbin/nologin
tcpdump:x:109:115::/nonexistent:/usr/sbin/nologin
tss:x:110:116:TPM software stack,,,:/var/lib/tpm:/bin/false
landscape:x:111:117::/var/lib/landscape:/usr/sbin/nologin
usbmux:x:112:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
student:x:1000:1000:student:/home/student:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
```
The first account in this file is the `root` account:
```bash
student@linux-ess:~$ head -1 /etc/passwd
root:x:0:0:root:/root:/bin/bash
```

We can see more info than just usernames. These lines contain the user identifier (`1000` for `student`), home folder location, default shell, ... 

?> <i class="fa-solid fa-circle-info"></i> You can find more information about this file, the columns and the contents by running the command `man 5 passwd`.

### Adding users (useradd)
To add users we can simply use the `useradd` command. Its important to note that we have to run this command with `sudo` rights. This is because it is a system command that affects the entire system. To add a new user with the username `teacher` we could run the following command:
```bash
student@linux-ess:~$ sudo useradd -m -d /home/teacher -c "Teacher Account" teacher
[sudo] password for student:
student@linux-ess:~$ tail -3 /etc/passwd
student:x:1000:1000:student:/home/student:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
teacher:x:1001:1001:Teacher Account:/home/teacher:/bin/sh
```
The `-d` takes in an argument and uses this argument as a path to where the homefolder has to be created. The `m` option (`create home`) will make sure the home folder actually gets created with the correct permissions. Lastly the `-c` (`comment`) option sets extra metadata to the user. 


?> <i class="fa-solid fa-circle-info"></i> Mind that the option -d is optional and if not specified it defaults to a directory with the same name as the username within the directory /home.


?> <i class="fa-solid fa-circle-info"></i> We can delete users by running the command `userdel -r teacher`. The option `-r` will also remove that user's homefolder.

As seen in the folder `/home` or in the file `/etc/passwd` the new user has been created:
```bash
student@linux-ess:~$ tail -1 /etc/passwd
teacher:x:1001:1001:Teacher Account:/home/teacher:/bin/sh
```

Every user has a userid (the third field in `/etc/passwd`). To view the userid of a user you can use the `id` command:
```bash
student@linux-ess:~$ id teacher
uid=1001(teacher) gid=1001(teacher) groups=1001(teacher)
student@linux-ess:~$ ls -l /home
total 8
drwxr-x--- 5 student student 4096 Nov  4 16:04 student
drwxr-x--- 2 teacher teacher 4096 Nov  7 20:28 teacher
```

#### Default values
The `useradd` command uses quite some default values. We can check these default values by running the following command:
```
student@linux-ess:~$ useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/sh
SKEL=/etc/skel
CREATE_MAIL_SPOOL=no
```
These settings are kept in the file `/etc/default/useradd` and can be changed at any time.

?> <i class="fa-solid fa-circle-info"></i> Notice that the default value for the shell is `/bin/sh`. It is good practice to alter this to `/bin/bash` so that every new user gets the `bourne again shell` as default.

#### /etc/skel
By default homefolders are created as a subdirectory of the `/home` directory. These folders aren't created from scratch. The contents of the folder `/etc/skel` are copied within each newly created homefolder. This means that if we alter any contents in this `skel` folder, this wil actually be copied to any new user that will be created in the future:

```bash
student@linux-ess:~$ ls -a /etc/skel
.  ..  .bash_logout  .bashrc  .profile
student@linux-ess:~$ sudo ls -a /home/teacher/
.  ..  .bash_logout  .bashrc  .profile
```

#### Default profile files
__.bashrc__: executed everytime a new shell (bash) is started

__.bash\_history__: holds the history (new commands get added to this file on closing of a shell)

__.profile__: executed when user logs in

### Editing users (usermod & userdel)
To edit a user's account configuration, we can use the `usermod` command. This command has several options that we can use to edit specific settings. For example to edit the comment field of a user we can run the following command:
```bash
student@linux-ess:~$ sudo usermod -c "John Doe" teacher
student@linux-ess:~$ tail -1 /etc/passwd
teacher:x:1002:1003:John Doe:/home/teacher:/bin/sh
```

To edit the default shell for a specific user we could do the following:
```bash
student@linux-ess:~$ tail -3 /etc/passwd
student:x:1000:1000:student:/home/student:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
teacher:x:1001:1001:Teacher Account:/home/teacher:/bin/sh
student@linux-ess:~$ sudo usermod -s /bin/bash teacher
student@linux-ess:~$ tail -3 /etc/passwd
student:x:1000:1000:student:/home/student:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
teacher:x:1001:1001:Teacher Account:/home/teacher:/bin/bash
```

?> View the manpage of `usermod` for all possible options.  
?> If we want to create a user that cannot be logged into, we can change it's shell to `/bin/false` or `/sbin/nologin`. The difference between these two is that `/sbin/nologin` gives a polite message that you cannot log in to this account before exiting. The option `/bin/false` directly exits without prompting anything. 

#### Setting user passwords
If we want to change our password we can use the `passwd` command:
```bash
student@linux-ess:~$ passwd
Changing password for student.
Current password:
New password:
Retype new password:
passwd: password updated successfully
```

As seen in the previous commands we created a new user with the username `teacher` but we never gave it a password. To do this we can run the `passwd` command with `sudo` rights and with a username as argument. This forces setting a new password for that specific user:
```bash
student@linux-ess:~$ sudo passwd teacher
New password:
Retype new password:
passwd: password updated successfully
```

?> <i class="fa-solid fa-circle-info"></i> Note that if we use `sudo passwd` that we are changing the password of the user root and not our password!

?> <i class="fa-solid fa-circle-info"></i> Note that you password has to be long and difficult enough, otherwise the new password will not be accepted.

The password gets stored in the file `/etc/shadow` for security reasons. Regular users cannot view the contents of this file:
```bash
student@linux-ess:~$ tail -1 /etc/shadow
tail: cannot open '/etc/shadow' for reading: Permission denied
student@linux-ess:~$ sudo tail -1 /etc/shadow
teacher:$y$j9T$Vtf.U//c4/N/CB8LzHfnl0$5iCgijrpqXfaA3v18w/nAL2rl8BmiBYX5rn5rf.j6B7:19171:0:99999:7:::
```
As seen in the example above the password isn't shown in plaintext. This is because Linux systems use hashing algoritms to encrypt the passwords. The algoritm used here is called _sha512_.


## Switching users (su)
To switch user accounts we could use the `exit` command to close the current shell and this will, eventually, end up in giving us the login prompt of the server. An alternative is to use the `su` (`switch user`) command:
```bash
student@linux-ess:~$ whoami; pwd
student
/home/student
student@linux-ess:~$ su - teacher
Password:
teacher@linux-ess:~$ whoami; pwd
teacher
/home/teacher
teacher@linux-ess:~$ exit
logout
student@linux-ess:~$ whoami; pwd
student
/home/student
```

Note that root can become whoever he wants without the need to know that users password:
```bash
student@linux-ess:~$ whoami; pwd
student
/home/student
student@linux-ess:~$ sudo su - teacher
teacher@linux-ess:~$ whoami; pwd
teacher
/home/teacher
teacher@linux-ess:~$ exit
logout
```

Note that to become root (without knowing his password) we can also use the `sudo` command:
```bash
student@linux-ess:~$ whoami; pwd
student
/home/student
student@linux-ess:~$ sudo su - root
root@linux-ess:~# whoami
root
root@linux-ess:~# pwd
/root
root@linux-ess:~# exit
logout
```

We want to be mindful of commands that we run as the `root` user. This user has permissions on all the files, folders and services on our system. This means that running commands as `root` can have a huge impact when being exploited.

## Group management

### View groupinfo of a user (id,groups)
To view the groups a user is added to we can use the commands `id` and `groups`:
```bash
student@linux-ess:~$ id teacher
uid=1001(teacher) gid=1001(teacher) groups=1001(teacher)
student@linux-ess:~$ groups teacher
teacher : teacher
```

### /etc/group
The file where the group info of the users is stored is `/etc/group`. We could also make changes to this file instead of using commands.
```bash
student@linux-ess:~$ tail -3 /etc/group
student:x:1000:
plocate:x:118:
teacher:x:1001:
```


### Adding groups (groupadd)
If there's a need for new groups we can do it with the `groupadd` command:
```bash
student@linux-ess:~$ sudo groupadd staff
student@linux-ess:~$ tail -2 /etc/group
teacher:x:1001:
staff:x:1002:
```

?> We can delete groups using the command `sudo groupdel staff`.

### Editing groups (groupmod)
If we need to change a group we can use `groupmod`:
```bash
student@linux-ess:~$ sudo groupmod -n personnel staff
student@linux-ess:~$ tail -1 /etc/group
personnel:x:1002:
```

### Edit group memberships (usermod)
If we want to add a user to a group we can use the `usermod` command:
```bash
student@linux-ess:~$ sudo usermod -a -G personnel teacher
student@linux-ess:~$ id teacher
uid=1001(teacher) gid=1001(teacher) groups=1001(teacher),50(personnel)
student@linux-ess:~$ groups teacher
teacher : teacher personnel
```

?> <i class="fa-solid fa-circle-info"></i> If we forget the `-a` option the user will only be in the specified group and will be removed from all the groups he was in. This can be a serious problem if the user was the only one in the sudo group!

?> <i class="fa-solid fa-circle-info"></i> If we want to remove a user from a group and the users is in many more groups we do not use the '-a' option and we have to specify all the groups he must remain in. In that case it is easier to edit the group file `/etc/group` by hand. 

?> <i class="fa-solid fa-circle-info"></i> A user knows a change in group membership only when he logs in. So after a change a user has to login again to notice the difference.

?> <i class="fa-solid fa-circle-info"></i> The primary group of a user is specified in `/etc/passwd` and is the default group set on a new file or directory created by that user.

## Permissions

From the very start, Unix (and thus Linux) was built as a multiuser operating system. Having multiple users on the same system means you need a way to keep users from accessing files from other users, and keep regular users from accessing files and programs that are intended to be used only by the system administrator. On the other hand users also need to be able to share files with others so they can collaborate effectively. As a system administrator being able to lock down or grant access to files is one the most important steps in keeping a system secure. 

As you have seen in the previous section, your system already comes with a sensible set of file permissions. As a regular user you have full control in your own homefolder. You can create, edit and remove files and folders from your own home-directory `/home/student`. If you try to make a file in the `/var` directory however you will get an error. You are able to see the user database in `/etc/passwd` but cannot edit it as a regular user. `/etc/shadow` holds the passwords of users, that is why you are not even allowed to read it. 

Permission errors are a common source of problems. Understanding and manipulating file permissions is a crucial step in becoming a competent Linux admin.

?> <i class="fa-solid fa-circle-info"></i> Just because you can, doesn't mean you should. When troubleshooting permission errors always remember that permissions are your first line of defense against malicious actors. Always ask yourself why a program or a user should have access, and err on the side of caution. Don't just grant permissions to get rid of the error!


### Octal notations

When looking at the extended info for a file using `ls` with the `-l` option. You'll see three sets of three permissions applied to a file. The possible permission are: **r**ead, **w**rite and e**x**ecute. Permission to read a file's content, permission to change a file's content and permission to execute a file as a script or program. When a permission is not granted, you'll find a - in the position of the permission denied. 

```bash
student@linux-ess:~/course$ ls -l
total 4
-rw-rw-r-- 1 student student    0 okt  2 19:36 config
drwxrwxr-x 2 student student 4096 okt  2 19:36 folder
-rw-rw-r-- 1 student student    0 okt  2 19:36 rights.jpg
-rw-rw-r-- 1 student student    0 okt  2 19:36 test.txt
```

?> <i class="fa-solid fa-circle-info"></i>Directories in Linux have the same set of permissions. But because you need execute to access files in the directory, there is little you can do without it. The common permissions are rwx for a directory where you can do everything, r-x for a read-only directory, and ofcourse --- when you want to block access completely. 

There are three sets because there are three different sets of people that permissions can be applied to. The first set describes the permissions for the owner of the file (the first name behind the permissions), the second applies to everyone that is a member of the group that owns the file (the second name). The last set is for everyone who doesn't fall under one of the first two categories. So in short: The three sets apply to **user**, **group** and **other**, in that order.

When a user creates a file he automatically becomes the owner of that file. The group that owns the file is determined by the user's **primary group**. By default a user's primary group is a group with the same name as the username, which is why you'll often see owner and group owner have the same name (like student student in the above example). The `/dev` folder, that contains the files representing your hardware, is one of the places where you'll find files owned by the root-user with a different group as owner.

```bash
student@linux-ess:~$ ls -l /dev/sr0
brw-rw----+ 1 root cdrom 11, 0 okt 2 14:47 sr0
```   

File permissions are written on disk as a field of bits in the file's properties. A bit is set to 1 when a permission is granted, 0 when it's not. So rwxrw-r-- becomes 111110100. Because humans are not very good at parsing binary sequences, they are represented as as octal numbers, numbers from 0 to 7 (000 to 111 in binary). To calculate the octal number remember that read is worth 4, write 2 and execute 1. Add those you need and you'll get the octal notation. The example above becomes 764 (rwx, 4+2+1=7, rw-, 4+2+0=6, r--, 4+0+0=4).

### Changing permissions (chmod)

To change the permissions on a file you can use the `chmod`-command.

To add or substract permissions of a file you can use the following method, where rwx stand for the rights you want to add or substract, and ugo stand for user, group and other respectively. If you don't specify for who you want the change, it is changed on all three:

```bash
student@linux-ess:~/course$ ls -l test.txt 
-rw-rw-r-- 1 student student 0 okt  2 19:36 test.txt
student@linux-ess:~/course$ chmod +x test.txt 
student@linux-ess:~/course$ ls -l test.txt 
-rwxrwxr-x 1 student student 0 okt  2 19:36 test.txt
student@linux-ess:~/course$ chmod g-w test.txt 
student@linux-ess:~/course$ ls -l test.txt 
-rwxr-xr-x 1 student student 0 okt  2 19:36 test.txt
student@linux-ess:~/course$ chmod go-rx test.txt
student@linux-ess:~/course$ ls -l test.txt  
-rwx------ 1 student student 0 okt  2 19:36 test.txt
```

To completely rewrite permissions you use chmod with an octal mode. 

```bash
student@linux-ess:~/course$ ls -l config
-rw-rw-r-- 1 student student    0 okt  2 19:36 config
student@linux-ess:~/course$ chmod 600 config 
student@linux-ess:~/course$ ls -l config
-rw------- 1 student student    0 okt  2 19:36 config
student@linux-ess:~/course$ chmod 744 config
student@linux-ess:~/course$ ls -l config
-rwxr--r-- 1 student student    0 okt  2 19:36 config
```

The latter option is faster when you have to completely rewrite permissions (since you don't need to check the existing permissions, just overwrite). The former can be practical for making quick changes like making a file executable.

### Changing ownership (chgrp, chown)

Besides changing the permissions of a file, you'll also need to change whom these permissions apply to, by changing the user or group that owns a file. You will need sudo to assign files to different users/groups.

To change the group owner of a file or directory, you can use the `chgrp` command. To change this recursively use the `-R` option

```bash
student@linux-ess:~$ ls -l course/
total 4
-rwxr--r-- 1 student student    0 okt  2 19:36 config
drwxrwxr-x 2 student student 4096 okt  2 19:36 folder
-rw-rw-r-- 1 student student    0 okt  2 19:36 rights.jpg
-rw-rw-rw- 1 student student    0 okt  2 19:36 test.txt
student@linux-ess:~$ sudo chgrp -R staff course/
student@linux-ess:~$ ls -l course/
total 4
-rwxr--r-- 1 student staff    0 okt  2 19:36 config
drwxrwxr-x 2 student staff 4096 okt  2 19:36 folder
-rw-rw-r-- 1 student staff    0 okt  2 19:36 rights.jpg
-rw-rw-rw- 1 student staff    0 okt  2 19:36 test.txt
student@linux-ess:~$ ls -ld course/
drwxrwxr-x 3 student staff 4096 okt  2 19:36 course/
```
The `chown` command is more versatile, it allows you to change owner and/or group. It has the same -R option to change an entire file-tree.

```bash
student@linux-ess:~/course$ sudo chown student2 rights.jpg #changes the owner
student@linux-ess:~/course$ ls -l rights.jpg
-rw-rw-r-- 1 student2 staff    0 okt  2 19:36 rights.jpg
student@linux-ess:~/course$ sudo chown root:personeel config folder #changes owner and group
student@linux-ess:~/course$ ls -l 
total 4
-rwxr--r-- 1 root     personeel    0 okt  2 19:36 config
drwxrwxr-x 2 root     personeel 4096 okt  2 19:36 folder
-rw-rw-r-- 1 student2 staff        0 okt  2 19:36 rights.jpg
-rw-rw-rw- 1 student  staff        0 okt  2 19:36 test.txt
student@linux-ess:~/course$ sudo chown :staff config #changes the group
student@linux-ess:~/course$ ls -l config
-rwxr--r-- 1 root     staff    0 okt  2 19:36 config
```

### Default permissions (umask)

A last thing we need to look at are the default permissions. What permissions are applied when you create new files and folders? 

The maximum permissions for new files is 666, so -rw-rw-rw-. New files are never created with execute permissions. This is enforced by kernel code so if you want to change that you'll have to start programming. It is ofcourse possible to add execute bits after file creation using `chmod` but it always requires a conscious decission for security reasons. Folders don't have this limitation as a folder without an execute bit set is quite useless. 

```bash
student@linux-ess:~/course$ touch file
student@linux-ess:~/course$ mkdir folder
student@linux-ess:~/course$ ls -l
total 4
-rw-rw-r-- 1 student student    0 okt 15 15:56 file
drwxrwxr-x 2 student student 4096 okt 15 15:56 folder
```
As you can see, we don't get the expected -rw-rw-rw- for the file, nor drwxrwxrwx for the folder. This is because most distributions are more strict than the Linux kernel allows. Using the kernel default would mean created files and folders are writable by every user on the system. They are however readable by `other` so beware of this with sensitive files.

The exact configuration of permissions for new files and folders is set by the `umask`. This is a value that defines the 'mask' that is applied for all processes. To see the current mask, use the command `umask`.

```bash
student@linux-ess:~/course$ umask
0002 #ignore the first 0 for now
```
So how does this work? We know the default is 666: if you substract the umask from that you get 664 or rw-rw-r-- (for folders we start with 777, so end with 775). A umask of 000 allows everything, a umask of 777 will make a new file have no permissions. The numbers still work the same (4 for read, 2 for write, 1 for execute) but this time you are using them to **mask** certain permission bits, or put more simply: deny certain permissions on new files and folders.

You can change the umask by using the same umask command.

```bash
student@linux-ess:~/course$ umask 000
student@linux-ess:~/course$ touch newfile1
student@linux-ess:~/course$ ls -l newfile1
-rw-rw-rw- 1 student student 0 okt 15 16:23 newfile1
student@linux-ess:~/course$ umask 026 #if you want to mask multiple bits, add them together
student@linux-ess:~/course$ touch newfile2
student@linux-ess:~/course$ ls -l newfile2
-rw-r----- 1 student student 0 okt 15 16:24 newfile2
student@linux-ess:~/course$ umask 077 
student@linux-ess:~/course$ mkdir newfolder1
student@linux-ess:~/course$ ls -ld newfolder1
drwx------ 2 student student 4096 okt 15 16:25 newfolder1
```
?> <i class="fa-solid fa-circle-info"></i>Setting the umask using the command changes the umask for your current terminal session. Exiting the terminal will reset it to the default value. To make it permanent add `umask <your umask>` to your user's `.bashrc` file in your home directory.

```bash
student@linux-ess:~/course$ touch file
student@linux-ess:~/course$ sudo touch file2
student@linux-ess:~/course$ ls -l
-rw-rw-r-- 1 student student 0 okt 15 16:44 file
-rw-r--r-- 1 root    root    0 okt 15 16:44 file2
```
One last thing to be aware of: If you look at the above files, you'll see that files created by the root user have a different umask set. This is explained by looking at the system-wide umask setting, found in the `/etc/login.defs` file.

```bash
student@linux-ess:~/course$ nano /etc/login.defs
UMASK           022 #line 151
...
USERGROUPS_ENAB yes #line 230
```
To change the setting system-wide you can change the value for umask here. The default umask specified is the one the root user uses (no write for anybody but the owner). The reason files created by regular users get an extra w for the group, is the option on line 230. This option specifies that for any non-root user that has the same user-id as group-id (so the primary group is unchanged) the group umask-bits gets changed to the user umask-bits, explaining the 002 umask seen above.

### Access control lists
The ACL feature was created to give users the ability to selectively share files and folders with other users and groups. Before ACL’s are usable, they need to be turned on when the filsystem is mounted. In our Ubuntu installation ACL’s are loaded in by standard. To add ACL’s to a file or folder, use the setfacl command. ACL’s can be looked at with the getfacl command. To add ACL’s you need to be the owner of the file or folder, if you are added by an ACL you will not be able to add ACL’s yourself. All ACL permissions are cumulative, this means if we are in 2 groups that are added to a file with ACL’s. One with r— rights and one with rwx rights, we will have rwx rights. 
With the setfacl command, we’ll be able to modify, with the -m parameter, or delete, with the -x parameter, ACL’s. 
```bash
student@linux-ess:~$ touch /tmp/memo.txt
student@linux-ess:~$ ls -l /tmp/memo.txt
-rw-rw-r-- 1 student student 0 sep 14 18:27 /tmp/memo.txt
student@linux-ess:~$ setfacl -m u:Tina:rw /tmp/memo.txt
student@linux-ess:~$ setfacl -m g:Sales:rw /tmp/memo.txt
student@linux-ess:~$ ls -l /tmp/memo.txt
-rw-rw-r--+ 1 student student 0 sep 14 18:27 /tmp/memo.txt
```
With getfacl we can check the existing ACL’s on a file or folder. Note that we can also see that ACL’s are set by a + in the ls -l command
```bash
student@linux-ess:~$ getfacl /tmp/memo.txt 
getfacl: Removing leading '/' from absolute path names
# file: tmp/memo.txt
# owner: student
# group: student
user::rw-
user:Tina:rw-
group::rw-
group:Sales:rw-
mask::rw-
other::r--
```
In previous example, we also see a mask option, this option decides the maximum permission. We can also add this parameter as follows:
```bash
student@linux-ess:~$ setfacl -m m:r /tmp/memo.txt 
student@linux-ess:~$ getfacl /tmp/memo.txt 
getfacl: Removing leading '/' from absolute path names
# file: tmp/memo.txt
# owner: student
# group: student
user::rw-
user:Tina:rw-			#effective:r--
group::rw-			#effective:r--
group:Sales:rw-			#effective:r--
mask::r--
other::r--
```
We can also add default ACL’s by adding the d: parameter. The default part makes sure new fils or folders get the same ACL’s as their parent directory. Note that this only applies if the user creating the file or folder has the permissions to do so! 
```bash
student@linux-ess:~$ mkdir /tmp/memos
student@linux-ess:~$ setfacl -m d:g:design:rwx /tmp/memos/
student@linux-ess:~$ getfacl /tmp/memos/
getfacl: Removing leading '/' from absolute path names
# file: tmp/memos/
# owner: student
# group: student
user::rwx
group::rwx
other::r-x
default:user::rwx
default:group::rwx
default:group:design:rwx
default:mask::rwx
default:other::r-x

student@linux-ess:~$ mkdir /tmp/memos/January
student@linux-ess:~$ getfacl /tmp/memos/January/
getfacl: Removing leading '/' from absolute path names
# file: tmp/memos/January/
# owner: student
# group: student
user::rwx
group::rwx
group:design:rwx
mask::rwx
other::r-x
default:user::rwx
default:group::rwx
default:group:design:rwx
default:mask::rwx
default:other::r-x

student@linux-ess:~$ touch /tmp/memos/January/19
student@linux-ess:~$ getfacl /tmp/memos/January/19
getfacl: Removing leading '/' from absolute path names
# file: tmp/memos/January/19
# owner: student
# group: student
user::rw-
group::rwx			#effective:rw-
group:design:rwx		#effective:rw-
mask::rw-
other::r--
```

### Enabling access control lists
Some Linux file systems have a standard support for ACLs via the kernel. With the following command we can check which file systems are enable to use ACL's on our system.
```bash
student@linux-ess:~$ grep POSIX_ACL /boot/config-$(uname -r)
CONFIG_EXT4_FS_POSIX_ACL=y
CONFIG_REISERFS_FS_POSIX_ACL=y
CONFIG_JFS_POSIX_ACL=y
CONFIG_XFS_POSIX_ACL=y
CONFIG_BTRFS_FS_POSIX_ACL=y
CONFIG_F2FS_FS_POSIX_ACL=y
CONFIG_FS_POSIX_ACL=y
CONFIG_SHIFT_FS_POSIX_ACL=y
CONFIG_NTFS3_FS_POSIX_ACL=y
CONFIG_TMPFS_POSIX_ACL=y
CONFIG_JFFS2_FS_POSIX_ACL=y
CONFIG_EROFS_FS_POSIX_ACL=y
CONFIG_CEPH_FS_POSIX_ACL=y
CONFIG_9P_FS_POSIX_ACL=y
```
File systems that don't have ACL support via the kernel are still able to get it via the mount option. ACL support is added with different methods:
*	The ACL option in the 4th field of the file /etc/stab
*	Adding the ACL line in the default mount option field in the superblock of the file system
*	Adding the ACL option to the mount command when you manually mount file systems
When the acl option is not present for your filesystem you can add the acl mount option with the command tune2fs -o. For example, you have a usb-stick with a ext4 file system named /dev/sdb1, this is seen in a later chapter. 
```bash
student@linux-ess:~$ sudo tune2fs -o acl /dev/sdb1
tune2fs 1.46.5 (30-Dec-2021)
student@linux-ess:~$ sudo tune2fs -l /dev/sdb1 | grep "mount options"
Default mount options:    user_xattr acl
```
A second option was to enable acl by adding the acl option in the file /etc/fstab, this automatically acitivates on startup of you system.
```bash
student@linux-ess:~$ cat /etc/fstab
/dev/sdc1 	/var/stuff 	ext4 	acl 		1 	     2
```
The last option was to enable acls when manually mounting a filesystem. We do not have an entry in the /etc/fstab file with this method. This method is only temporary, on restart our mount will be gone. 
```bash
student@linux-ess:~$ sudo mount -o acl /dev/sdb1 /var/stuff
```
