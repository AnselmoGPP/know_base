# Linux


## Table of contents

+ [Introduction](#introduction)
+ [Installation](#installation)
+ [Command line](#command-line)
  + [Basic commands](#basic-commands)
  + [Control flow](#control-flow)
  + [File descriptor](#file-descriptor)
  + [Permissions](#permissions)
  + [Directories](#directories)


## Introduction

Computers use a processor to store and manipulate information inside them in binary code. 

**Processor**: It can be programmed to do different operations. It manages information encoded in binary code: zero and one values asigned to variables allocated in memory addresses over which the processor operates. The processor's activity is just to move these values from some addresses to others and to interchange their values (low level).

**Operative system (OS)**: Program that allows the user communicate with the processor. It determines how the computer works, what we can do with it, and how we do it. We expect from a computer that it executes efficiently the tasks we assigned to it.

### Unix

#### Description

Unix is a computer Operating System developed around 1969 at “AT&T Bell Labs” by Ken Thompson and Dennis Ritchie (who also designed the C programming language).

- **Multiuser system:** Several people can use a Unix computer at the same time.
- **Multitasking environment:** A user can run multiple programs at the same time.
- There are various Unix variants available in the market (Linux, Solaris Unix, AIX, HP Unix, BSD, …).

It’s made of 3 parts:

- **Kernel** or **Operative system**: The computer programs that allocate the system resources and coordinate all the details of the computer’s internals. It’s a set of programs that act as a link between the computer and the user.
- **Shell**: Program users use to communicate with the kernel (interface user-kernel). It is a command line interpreter (CLI) (it translates commands entered by the user and converts them into a language understood by the kernel).
- **Programs**

#### Architecture

All versions of Unix have the following 4 basics:

- **Kernel**: It interacts with the hardware and most of the tasks (memory management, task scheduling, file management, …).
- **Shell**: The utility that processes your requests. It interprets the command you enter (cp, mv, cat, grep, id, wc, nroff…) and calls the program that you want. The shell uses standard syntax for all commands. C Shell, Bourne Shell and Korn Shell are the most famous shells which are available with most of the Unix variants.
- **Commands and Utilities**: There are over 250 standard commands plus numerous others provided through 3rd party software. All the commands come along with various options.
- **Files and Directories**: All the data of Unix is organized into files. All files are then organized into directories. These directories are further organized into a tree-like structure called the **filesystem**.

Structure: hardware > kernel > shell commands > application layer

- Hardware
  - Kernel
    - cc
      - cpp   comp   as   id
    - Other application programs
      - nroff   sh   who   a.out   date   wc   grep   ed   vi

Everything in UNIX is either a **file** or a **process**:

- **Process**: An executing program identified by a unique PID (Process IDentifier)
- **File**: Collection of data. Created by users using text editors, compilers, etc.

#### Boot process

(Extracted from [Arch boot process](https://wiki.archlinux.org/index.php/Arch_boot_process))

- **POST** (Power On Self Test): Moderboard first process
- **UEFI** (formerly, BIOS)  >  bootloader (grub, windows bootloader…)
- **Kernel** of Linux (version x) (Kernel space)
- **init** (systemd: system daemon, process id = 0) (user space)
- **login** processes (getty, tty) (6 or 7) (ctrl + alt + F1-F7)
  - F1-f6: Shell bash > .profile > .bashrc > startx
  - F7: lightdm (display manager) (sudo systemctl restart/disable… lightdm): Executes like the others, but using X11 display service protocol (implementation: Xorg), which call start x with more options for GUI

#### Basic commands

When you turn on the system, you have to log in by entering your user name and password. Then, you will be provided with a command prompt (or $ prompt ) where you type all your commands.

- See calendar

```
$ cal
```

- Change password

```
$ passwd
```

- List out all the files or directories available in a directory. Entries starting with **d…**. represent directories.

```
ls -l
total 5832
drwxrwxr-x  2 amrood amrood      4096 Dec 25 09:59 uml
-rw-rw-r--  1 amrood amrood      5341 Dec 25 08:38 uml.jpg
drwxr-xr-x  2 amrood amrood      4096 Feb 15  2006 univ
```

- Who are you?

```
$ whoami
```
- Who is logged in to the computer at the same time. Three commands available based on how much you wish to know about the other users.

```
$ users
$ who
$ w
```

- Log out from the system

```
$ logout
```

- Shutdown: Different ways:
  - `$ shutdown`: Shutdown the system.
  - `$ poweroff`: Shut down the system by powering off:
  - `$ init 0`: Power off the system using predefined scripts to synchronize and clean up the system prior to shutting down:
  - `$ halt`: Bring the system down immediately:
  - `$ init 6`: Reboot the system by shutting it down completely and then restarting it:
  - `$ reboot`: Reboot the system:

Usually, you need to be the super-user or **root** (the most privileged account on a Unix system) to shut down the system.

#### Filesystem Hierarchy Standard (FHS)

It defines the structure of file systems on Linux and other UNIX-like operating systems. However, Linux file systems also contain some directories not defined by the standard.

- **`/` – root directory**

Everything on your Linux system is located under the `/` directory. Linux doesn’t have drive letters. Another partition appear in another folder under `/`.

- **`/bin` – essential user binaries**

Contains essential user binaries (programs) that must be present when the system is mounted in single-user mode (bash shell, …). Applications such as Firefox are stored in **/usr/bin**, while important system programs and utilities such as the bash shell are located in /bin. The **/usr** directory may be stored on another partition – placing these files in the /bin directory ensures the system will have these important utilities even if no other file systems are mounted.

- **`/sbin` – system administration binaries**

Similar to /bin. Contains essential system administration binaries, generally intended to be run by the root user for system administration.

- **`/boot` – static boot files**

Contains the files needed to boot the system (GRUB boot loader’s files, your Linux kernels…). The boot loader’s configuration files aren’t located here, though – they’re in /etc with the other configuration files.

- **`/cdrom` – Historical Mount Point for CD-ROMs**

It isn’t part of the FHS standard. It’s a temporary location for CD-ROMs inserted in the system. However, the standard location for temporary media is inside the **/media** directory.

- **`/dev` – Device files**

Linux exposes devices as files, and the /dev directory contains a number of special files that represent devices. These are not actual files as we know them, but they appear as files – for example, /dev/sda represents the first SATA drive in the system. If you wanted to partition it, you could start a partition editor and tell it to edit /dev/sda.

This directory also contains pseudo-devices, which are virtual devices that don’t actually correspond to hardware. For example, /dev/random produces random numbers. /dev/null is a special device that produces no output and automatically discards all input – when you pipe the output of a command to /dev/null, you discard it.

More info: [Linux directory structure explained](https://www.howtogeek.com/117435/htg-explains-the-linux-directory-structure-explained/)

#### Links

- [Learn Unix](https://www.tutorialspoint.com/unix/index.htm)
- [Unix tutorial](http://www.ee.surrey.ac.uk/Teaching/Unix/unix0.html)

### Linux

#### Linux operative system

The MIT student Richard Stallman started in 1984 the project **GNU** ("GNU is Not Unix") that aimed to create a completely free OS built around the conceptual framework of UNIX. He organized the **FSF** (Free Software Foundation) to sell open-source software to help feed the programmers working on GNU. The **GPL** (GNU General Public License) uses the copyright law to protect the freedom of the software users (they can use the software in any way they choose). Linus Torvalds began writing **Linux** in 1991, and soon many programmers began to collaborate on his project. Linux just had a core (kernel) and some Unix tools from the GNU project. Today, there are multiple Linux distributions.

**Linux**: Unix-type OS. It's the most efficient, secure and economical OS. Superior to any other:

- It makes efficient use of available hardware resources. It is free (including updates).
- It includes free packages for any task. The Linux operating system is based on a hierarchy of permissions and users.
- To use the computer, you must be registered as a user: with a login, password and working directory (the only place with write permission). To modify anything that affects the configuration, you need to log in as an administrator (root).
- The computer records all connections made (successful and unsuccessful).

**Linux is**:

- **Multiuser**: More than one can be logged in to a single computer at the same time.
- **Multiprocesser**: Several programs can run at once (pre-emptive multitasking).
- **Multiplatform**: Currently runs in more than 24 platforms (hardware types).
- **Interoperable**: It can interact with most network protocols (languages) and OSs.
- **Scalable**: It can run in a platform of any size (tiny electronic photo frame, huge industrial-server system, etc.).
- **Portable**: Linux is written in C (language for writing OSs-level software) and can be readily ported (translated) to run on new computer hardware.
- **Flexible**: You can configure Linux OS as any computing appliance you want (network host, router, graphical workstation, office PC, Web server, cluster, home entertainment…).
- **Stable**: The Linux kernel is highly mature.
- **Efficient**: It’s modular design enables you to include only the components you want.
- **Free**: It uses the GNU General Public Licence (GPL), that ensures that Linux will always be open to anyone. Nobody can own Linux, although they can have their own copyrights and trademarks on their various brands of it (Red Hat, Novell…).

**Distribution**:

A distribution (distro) is a complete Linux system package. It contains the Linux kernel, the GNU project’s tools, and some open-source software to provide diverse functionaly to the system. Most distributions are customized for specific user groups (business, multimedia fans, software devs, home users…). Linux distributions are often divided in:

- **Core Linux distributions**: Contains the Linux and GNU operating systems, one or more graphical desktop environments, and just about every Linux application that is available, ready to install and run. Some popular distributions:

  - Slackware
  - RedHat
  - Fedora (heir of RedHat)
  - Gentoo
  - Mandriva
  - openSuSe
  - Debian

- **LiveCD test distributions**
- **Specialized distributions**

A single Linux distribution often appears in different versions (example: Fedora core [full], Fedora LiveCD [subset]). Many specialized Linux distributions (like Ubuntu) are based on the Debian core (Ubuntu uses the same installation files as Debian, but packages a small fraction of a full Debian system).

Some distributions are free (Debian, Ubuntu, Fedora…), and others are commercial (RedHad, Suse, Novell…).

Popular distributions for __pentesting__ are **Parrot** and **Kali**.

#### Structure and operation

**Server X**: Application that provides the other graphic applications a window environment and desktop environment.

**Desktop environment**: Application that provides an integrated view of all applications so that they look similar. There are many different ones (Gnome, KDE, Xfce…). We can install more than one environment and try them out (when logging in, we can choose which graphical environment to use). If we have several installed, we can use the applications from the other environments from any of them.

**Task distribution**: Linux philosophy. Common instructions between applications form function __libraries__. Data form shared __data files__. Applications that perform specialised tasks useful to other applications are installed as __services__ (X server, web server…). Each task is performed by a single actor (application, service, library, data file). This modular design allows parts to be improved without having to change the whole.

**Directories and file systems**: Everything is a file in Linux (directories, files, devices/nodes…). All files are organized in a tree, where the highest level one is the root directory (`/`). Below root there're various directories common to most GNU/Linux distributions:

- **User:**
  - `/home`: Personal directories for the different users.
  - `/root`: Personal directory of the root user (superuser).
  - `/usr` (user): Applications and files accessible for most users.
    - `/usr/bin` (binaries): Applications for users.
    - `/usr/lib32`, `/usr/lib64`: Functions libraries for the applications for the users.
    - `/usr/share`: Shared data from the applications.
  - `/opt` (optional): Place for installing optional applications (from 3rd parties).
- **System:**
  - `/usr` (user):
    - `/usr/bin`: OS binaries (applications).
    - `/usr/sbin`: System binaries.
    - `/usr/lib`: OS functions libraries (others: `lib32`, `lib64`, `libx32`).
  - `/etc`: System (and applications) configurations, boot scripts, etc.
  - `/boot`: Files needed for bootting (including configuration files) and cores.
  - `/dev` (device): Device files.
  - `/media`: Partitions automatically mounted (loaded) on the hard drive and removable media (CDs, digital cameras…).
  - `/mnt` (mounted): Files systems mounted manually on the hard drive.
  - `/proc` (process): Special dynamic directory that keeps information about the system state, including processes currently in progress.
  - `/srv` (server): It can contain files that are served to other systems.
  - `/sys` (system): System files.
  - `/tmp` (temporary): Temporary files.
  - `/var` (variable): Variable files (registries files, databases…).
  - `/cdrom`
  - `/run`
  - `/snap`
- **Others** (not seen):
  - `/initrd`: Used when a custom `initrd` boot process is created.
  - `/lost+found`: "Lost+found" system for files under root directory (`/`).

#### Packages installation/uninstallation

The most used **package management systems** in Linux are:

- **apt** (Debian, Ubuntu, and related)
- **yum** (Fedora and related)

These tools use **repositories** (packages storages), and let you get the latest free applications versions and keep the system updated.

**Package**: File containing the files that have to be copied to the disk and information about what other packages need to be installed for working correctly. They usually have extensions like `.deb` (Debian, Ubuntu, and similar) or `.rpm` (Fedora and RedHat heirs).

**Repositorios**: Internet sites (HTTP or FTP servers) containing updated packages available for a version of a distribution. The computer keeps a list of the packages it contains and their dependencies information. Useful commands are:

- `apt-get update` or `yum update`: Update the list. It's recommended to do it before installing new packages to guarantee that downloaded files will satisfy the dependencies (new properties in an application may require a new library). 
- `apt-cache search gnuplot` or `yum search gnuplot`: Look for a package using his name or related words. A package's name contains all information for guaranteeing that is is adequate for our machines (application/library's name and version).
- `apt-get install gnuplot` or `yum install gnuplot`: Install a package. We will be informed of its dependencies, that they will be installed, recommendations about other packages (like `gnuplot-doc), etc. After this, the package is installed.
- `apt-get remove plotdrop` or `yum remove plotdrop`: Uninstall a package. The package manager won't remove anything that can affect other applications.

#### Links

- [Bash programming introduction](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html)
- [Arch Linux](https://wiki.archlinux.org/index.php/Arch_boot_process)
- [Unix and Linux commands help](https://www.computerhope.com/unix.htm)


## Installation

Linux can be installed in different ways:

- Main OS is Linux
- Dual boot: Linux & Windows
- Virtual machine (VMWare, etc.)
- WSL (Linux installed directly in Windows)

When you mount an ISO image as a virtual disk, this happens at the OS level. Not at the hardware level. When your running operating system stops, the virtual device goes away. So **it's not possible to boot a physical machine from a virtual drive**.

Whether or not you need to create physical installation media depends on how you want to install Ubuntu:

- If you want to **install it separately from Windows** (either alongside it or replacing it) then you need to create real physical installation media. You can burn the ISO image to a DVD (or to a CD, if you’re installing Ubuntu 12.04 or earlier). Or you can write it to a USB flash drive.
- If you want to **install it inside Windows** (i.e. contained within the pre-existing Windows partition and booted using the Windows boot loader), then you do not need to create physical installation media.

### WSL (Windows Subsystem for Linux)

WSL is a Linux OS (only command line) in your Windows OS ([installation](https://learn.microsoft.com/es-es/windows/wsl/install)). Through the folder `/mnt` you have access to Windows. The programs execute directly on the machine hardware, not in a virtual machine. It enables direct calls between Linux and Windows systems (through the `/mnt` folder), removing the need for SSL transport.

- WSL 1: Interface that simulates a Linux kernel.
- WSL 2 (default): It has a real Linux kernel.

### Installing Linux from USB flash drive

**Get the needed material:**

- Ubuntu Desktop 18.04 LTS ([link](https://www.ubuntu.com/download/desktop))
- Rufus (free open source USB stick writing tool) ([link](https://rufus.ie/es_ES.html))
- 4 Gb or larger stick/flash drive

**Create a bootable USB stick/flash drive:**

- Run Rufus and complete the fields, selecting your Ubuntu ISO file and your device.

![Cache types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/rufus.png)

- Rufus may need to automatically download additional files. Let it do it.
- Rufus asks whether write an ISO or DD. Select ISO.
- Remember: All data stored in the device will be deleted.

**Install Ubuntu from the USB stick/flash drive:**

- Go to the UEFI menu > firmware options. Once there, activate the options for making the computer boot from the USB device. Make sure Rufus created a correct bootable USB device or computer may not detect a bootable USB.
- Restart the PC and installation will begin.

**Links:**

- [Install Ubuntu desktop](https://tutorials.ubuntu.com/tutorial/tutorial-install-ubuntu-desktop?_ga=2.79656276.1750103980.1542924580-927265707.1542924580#0)
- [Create a bootable USB stick on Windows](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-windows#0)
- [Rufus](https://rufus.ie/es_ES.html)
- [Make a full portable installation on a USB HDD](https://www.dionysopoulos.me/portable-ubuntu-on-usb-hdd/)

### Installing Linux (Ubuntu) in a Virtual machine (VMware WP)

**Download the needed software:**

- Ubuntu Desktop 18.04 LTS ([link](https://www.ubuntu.com/download/desktop))
- VMware Workstation Player 15 ([link](https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html))

**Create a virtual machine with Ubuntu inside:**

- Install the virtual machine (VMware)
- Run it and select “Create a new virtual machine”
- Select “Installer disc image file (iso)” and select your Ubuntu iso file
- Select a few installation options

![Cache types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/vmw.png)

- Restart your system

### Errors you may encounter

#### USB errors

**Ubuntu is not detecting the Windows OS (dual boot) ([link](https://www.techsupportpk.com/2020/04/how-to-fix-ubuntu-not-detecting-windows.html)):**

- Right click on the **C:\volume** > Properties > Tools > Check (this scans and fixes errors automatically)
- Windows PowerShell (admin) > `chkdsk C: /F` (this scans and fixes errors on the next reboot)
- Reboot your system manually and let the `chkdsk` command complete its process
- `shutdown` Windows from the `start` menu
- Boot with Ubuntu installation media and see if it detects Windows
  
#### Virtual machine errors

**Error: Intel VT-x is disabled ([link](https://www.howtogeek.com/213795/how-to-enable-intel-vt-x-in-your-computers-bios-or-uefi-firmware/)):**
  
![Cache types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/ubuntu_vmw.png)

Modern CPUs include hardware virtualization features that help accelerate virtual machines. Those features aren’t always enabled by default. In order to work , these virtual machine apps need hardware acceleration features built into modern CPUs. For **Intel CPUs**, this means **Intel VT-x** hardware acceleration. For **AMD CPUs**, it means **AMD-V** hardware acceleration. Reasons why this error message may appear:

- The __hardware acceleration feature may be disabled__. On systems with an Intel CPU, the Intel VT-x feature can be disabled via a [BIOS or UEFI](https://www.howtogeek.com/56958/htg-explains-how-uefi-will-replace-the-bios/) firmware setting. In fact, it’s often disabled by default on new computers. On systems with an AMD CPU, this won’t be a problem. The AMD-V feature is always enabled, so there’s no BIOS or UEFI setting to change.
- __Microsoft’s Hyper-V is installed__. It’s greedy and takes over those hardware acceleration features, so other virtualization apps won’t be able to access them.

Solutions:

- __Turn Intel VT-x on in your BIOS or UEFI firmware__: Old PCs use BIOS, modern PCs use UEFI.
  - BIOS: Access to it pressing the appropriate button when PC is first booting.
  - UEFI: Restart the computer while pressing shift. Usual route: Solve problems > Advanced options > UEFI firmware configuration > Restart > Configuration > Intel Virtual Technology > Enable.
- __Uninstall Hyper-V__: Control panel > Uninstall a program > Turn Windows features on or off > (clear Hyper-V checkbox).

**Error: Ubuntu isn’t fullscreen inside the virtual machine**

- In VMware virtual machine go to: “Player > Manage > Install VMware tools”. This will install VMware tools in your guest OS.
- Restart the virtual machine.

In: “Player > Manage > Virtual machine settings > Display” you can make some display configurations (maybe you can only modify values here before opening the virtual machine).

Note: In VirtualBox, it is used the “Guest additions” for this.

**Error: Keyboard has wrong characters**

In the “Configuration” menu (it’s at the top right corner) > Region and language > Input sources > Spanish (to install that language go to “Manage installed languages”).

**Share folders with the host**

In the screen where you select the virtual machine you want to boot, select “Edit virtual machine settings” (of a certain virtual machine) and go to the “Options” > “Shared folder“. There, you can select the directories from the host that you want to be accessible from your virtual machine.

**How to connect sensors to the virtual machine using a switch**

- Change the network connection of the virtual machine to `Bridged` (connected directly to the physical network) (`Virtual machine settings/Network adapter/Network connection/Bridged`).
- Change the PC's IP address to match that of the switch (`Centro de redes y recursos compartidos/”your_conexion”/Cambiar la configuración del adaptador/Protocolo de Internet versión 4 (TCP/IPv4)/Usar la siguiente dirección IP`). Example: If the switch has IP 192.168.1.1, then change the IP of your PC connected to the switch to, for example, 192.168.1.70.


## Command line

### Basic commands

Each command is a path (or alias of a path) to a binary that is somewhere and which it executes. This path may be absolute (exact match) or relative (used to look for the binary in all the paths specified in the `$PATH` environment variable. Use `which X` or `command -v X` to see the absolute path of command `X`.

Some environment variables (EV):

- `$PATH`: Places to look for binaries.
- `$SHELL`: Shell you use. Show available shells with `cat/etc/shells`. Change shell putting its name (`sh`, `bash`…).
- `HOME`: Path to home directory.

Some key files:

- `/dev/null`: Black hole. Anything sent here dissapears.
- `bin/bash`: Available shells.
- `/etc/passwd`: Lists of existing users.
- `/etc/group`: List of existing groups.
- `/etc/hosts`: Used for matching an FQDN with the server IP hosting a specific domain. Useful when a DNS server isn't available.

Main commands:

- `pwd`: Print working directory.
- `ls`, `ls X`, `ls -l`: List files in current/given directory.
- `cd X`, `cd ..`, `cd /`, `cd`: Change directory to X/previous dir/root dir/home dir.
- `whoami`: Get username.
- `id`: Get the groups you belong to. The existing groups are visible in the file `/etc/group`.
- `echo hello` / `echo $PATH`: Print "hello" / Print `$PATH`.
- `cat filename`: See file content. Move with av-pag, re-pag, or arrows. Exit with `q`.
  - `cat filename | grep "abc"` (pipe): Take output from `cat` and show only the lines containing "abc". Include `-n` at the end to show the line number.
- `cp some/file filecopy`: Copy `some/file` in current directory and name it `filecopy`.
- Verbose (`-V`): Flag for getting more info about an executed command.
- `find . -name "filename"`: Look for a file in current directory recursively.
- `A | xargs B`: Use output from command `A` as arguemnt for command `B`. Example: `which python3.9 | xargs ls -l` (show files in the directory where `python3.9` is).
- `ctrl + l`: Clean window.
- `ctrl + c`: Cancel process.
- `exit`: Exit console. Force exit with `Alt + W`.
- `ps` / `ps -e`: Show your processes / Show all processes (system-wide).
- Basic commands: [[ciberninjas](https://ciberninjas.com/chuleta-comandos-linux/)], [[bonaval](https://www.bonaval.com/kb/cheats-chuletas/comandos-basicos-linux)], [[famaf](https://www.famaf.unc.edu.ar/~vmarconi/numerico1/comandos.pdf)], [[fing.edu](https://www.fing.edu.uy/inco/cursos/sistoper/recursosLaboratorio/tutorial0.pdf)].

### Control flow

- `X; Y`: Execute a series of commands (first `X`, then `Y`). Concatenate using `;`.
- `X && Y`: Execute operand `X`. If it was successful, execute operand `Y`.
- `X || Y`: Execute operand `X`. If it failed, execute operand `Y`.
- `echo $?`: Show state/error code of the command previously executed.
- `>`: Redirect some output to somewhere.
  - Outputs: `1` (stdout, output), `2` (stderr, error code), `&` (stdout and stderr).
  - `cat/etc/hosts 1 > /dev/null` (also `>` alone): Forward `cat` stdout to file `null`.
  - `whoam 2 > /dev/null`: Forward `whoam` stderr to `null`.
  - `cat /etc/host &> /dev/null`: Forward `cat` stdout and stderr to `null`.
  - `cat /etc/host > /dev/null 2>&1`: Forward stdout to `null`, and output stderr to stdout (so errors are sent to `null` too).
- Background process:
  - `wireshark &>/dev/null &`: Place `&` at the end to execute a process in the background. It outputs the PID (process id).
  - `wireshark &>/dev/null & disown`: Place `disown` at the end to make it independent of the parent process (example: the console process).

### File descriptor

- `pwd > filename`: Send output to file.
- `exec 3<> filename`: Create file with read (`<`) and write (`>`) capabilities called `filename` and identify it with a 3.
- `file filename`: Determine type of the file (output example: `file empty`).
- `pwd > &3`: Send output to the file. Subsequent additions are appended.
- `exec 4>&3`: Now descriptor 4 also identifies the file indentified with descriptor 3.
  - `exec 4>&3-`: The same, but invalidating descriptor 3 at the end.
- `exec 3  &-`: Invalidate descriptor number (not assigned to a file anymore).
- [Bash redirections cheat sheet](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/bash_redirections_cheat_sheet.pdf)

### Permissions

Each file and directory has permissions (read, write, execute) associated to different entites (owner user, group, anybody else). These entities and their permissions can only be changed by the owner and the superuser (`su`).

- 



### Directories


