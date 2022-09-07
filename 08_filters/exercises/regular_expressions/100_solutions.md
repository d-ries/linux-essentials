# Solutions on Regular Expressoins

?> <i class="fa-solid fa-circle-info"></i> http://www.regular-expressions.info/

## Task 1
Create the file regtest.txt with the following content:

```
apple
banana
apricot
peer
peach
strawberry
mango
grape
orange
5isanumber
123
123abc
abc123
35abcd35
5five5
55fivefive55
555fivefivefive555
77sevenseven77
@d
@tsign@@
atsiiiiiiiiiiiign
```

<br/>![](images/2022-08-15-16-03-27.png)
<br/>![](images/2022-08-15-16-03-32.png)

## Task 2
Use regular expressions to filter the lines that:

1.	Contain the letter a
<br/>![](images/2022-08-15-16-03-54.png)

2.	Contain the letter a or s
<br/>![](images/2022-08-15-16-05-07.png)
<br/>![](images/2022-08-15-16-05-11.png)
<br/>![](images/2022-08-15-16-05-16.png)

3.	Contain the letter a and s
<br/>![](images/2022-08-15-16-05-29.png)

4.	Contain a @
<br/>![](images/2022-08-15-16-05-39.png)

5.	Start with the letter p
<br/>![](images/2022-08-15-16-05-51.png)

6.	End with the letter t 
<br/>![](images/2022-08-15-16-06-01.png)

7.	Start with a number 
<br/>![](images/2022-08-15-16-06-16.png)

8.	Start with a number and end with a letter 
<br/>![](images/2022-08-15-16-06-27.png)

9.	Contains 2 or more consecutive letters a

<br/>![](images/2022-08-15-16-06-37.png)

?> <i class="fa-solid fa-circle-info"></i> Without the + is also possible here:

<br/>![](images/2022-08-15-16-07-00.png)


10.	Only contains numbers
<br/>![](images/2022-08-15-16-07-14.png)

11.	Only contains letters
<br/>![](images/2022-08-15-16-07-23.png)

12.	Contains one or more numbers, followed by one or more letters
<br/>![](images/2022-08-15-16-07-34.png)

13.	Contains one or more numbers, followed by one or more letters and ending with a number. 
<br/>![](images/2022-08-15-16-07-43.png)


## Task 3
Use sed to: 

1.	To create a file regtest_5.txt from the file regtest.txt where all numbers 5 are replaced with "five"
<br/>![](images/2022-08-15-16-07-59.png)

2.	To create a file regtest_7.txt from the file regtest.txt where the text ‘seven’ is replaced by the number 7
<br/>![](images/2022-08-15-16-08-09.png)

3.	To create a file regtest_at.txt from the file regtest.txt where all the @ symbols are replaced by _at_
<br/>![](images/2022-08-15-16-08-18.png)

?> <i class="fa-solid fa-circle-info"></i>  !!! For extended regex you need to use sed -r ‘s/extendedregex/tochange/g’. The -r ensures that sed uses extended regexes 


## Task 4
Count the amount of time 5 can be found in regtest.txt
search the manpage of grep for a solution

<br/>![](images/2022-08-15-16-08-48.png)
<br/>![](images/2022-08-15-16-08-52.png)

## Task 5
Search in the bash manpage to the header name "REDIRECTION" (The text starts at the left-side line) . Is this search-function case sensitive? 
<br/>![](images/2022-08-15-16-09-03.png)

?> <i class="fa-solid fa-circle-info"></i>  If you only use lowercase, the search function is not case sensitive. The moment you type an uppercase letter, it becomes case sensitive. 

## Task 6
Try with the same regular expression to only show hidden files from your home folder. 
<br/>![](images/2022-08-15-16-09-29.png)

