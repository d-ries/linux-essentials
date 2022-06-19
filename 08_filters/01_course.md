# Filters and file operations
When working with (text) files we often want to perform operations to manipulate the file contents to get a specific output. 

For example: We have a huge logfile that logs all login attemps for our application where it logs usernames, ip adresses, timestamps, location, ISP info, metadata, ... We might want to quickly lookup all incorrect login attemps by user X and see what IP addresses he was connecting from. We could manually go through the file line by line to check it but often that process is long and tedious. What we want to do is use commands to filter, manipulate and structure the data to the desired result. To do this we can use a wide set of filter and structure commands that we can link together using _pipes_.

For the examples in this chapter we will use a log file filled with data. To download this file you can run the following command:
```bash
student@linux-ess:~$ wget https://d-ries.github.io/linux-essentials/data/auth.log
--2022-06-19 18:15:24--  https://d-ries.github.io/linux-essentials/data/auth.log
Resolving d-ries.github.io (d-ries.github.io)... 185.199.109.153, 185.199.108.153, 185.199.111.153, ...
Connecting to d-ries.github.io (d-ries.github.io)|185.199.109.153|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1730 (1.7K) [text/plain]
Saving to: 'auth.log'

auth.log                      100%[=================================================>]   1.69K  --.-KB/s    in 0s

2022-06-19 18:15:25 (5.32 MB/s) - 'auth.log' saved [1730/1730]
student@linux-ess:~$ cat auth.log
Jun 09 11:11:11 linux-ess: Server listening on 0.0.0.0 port 22.
Jun 09 11:11:11 linux-ess: Server listening on :: port 22.
Jun 09 12:32:24 linux-ess: Accepted publickey for: johndoe from 85.245.107.42 port 54259 ssh2: RSA SHA256:K18kPGZrTiz7g>
Jun 10 21:38:01 linux-ess: Failed password for: student from 192.168.0.1 port 37362 ssh2
Jun 10 21:39:01 linux-ess: Failed password for: johndoe from 192.168.0.2 port 37849 ssh2
Jun 10 21:42:01 linux-ess: Accepted password for: student from 84.298.138.41 port 48785 ssh2
Jun 14 14:12:33 linux-ess: Accepted password for: johndoe from 192.168.0.3 port 38654 ssh2
Jun 14 14:14:12 linux-ess: Accepted publickey for: student from 85.245.107.42 port 48298 ssh2: RSA SHA256:Keo89erjOEkmo>Jun 15 17:42:18 linux-ess: Failed password for: janedoe from 192.168.0.10 port 48239 ssh2
Jun 17 18:22:22 linux-ess: Accepted password for: janedoe from 192.168.0.10 port 43448 ssh2
Jun 19 22:43:23 linux-ess: Failed password for: johndoe from 85.245.107.42 port 22834 ssh2: RSA SHA256:eoKmezlE3iOp38Dj>Jun 22 08:04:00 linux-ess: Accepted password for: johndoe from 192.168.0.99 port 38299 ssh2
Jun 22 21:11:11 linux-ess: Failed password for: doeg from 192.168.0.10 port 44293 ssh2
Jun 22 21:11:11 linux-ess: Failed password for: doeg from 192.168.0.10 port 48987 ssh2
Jun 22 21:11:11 linux-ess: Failed password for: doeg from 192.168.0.10 port 22658 ssh2
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 34598 ssh2
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 87568 ssh2
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 77898 ssh2
Jun 22 21:11:12 linux-ess: Accepted password for: doeg from 192.168.0.10 port 44293 ssh2
```

## Using pipes
A pipe (`|`) is a specific symbol that we can use to link commands together. The pipe symbol will take the `stdout` from the previous command and fowards it to the `stdin` of the next command:
 ```bash
student@linux-ess:~$ head -3 auth.log | tail -2 auth.log
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 77898 ssh2
Jun 22 21:11:12 linux-ess: Accepted password for: doeg from 192.168.0.10 port 44293 ssh2
```
The example above will run the `head -3` command which will take the first 3 lines of the file `auth.log`. The output containing the first 3 lines of the file will then be used as input for the `tail -2` command which results in taking the bottom 2 lines of the first 3 lines of the file `auth.log`. This means that the result is the second and third line of the file.

You can use as many pipes as you want in a command line. It will just keep passing the output of a command to the input of the next command and so on:
```bash
student@linux-ess:~$ cat auth.log | head | tail -3 | tail -2 | head -1
Jun 17 18:22:22 linux-ess: Accepted password for: janedoe from 192.168.0.10 port 43448 ssh2
```

### Write to file (tee)
Sometimes you want to temporarily write the results to a seperate file while continuing to work with pipes to get a certain end result. This command will forward the `stdin` to the `stdout` but will also store the `stdin` in a file provided as an argument:
```bash
student@linux-ess:~$ tail -3 auth.log | tee temp_log | tail -1
Jun 22 21:11:12 linux-ess: Accepted password for: doeg from 192.168.0.10 port 44293 ssh2
student@linux-ess:~$ cat temp_log
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 87568 ssh2
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 77898 ssh2
Jun 22 21:11:12 linux-ess: Accepted password for: doeg from 192.168.0.10 port 44293 ssh2
```

tee is also often used to put results in a file where you don't have the right privileges and need to use `sudo`:
```bash
student@linux-ess:~$ tail -3 auth.log | head -1 > /filteredlogfile
-bash: /filteredlogfile: Permission denied
student@linux-ess:~$ sudo tail -3 auth.log | head -1 > /filteredlogfile
-bash: /filteredlogfile: Permission denied
student@linux-ess:~$ tail -3 auth.log | head -1 | tee /filteredlogfile
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 87568 ssh2
tee: /filteredlogfile: Permission denied
student@linux-ess:~$ cat /filteredlogfile
cat: qdfqdf: No such file or directory
student@linux-ess:~$ tail -3 auth.log | head -1 | sudo tee /filteredlogfile
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 87568 ssh2
student@linux-ess:~$ cat /filteredlogfile
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 87568 ssh2
```

?> If you want to add to the output file with tee you can specify the option `-a`
```bash
student@linux-ess:~$ head -1 auth.log | sudo tee -a /filteredlogfile
Jun 09 11:11:11 linux-ess: Server listening on 0.0.0.0 port 22.
student@linux-ess:~$ cat /filteredlogfile
Jun 22 21:11:12 linux-ess: Failed password for: doeg from 192.168.0.10 port 87568 ssh2
Jun 09 11:11:11 linux-ess: Server listening on 0.0.0.0 port 22.
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

Sometimes we might want to see more than just the line that contains the keyword. Imagine we want to see some more context as to where the file is located. We can customize the grep command to show lines before or/and after the result as follows:
```bash
student@linux-ess:~$ cat example.log
this is line one
this is line two
this is line three
this is line four
this is line five
student@linux-ess:~$ cat example.log | grep -A1 three
this is line three
this is line four
student@linux-ess:~$ cat example.log  | grep -B2 three
this is line one
this is line two
this is line three
student@linux-ess:~$ cat example.log | grep -C1 three
this is line two
this is line three
this is line four
```

#### Regular expressions
In the examples above we only used simple keywords to find contents in a file. Sometimes we want to filter on dynamic content. Imagine finding all logins from an ip address containing '192' followed by other characters, or finding users that have "doe" as a lastname. To achieve this we have to use a dynamic syntax called a regular expression.

Regular expressions can turn into a real rabbit hole. We will only focus on the most used cases and a couple of practical examples but know that there is a whole _regex_ world to be explored that is beyond the scope of this course!

The `grep` command can use different kinds of _regex_ patterns. By default it uses _basic regular expressions (BRE)_ but for alot of cases we want to extend this to _extended regular expressions (ERE). To do this we have to use the `-E` option in the  `grep` command. This gives us alot more functionality when it comes to building dynamic search queries. **Alot of the commands explained below wont work without the `-E` option!**

For the examples used in this (sub)chapter we will use a seperate file that you can download using the command below:
```bash
wget https://d-ries.github.io/linux-essentials/data/regexlist.txt
```

To start of we will use some special symbols that we've used before. We've seen the impact of an asterix (`*`) in the chapter about _file globbing_. An asterix has a similar functionality in a regex but there are some important key differences:
- In file globbing a `*` sign means 0, one or more of any type of character
- In a regex, a `*` sign means 0, one or more **of the previous character, if available**

Take the example below. We expect only the `pxl` variants to show up, but as we can see in the output all of the file contents show. This is because every line matches the regex `zero, one or more of the letter p`:
 ```
 student@linux-ess:~$ cat regexlist.txt | grep -E "p*"
Dries
Gert
Niek
Lode
Maarten
Tom
David
Bert
Tim
Tommy
pxl
pxxl
pxxxl
pxxxxl
pl
This is a test
This has been tested
192
172
127
192.168.0.1
192.168.1.1
192.168.1.2
172.16.0.4
127.0.0.1
dries.swinnen@pxl.be
http://pxl.be
https://pxl.be
``` 

We can solve this by using the following syntax:
```bash
student@linux-ess:~$ cat regexlist.txt | grep -E "px*"
pxl
pxxl
pxxxl
pxxxxl
pl
```
Now we tell the regex to find lines that contain a `p` followed by zero, one or more `x` characters. This is exactly why `pl` shows up (it contains zero of the character x). Imagine if we wanted to use a regex that contains one or more of a character rather than zero, one or more. We can do this using the `+` sign:
```bash
student@linux-ess:~$ cat regexlist.txt | grep -E "px+"
pxl
pxxl
pxxxl
pxxxxl
```

To take it even a step further, what about exactly 3 occurences? Easy, we can do this as follows:
```bash
student@linux-ess:~$ cat regexlist.txt | grep -E "px{3}"
pxxxl
pxxxxl
```
The `{3}` is linked to the character before that. Notice how the one with 4 `x`'s shows up aswell. This is because 4 times the letter `x` contains 3 times the letter `x`. We could solve this by adding the letter `l` afterwards.

Imagine now we wanted to check for lines that start or end with a specific character or character set. We'll start of with lines starting with a specific character:
```bash
student@linux-ess:~$ cat regexlist.txt | grep -E "^[DGN]"
Dries
Gert
Niek
David
```
The example above uses a `^` sign that indicates the start of a line. Next up we use square brackets `[ ]` that we can use to add characters that can be used as the start of the line. In this case the letters `D`, `G`, and `N`. We could aslo use ranges:
```bash
student@linux-ess:~$ cat regexlist.txt | grep -E "^[0-9]"
192
172
127
192.168.0.1
192.168.1.1
192.168.1.2
172.16.0.4
127.0.0.1
student@linux-ess:~$ cat regexlist.txt | grep -E "^[a-z]"
pxl
pxxl
pxxxl
pxxxxl
pl
dries.swinnen@pxl.be
https://pxl.be
http://pxl.be
```
?> The square brackets are not linked to the beginning and end of a line, so you can use them wherever in the regex. Be aware that these are case sensitive!

To check for lines ending with a specific character we can use a `$` sign:
```bash
student@linux-ess:~$ cat regexlist.txt | grep -E "e$"
Lode
dries.swinnen@pxl.be
https://pxl.be
http://pxl.be
student@linux-ess:~$ cat regexlist.txt | grep -E "[0-9]$"
192
172
127
192.168.0.1
192.168.1.1
192.168.1.2
172.16.0.4
127.0.0.1
```

So what about matching exactly 1 character? A `.` translates to exactly one character of any type:
```bash
student@linux-ess:~$ cat regexlist.txt | grep -E ".... "
This is a test
This has been tested
```
The example above translates to `4 characters of any type followed by a space`. We can combine this with starts & endings again aswell: 
```bash
student@linux-ess:~$ cat regexlist.txt | grep -E "^...\."
192.168.0.1
192.168.1.1
192.168.1.2
172.16.0.4
127.0.0.1
```
This translates to `start with any type of character` (`^.`) followed by 2 more characters of any type (`..`), followed by a regular dot (`\.`). Notice how we escaped the last dot so it doesn't get interpreted as a special regex character!

#### Pattern examples
#TODO: uitwerking analyse/ontleding regex
Creating a regex that checks for a IPv4 address:
```bash
student@linux-ess:~$ cat regexlist.txt | grep -E "^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}$"
192.168.0.1
192.168.1.1
192.168.1.2
172.16.0.4
127.0.0.1
```
Note that this does not validate a valid IPv4 address, whether or not it is public or private or if the number ranges are in the `1-255` range.

?> The `{1,3}` syntax means that the previous characters needs to appear between 1 and 3 times!

Creating a regex that checks for a valid e-mail address format:
```bash
student@linux-ess:~$ cat regexlist.txt | grep -E "^.+\@[a-z,A-Z,0-9]+\.[a-z]+"
dries.swinnen@pxl.be
```

Creating a regex that checks for a valid url format:
```bash
student@linux-ess:~$ cat regexlist.txt | grep -E "https?://.+\."
https://pxl.be
http://pxl.be
```
Note that this example does not check for valid domain names.

?> The questionmark (`?`) in a regex means the previous character is _optional_!

### Using content structure (cut,sort,uniq)
#### Using columns (cut)
Using the `cut` command we can split lines in a file into columns. To do this we have to define a delimiter (a set of one or more characters that defines the start of a new column) for example a `space` or `:` sign. Then we can select which columns the command should display:
```bash
student@linux-ess:~$ head -3 auth.log | cut -d":" -f1
Jun 09 11
Jun 09 11
Jun 09 12
```
As you can see in the example above we used the `:` sign as the delimiter. We then used the `-f` optoin to only display the first column. A full line in this log file looks like this:
```
Jun 09 11:11:11 linux-ess: Server listening on 0.0.0.0 port 22.
```
This means that the first column ends on the `:` sign in the time notation. The second column exists out of the minutes part of the time notation, the third column the seconds of the time notation and the hostname and so on. We can also tell the command to display multiple columns:
```bash
student@linux-ess:~$ head -3 auth.log | cut -d":" -f1,2,3
Jun 09 11:11:11 linux-ess
Jun 09 11:11:11 linux-ess
Jun 09 12:32:24 linux-ess
```

Another nice example of where we can use this is the `/etc/passwd` file where we can easily filter all the usernames and there homefolder locations:
```bash
student@linux-ess:~$ tail -3 /etc/passwd | cut -d":" -f1,6
pollinate:/var/cache/pollinate
dries:/home/dries
student:/home/student
```

#### Using sorting (sort & uniq)
```bash
student@linux-ess:~$ cat auth.log | cut -d ':' -f5 | cut -d' ' -f2 | sort | uniq

doeg
janedoe
johndoe
student
```

#### Using counts (wc)
```bash
student@linux-ess:~$ wc auth.log
  17  245 1731 auth.log
```

```bash
student@linux-ess:~$ wc -l auth.log # numer of lines
17 auth.log
student@linux-ess:~$ wc -w auth.log # number of words
245 auth.log
student@linux-ess:~$ wc -c auth.log # number of bytes
1731 auth.log
```

## Manipulating output
### Translate (tr)
The `tr` command allows us to _translate_ certain characters to other characters. I takes in 2 arguments:
* The character (or set of characters) that needs to be replaced
* The chracter (or set of characters) the previous set needs to be replaced by

We can see a simple examle below:
```bash
student@linux-ess:~$ head -3 auth.log | tr 'e' 'E'
Jun 09 11:11:11 linux-Ess: SErvEr listEning on 0.0.0.0 port 22.
Jun 09 11:11:11 linux-Ess: SErvEr listEning on :: port 22.
Jun 09 12:32:24 linux-Ess: AccEptEd publickEy for: johndoE from 85.245.107.42 port 54259 ssh2: RSA SHA256:K18kPGZrTiz7g>
```
all of the letters `e` in the output will be changed to the capital `E`. As said in the explanation above we can use ranges or sets of characters aswell:
```bash
student@linux-ess:~$ head -3 auth.log | tr 'a-z' 'A-Z'
JUN 09 11:11:11 LINUX-ESS: SERVER LISTENING ON 0.0.0.0 PORT 22.
JUN 09 11:11:11 LINUX-ESS: SERVER LISTENING ON :: PORT 22.
JUN 09 12:32:24 LINUX-ESS: ACCEPTED PUBLICKEY FOR: JOHNDOE FROM 85.245.107.42 PORT 54259 SSH2: RSA SHA256:K18KPGZRTIZ7G>
```
It's not just regular characters we can replace. We can use special characters such as newlines or tabs as follows:
```bash
student@linux-ess:~$ head -3 auth.log | tr '\n' ' '
Jun 09 11:11:11 linux-ess: Server listening on 0.0.0.0 port 22. Jun 09 11:11:11 linux-ess: Server listening on :: port 22. Jun 09 12:32:24 linux-ess: Accepted publickey for: johndoe from 85.245.107.42 port 54259 ssh2: RSA SHA256:K18kPGZrTiz
```
The example above changes all the _newlines_ to _spaces_.

Imagine we have some data that has multiple occurances of a specific character and we only want it to display one. We can use the `-s` option to delete any recurring characters:
```bash
student@linux-ess:~$ head -3 auth.log | tr -s '1'
Jun 09 1:1:1 linux-ess: Server listening on 0.0.0.0 port 22.
Jun 09 1:1:1 linux-ess: Server listening on :: port 22.
Jun 09 12:32:24 linux-ess: Accepted publickey for: johndoe from 85.245.107.42 port 54259 ssh2: RSA SHA256:K18kPGZrTiz7g>
```

lastly we have the option `-d` that will _delete_ any of the character(s) we define in the text:
```bash
student@linux-ess:~$ head -3 auth.log | tr -d ':'
Jun 09 111111 linux-ess Server listening on 0.0.0.0 port 22.
Jun 09 111111 linux-ess Server listening on  port 22.
Jun 09 123224 linux-ess Accepted publickey for johndoe from 85.245.107.42 port 54259 ssh2 RSA SHA256K18kPGZrTiz7g>
```

### Stream editor (sed)
`sed` is an advanced stream editor that can perform editing function using regular expressions. Remember the `rename` command? We can use the same syntax of regular expressions here:
```bash
student@linux-ess:~$ tail -4 auth.log | sed 's/Failed/Incorrect/'
Jun 22 21:11:12 linux-ess: Incorrect password for: doeg from 192.168.0.10 port 34598 ssh2
Jun 22 21:11:12 linux-ess: Incorrect password for: doeg from 192.168.0.10 port 87568 ssh2
Jun 22 21:11:12 linux-ess: Incorrect password for: doeg from 192.168.0.10 port 77898 ssh2
Jun 22 21:11:12 linux-ess: Accepted password for: doeg from 192.168.0.10 port 44293 ssh2
```
The example above wil change the string `Failed` to `Incorrect` for every line. Mind that this will only change the string once per line. This is something we need to be aware of as we can see in the example below:

```bash
student@linux-ess:~$ echo example this is an example | sed 's/example/test/'
test this is an example
```
Only the first occurence of `example` is changed to `test`. If we want the `sed` command to change every occurence in a line, we have to use the `g` (global) flag as seen below:
```bash
student@linux-ess:~$ echo example this is an example | sed 's/example/test/g'
test this is an test
```
?> There is also an `i` flag that will make the regex case insensitive!

Lastly we will look at the `d` flag which will remove any occurence of the string in a line:
```bash
student@linux-ess:~$ tail -8 auth.log | sed '/doeg/d'
Jun 19 22:43:23 linux-ess: Failed password for: johndoe from 85.245.107.42 port 22834 ssh2: RSA SHA256:eoKmezlE3iOp38Dj>Jun 22 08:04:00 linux-ess: Accepted password for: johndoe from 192.168.0.99 port 38299 ssh2
```

 ## Examples
 Below are some interesting examples that combine the commands described in this chapter that might help you further understand filters and their strength.

  #TODO
