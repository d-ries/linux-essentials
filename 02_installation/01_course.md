# Installation

## Virtualisation
To install servers that offer services (such as a minecraft server!) you will need a server with a public IP address. Usually you would go to a cloud provider where you can rent a server for a fixed fee / month. For this course we will simulate this process by using a virtual machine.

Virtualisation is a concept where you can run a computer system with an operating system virtually on another system. This makes it possible to have multiple _guest operating systems_ with their own virtual hardware on one _host system_.

![Virtualization](../images/02/Virtualization.png)

For this course we want to use and install the operating system [Ubuntu server](https://ubuntu.com/download/server) in a virtual environment. You could use any Linux distribution you want. For this course we will use a debian based distro.

?> :fa-solid fa-list-check: _Download the `.iso` file for Ubuntu server using [this link](https://ubuntu.com/download/server). A `.iso` file is an exact copy of a CD/DVD. You will use this later to install the operating system in your virtual machine._

![Download Ubuntu Server](../images/02/GetUbuntuServer_Download_Ubuntu.png)

## Virtualisation software
To use virtualisation there are several options. The most common virtualisation software is:
- VMware workstation
- Virtualbox
- Hyper-V

In this course we will use and support VMware but the other software packages are similar. Students of PXL University College will get a free educational licence to use VMware Workstation pro through [BrightSpace](https://itacademy.brightspace.com/).

## Create a new VM
To create a new virtual machine (VM) in VMWare you go to the menu `file`>`New virtual machine`. The wizard to create a new VM will appear.

![VMware File New Vm](../images/02/VMware_File_New_VM.png)

In the first screen we select the option `Typical`:

![VMware Install Typical](../images/02/VMware_Typical.png)

Next we choose to `install the operating system later`:

![VMware Install Operating System Later](../images/02/VMware_Operating_System_Later.png)

Next we choose the operating system `Linux`. In the version dropdown we select `Ubuntu 64 bit`. This is the Linux distribution that we will use during this course.

![VMware Ubuntu 64bit](../images/02/VMware_Ubuntu_64bit.png)

In the next screen we give the virtual machine a name. You can also specify a different folder to store the virtual machine on your computer.

![VMware Name The VM](../images/02/VMware_Name_The_VM.png)

In the next screen we configure the virtual harddisk size for the VM. We will create a disk that has 20GB storage. We can expand this later if needed:

![VMware Disk Size](../images/02/VMware_Disk_Size.png)

We have to click on `Customize Hardware` to configure the virtual machine a little more:

![VMware Customize Hardware](../images/02/VMware_Customize_Hardware.png)

We still need to link the Ubuntu-server ISO file to the virtual CD-rom drive. We do this by selecting `New CD/DVD` and browsing to the downloaded `iso` file:

![VMware Select ISO](../images/02/VMware_Select_ISO.png)

Click on `Finish` and the virtual machine will be created.

![VMware Finish](../images/02/VMware_Finish.png)

You can now boot the VM by clicking the green arrow icon. This will boot the virtual machine and run the installation process.

![VMware Finish](../images/02/VMware_Start_VM.png)

## Installation Ubuntu server
As described earlier we will use the distro Ubuntu. After creating and booting the virtual machine there will be an installation process that we need to run through. You will notice that there is no mouse pointer available. We will use the keypoint arrow keys & enter key to navigate through the steps.

?> <i class="fa-solid fa-circle-info"></i> Does booting the VM result in the error `This host supports Intel VT-x, but Intel VT-x is diabled`? You will have to activate the VT-X option in the BIOS of your laptop. More information can be found in [this article](https://www.qtithow.com/2020/12/fix-error-this-host-supports-Intel-VT-x.html).


We make the choice to Try or Install:

![Ubuntu_Server_Try_Or_Install](../images/02/Ubuntu_Server_Try_Or_Install.png)

We start the installation process by selecting the laguage. We choose English:

![Ubuntu_Server_Language](../images/02/Ubuntu_Server_Language.png)

We skip the installer update:

![Ubuntu_Server_No_Installer_Update](../images/02/Ubuntu_Server_No_Installer_Update.png)

Choose the correct keyboard layout. For `azerty` select `Belgian`:

![Ubuntu_Server_Keyboard_Belgian](../images/02/Ubuntu_Server_Keyboard_Belgian.png)

In the next 7 steps we dont make any changes. We just press `Done` or `Continue` :

![Ubuntu_Server_Base_For_The_Installation](../images/02/Ubuntu_Server_Base_For_The_Installation.png)

![Ubuntu_Server_Network_Connections](../images/02/Ubuntu_Server_Network_Connections.png)

![Ubuntu_Server_Proxy_Settings](../images/02/Ubuntu_Server_Proxy_Settings.png)

![Ubuntu_Server_Archive_Mirror](../images/02/Ubuntu_Server_Archive_Mirror.png)

![Ubuntu_Server_Storage_Config](../images/02/Ubuntu_Server_Storage_Config.png)

![Ubuntu_Server_Storage_Config_Overview](../images/02/Ubuntu_Server_Storage_Config_Overview.png)

![Ubuntu_Server_Storage_Config_Overview_Confirmation](../images/02/Ubuntu_Server_Storage_Config_Overview_Confirmation.png)

Next up we create a user account that we use to login to the operating system. We use following credentials:
```
username: student
server name: linux-ess
password: pxl
```

![Ubuntu_Server_Storage_Username_student_Servername_linux-ess](../images/02/Ubuntu_Server_Storage_Username_student_Servername_linux-ess.png)

For Extra Packages we will only opt to install `SSH server`:

![Ubuntu_Server_Storage_SSH](../images/02/Ubuntu_Server_Storage_SSH_WEL.png)

![Ubuntu_Server_Storage_Featured_Server_Snaps](../images/02/Ubuntu_Server_Storage_Featured_Server_Snaps.png)

The operating system will be installed and configured. After a while the `Reboot now` option will appear. This indicates that the installation is complete:
![Ubuntu_Server_Reboot](../images/02/Ubuntu_Server_Reboot.png)

During the Reboot process you will have to press the `enter` key on your keyboard :

![Ubuntu_Server_Press_Enter_To_Reboot](../images/02/Ubuntu_Server_Press_Enter_To_Reboot.png)

Once the server is rebooted, you will have to press the `enter` key again to see the login prompt.

![Ubuntu_Server_Press_Enter_To_See_Login](../images/02/Ubuntu_Server_Press_Enter_To_See_Login.png)

  
  
All of these steps can also be viewed in the video below:
<iframe width="560" height="315" src="https://www.youtube.com/embed/u8WLsyMuSgw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
