# Advanced command structures

## shell expansion

example white space removal

### Single and double quotes

## File globbing
When using commands, we can get the shell to generate filenames dynamically. For example: we might want to find all the files starting with `temp` followed by whatever text or extention. The concept where we generate file names dynamically is called _file globbing_. There are a couple of special characters that we can use as seen in the example below:
```bash
student@linux-ess:~/globbing$ ls
File4  File5  FileABC  Filec  afilea  file1  file2  file3  filea  fileb  filebc
student@linux-ess:~/globbing$ ls file*
file1  file2  file3  filea  fileb  filebc
student@linux-ess:~/globbing$ ls *a
afilea  filea
student@linux-ess:~/globbing$ ls *a*
afilea  filea
student@linux-ess:~/globbing$ ls F*
File4  File5  FileABC  Filec
student@linux-ess:~/globbing$ ls F*ile*
File4  File5  FileABC  Filec
```
an asterix (`*`) in _file globbing_ means zero, one or more characters. This is often called a wildcard that we can use one or multiple times in a filename. Another option would be a question mark (`?`) which is interpreted as exactly _one character_ as een in the following example:
```bash
student@linux-ess:~/globbing$ ls
File4  File5  FileABC  Filec  afilea  file1  file2  file3  filea  fileb  filebc
student@linux-ess:~/globbing$ ls File?
File4  File5  Filec
student@linux-ess:~/globbing$ ls file??
filebc
student@linux-ess:~/globbing$ ls ?fi*
afilea
```

Lastly we can also use square brackets (`[ ]`) which usually contain one or more characters in between the brackets. The brackets define one character that matches one of the characters between the brackets:
```bash
student@linux-ess:~/globbing$ ls
File4 File5 FileABC Filec afilea file1 file2 file3 filea fileb filebc
student@linux-ess:~/globbing$ ls file[12]
file1  file2
student@linux-ess:~/globbing$ ls file[a]
filea
student@linux-ess:~/globbing$ ls file[1ac]
file1  filea  fileb
```
When using brackets we can also define ranges:
```bash
student@linux-ess:~/globbing$ ls
File4  File5  FileABC  Filec  afilea  file1  file2  file3  filea  fileb  filebc
student@linux-ess:~/globbing$ ls file[a-z]
filea  fileb
student@linux-ess:~/globbing$ ls File[A-Z]*
FileABC
student@linux-ess:~/globbing$ ls file[0-9]
file1  file2  file3
```
### Prevent file globbing
We can prevent file globbing by _escaping_ the special characters in our command. Escaping can be done by placing a `\` in front of the character. This tells the shell to interpret the next character as a regular symbol rather than the special operation:
```bash
student@linux-ess:~/globbing$ ls
 File4   File5   FileABC   Filec   afilea  'file*'   file1   file2   file3   filea   fileb   filebc
student@linux-ess:~/globbing$ ls file*
'file*'   file1   file2   file3   filea   fileb   filebc
student@linux-ess:~/globbing$ ls file\*
'file*'
```
## Aliases

## I/O redirection

## Control operators


