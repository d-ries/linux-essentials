# Users and permissions
As with any operating system we will be working with different users on the system. We've been using the user `student`. We can confirm this by running the command `whoami`. Another command we can run is the command `who` or `w`. This will show us all of the users that are logged in on the system (mind that both commands have a different output!).

## User management
### /etc/passwd
As we've seen before a lot in Linux is done using config files. The same can be said about user management. User configuration is stored in the file `/etc/passwd`. It contains a list of user accounts and some metadata seperated by colons:
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

We can see more info that just usernames. These lines contain the user identifier (`1000` for `student`), home folder location, default shell, ... 

?> <i class="fa-solid fa-circle-info"></i> You can find more information about this file, the columns and the contents by running the command `man 5 passwd`.

### Adding users (useradd)
To add users we can simply use the `useradd` command. Its important to note that we have to run these commands with `sudo` rights. This is because it are system commands that affect the entire system. To add a new user with the username `teacher` we could run the following command:
```bash
student@linux-ess:~$ sudo useradd -m -d /home/teacher -c "Teacher Account" teacher
[sudo] password for student:
student@linux-ess:~$ tail -3 /etc/passwd
student:x:1000:1000:student:/home/student:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
teacher:x:1001:1001:Teacher Account:/home/teacher:/bin/sh
```
The `-d` takes in an argument and uses this argument as a path to where the homefolder has to be created. The `m` option (`create home`) will make sure the home folder actually gets created with the correct permissions. Lastly the `-c` (`comment`) option sets extra metadata to the user. 

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
By default homefolders are created as a subdirectory of the `/home` directory. These folders aren't created by scratch. It uses a template that is located in `/etc/skel`. This means that if we alter any contents in this `skel` folder, this wil actually be copied to any new users we create in the future:

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
To edit a user's account info, we can use the `usermod` command. This command has several options that we can use to edit specific things. For example to edit the comment field op a user we can run the following command:
```bash
student@linux-ess:~$ sudo usermod -c "Gert VW" teacher
student@linux-ess:~$ tail -1 /etc/passwd
teacher:x:1002:1003:Gert VW:/home/teacher:/bin/sh
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

?> All of the options that we can use can be found in the manpage by running `man usermod`.

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

### Octal notations

### Changing permissions (chmod)

### Changing ownership (chgrp, chown)

### Default permissions (umask)

### Access control lists
The ACL feature was created to give users the ability to selectively share files and folders with other users and groups. Before ACL’s are usable, they need to be turned on when the filsystem is mounted. In our Ubuntu installation ACL’s are loaded in by standard. To add ACL’s to a file or folder, use the setfacl command. ACL’s can be looked at with the getfacl command. To add ACL’s you need to be the owner of the file or folder, if you are added by an ACL you will not be able to add ACL’s yourself. All ACL permissions are cumulative, this means if we are in 2 groups that are added to a file with ACL’s. One with r— rights and one with rwx rights, we will have rwx rights. 
With the setfacl command, we’ll be able to modify, with the -m parameter, or delete, with the -x parameter, ACL’s. 
```bash
student@linux-ess-desktop:~$ touch /tmp/memo.txt
student@linux-ess-desktop:~$ ls -l /tmp/memo.txt
-rw-rw-r-- 1 student student 0 sep 14 18:27 /tmp/memo.txt
student@linux-ess-desktop:~$ setfacl -m u:Tina:rw /tmp/memo.txt
student@linux-ess-desktop:~$ setfacl -m g:Sales:rw /tmp/memo.txt
student@linux-ess-desktop:~$ ls -l /tmp/memo.txt
-rw-rw-r--+ 1 student student 0 sep 14 18:27 /tmp/memo.txt
```
With getfacl we can check the existing ACL’s on a file or folder. Note that we can also see that ACL’s are set by a + in the ls -l command
```bash
student@linux-ess-desktop:~$ getfacl /tmp/memo.txt 
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
student@linux-ess-desktop:~$ setfacl -m m:r /tmp/memo.txt 
student@linux-ess-desktop:~$ getfacl /tmp/memo.txt 
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
student@linux-ess-desktop:~$ mkdir /tmp/memos
student@linux-ess-desktop:~$ setfacl -m d:g:design:rwx /tmp/memos/
student@linux-ess-desktop:~$ getfacl /tmp/memos/
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

student@linux-ess-desktop:~$ mkdir /tmp/memos/January
student@linux-ess-desktop:~$ getfacl /tmp/memos/January/
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

student@linux-ess-desktop:~$ touch /tmp/memos/January/19
student@linux-ess-desktop:~$ getfacl /tmp/memos/January/19
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
student@linux-ess-desktop:~$ grep POSIX_ACL /boot/config-$(uname -r)
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
student@linux-ess-desktop:~$ sudo tune2fs -o acl /dev/sdb1
tune2fs 1.46.5 (30-Dec-2021)
student@linux-ess-desktop:~$ sudo tune2fs -l /dev/sdb1 | grep "mount options"
Default mount options:    user_xattr acl
```
A second option was to enable acl by adding the acl option in the file /etc/fstab, this automatically acitivates on startup of you system.
```bash
student@linux-ess-desktop:~$ cat /etc/fstab
/dev/sdc1 	/var/stuff 	ext4 	acl 		1 	     2
```
The last option was to enable acls when manually mounting a filesystem. We do not have an entry in the /etc/fstab file with this method. This method is only temporary, on restart our mount will be gone. 
```bash
student@linux-ess-desktop:~$ sudo mount -o acl /dev/sdb1 /var/stuff
```