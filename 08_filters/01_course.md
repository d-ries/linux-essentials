# Filters and file operations
When working with (text) files we often want to perform operations on them to manipulate the file contents to get a specific output. 

For example: We have a huge logfile that logs all login attemps for our application where it logs usernames, ip adresses, timestamps, location, ISP info, metadata, ... We might want to quickly lookup all incorrect login attemps by user X and see what IP addresses he's connected from. We could manually go through the file and check the records like that but often that process is long and tedious. What we want to do is use commands to filter, manipulate and structure the data to the desired result. To do this we can use a wide set of filter and structure commands that we can link using _pipes_.

For the examples in this chapter we will use a log file filled with data. To download this file you can run the following command:
```bash
wget https://d-ries.github.io/linux-essentials/data/auth.log
```

## Using pipes
A pipe (`|`) is a specific symbol that we can use to link commands together. The pipe symbol will take the `stdout` from the first command and fowards it to the `stdin` from the next command:
 ```bash
student@linux-ess:~$ head -3 auth.log | tail -2 auth.log
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 77898 ssh2
Jun 22 21:11:12 linux-ess: Accepted password for: doeg from 192.168.0.10 port 44293 ssh2
```
The example above will run the `head -3` command which will take the first 3 lines of the file `auth.log`. The output containing the first 3 lines of the file will then be used as input for the `tail -2` command which results in taking the bottom 2 lines of the first 3 lines of the file `auth.log`.

You can use as many pipes as you want in a command. They will just keep passing the output of the previous command to the next command and so on:
```bash
student@linux-ess:~$ cat auth.log | head | tail -3 | tail -2 | head -1
Jun 17 18:22:22 linux-ess: Accepted password for: janedoe from 192.168.0.10 port 43448 ssh2
```

### Write to file (tee)
Sometimes you want to temporary write te result to a seperate file while continuing to work with pipes to get a certain end result. This command will forward the `stdin` to the `stdout` and it will aslo forward `stdin` towards a file provided as an argument:
```bash
student@linux-ess:~$ tail -3 auth.log | tee temp_log | tail -1
Jun 22 21:11:12 linux-ess: Accepted password for: doeg from 192.168.0.10 port 44293 ssh2
student@linux-ess:~$ cat temp_log
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 87568 ssh2
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 77898 ssh2
Jun 22 21:11:12 linux-ess: Accepted password for: doeg from 192.168.0.10 port 44293 ssh2
```

## Filtering output
### Using content filters (grep)
We often want to browse files and get certain lines containing certain strings or patterns. This is where the `grep` command comes in. `grep` is one of the most used filter commands in Linux systems. We can use it as a standalone command as follows:
```bash
student@linux-ess:~$ grep jane auth.log
Jun 15 17:42:18 linux-ess: Failed password for: janedoe from 192.168.0.10 port 48239 ssh2
Jun 17 18:22:22 linux-ess: Accepted password for: janedoe from 192.168.0.10 port 43448 ssh2
```
Or we can use it as a _pipe_:
```bash
student@linux-ess:~$ cat auth.log | grep jane
Jun 15 17:42:18 linux-ess: Failed password for: janedoe from 192.168.0.10 port 48239 ssh2
Jun 17 18:22:22 linux-ess: Accepted password for: janedoe from 192.168.0.10 port 43448 ssh2
```
Both commands give the same result and work the same. What we can see is that the `grep` command will filter the file contents based on a keyword (in this case `jane`). 

An important note to make is that, by default, `grep` is a case sensitive command. It will only show the lines in the file containing that specific keyword. Note that writing the keyword in caps will result in 0 lines being returned:
```bash
student@linux-ess:~$ cat auth.log | grep JANE
student@linux-ess:~$
```
However there is an option (`-i`) to make grep work case insensitive: 
```bash
student@linux-ess:~$ cat auth.log | grep -i JANE
Jun 15 17:42:18 linux-ess: Failed password for: janedoe from 192.168.0.10 port 48239 ssh2
Jun 17 18:22:22 linux-ess: Accepted password for: janedoe from 192.168.0.10 port 43448 ssh2
```

Another interesting option is `-v` which will return all lines _not_ containing the keyword:
```bash
student@linux-ess:~$ cat auth.log | grep -v password
Jun 09 11:11:11 linux-ess: Server listening on 0.0.0.0 port 22.
Jun 09 11:11:11 linux-ess: Server listening on :: port 22.
Jun 09 12:32:24 linux-ess: Accepted publickey for: johndoe from 85.245.107.42 port 54259 ssh2: RSA SHA256:K18kPGZrTiz7gkeOeirKlzmgIogh

Jun 14 14:14:12 linux-ess: Accepted publickey for: student from 85.245.107.42 port 48298 ssh2: RSA SHA256:Keo89erjOEkmo9erjkDw
```

Knowing that we can use multiple pipes (`|`) in a command, we can combine multiple grep commands aswell. Imagine the scenario where we want to find only successful login attemps made by the user `janedoe`. We could do this as follows:
```bash
student@linux-ess:~$ cat auth.log | grep janedoe | grep -vi failed
Jun 17 18:22:22 linux-ess: Accepted password for: janedoe from 192.168.0.10 port 43448 ssh2
```
or (there are multiple correct answers here)
```
student@linux-ess:~$ cat auth.log | grep janedoe | grep Accepted
Jun 17 18:22:22 linux-ess: Accepted password for: janedoe from 192.168.0.10 port 43448 ssh2
```

#### Regular expressions

### Using content structure

#### Using columns (cut)

#### Using sorting (sort & uniq)

#### Using counts (wc)

#### using columns (comm)

## Manipulating output content

### Translate (tr)

### Stream editor (sed)



