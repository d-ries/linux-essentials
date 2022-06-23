# Users and permissions
As with any operating system we will be working with different users on the system. We've been using the user `student`. We can confirm this by running the command `whoami`. Another command we can run is the command `who` or `w`. This will show us all of the users that are logged in on the system (mind that both commands have a different output!).

## User management

### /etc/passwd
As we've seen before alot in Linux is done using config files. The same can be said about user management. Users are kept in the file `/etc/passwd`. This contains a list with useraccounts and some metadata seperated by colons:
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
dries:x:1000:1000:,,,:/home/dries:/bin/bash
```
The first account in this file is the `root` account:
```bash
student@linux-ess:~$ head -1 /etc/passwd
root:x:0:0:root:/root:/bin/bash
```
You can find more information about this file, the columns and the contents by running the command `man 5 passwd`.

### Adding users (useradd)

```bash
student@linux-ess:~$ sudo useradd -m -d /home/ventieldopje24 -c "Dries Swinnen" ventieldopje24
[sudo] password for student:
student@linux-ess:~$
```

?> We can delete users by running the command `userdel -r ventieldopje24`. The option `-r` will remove that user's homefolder.

#### Homefolders

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
These settings are kept in the file `/etc/default/useradd` and can be changed at any time.

/etc/skel

#### Default profile files
.bash_profile
.bashrc
.bash_logout
.bash_history
.profile

### Editing users (usermod & userdel)

```bash
ventieldopje24:x:1001:1001:Dries Swinnen:/home/ventieldopje24:/bin/sh
student@linux-ess:~$ sudo usermod -c 'hackerman' ventieldopje24
student@linux-ess:~$ tail -1 /etc/passwd
ventieldopje24:x:1001:1001:hackerman:/home/ventieldopje24:/bin/sh
```

#### Setting user passwords
```bash
student@linux-ess:~$ sudo passwd ventieldopje24
New password:
Retype new password:
passwd: password updated successfully
```

```bash
student@linux-ess:~$ sudo tail -1 /etc/shadow
ventieldopje24:$6$4vg/x5qVib6l64Ag$jAru5Ov9l1jr6gfeoJO5LWDX5AiVADusToKSKT9H4u3Ih.KgZnWnZeM7N9.csfrqdABezJQbCSsD4j4YG/nFk1:19166:0:99999:7:::
```


```bash
student@linux-ess:~$ sudo usermod -L ventieldopje24
```


## Switching users (su)
```bash
student@linux-ess:~$ su ventieldopje24
Password:
$ whoami
ventieldopje24
$ cd
$ pwd
/home/ventieldopje24
$ exit
student@linux-ess:~$
```

## Sudo
```bash
student@linux-ess:~$ sudo su ventieldopje24
$ whoami
ventieldopje24
```

```bash
student@linux-ess:~$ sudo su root
root@linux-ess:/home/student# whoami
root
```


## Group management
```bash
student@linux-ess:~$ groups
student adm dialout cdrom floppy sudo audio dip video plugdev netdev
```

### /etc/group
```bash
student@linux-ess:~$ tail -2 /etc/group
student:x:1000:
ventieldopje24:x:1001:
```


### Adding groups (groupadd).
```bash
student@linux-ess:~$ sudo groupadd pxl
student@linux-ess:~$ tail -2 /etc/group
ventieldopje24:x:1001:
pxl:x:1002:
```

?> We can delete groups using the command `sudo groupdel pxl`.

### Editing groups (groupmod)

```bash
student@linux-ess:~$ sudo groupmod -n hogeschool-pxl pxl
student@linux-ess:~$ tail -1 /etc/group
hogeschool-pxl:x:1002:
```

### Edit group memberships (usermod)

```bash
student@linux-ess:~$ sudo usermod -a -G pxl student
student@linux-ess:~$ su student
Password:
student@linux-ess:~$ groups
student adm dialout cdrom floppy sudo audio dip video plugdev netdev pxl
```

## Permissions

### Octal notations

### Changing permissions (chmod)

### Changing ownership (chgrp, chown)

### Default permissions (umask)

