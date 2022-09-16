# Assignments CH11
?> _Note that these assignments are considered extra's that will not be evaluated on any exam._

## Task 1
List all processes running on your system, showing a full set of columns. Pipe that output to the less command so you can page through the list of processes.

## Task 2
List all processes running on the system, and sort those processes by the name of the user running each process. Pipe that output to the less command so you can page through the list of processes.

## Task 3
List all processes running on the system, and display the following columns of information: process ID, user name, nice-value and the command.

## Task 4
Run the top command to view processes running on your system. Go back and forth between sorting by CPU usage and memory consumption.

## Task 5
Start the gedit process from your desktop. Make sure you run it as the user you are logged in as. Use the System Monitor window to kill that process.

## Task 6
Run the gedit process again. This time, using the kill command, send a signal to the gedit process that causes it to pause (stop). Try typing some text into the gedit window and make sure that no text appears yet.

## Task 7
Use the killall command to tell the gedit command you paused in the previous exercise to continue working. Make sure the text you type in after gedit was paused now appears on the window.

## Task 8
Run the gnome-calculator command about 20 times in the background. When you have had enough fun, kill all calculator-window processes in one command using killall.

## Task 9
As a regular user, run the gedit command so it starts with a nice value of 5.

## Task 10
Using the renice command, change the nice value of the gedit command you just started to 7. Use the ps command to verify that the current nice value for the gedit command is now set to 7. 