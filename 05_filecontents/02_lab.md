# Lab <!-- {docsify-ignore} -->
In the previous lab Linus created a couple of folders and files. The issue is that these files are still empty. In this lab we will add content to some of the existing files and add some new files as well. 

We start of with the easiest way of entering text into a file. We can do this using a text editor such as `nano`.  Linus uses the `nano linuscraft/todo` command to give the todo file the following contents:
```
TODO LINUSCRAFT
===============
start server - unfinished
automate backups - unfinished
create a website - unfinished
create an account for Mark - unfinished
install security updates - unfinished
create directory sturcture - done
install server - done
design logo - done
```
?> <i class="fa-solid fa-circle-info"></i> Be mindfull of the spacings, capital letters & dashes. These are important in one of the following chapters!

We can save the file using the keyboard combination `ctrl + o`. It will prompt to confirm the path to the file(name). If you press enter the file contents will be saved. 

Make sure to check if the content is correctly saved by using the command `cat linuscraft/todo`. If we only want to check the last couple of lines we could also use the `tail linuscraft/todo` command.

<i class="fa-solid fa-pencil"></i> Wan't a challenge? Try using the editor `vi` or `vim` to insert the text. This is a special and popular text editor which has a command and insert mode. More information about this editor which you have to read first can be found [here](https://linuxfoundation.org/blog/classic-sysadmin-vim-101-a-beginners-guide-to-vim/).

The command above uses a relative path to the existing `todo` file.   
  
We can also use nano to create new files by specifying a filename that not yet exists:
```bash
student@linux-ess:~/linuscraft$ nano playerinfo/dries.txt
```

We give this file the following contents:
```
player aliases: dries, 3s, d r 1 3 s
age: 32
Notes:
- Has way to much free time, is always online
- Likes to grief other people's bases
```

The `contact` file only exists out of Linus his e-mail address. We can easily insert this using the `echo` command:
```bash
student@linux-ess:~/linuscraft$ echo linus@pxl.be > ./contact
student@linux-ess:~/linuscraft$ cat contact
linus@pxl.be
```

<i class="fa-solid fa-pencil"></i> What happens if we run the command `echo mark@pxl.be > ./contact` after running the command above? Try using two `echo` commands to add both Linus and Mark's contact details!

Next up Linus wants to quickly view the top 2 items on his todo list. We can do this by using the `head` command:
```bash
student@linux-ess:~/linuscraft$ head -2 todo
TODO LINUSCRAFT
===============
```
We notice that this is not the output we want as it only shows the title of the text file. We adjust the command as follows:
```bash
student@linux-ess:~/linuscraft$ head -4 todo
TODO LINUSCRAFT
===============
start server - unfinished
automate backups - unfinished
```
<i class="fa-solid fa-pencil"></i> What if we had a really long todo list that does not fit our CLI window. Try adding a couple more todo items to try this out. What command could you use to scroll through this list?

Lastly Linus wants to create a `playerlist` file comming from the contents of the `playerinfo` folder. We could create a listing of all the text files of all the players and save this to the `playerinfo` file rather than typing all the names manually. We can do this as follows:
```bash
student@linux-ess:~/linuscraft$ ls -l playerinfo/ > playerlist
student@linux-ess:~/linuscraft$ cat playerlist
total 4
-rw-r--r-- 1 dries dries 113 Sep  6 12:50 dries.txt
-rw-r--r-- 1 dries dries   0 Aug 25 09:04 linus.txt
```
As you can see in the output the file contents of playerlist contains alot of extra information that we kinda want to get rid off, but we will learn how to do so in one of the next chapters. For now this will suffice.
