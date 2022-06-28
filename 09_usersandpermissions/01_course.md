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
student:x:1000:1000:,,,:/home/student:/bin/bash
```
The first account in this file is the `root` account:
```bash
student@linux-ess:~$ head -1 /etc/passwd
root:x:0:0:root:/root:/bin/bash
```
We can see more info that just usernames. These lines contain the user identifier (`1000` for `student`), home folder location, default shell, ... You can find more information about this file, the columns and the contents by running the command `man 5 passwd`.

### Adding users (useradd)
To add users we can simply use the `useradd` command. Its important to note that we have to run these commands with `sudo` rights. This is because it are system commands that affect the entire system. To add a new user with the username `ventieldopje24` we could run the following command:
```
student@linux-ess:~$ sudo useradd -m -d /home/ventieldopje24 -c "Dries Swinnen" ventieldopje24
[sudo] password for student:
student@linux-ess:~$
```
The `-d` takes in an argument and uses this argument as a path to where the homefolder has to be created. The `m` option (`create home`) will make sure the home folder actually gets created with the correct permissions. Lastly the `-c` (`comment`) option sets extra metadata to the user. 

?> We can delete users by running the command `userdel -r ventieldopje24`. The option `-r` will remove that user's homefolder. As seen in the folder `/home` or in the file `/etc/passwd` the new user has been created:
```bash
student@linux-ess:~$ tail -1 /etc/passwd
ventieldopje24:x:1001:1001:hackerman:/home/ventieldopje24:/bin/sh
```

#### Homefolders
By default homefolders are created in the `/home` directory. These folders aren't created by scratch. It uses a template that is located in `/etc/skel`. This means that if we edit any contents in this `skel` folder, it wil actually be copied to any new users we create. The `useradd` command uses quite some default values. We can check these default values by running the following command:
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

#### Default profile files
#todo
.bashrc
.bash_history
.profile

### Editing users (usermod & userdel)
To edit a user's account info, we can use the `usermod` command. This command has several options that we can use to edit specific things. For example to edit the commend field op a user we can run the following command:
```bash
ventieldopje24:x:1001:1001:Dries Swinnen:/home/ventieldopje24:/bin/sh
student@linux-ess:~$ sudo usermod -c 'hackerman' ventieldopje24
student@linux-ess:~$ tail -1 /etc/passwd
ventieldopje24:x:1001:1001:hackerman:/home/ventieldopje24:/bin/sh
```

#### Setting user passwords
As seen in the previous commands we created a new user with the username `ventieldopje24` but we never gave it a password. To do this we can run the `passwd` command with `sudo` rights and with a username as argument. This forces setting a new password for that specific user:
```bash
student@linux-ess:~$ sudo passwd ventieldopje24
New password:
Retype new password:
passwd: password updated successfully
```
?> Note that when you run the `passwd` command without a username and without `sudo` rights, we can change our current user's password!

Passwords are stored in another configuration file called `/etc/shadow`. To view this file we'll need `sudo` rights:
```
student@linux-ess:~$ sudo tail -1 /etc/shadow
ventieldopje24:$6$4vg/x5qVib6l64Ag$jAru5Ov9l1jr6gfeoJO5LWDX5AiVADusToKSKT9H4u3Ih.KgZnWnZeM7N9.csfrqdABezJQbCSsD4j4YG/nFk1:19166:0:99999:7:::
```
As seen in the example above the password isn't shown in plaintext. This is because Linux systems use hashing algoritms to encrypt the passwords. The algoritm used here is called _sha512_.

The user `ventieldopje24` is now ready to login on the system with its set password. We can always lock accounts using the `usermod` command:
```bash
student@linux-ess:~$ sudo usermod -L ventieldopje24
```
This will add an exclamation mark (`!`) in front of the password. This tells the system that the user account is not allowed to login to the system.

## Switching users (su)
To switch user accounts we could use the `exit` command to close the current shell and this will, eventually, end up in giving us the login prompt of the server. An alternative is to use the `su` (`switch user`) command:
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
This command will prompt the password of the user you want to login to. As seen in the example above we switched to the user `ventieldopje24` with the password we've set previously. After that we run the `cd` command to go to the users homefolder (and check this running the `pwd` command). After that we run the `exit` command which will close down the shell and return to the original shell where we ran the `su ventieldopje24` command.

## Sudo
Note that when you run the `su` command with `sudo` rights, you will not be prompted to enter that users password (if you still get a password prompt, its the password of the account running the `sudo` command). This will skip any login checks and switch straight to the user provided:
```bash
student@linux-ess:~$ sudo su ventieldopje24
$ whoami
ventieldopje24
```

By default the user `root` has no password set. So we cannot login as root using a password. What we can do is run `su` with `sudo` rights to skip any password checks and login straight as `root`:
```bash
student@linux-ess:~$ sudo su root
root@linux-ess:/home/student# whoami
root
```
We want to be mindfull of commands that we run as the `root` user. This user has permissions on all the files, folders and services on our system. This means that running commands as `root` can have a huge impact when being exploited.

## Group management
```
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

```
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
