# Assignment CH2
## Task 1 - Download Ubuntu Desktop
Linux also has a desktop version. Download [Ubuntu Desktop](https://ubuntu.com/download/desktop).

![DownloadUbuntuDesktop](../images/02/GetUbuntuDesktop_Download_Ubuntu.png)

## Task 2 - Install Ubuntu Desktop
Install [Ubuntu Desktop](https://ubuntu.com/download/desktop) in a new virtual machine and explore the interface.

### Create the new VM
To create a new virtual machine (VM) in VMWare you go to the menu `file`>`New virtual machine`. The wizard to create a new VM will appear.

![VMware File New Vm](../images/02/VMware_File_New_VM.png)

In the first screen we select the option `Typical`:

![VMware Install Typical](../images/02/VMware_Typical.png)

Next we choose to `install the operating system later`:

![VMware Install Operating System Later](../images/02/VMware_Operating_System_Later.png)

Next we choose the operating system `Linux`. In the version dropdown we select `Ubuntu 64 bit`. This is the Linux distribution that we will use during this course.

![VMware Ubuntu 64bit](../images/02/VMware_Ubuntu_64bit.png)

In the next screen we give the virtual machine a name. You can also specify a different folder to store the virtual machine on your computer.

![VMware Name The VM](../images/02/LAB_VMware_Name_The_VM.png)

In the next screen we configure the virtual harddisk size for the VM. We will create a disk that has 30GB of storage. Mind that the disk size will grow from 0GB till max 30GB while we are saving to the disk:

![VMware Disk Size](../images/02/LAB_VMware_Disk_Size.png)

We have to click on `Customize Hardware` to configure the virtual machine a little more:

![VMware Customize Hardware](../images/02/LAB_VMware_Customize_Hardware.png)

We still need to link the Ubuntu-server ISO file to the virtual CD-rom drive. We do this by selecting `New CD/DVD` and browsing to the downloaded `iso` file:

![VMware Select ISO](../images/02/LAB_VMware_Select_ISO.png)

Click on `Finish` and the virtual machine will be created.

![VMware Finish](../images/02/LAB_VMware_Finish.png)

You can now boot the VM by clicking the green arrow icon. This will boot the virtual machine and run the installation process.

![VMware Finish](../images/02/LAB_VMware_Start_VM.png)


### Installation Ubuntu Desktop

?> <i class="fa-solid fa-circle-info"></i> Does booting the VM result in the error `This host supports Intel VT-x, but Intel VT-x is diabled`? You will have to activate the VT-X option in the BIOS of your laptop. More information can be found in [this article](https://www.qtithow.com/2020/12/fix-error-this-host-supports-Intel-VT-x.html).

When booting the VM for the first time we need to press `enter` or wait 30 seconds:

![Ubuntu_Desktop_First_Grub](../images/02/LAB_Ubuntu_Desktop_First_Grub.png)

We have to wait a few seconds for the boot to finish:

![Ubuntu_Desktop_First_Boot_Screen](../images/02/LAB_Ubuntu_Desktop_First_Boot_Screen.png)

In the next few steps there will be an installation process that we need to go through. 

We make the choice to Install:

![Ubuntu_Desktop_Try_Or_Install](../images/02/LAB_Ubuntu_Desktop_Try_Or_Install.png)

We choose the correct keyboard layout. For `azerty` we select `Belgian`:

![Ubuntu_Desktop_Keyboard_AZERTY](../images/02/LAB_Ubuntu_Desktop_Keyboard_Belgian.png)

?> <i class="fa-solid fa-circle-info"></i> If you have a QWERTY keyboard you have to stick with `English (US)`

We go for the normal installation with some extra closed-source drivers and software:

![Ubuntu_Desktop_Normal_Install](../images/02/LAB_Ubuntu_Desktop_Normal_Install.png)

We choose to erase the disk and install Ubuntu Desktop on it:

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Erase_Disk.png)

We choose to apply the changes by writing the changes to disk:

![Ubuntu_Desktop_Write_Changes_To_Disk](../images/02/LAB_Ubuntu_Desktop_Write_Changes_To_Disk.png)

?> <i class="fa-solid fa-circle-info"></i> Mind that you erase the Virtual Disk of your VM. `The hard disk of your computer/laptop will not be erased!`
  
For the TimeZone we pinpoint Brussels on the map or write it in the textbox:

![Ubuntu_Desktop_TimeZone_Brussels](../images/02/LAB_Ubuntu_Desktop_TimeZone_Brussels.png)

We specify the username and computername:

![Ubuntu_Desktop_Username_and_Computername](../images/02/LAB_Ubuntu_Desktop_Username_and_Computername.png)

Now we have to wait untill the installation is finished:

![Ubuntu_Desktop_Installaton_Runs](../images/02/LAB_Ubuntu_Desktop_Installaton_Runs.png)

Once the installation is finished we have to click on `Restart Now` to reboot the VM:

![Ubuntu_Desktop_Reboot_After_Install](../images/02/LAB_Ubuntu_Desktop_Reboot_After_Install.png)

On the last screen just press `enter`. The computer will reboot and the installation will be finished:

![Ubuntu_Desktop_Enter_to_Restart](../images/02/LAB_Ubuntu_Desktop_Enter_to_Restart.png)

## Task 3 - Login for the first time
The very first time we login we have to go through some configuration screens:

?> <i class="fa-solid fa-circle-info"></i> If a window named `Software Updater` pops up we can click `Remind Me Later`

![Ubuntu_Desktop_First_Login_Click_Student](../images/02/LAB_Ubuntu_Desktop_First_Login_Click_Student.png)

![Ubuntu_Desktop_First_Login_Enter_Password](../images/02/LAB_Ubuntu_Desktop_First_Login_Enter_Password.png)

![Ubuntu_Desktop_First_Login_Online_Accounts](../images/02/LAB_Ubuntu_Desktop_First_Login_Online_Accounts.png)

![Ubuntu_Desktop_First_Login_Help_Improve](../images/02/LAB_Ubuntu_Desktop_First_Login_Help_Improve.png)

![Ubuntu_Desktop_First_Login_Privacy](../images/02/LAB_Ubuntu_Desktop_First_Login_Privacy.png)

![Ubuntu_Desktop_First_Login_Ready_To_Go](../images/02/LAB_Ubuntu_Desktop_First_Login_Ready_To_Go.png)


## Task 4 - Take a snapshot of the VM
Before doing anything else, it's good practice to have a savepoint in time. If, at a later time, our Ubuntu Desktop breaks, we can allways return to this savepoint in time.
Being able to roll back to this point will be a time saver, because otherwise we will need to install the Linux system again from scratch.

`Take a snapshot of the Ubuntu Desktop VM, named "Clean Install"` as follows:

_First shutdown the VM..._

![Ubuntu_Desktop_Snapshot_Poweroff](../images/02/LAB_Ubuntu_Desktop_Snapshot_Poweroff.png)

![Ubuntu_Desktop_Snapshot_Poweroff_Confirm](../images/02/LAB_Ubuntu_Desktop_Snapshot_Poweroff_Confirm.png)


_VM/Snapshot/Take Snapshot..._
 
![Ubuntu_Desktop_Snapshot_Take_Snapshot](../images/02/LAB_Ubuntu_Desktop_Snapshot_Take_Snapshot.png)

![Ubuntu_Desktop_Snapshot_Take_Snapshot_Name](../images/02/LAB_Ubuntu_Desktop_Snapshot_Take_Snapshot_Name.png)


?> <i class="fa-solid fa-circle-info"></i> At a later time you can always go back to this savepoint in time with:

_VM/Snapshot/Revert to Snapshot..._



## Task 5 - Get to know the Desktop Environment
In the Ubuntu desktop machine, try to execute the following subtasks:
- Try to add a user with your name.
- Create a new text file with the tool "Text Editor" (=gedit).
- Pin the Terminal -application to the Dock (=launcher).
- Configure the Thunderbird app to use your school email.
- Surf to the school website.

This is all we are going to do with the Desktop version. The focus of this course is towards the Server version. So it is safe to delete this virtual machine if you don't want to explore any further.
