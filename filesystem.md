# Linux file system

* forward slash instead of the back slash
* case sensitive file names
* files and directories that start with `.` are hidden
* structure and layout is outlined in the [filesystem hierarchy standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard) (FHS) which is maintained by the Linux Foundation

# bin 
* short for binaries
* basic binaries for commands like `ls`, `cat`, `grep`

# sbin
* system binaries that only a system administrator would use
* accessible when running in single user mode
  * special mode that boots you in as a root user to allow you to do system repairs and upgrades or testing 
  * networking is usually disabled because of security issues

# boot
* everything your OS needs to boot e.g. boot loaders

# cdrom
* legacy mounting point for your cd-rom
* not in all distros

# dev
* where your devices live
  * your hardware disk is found in `/dev/sda`, and a partition on that disk would be `/dev/sda1`
  * webcam, keyboard, etc.
* applications and drivers will access this, but this is rarely something a user should be touching

# etc
* system-wide configurations
  * `apt` package manager's list of all your repository sources your system connects to and various settings 
  
# home
* each user has their own home folder 
* admin permissions can access other user's folders

# lib, lib32, lib64
* library files that applications can use to perform various functions
* required by the binaries in `bin` and `sbin`

# media, mnt
*  mounted drives
  * floppy disk, USB stick, external hard drive, network drive, second hard drive, etc.
* if mounting manually, use `/mnt/`
* OS manages `/media/`

# opt
* optional folder, where manually installed software from vendors

# proc
* pseudo files that contain information about system processes and resources
* every process will have a directory named after its `process id`

# root
* root users home folder
* does not contain the typical directories inside the home folder
* requires root permissions to access
* location of this directory also ensures that root always has access to its home folder, in case you have the regular users home directory stored on another drive which you cannot access

# run
* different distros use this in slightly different ways
* tempfs file system
  * it runs in RAM
  * everything in this is gone when the system's rebooted or shut down
* it's used for processes that start early in the boot procedure to store runtime information that they use to function 

# snap
* where snap packages are stored
* mainly used by Ubuntu

# srv
* service directory where service data is stored
* files that will be accessed by external users when running a web or FTP server
* allows for better security since it's at the root of the drive, and it also allows you to easily mount this folder from another hard drive

# sys
* a way to interact with the kernel
* created every time the system boots

# tmp
* where files are temporarily stored by applications that could be used during a session

# usr
* where applications will be installed that are used by the user
  * as opposed to the bin directory is used by the system and system administrator to perform maintenance
* aka UNIX system resource
  * any applications installed here are considered non-essential for basic system operation

# var
* contains files and directories that are expected to grow in size
  * `/var/crash/` holds information about processes that have crashed
  * `/var/log/` contains log files for the system and applications
  * databases for mail and temporary storage for printer queues