# Assignment CH6

In this assignment we will use `apt` instead of `apt-get` and `apt-cache`which are older commands

## Task 1
Update the local APT cache. This will get the latest info from the repositories  
sudo apt update

## Task 2
Upgrade all installed packages to the latest available version  
sudo apt upgrade

## Task 3
Search for a package that has something to do with 'usage stats'. You will see `btop` as one of the results. Install the package and run the app  
apt search usage stats  
sudo apt install btop  
btop  

## Task 4
Search for a package that has something to do with colorful cat. You will see `lolcat` as one of the results. Install the package and run the following commands:  
cd  
cat .bash_history  
lolcat .bash_history  
  
apt search colorful cat  
sudo apt install lolcat  
cat .bash_history  
lolcat .bash_history  

## Task 5
Install the package 'neofetch' and run the app  
sudo apt install neofetch

## Task 6
Search with apt for "the matrix" and install the package which resembles the display of the matrix movie. Run the app  
apt search "the matrix"  
sudo apt install cmatrix  
cmatrix  

## Task 7
Remove the package btop from the system. You shouldn't be able to run it anymore  
sudo apt remove btop  

## Task 8
List the packages that are installed with apt. In the list you will see one entry for `caca-utils`. Search in the manpage of 'apt' how you can see some info of this packages. You will see that this package holds several utilities. Try the last two. Tip: You can push 'enter' to try and see different things. Use `ctrl+c` to quit a utility.  
apt list --installed  
apt show caca-utils  
cacafire  
cacademo  

## Task 9
Search for a snap package via the description "resource monitor"    
snap search resource monitor  

## Task 10
Read the information about the snap `btop`  
snap info btop  

## Task 11
Install the snap `btop`  
sudo snap install btop  

## Task 12
Run btop    
btop

## Task 13
Show a list op installed snaps  
snap list 

## Task 14
Remove the snap btop  
sudo snap remove btop

## Task 15
Show a list op installed snaps  
snap list  

## Task 16
Show the history of changes in snap
snap changes 

## Task 17
Check if the snap 'asciiquarium' exists. Read some info about the snap, install it and run it  
snap search asciiquarium  
snap info asciiquarium  
sudo snap install asciiquarium  
asciiquarium  
ctrl+c  

## Task 18
Try to install the minetest client on your Ubuntu Desktop and connect with the server to play the game. After installation you will find mimetest between your applicataions in the GUI.  Make sure that your minetest server is runnen. If not, use ctrl+r and search for mimetest untill you see the following command: minetest --server --world ~/linuscraft/serverfiles/myworld --logfile ~/linuscraft/serverfiles/logfile.txt    

sudo apt install minetest


