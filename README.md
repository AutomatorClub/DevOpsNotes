Unix Toolbox

This document is a collection of Unix/Linux/BSD commands and tasks which
are useful for IT work or for advanced users. This is a practical guide
with concise explanations, however the reader is supposed to know what
s/he is doing.  

1.  [System](https://github.com/AutomatorClub/DevOpsNotes/blob/main/README.md#system)
2.  [Processes](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#processes)
3.  [File System](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#filesystem)
4.  [Network](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#network)
5.  [SSH SCP](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#ssh)
6.  [VPN with SSH](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#vpn)
7.  [RSYNC](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#rsync)
8.  [SUDO](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#sudo)
9.  [Encrypt Files](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#crypt)
10. [Encrypt Partitions](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#cryptpart)
11. [SSL Certificates](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#certs)
12. [CVS](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#cvs)
13. [SVN](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#svn)
14. [Useful Commands](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#other)
15. [Install Software](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#software)
16. [Convert Media](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#convert)
17. [Printing](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#printing)
18. [Databases](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#databases)
19. [Disk Quota](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#quota)
20. [Shells](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#shells)
21. [Scripting](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#scripting)
22. [Programming](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#programming)
23. [Online Help](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#onlinehelp)


# System

[Hardware](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#hardwareinfo)|
[Statistics](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#loadstats) |
[Users](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#users)|
[Limits](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#limits)|
[Runlevels](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#runlevels)|
[root password](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#resetpasswd)|
[Compile kernel](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#compilekernel)|
[Repair grub](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#grub)|
[Misc](https://github.com/AutomatorClub/DevOpsNotes/edit/main/README.md#sysmisc)


Running kernel and system information

    # uname -a                           # Get the kernel version (and BSD version)
    # lsb_release -a                     # Full release info of any LSB distribution
    # cat /etc/SuSE-release              # Get SuSE version
    # cat /etc/debian_version            # Get Debian version

Use /etc/`DISTR`-release with `DISTR=` lsb (Ubuntu), redhat, gentoo,
mandrake, sun (Solaris), and so on. See also `/etc/issue`.

    # uptime                             # Show how long the system has been running + load
    # hostname                           # system's host name
    # hostname -i                        # Display the IP address of the host. (Linux only)
    # man hier                           # Description of the file system hierarchy
    # last reboot                        # Show system reboot history

## Hardware Informations

Kernel detected hardware

    # dmesg                              # Detected hardware and boot messages
    # lsdev                              # information about installed hardware
    # dd if=/dev/mem bs=1k skip=768 count=256 2>/dev/null | strings -n 8 # Read BIOS

### Linux

    # cat /proc/cpuinfo                  # CPU model
    # cat /proc/meminfo                  # Hardware memory
    # grep MemTotal /proc/meminfo        # Display the physical memory
    # watch -n1 'cat /proc/interrupts'   # Watch changeable interrupts continuously
    # free -m                            # Used and free memory (-m for MB)
    # cat /proc/devices                  # Configured devices
    # lspci -tv                          # Show PCI devices
    # lsusb -tv                          # Show USB devices
    # lshal                              # Show a list of all devices with their properties
    # dmidecode                          # Show DMI/SMBIOS: hw info from the BIOS

### FreeBSD

    # sysctl hw.model                    # CPU model
    # sysctl hw                          # Gives a lot of hardware information
    # sysctl hw.ncpu                     # number of active CPUs installed
    # sysctl vm                          # Memory usage
    # sysctl hw.realmem                  # Hardware memory
    # sysctl -a | grep mem               # Kernel memory settings and info
    # sysctl dev                         # Configured devices
    # pciconf -l -cv                     # Show PCI devices
    # usbdevs -v                         # Show USB devices
    # atacontrol list                    # Show ATA devices
    # camcontrol devlist -v              # Show SCSI devices

## Load, statistics and messages

The following commands are useful to find out what is going on on the
system.

    # top                                # display and update the top cpu processes
    # mpstat 1                           # display processors related statistics
    # vmstat 2                           # display virtual memory statistics
    # iostat 2                           # display I/O statistics (2 s intervals)
    # systat -vmstat 1                   # BSD summary of system statistics (1 s intervals)
    # systat -tcp 1                      # BSD tcp connections (try also -ip)
    # systat -netstat 1                  # BSD active network connections
    # systat -ifstat 1                   # BSD network traffic through active interfaces
    # systat -iostat 1                   # BSD CPU and and disk throughput
    # ipcs -a                            # information on System V interprocess
    # tail -n 500 /var/log/messages      # Last 500 kernel/syslog messages
    # tail /var/log/warn                 # System warnings messages see syslog.conf

## Users

    # id                                 # Show the active user id with login and group
    # last                               # Show last logins on the system
    # who                                # Show who is logged on the system
    # groupadd admin                     # Add group "admin" and user colin (Linux/Solaris)
    # useradd -c "Colin Barschel" -g admin -m colin
    # usermod -a -G <group> <user>       # Add existing user to group (Debian)
    # groupmod -A <user> <group>         # Add existing user to group (SuSE)
    # userdel colin                      # Delete user colin (Linux/Solaris)
    # adduser joe                        # FreeBSD add user joe (interactive)
    # rmuser joe                         # FreeBSD delete user joe (interactive)
    # pw groupadd admin                  # Use pw on FreeBSD
    # pw groupmod admin -m newmember     # Add a new member to a group
    # pw useradd colin -c "Colin Barschel" -g admin -m -s /bin/tcsh 
    # pw userdel colin; pw groupdel admin
    # vi /etc/security/pwquality.conf    # To edit password policy
    # chage -l admin                     # To list current account aging type
    # chage -I -1 -m 0 -M 99999 -E -1 admin      # To disable password aging / expiration for user admin

Encrypted passwords are stored in /etc/shadow for Linux and Solaris and
/etc/master.passwd on FreeBSD. If the master.passwd is modified manually
(say to delete a password), run `# pwd_mkdb -p master.passwd` to rebuild
the database.  
  
To temporarily prevent logins system wide (for all users but root) use
nologin. The message in nologin will be displayed (might not work with
ssh pre-shared keys).

    # echo "Sorry no login now" > /etc/nologin       # (Linux)
    # echo "Sorry no login now" > /var/run/nologin   # (FreeBSD)

## Limits

Some application require higher limits on open files and sockets (like a
proxy web server, database). The default limits are usually too low.

### Linux

#### Per shell/script

The shell limits are governed by `ulimit`. The status is checked with
`ulimit -a`. For example to change the open files limit from 1024 to
10240 do:

    # ulimit -n 10240                    # This is only valid within the shell

The `ulimit` command can be used in a script to change the limits for
the script only.

#### Per user/process

Login users and applications can be configured in
`/etc/security/limits.conf`. For example:

    # cat /etc/security/limits.conf
    *   hard    nproc   250              # Limit user processes
    asterisk hard nofile 409600          # Limit application open files

#### System wide

Kernel limits are set with sysctl. Permanent limits are set in
`/etc/sysctl.conf`.

    # sysctl -a                          # View all system limits
    # sysctl fs.file-max                 # View max open files limit
    # sysctl fs.file-max=102400          # Change max open files limit
    # echo "1024 50000" > /proc/sys/net/ipv4/ip_local_port_range  # port range
    # cat /etc/sysctl.conf
    fs.file-max=102400                   # Permanent entry in sysctl.conf
    # cat /proc/sys/fs/file-nr           # How many file descriptors are in use

### FreeBSD

#### Per shell/script

Use the command `limits` in csh or tcsh or as in Linux, use `ulimit` in
an sh or bash shell.

#### Per user/process

The default limits on login are set in `/etc/login.conf`. An unlimited
value is still limited by the system maximal value.

#### System wide

Kernel limits are also set with sysctl. Permanent limits are set in
`/etc/sysctl.conf` or `/boot/loader.conf`. The syntax is the same as
Linux but the keys are different.

    # sysctl -a                          # View all system limits
    # sysctl kern.maxfiles=XXXX          # maximum number of file descriptors
    kern.ipc.nmbclusters=32768           # Permanent entry in /etc/sysctl.conf
    kern.maxfiles=65536                  # Typical values for Squid
    kern.maxfilesperproc=32768
    kern.ipc.somaxconn=8192              # TCP queue. Better for apache/sendmail
    # sysctl kern.openfiles              # How many file descriptors are in use
    # sysctl kern.ipc.numopensockets     # How many open sockets are in use
    # sysctl net.inet.ip.portrange.last=50000 # Default is 1024-5000
    # netstat -m                         # network memory buffers statistics

See The [FreeBSD handbook Chapter
11](http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/configtuning-kernel-limits.html)<span class="fn">http://www.freebsd.org/handbook/configtuning-kernel-limits.html</span>
for details. And also [FreeBSD performance
tuning](http://serverfault.com/questions/64356/freebsd-performance-tuning-sysctls-loader-conf-kernel)<span class="fn">http://serverfault.com/questions/64356/freebsd-performance-tuning-sysctls-loader-conf-kernel</span>

### Solaris

The following values in `/etc/system` will increase the maximum file
descriptors per proc:

    set rlim_fd_max = 4096               # Hard limit on file descriptors for a single proc
    set rlim_fd_cur = 1024               # Soft limit on file descriptors for a single proc

## Runlevels

### Linux

Once booted, the kernel starts `init` which then starts `rc` which
starts all scripts belonging to a runlevel. The scripts are stored in
/etc/init.d and are linked into /etc/rc.d/rcN.d with N the runlevel
number.  
The default runlevel is configured in /etc/inittab. It is usually 3 or
5:

    # grep default: /etc/inittab                                         
    id:3:initdefault:

The actual runlevel can be changed with `init`. For example to go from 3
to 5:

    # init 5                             # Enters runlevel 5

- 0 Shutdown and halt
- 1 Single-User mode (also S)
- 2 Multi-user without network
- 3 Multi-user with network
- 5 Multi-user with X
- 6 Reboot

Use `chkconfig` to configure the programs that will be started at boot
in a runlevel.

    # chkconfig --list                   # List all init scripts
    # chkconfig --list sshd              # Report the status of sshd
    # chkconfig sshd --level 35 on       # Configure sshd for levels 3 and 5
    # chkconfig sshd off                 # Disable sshd for all runlevels

Debian and Debian based distributions like Ubuntu or Knoppix use the
command `update-rc.d` to manage the runlevels scripts. Default is to
start in 2,3,4 and 5 and shutdown in 0,1 and 6.

    # update-rc.d sshd defaults          # Activate sshd with the default runlevels
    # update-rc.d sshd start 20 2 3 4 5 . stop 20 0 1 6 .  # With explicit arguments
    # update-rc.d -f sshd remove         # Disable sshd for all runlevels
    # shutdown -h now (or # poweroff)    # Shutdown and halt the system

### FreeBSD

The BSD boot approach is different from the SysV, there are no
runlevels. The final boot state (single user, with or without X) is
configured in `/etc/ttys`. All OS scripts are located in `/etc/rc.d/`
and in `/usr/local/etc/rc.d/` for third-party applications. The
activation of the service is configured in `/etc/rc.conf` and
`/etc/rc.conf.local`. The default behavior is configured in
`/etc/defaults/rc.conf`. The scripts responds at least to
start\|stop\|status.

    # /etc/rc.d/sshd status
    sshd is running as pid 552.
    # shutdown now                       # Go into single-user mode
    # exit                               # Go back to multi-user mode
    # shutdown -p now                    # Shutdown and halt the system
    # shutdown -r now                    # Reboot

The process `init` can also be used to reach one of the following states
level. For example `# init 6` for reboot.

- 0 Halt and turn the power off (signal `USR2`)
- 1 Go to single-user mode (signal `TERM`)
- 6 Reboot the machine (signal `INT`)
- c Block further logins (signal `TSTP`)
- q Rescan the ttys(5) file (signal `HUP`)

### Windows

Start and stop a service with either the `service name` or
`"service description"` (shown in the Services Control Panel) as
follows:

    net stop WSearch
    net start WSearch                    # start search service
    net stop "Windows Search"
    net start "Windows Search"           # same as above using descr.

## Reset root password

### Linux method 1

At the boot loader (lilo or grub), enter the following boot option:

    init=/bin/sh

The kernel will mount the root partition and `init` will start the
bourne shell instead of `rc` and then a runlevel. Use the command
`passwd` at the prompt to change the password and then reboot. Forget
the single user mode as you need the password for that.  
If, after booting, the root partition is mounted read only, remount it
rw:

    # mount -o remount,rw /
    # passwd                             # or delete the root password (/etc/shadow)
    # sync; mount -o remount,ro /        # sync before to remount read only
    # reboot

### FreeBSD method 1

On FreeBSD, boot in single user mode, remount / rw and use passwd. You
can select the single user mode on the boot menu (option 4) which is
displayed for 10 seconds at startup. The single user mode will give you
a root shell on the / partition.

    # mount -u /; mount -a               # will mount / rw
    # passwd
    # reboot

### Unixes and FreeBSD and Linux method 2

Other Unixes might not let you go away with the simple init trick. The
solution is to mount the root partition from an other OS (like a rescue
CD) and change the password on the disk.

- Boot a live CD or installation CD into a rescue mode which will give
  you a shell.
- Find the root partition with fdisk e.g. fdisk /dev/sda
- Mount it and use chroot:

<!-- -->

    # mount -o rw /dev/ad4s3a /mnt
    # chroot /mnt                        # chroot into /mnt
    # passwd
    # reboot

## Kernel modules

### Linux

    # lsmod                              # List all modules loaded in the kernel
    # modprobe isdn                      # To load a module (here isdn)

### FreeBSD

    # kldstat                            # List all modules loaded in the kernel
    # kldload crypto                     # To load a module (here crypto)

## Compile Kernel

### Linux

    # cd /usr/src/linux
    # make mrproper                      # Clean everything, including config files
    # make oldconfig                     # Reuse the old .config if existent
    # make menuconfig                    # or xconfig (Qt) or gconfig (GTK)
    # make                               # Create a compressed kernel image
    # make modules                       # Compile the modules
    # make modules_install               # Install the modules
    # make install                       # Install the kernel
    # reboot

### FreeBSD

Optionally update the source tree (in `/usr/src`) with csup (as of
FreeBSD 6.2 or later):

    # csup <supfile>

I use the following supfile:

    *default host=cvsup5.FreeBSD.org  # www.freebsd.org/handbook/cvsup.html#CVSUP-MIRRORS
    *default prefix=/usr 
    *default base=/var/db
    *default release=cvs delete tag=RELENG_7
    src-all

To modify and rebuild the kernel, copy the generic configuration file to
a new name and edit it as needed (you can also edit the file `GENERIC`
directly). To restart the build after an interruption, add the option
`NO_CLEAN=YES` to the make command to avoid cleaning the objects already
build.

    # cd /usr/src/sys/i386/conf/
    # cp GENERIC MYKERNEL
    # cd /usr/src
    # make buildkernel KERNCONF=MYKERNEL
    # make installkernel KERNCONF=MYKERNEL

To rebuild the full OS:

    # make buildworld                    # Build the full OS but not the kernel
    # make buildkernel                   # Use KERNCONF as above if appropriate
    # make installkernel
    # reboot
    # mergemaster -p                     # Compares only files known to be essential
    # make installworld
    # mergemaster -i -U                  # Update all configurations and other files
    # reboot

For small changes in the source you can use NO_CLEAN=yes to avoid
rebuilding the whole tree.

    # make buildworld NO_CLEAN=yes       # Don't delete the old objects
    # make buildkernel KERNCONF=MYKERNEL NO_CLEAN=yes

## Repair grub

So you broke grub? Boot from a live cd, \[find your linux partition
under `/dev` and use `fdisk` to find the linux partion\] mount the linux
partition, add /proc and /dev and use `grub-install /dev/xyz`. Suppose
linux lies on `/dev/sda6`:

    # mount /dev/sda6 /mnt               # mount the linux partition on /mnt
    # mount --bind /proc /mnt/proc       # mount the proc subsystem into /mnt
    # mount --bind /dev /mnt/dev         # mount the devices into /mnt
    # chroot /mnt                        # change root to the linux partition
    # grub-install /dev/sda              # reinstall grub with your old settings

## Misc

Disable OSX virtual memory (repeat with `load` to re-enable). Faster
system, but a little risky.

    # sudo launchctl unload -w /System/Library/LaunchDaemons/com.apple.dynamic_pager.plist
    # sleep 3600; pmset sleepnow           # go to standby in one hour (OSX)
    # defaults write -g com.apple.mouse.scaling -float 8
                                         # OSX mouse acceleration (use -1 to reverse)
