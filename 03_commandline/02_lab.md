# Lab <!-- {docsify-ignore} -->

## Finding useful commands

On the [downloads page of the Minetest website](https://www.minetest.net/downloads/) we see a link that points to a specific ubuntu url called `packages.ubuntu.com/...`. This means that you can install the `minetest` package using a CLI tool.

![CLI_LAB_Download_Minetest](../images/03/lab_minetest_download.PNG)

## Finding an installation tool

Linus needs to install this minetest on his server in some way. He needs to find a command that allows him to install packages.

Linus uses the `man` command to find a list of commands that have the keyword _package_ in their description:
```bash
man -k package                    or                    apropos package
```
The command will give the following output:
```
student@linux-ess:~$ man -k package
apt-extracttemplates (1) - Utility to extract debconf config and templates from Debian packages
apt-get (8)          - APT package handling utility -- command-line interface
apt-mark (8)         - show, set and unset various settings for a package
apt-sortpkgs (1)     - Utility to sort package index files
check-language-support (1) - returns the list of missing packages in order to provide a complete language environment
debconf-apt-progress (1) - install packages using debconf to display a progress bar
dh_bash-completion (1) - install bash completions for package
```
The `apt-get` command in this list looks promising. Linus decides to investigate the `apt-get` command. First of he does this by using the `whatis` command:
```bash
whatis apt-get
```
He wants to get more information about the usage of the command so he decides to view te manpage:
```bash
man wget
```
This command gives us the full _manual_ of the `apt-get` command:

```
APT-GET(8)                                               APT                                               APT-GET(8)

NAME
       apt-get - APT package handling utility -- command-line interface

SYNOPSIS
       apt-get [-asqdyfmubV] [-o=config_string] [-c=config_file] [-t=target_release] [-a=architecture] {update |
               upgrade | dselect-upgrade | dist-upgrade | install pkg [{=pkg_version_number | /target_release}]...  |
               remove pkg...  | purge pkg...  | source pkg [{=pkg_version_number | /target_release}]...  |
               build-dep pkg [{=pkg_version_number | /target_release}]...  |
               download pkg [{=pkg_version_number | /target_release}]...  | check | clean | autoclean | autoremove |
               {-v | --version} | {-h | --help}}

DESCRIPTION
       apt-get is the command-line tool for handling packages, and may be considered the user's "back-end" to other
       tools using the APT library. Several "front-end" interfaces exist, such as aptitude(8), synaptic(8) and
       wajig(1).

       Unless the -h, or --help option is given, one of the commands below must be present.

       update
           update is used to resynchronize the package index files from their sources. The indexes of available
           packages are fetched from the location(s) specified in /etc/apt/sources.list. For example, when using a
           Debian archive, this command retrieves and scans the Packages.gz files, so that information about new and
           updated packages is available. An update should always be performed before an upgrade or dist-upgrade.
           Please be aware that the overall progress meter will be incorrect as the size of the package files cannot
           be known in advance.

       upgrade
       ...
       install
           install is followed by one or more packages desired for installation or upgrading. Each package is a
           package name, not a fully qualified filename (for instance, in a Debian system, apt-utils would be the
           argument provided, not apt-utils_2.0.6_amd64.deb). All packages required by the package(s) specified for
           installation will also be retrieved and installed. The /etc/apt/sources.list file is used to locate the
           desired packages. If a hyphen is appended to the package name (with no intervening space), the identified
           package will be removed if it is installed. Similarly a plus sign can be used to designate a package to
           install. These latter features may be used to override decisions made by apt-get's conflict resolution
           system.

           A specific version of a package can be selected for installation by following the package name with an
           equals and the version of the package to select. This will cause that version to be located and selected
           for install. Alternatively a specific distribution can be selected by following the package name with a
           slash and the version of the distribution or the Archive name (stable, testing, unstable).

           Both of the version selection mechanisms can downgrade packages and must be used with care.

           This is also the target to use if you want to upgrade one or more already-installed packages without
           upgrading every package you have on your system. Unlike the "upgrade" target, which installs the newest
           version of all currently installed packages, "install" will install the newest version of only the
           package(s) specified. Simply provide the name of the package(s) you wish to upgrade, and if a newer
           version is available, it (and its dependencies, as described above) will be downloaded and installed.

           Finally, the apt_preferences(5) mechanism allows you to create an alternative installation policy for
           individual packages.
       ...
```
He can navigate the manpage using the arrow keys on the keyboard. After reading through the manpage he closes it by pressing the `q` key on his keyboard. Using the info in the manpage. We can see that the `apt-get` command has a sub command called `install`. Linus figures out he can use this to install minetest on his system.

## Installing Minetest
With the knowledge he just gathered he tries to install Minetest:

```bash
student@linux-ess:~$ apt-get install minetest
E: Could not open lock file /var/lib/dpkg/lock-frontend - open (13: Permission denied)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), are you root?
```

We see we get an error (`permission denied`). It is important that we learn to analyse error messages. As we can see the error also refers to the user `root`. In this chapter we've seen that some commands require _administrator rights_ to run. `apt-get` is a system command that impacts the entire system, so this command requires special rights. We can run this command as a super user by using the `sudo` command:

?> <i class="fa-solid fa-circle-info"></i> Use the `up arrow` to use the _history_ and use the `left arrow` or `home key` to go to the _beginning of the line_ to type sudo.

```bash
student@linux-ess:~$ sudo apt-get install minetest
[sudo] password for dries:
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
...
Setting up minetest (5.1.1+repack-1build1) ...
Processing triggers for mime-support (3.64ubuntu1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.2) ...
Processing triggers for man-db (2.9.1-1) ...
```

?> <i class="fa-solid fa-circle-info"></i> If you get an error running the command above, try running `sudo apt-get update` and run the `sudo apt-get install minetest` command again. We will learn about updating `apt` repositories in chapter 6.

The command above will prompt for your password and might prompt to ask you if you are sure you want to install a bunch of packages. 

The installation is succesfull (we think, we don't really get a success message or anything). Linus sees a whole bunch of output, but he has no clue where minetest is located or how he can even run the server files. In the next chapter we will explore how files & folders in Linux work.

Sometimes its beneficial if we can copy & paste text into our CLI environment. When using the CLI in the virtual machine we cannot do this. We could connect to the virtual machine using SSH. This is a protocol that allows remote connections to machines that we can't physically access. One of the benefits of using SSH is that we can also copy and paste text into our CLI.

## Setting up a SSH connection

The procedure via SSH would be als follows:

*First* we need to get the IP adres of the server. We type `ip a` and look for the IP address of our network interface (ens33)
```bash
ip a
```

![CLI_LAB_ip_a](../images/03/CLI_LAB_ip_a.png)
<br />

*Second* we need to open Powershell on the Desktop and make a ssh-connection to the server. We are now working on the server from our desktop. Cool, isn't it?
```bash
ssh student@<server-ip>
```

![CLI_LAB_Powershell_SSH](../images/03/CLI_LAB_Powershell_SSH.png)
<br />

As you can see we now get a prompt. This is a shell on our Ubuntu server running in VMWare. The idea might sound weird because we have the virtual machine with a CLI running on our laptop. But imagine a scenario where the virtual machine wouldn't be running on our laptop but instead would be hosted somewhere on Amazon web services in the cloud. We would use the `ssh user@server-ip` command on our device to connect to that VM.

You can choose to stay working on your desktop using the `ssh` command in Powershell or go back to your VM in the interface of VMware Workstation.
