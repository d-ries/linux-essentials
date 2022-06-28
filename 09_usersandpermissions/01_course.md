# Users and permissions
As with any operating system we will be working with different users on the system. We've been using the user `student`. We can confirm this by running the command `whoami`. Another command we can run is the command `who` or `w`. This will show us all of the users that are logged in on the system (mind that both commands have a different output!).

## User management

### /etc/passwd
As we've seen before a lot in Linux is done using config files. The same can be said about user management. User configuration is stored in the file `/etc/passwd`. It contains a list of user accounts and some metadata seperated by colons:
```bash
student@linux-ess:~$ tail /etc/passwd
syslog:x:104:110::/home/syslog:/usr/sbin/nologin
_apt:x:105:65534::/nonexistent:/usr/sbin/nologin
tss:x:106:111:TPM software stack,,,:/var/lib/tpm:/bin/false
uuidd:x:107:112::/run/uuidd:/usr/sbin/nologin
tcpdump:x:108:113::/nonexistent:/usr/sbin/nologin
sshd:x:109:65534::/run/sshd:/usr/sbin/nologin
landscape:x:110:115::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:111:1::/var/cache/pollinate:/bin/false
student:x:1000:1000:,,,:/home/student:/bin/bash
```
The first account in this file is the `root` account:
```bash
student@linux-ess:~$ head -1 /etc/passwd
root:x:0:0:root:/root:/bin/bash
```
?> <i class="fa-solid fa-circle-info"></i> You can find more information about this file, the columns and the contents by running the command `man 5 passwd`.

### Adding users (useradd)
### useradd

```bash
student@linux-ess:~$ sudo useradd -m -d /home/teacher -c "Teacher Account" teacher
[sudo] password for student:
student@linux-ess:~$ tail -3 /etc/passwd
student:x:1000:1000:student:/home/student:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
teacher:x:1001:1001:Teacher Account:/home/teacher:/bin/sh
```

?> <i class="fa-solid fa-circle-info"></i> We can delete users by running the command `userdel -r teacher`. The option `-r` will also remove that user's homefolder.

?> <i class="fa-solid fa-circle-info"></i> Every user has a userid (the third field in `/etc/passwd`). To view the userid of a user you can use the `id` command:
```bash
student@linux-ess:~$ id teacher
uid=1001(teacher) gid=1001(teacher) groups=1001(teacher)
```

?> <i class="fa-solid fa-circle-info"></i> Before we can login with the new user we have to give him a password with the `passwd` command:
```bash
student@linux-ess:~$ sudo passwd teacher
New password:
Retype new password:
passwd: password updated successfully
```

#### Setting user passwords
The password gets stored in the file `/etc/shadow` for security reasons. Regular users cannot view the contents of this file:
```bash
student@linux-ess:~$ tail -1 /etc/shadow
tail: cannot open '/etc/shadow' for reading: Permission denied
student@linux-ess:~$ sudo tail -1 /etc/shadow
teacher:$y$j9T$Vtf.U//c4/N/CB8LzHfnl0$5iCgijrpqXfaA3v18w/nAL2rl8BmiBYX5rn5rf.j6B7:19171:0:99999:7:::
```

#### Default values 
The default values used for adding a new user are kept in the file `/etc/default/useradd` and can be changed at any time:
```bash
student@linux-ess:~$ useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/sh
SKEL=/etc/skel
CREATE_MAIL_SPOOL=no
```

#### /etc/skel
The default files a new user gets copied to his homefolder are stored in `/etc/skel`:
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

## Switching users (su)
Instead of loging out to login as a different user you can temporarily switch to another user:
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

?> <i class="fa-solid fa-circle-info"></i> Note that root can become whoever he wants without the need to know that users password:
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

?> <i class="fa-solid fa-circle-info"></i> Note that to become root (without knowing his password) we can also use the `sudo` command:
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


### Adding groups (groupadd).
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

?> <i class="fa-solid fa-circle-info"></i> If you forget the `-a` option the user will only be in the specified group and will be removed from all the groups he was in. This can be a serious problem if the user was the only one in the sudo group!

?> <i class="fa-solid fa-circle-info"></i> The primary group of a user is specified in `/etc/passwd` and is the default group set on a new file or directory created by that user.


## Permissions

### Octal notations

### Changing permissions (chmod)

### Changing ownership (chgrp, chown)

### Default permissions (umask)
