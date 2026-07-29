# Linux commands 

### 1. ps 

* It allows us to see whats actually running on our server , the processes that are running on our serever 

```bash
ps 
```
```bash
PID  TTY          TIME  CMD
3729 pts/0    00:00:00 bash
4725 pts/0    00:00:00 ps
```
explaining the output ;
1. PID - the Processes ID , each processe in the linux system has a unique ID eg the PID for bash is 3729
2. TTY - Refers to the terminal that the process is working on 
3. Time - refers to the CPU time , how much time the process has been utiliing the CPU
4. CMD - The command that is running as part of that process

to run all  process , we use 

```bash
 ps x
```

```bash
PID TTY      STAT   TIME COMMAND
   1744 ?        Ss     0:00 /usr/lib/systemd/systemd --user
   1746 ?        S      0:00 (sd-pam)
   1766 ?        Ss     0:00 /usr/bin/dbus-daemon --session --address=systemd: 
   1767 ?        S<sl   0:00 /usr/bin/pipewire
   1768 ?        Ssl    0:00 /usr/bin/pipewire -c filter-chain.conf
   1769 ?        S<sl   0:00 /usr/bin/wireplumber
   1771 ?        S<sl   0:00 /usr/bin/pipewire-pulse
   1772 ?        SLsl   0:00 /usr/bin/gnome-keyring-daemon --foreground --compo
   1773 ?        Ss     0:00 /usr/bin/mpris-proxy
   1807 tty2     Ssl+   0:00 /usr/libexec/gdm-wayland-session /usr/bin/gnome-se
   1818 tty2     Sl+    0:00 /usr/libexec/gnome-session-binary
   1862 ?        Ssl    0:00 /usr/libexec/gcr-ssh-agent --base-dir /run/user/10
   1863 ?        Ssl    0:00 /usr/libexec/gnome-session-ctl --monitor
   1864 ?        Ss     0:00 /usr/bin/ssh-agent -D
   1876 ?        Ssl    0:00 /usr/libexec/gvfsd
   1882 ?        Sl     0:00 /usr/libexec/gvfsd-fuse /run/user/1001/gvfs -f
   1884 ?        Ssl    0:00 /usr/libexec/gnome-session-binary --systemd-servic
   1916 ?        Sl     0:00 /usr/libexec/at-spi-bus-launcher --launch-immediat
   1917 ?        Ssl    0:30 /usr/bin/gnome-shell
   1930 ?        S      0:00 /usr/bin/dbus-daemon --config-file=/usr/share/defa
   1966 ?        Sl     0:00 /usr/libexec/at-spi2-registryd --use-gnome-session
   1985 ?        Ssl    0:00 /usr/libexec/xdg-permission-store
   1987 ?        Sl     0:00 /usr/libexec/gnome-shell-calendar-server
   1997 ?        Ssl    0:00 /usr/libexec/evolution-source-registry
   1998 ?        Ssl    0:00 /usr/libexec/dconf-service
   2007 ?        Sl     0:00 /usr/bin/gjs -m /usr/share/gnome-shell/org.gnome.S
   2015 ?        Ssl    0:02 /usr/bin/ibus-daemon --panel disable
   2017 ?        Ssl    0:00 /usr/libexec/gsd-a11y-settings
   2021 ?        Ssl    0:00 /usr/libexec/gsd-color
   2027 ?        Ssl    0:00 /usr/libexec/gsd-datetime
   2030 ?        Ssl    0:00 /usr/libexec/gsd-housekeeping
   2033 ?        Ssl    0:00 /usr/libexec/gsd-keyboard
   2038 ?        Ssl    0:00 /usr/libexec/gsd-media-keys
   2047 ?        Ssl    0:00 /usr/libexec/gsd-power
   2048 ?        Ssl    0:00 /usr/libexec/gsd-print-notifications
   2050 ?        Sl     0:00 /usr/libexec/gsd-disk-utility-notify
   2057 ?        Ssl    0:00 /usr/libexec/gsd-rfkill
   2068 ?        Ssl    0:00 /usr/libexec/gsd-screensaver-proxy
   2079 ?        Sl     0:07 /usr/bin/gnome-software --gapplication-service
   2090 ?        Ssl    0:00 /usr/libexec/gsd-sharing
   2094 ?        Ssl    0:00 /usr/libexec/gsd-smartcard
   2095 ?        Ssl    0:00 /usr/libexec/gsd-sound
   2097 ?        Sl     0:00 /usr/libexec/evolution-data-server/evolution-alarm
   2098 ?        Ssl    0:00 /usr/libexec/gsd-usb-protection
   2107 ?        Ssl    0:00 /usr/libexec/gsd-wacom
   2174 ?        Sl     0:00 /usr/libexec/ibus-dconf
   2177 ?        Sl     0:01 /usr/libexec/ibus-extension-gtk3
   2188 ?        Sl     0:00 /usr/libexec/ibus-portal
   2207 ?        Sl     0:00 /usr/bin/gjs -m /usr/share/gnome-shell/org.gnome.S
   2230 ?        Sl     0:00 /usr/bin/Xwayland :0 -rootless -noreset -accessx -
   2233 ?        Ssl    0:00 /usr/libexec/gvfs-udisks2-volume-monitor
   2239 ?        Ssl    0:00 /usr/libexec/gvfs-goa-volume-monitor
   2244 ?        Sl     0:00 /usr/libexec/goa-daemon
   2258 ?        Sl     0:00 /usr/libexec/goa-identity-service
   2264 ?        Ssl    0:00 /usr/libexec/gvfs-afc-volume-monitor
   2275 ?        Ssl    0:00 /usr/libexec/evolution-calendar-factory
   2276 ?        Ssl    0:00 /usr/libexec/gvfs-gphoto2-volume-monitor
   2284 ?        Ssl    0:00 /usr/libexec/gvfs-mtp-volume-monitor
   2298 ?        Ssl    0:00 /usr/libexec/evolution-addressbook-factory
   2312 ?        Sl     0:00 /usr/libexec/ibus-engine-simple
   2358 ?        Ssl    0:00 /usr/libexec/xdg-desktop-portal
   2365 ?        SNsl   0:00 /usr/libexec/localsearch-3
   2370 ?        Ssl    0:00 /usr/libexec/xdg-document-portal
   2382 ?        Ssl    0:00 /usr/libexec/xdg-desktop-portal-gnome
   2390 ?        Ssl    0:00 /usr/libexec/gsd-xsettings
   2414 ?        Sl     0:00 /usr/libexec/mutter-x11-frames
   2441 ?        Sl     0:00 /usr/libexec/ibus-x11
   2456 ?        Ssl    0:00 /usr/libexec/xdg-desktop-portal-gtk
   2501 ?        Ssl    0:00 /usr/libexec/gvfsd-metadata
   2521 ?        Sl     0:00 /usr/libexec/gsd-printer
   2617 ?        Sl     0:26 /opt/google/chrome/chrome
   2622 ?        S      0:00 cat
   2623 ?        S      0:00 cat
   2625 ?        Sl     0:00 /opt/google/chrome/chrome_crashpad_handler --monit
   2627 ?        Sl     0:00 /opt/google/chrome/chrome_crashpad_handler --no-pe
   2635 ?        S      0:00 /opt/google/chrome/chrome --type=zygote --no-zygot
   2636 ?        S      0:00 /opt/google/chrome/chrome --type=zygote --crashpad
   2638 ?        S      0:00 /opt/google/chrome/chrome --type=zygote --crashpad
   2667 ?        Sl     0:12 /opt/google/chrome/chrome --type=gpu-process --ozo
   2671 ?        Sl     0:15 /opt/google/chrome/chrome --type=utility --utility
   2684 ?        Sl     0:00 /opt/google/chrome/chrome --type=utility --utility
   2724 ?        Sl     0:00 /opt/google/chrome/chrome --type=renderer --top-ch
   2810 ?        Sl     0:26 /opt/google/chrome/chrome --type=renderer --crashp
   2867 ?        Sl     0:09 /opt/google/chrome/chrome --type=renderer --crashp
   2875 ?        Sl     0:00 /opt/google/chrome/chrome --type=renderer --crashp
   2896 ?        Sl     0:00 /opt/google/chrome/chrome --type=renderer --crashp
   2922 ?        Sl     0:08 /opt/google/chrome/chrome --type=renderer --crashp
   2972 ?        Sl     0:00 /opt/google/chrome/chrome --type=renderer --crashp
   3020 ?        Sl     0:00 /opt/google/chrome/chrome --type=utility --utility
   3065 ?        Sl     0:06 /opt/google/chrome/chrome --type=renderer --crashp
   3117 ?        Sl     0:35 /opt/google/chrome/chrome --type=renderer --crashp
   3141 ?        Sl     0:01 /opt/google/chrome/chrome --type=renderer --crashp
   3223 ?        Sl     1:48 /opt/google/chrome/chrome --type=renderer --crashp
   3273 ?        Sl     0:00 /usr/bin/gnome-calendar --gapplication-service
   3335 ?        Sl     0:00 /usr/libexec/gvfsd-trash --spawner :1.17 /org/gtk/
   3458 ?        SLl    0:16 /usr/share/code/code
   3462 ?        S      0:00 /usr/share/code/code --type=zygote --no-zygote-san
   3463 ?        S      0:00 /usr/share/code/code --type=zygote
   3465 ?        S      0:00 /usr/share/code/code --type=zygote
   3493 ?        Sl     0:00 /usr/share/code/chrome_crashpad_handler --monitor-
   3510 ?        Sl     0:19 /usr/share/code/code --type=gpu-process --ozone-pl
   3516 ?        Sl     0:00 /usr/share/code/code --type=utility --utility-sub-
   3555 ?        Rl     1:33 /usr/share/code/code --type=renderer --crashpad-ha
   3588 ?        Sl     0:10 /opt/google/chrome/chrome --type=renderer --crashp
   3613 ?        Sl     0:29 /usr/share/code/code --type=utility --utility-sub-
   3628 ?        Sl     0:04 /usr/share/code/code --type=utility --utility-sub-
   3629 ?        Sl     0:00 /usr/share/code/code --type=utility --utility-sub-
   3681 ?        Sl     0:02 /usr/share/code/code --type=utility --utility-sub-
   3716 ?        Sl     0:01 /opt/google/chrome/chrome --type=renderer --crashp
   3728 ?        Sl     0:02 /usr/share/code/code /usr/share/code/resources/app
   3729 pts/0    Ss+    0:00 /usr/bin/bash --init-file /usr/share/code/resource
   3763 ?        Sl     0:19 /opt/google/chrome/chrome --type=renderer --crashp
   3888 ?        Sl     0:09 /opt/google/chrome/chrome --type=renderer --crashp
   3900 ?        Sl     0:01 /opt/google/chrome/chrome --type=renderer --crashp
   3908 ?        Sl     0:00 /opt/google/chrome/chrome --type=renderer --crashp
   3996 ?        Sl     0:03 /opt/google/chrome/chrome --type=renderer --crashp
   4018 ?        Sl     0:02 /opt/google/chrome/chrome --type=renderer --crashp
   4062 ?        Sl     0:00 /opt/google/chrome/chrome --type=renderer --crashp
   4099 ?        Sl     0:03 /opt/google/chrome/chrome --type=renderer --crashp
   4113 ?        Sl     0:19 /opt/google/chrome/chrome --type=renderer --crashp
   4192 ?        Sl     0:04 /opt/google/chrome/chrome --type=renderer --crashp
   4228 ?        Sl     0:02 /opt/google/chrome/chrome --type=renderer --crashp
   4341 ?        Sl     0:00 /usr/libexec/gvfsd-recent --spawner :1.17 /org/gtk
   4365 ?        Sl     0:00 /usr/libexec/gvfsd-network --spawner :1.17 /org/gt
   4372 ?        Sl     0:00 /usr/libexec/gvfsd-dnssd --spawner :1.17 /org/gtk/
   5062 pts/1    Ss+    0:00 /usr/bin/bash --init-file /usr/share/code/resource
   5233 pts/2    Ss     0:00 /usr/bin/bash --init-file /usr/share/code/resource
   5389 ?        Sl     0:00 /opt/google/chrome/chrome --type=renderer --crashp
   5499 ?        Sl     0:00 /opt/google/chrome/chrome --type=renderer --crashp
   5581 ?        S      0:00 /bin/sh -c "/usr/share/code/resources/app/out/vs/b
   5582 ?        S      0:00 /bin/bash /usr/share/code/resources/app/out/vs/bas
   5585 ?        S      0:00 sleep 1
   5587 pts/2    R+     0:00 ps x 
```
Explain the command ;
1. PID - process ID
2. TTY 
   * ? means background process.
   * tty2 means graphical session.
   * pts/0 means virtual terminal

3. STAT ( THE PROCESS STATUS)
   * R - The process is running 
   * S - sleeping state.
   * s - Session leader process.
   * l - Multi-threaded process execution.
   * < - High priority process.
   * N - Low priority process.
   * L - Pages locked into memory.
   * +-  They are working right at that moment 
   * sl - The sleeping multi-tasker -This app is idle right now, but it is split into multiple pieces so it can work fast when it wakes up. 
   * Ss - The sleeping leader - This is a core background program that manages other smaller programs. If this boss dies, its helpers die too
   * Ssl - The Sleeping Multi-Tasking leader , A powerful background service that is currently waiting, but runs multiple parts under a main leader.
   * S< sl The Important Sleeping Boss - < - high priority ,- This process is very important. The computer gives it resources first so your system doesn't lag. eg Your audio system (pipewire) uses this so your music never stutters.
   * l+ & Ssl+ - The Visible Sleeping Helpers , These processes are running on a specific screen station (tty2) that you can actually see and interact with, rather than being completely hidden in the background.
   * SNsl -The Polite Sleeping Boss , N - low priority ,This process is polite. It tells the computer, "Give power to other apps first, I can wait." Your file searcher (localsearch-3) uses this so it doesn't slow down your gaming or browsing while it scans files. 
   * R+ - The Active Worker - R - actively running right now , + - working right infront of you . This process is awake and doing heavy lifting at this exact microsecond. In your list, ps x is R+ because it was actively working to print out the list for you!

### 2. apt ( Package Management)
It The main tool used to install, remove, and manage software apps on your system.

Most used commands:
  * list - list packages based on package names
  * search - search in package descriptions
  * show - show package details
  * install - install packages
  * reinstall - reinstall packages
  * remove - remove packages
  * autoremove - automatically remove all unused packages
  * update - update list of available packages
  * upgrade - upgrade the system by installing/upgrading packages
  * full-upgrade - upgrade the system by removing/installing/*   upgrading packages
  * edit-sources - edit the source information file
  * modernize-sources - modernize .list files to .sources files
  * satisfy - satisfy dependency strings

Example 1 ; 
command ; apt list - list packages on the packages name 

```bash
 apt list
```
expected output ; 

```bash
0ad-data-common/stable 0.27.0-1 all
0ad-data/stable 0.27.0-1 all
0ad/stable 0.27.0-2+b1 amd64
0install-core/stable 2.18-2.1 amd64
0install/stable 2.18-2.1 amd64
0xffff/stable 0.9-1+b1 amd64
2048-qt/stable 0.1.6-2+b4 amd64
2048/stable 1.0.3-1 amd64
2ping/stable 4.5-1.2 all
2vcard/stable 0.6-5 all
3270-common/stable 4.3ga10-5 amd64
389-ds-base-dev/stable 3.1.2+dfsg1-1+deb13u1 amd64
389-ds-base-libs/stable 3.1.2+dfsg1-1+deb13u1 amd64
389-ds-base/stable 3.1.2+dfsg1-1+deb13u1 amd64
389-ds/stable 3.1.2+dfsg1-1+deb13u1 all
3d-ascii-viewer/stable 1.4.0+git20240503+ds-2 amd64 
```
* since they dont have an nstalled label next to them , it means non of them are cxurrently installed in our computer .

GAMES AND VISUAL TOOLS ;
1. 0ad / 0ad-data / 0ad-data-common
2. 2048 / 2048-qt
3. 3d-ascii-viewer

DAILY HELPER TOOLS
1. 0install / 0install-core - A software downloader that lets you run applications directly from the internet without going through normal installation steps.
2. 2vcard-  A converter script that takes your old email address books and converts them into standard contact files (.vcf) that smartphones can read.
3. 3270-common - Part of an emulator tool used to connect your modern PC to giant, old-school IBM mainframe computers.

NETWORK AND HARDWARE UTILITIES ;
1. 0xffff: A highly specialized flash tool used by developers to unbrick, tweak, or update the internal firmware on older Nokia internet tablet devices.
2. 2ping: A network testing tool. It sends data packets back and forth between two computers to see how fast your internet connection is and if any data is getting lost.

COPERATE SERVER TOOLS ;
1. 389-ds / 389-ds-base / 389-ds-base-dev / 389-ds-base-libs: This is an enterprise-grade Directory Server (hence the ds). Companies use this backend database to manage thousands of employee usernames, network passwords, and computer permissions in one central place.

### 3. uname
Prints out details about the "brain" (Kernel) of your operating system.

Command used; 

```bash
uname
```
Expected output ; 

```bash
Linux
```
Example 1 ; Full information check

```bash
uname -a 
```
Expected output ; 

```bash
Linux gwekesa 6.12.94+deb13-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.12.94-1 (2026-06-20) x86_64 GNU/Linux
```
Explanation of the command ;
1. Displays the OS name - Which is Linux 
2. Your Computer local name - gwekesa 
3. the exact kernal version build - 6.12.94+deb13
4. The architecture type - amd64

### 4. du (Disk Usage)
Counts how much space folders and files are taking up on your hard drive (stands for Disk Usage).

command used;

```bash
du
``` 
Expected output ;

* shows number alone

```bash
8       ./quatrix-mentorship/.git/objects/c2
4       ./quatrix-mentorship/.git/objects/pack
68      ./quatrix-mentorship/.git/objects
232     ./quatrix-mentorship/.git
``` 
### Example 1 . Human readable size of the current folder
* using -h , helps you to see the K,G,M instead of the number alone .

command used ; 
```bash
du -sh
``` 
Expected output ; 

```bash
6.7G 
``` 
Explain the command ; 
1. s- means the summary 
2. h - means human-readable 
3. . - means right here in the main directory 
4. 6.7 Gigabytes - is the combined total size of absolutely everything inside my home folder .

### Example 2 ; Checking the specific item inside a folder 

Command used;

```bash
du -h --max-depth=1
``` 
Expected output ; 

```bash
392K    ./desktop
1.2M    ./quatrix_mentorship
20K     ./.vscode
4.0K    ./Templates
4.0K    ./quatrix
1.2M    ./documents
76K     ./.pki
6.7G    .
``` 
Explain the command ; 

This command tells your computer to break down that 6.7G total and show you the size of each individual folder sitting directly inside your current directory

1. du - disk usage

2. -h - human readable 

3. --max-depth=1 - it sets a depth limit , tells the tool to only look 1 folder deep hence shows the sizes of the immediate folders and hides thousands of tiny-subfolders inside them hence the screen is clean and readable .

4. 1.2/392 - The exacts storage footprint of that folder 


#### 9. df (Disk Free)
Shows the overall storage space available on your entire computer drives (stands for Disk Free).

command used ;

```bash
df
``` 
Expected output ; 

```bash
Filesystem     1K-blocks     Used Available Use% Mounted on
udev             3821484        0   3821484   0% /dev
tmpfs             778628     1844    776784   1% /run
/dev/nvme0n1p2 236130176 31444256 192618388  15% /
tmpfs            3893136   164040   3729096   5% /dev/shm
efivarfs             192      103        85  55% /sys/firmware/efi/efivars
tmpfs               5120       12      5108   1% /run/lock
tmpfs               1024        0      1024   0% /run/credentials/systemd-journald.service
tmpfs            3893136    98612   3794524   3% /tmp
/dev/nvme0n1p1    997456     8984    988472   1% /boot/efi
tmpfs             778624      112    778512   1% /run/user/1001
``` 

Explain the command ;

1. Filesystem: The name of the actual hardware drive partition or virtual memory chunk.

   * udev (The Device Manager Desk) - A special virtual manager that handles physical hardware plugs. eg ,  When you plug in a USB mouse, a thumb drive, or a printer, udev instantly wakes up, recognizes what it is, and creates a virtual file for it inside the /dev folder so your apps can use it. It takes up 0 bytes of real hard drive space.

   * tmpfs (The Temporary RAM Scratchpads) - A "Temporary File System" created inside your computer's high-speed RAM memory, not your physical hard drive.

   * /dev/nvme0n1p1 & /dev/nvme0n1p2 (Your Real SSD Hard Drive)
          - nvme0 = The first NVMe storage card plugged into your motherboard.
          - n1 = Namespace 1 (the storage area on that card).
          - p1 and p2 = Partition 1 and Partition 2. Your one physical drive is digitally split into two separate rooms.
    
    * efivarfs & efivars (The Motherboard Brain Link) - A specialized bridge that lets Linux talk directly to your computer motherboard's core firmware (called UEFI or BIOS).

2. Size - The total maximum storage capacity allocated to that section.

3. Used: How much space is actively occupied by data right now.

4. Avail: How much empty room is left over for you to use.

5. Use%: The percentage of space used (like a phone battery icon, but for storage clutter).

6. Mounted on: The folder destination path where Linux hooks up that drive so you can access it.

# Process Management (top,kill ,pkill)

#### 10. top 
A live, real-time scoreboard that shows what apps are processing at that second and how much energy they are using and which one slowing down 

command used;
```bash
top
``` 
Expected output ;

```bash
top - 12:21:07 up  1:29,  1 user,  load average: 0.35, 0.38, 0.37
top - 12:21:09 up  1:29,  1 user,  load average: 0.35, 0.38, 0.37
top - 12:21:09 up  1:29,  1 user,  load average: 0.35, 0.38, 0.37
top - 12:21:09 up  1:29,  1 user,  load average: 0.35, 0.38, 0.37
Tasks: 313 total,   2 running, 311 sleeping,   0 stopped,   0 zombie
%Cpu(s): 22.7 us,  4.5 sy,  0.0 ni, 70.5 id,  0.0 wa,  0.0 hi,  2.3 si,  0.0 st 
MiB Mem :   7603.8 total,    291.6 free,   6153.3 used,   2253.2 buff/cache     
MiB Swap:   7847.0 total,   7762.7 free,     84.2 used.   1450.5 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND  
top - 12:22:44 up  1:31,  1 user,  load average: 0.28, 0.36, 0.36
Tasks: 315 total,   1 running, 314 sleeping,   0 stopped,   0 zombie
%Cpu(s): 10.5 us,  1.1 sy,  0.0 ni, 88.3 id,  0.1 wa,  0.0 hi,  0.1 si,  0.0 st 
MiB Mem :   7603.8 total,    248.4 free,   6301.6 used,   2339.2 buff/cache     
MiB Swap:   7847.0 total,   7647.2 free,    199.8 used.   1302.2 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND  
   4228 pkinoti   20   0 1448.5g 513840 137040 S  58.1   6.6   4:06.37 chrome   
   3555 pkinoti   20   0 1452.0g 424644 123072 S  11.0   5.5  11:30.03 code     
   1917 pkinoti   20   0 4959352 176012  75420 S   7.6   2.3   4:40.08 gnome-s+ 
   3510 pkinoti   20   0   49.0g 136488  92652 S   5.6   1.8   3:06.00 code     
   2667 pkinoti   20   0   53.2g 207216 114204 S   5.0   2.7   1:46.05 chrome   
   3458 pkinoti   20   0 1450.2g 233856 159012 S   4.3   3.0   2:09.55 code     
   2617 pkinoti   20   0   53.0g 535340 346220 S   1.7   6.9   1:55.95 chrome   
   3613 pkinoti   20   0 1450.4g 376236 140588 S   1.3   4.8   2:06.03 code     
   2671 pkinoti   20   0   52.5g 150552 112360 S   1.0   1.9   0:28.07 chrome   
     45 root      20   0       0      0      0 S   0.3   0.0   0:01.08 ksoftir+ 
     46 root      20   0       0      0      0 I   0.3   0.0   0:08.93 kworker+ 
    233 root       0 -20       0      0      0 I   0.3   0.0   0:00.17 kworker+ 
    653 root       0 -20       0      0      0 I   0.3   0.0   0:08.71 kworker+ 
   2177 pkinoti   20   0  417092  26008  14352 S   0.3   0.3   0:04.22 ibus-ex+ 
   4113 pkinoti   20   0 1456.0g 335552 131808 S   0.3   4.3   0:34.44 chrome   
  11180 pkinoti   20   0   10532   5944   3696 R   0.3   0.1   0:00.41 top      
      1 root      20   0   24332  15120  10820 S   0.0   0.2   0:01.02 systemd  
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kthreadd 
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_wo+ 
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker+ 
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker+ 
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker+ 
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker+ 
      8 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker+ 
     10 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker+ 
     11 root      20   0       0      0      0 I   0.0   0.0   0:00.78 kworker+ 
     13 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker+ 
     14 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tas+ 
     15 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tas+ 
     16 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tas+ 
     17 root      20   0       0      0      0 S   0.0   0.0   0:00.15 ksoftir+ 
``` 
Explain the output;

### section 1 ; the header 

top - 12:22:17 up  1:30,  1 user,  load average: 0.24, 0.36, 0.36

1. 12:22:17: The exact current time of day.

2. up 1:30: Your computer has been turned on and running for 1 hour and 30 minutes.

3. 1 user: Only one user account (pkinoti) is currently logged into the machine.

4. load average: 0.24, 0.36, 0.36: The work pressure on your CPU over the last 1 minute, 5 minutes, and 15 minutes. Anything under 1.0 means your computer is running smoothly and is not stressed at all.

### section 2 ; Task what the app are doing 

Tasks: 315 total,   2 running, 313 sleeping,   0 stopped,   0 zombie

1. 315 total - There are 315 individual app parts (processes) open right now.

2. 2 running: Only 2 apps are actively calculating data at this exact microsecond (one of them is top itself!).

3. 313 sleeping: 313 apps are sitting quietly in the background, napping until you click on them.

4. 0 zombie: Dead processes that didn't clean up properly. You have zero, which is perfect.

### section 3 ; cpu usage 

%Cpu(s):  7.3 us,  1.5 sy,  0.0 ni, 91.1 id,  0.0 wa,  0.0 hi,  0.1 si,  0.0 st

 * 7.3 us: User apps (like Chrome and VS Code) are using 7.3% of your CPU.

 * 1.5 sy: The background Linux system itself is using 1.5% of your CPU.

 * 91.1 id: Your CPU is 91.1% Idle (relaxing). Your processor has plenty of power to spare.

### Section 4; Memory Usage (RAM & SWAP)

MiB Mem :   7603.8 total,    477.8 free,   6072.5 used,   2152.2 buff/cacheMiB Swap:   7847.0 total,   7647.2 free,    199.8 used.   1531.2 avail Mem

1. 7603.8 total: You have roughly 8 Gigabytes of total RAM memory.

2. 6072.5 used: Your open apps are currently using about 6 Gigabytes of that RAM.

3. 477.8 free / 1531.2 avail Mem: You have about 1.5 Gigabytes of memory left over for opening new things.

4. MiB Swap: Emergency memory on your hard drive. Since your regular RAM is almost full, Linux put a tiny bit of data (199.8 used) into your emergency pool to keep things stable.

### section 5 ; The top apps 

Your apps are sorted automatically by who is using the most CPU power at this exact moment.
 

 # QUESTIONS AND TASKS 

 ## 1. Installation of applications in Debian:

i) How do you install applications on the command line? Install the following applications: gedit, kwrite, vim, rsyslog, xfce4-terminal and Google Chrome.

ii)How does one uninstall an application?
 
 #### Step 1 : Update the package index 

 * Before Installing any program , you must refresh your system knowldge of what software exists online 

```bash
sudo apt update
```
#### Step 2 : Installing Standard Apps (gedit, kwrite, vim, rsyslog, xfce4-terminal)

* The applications are open - source and and already saved inside Debian's official online library. You can install them all at the exact same time. 

```bash
sudo apt install -y gedit kwrite vim rsyslog xfce4-terminal
```
#### Step 3: Install Third-Party Apps (Google Chrome)

* Google chrome is owned by Google so debian is not allowed to keep it in its official open-source warehouse .Hence, we must download it directly from google .

```bash
                                                                             
```
* To verify they have been installed ;

```bash
apt list --installed gedit kwrite vim rsyslog xfce4-terminal google-chrome-stable
```
II) How to uninstall Application 

 a) 

```bash
sudo apt purge -y gedit kwrite vim rsyslog xfce4-terminal google-chrome-stable
```
Explanation 

1. sudo ; Grants administrator permissions to delete system software.  

1. apt purge: Completely uninstalls the applications and destroys all of their system configuration files.

3. -y: Automatically answers "yes" to the confirmation prompt, allowing the uninstallation to run hands-free.

 b) Cleaning up leftover background files 

```bash
sudo apt autoremove -y
```
 c)  To verify they have been deleted 

```bash
apt list --installed gedit kwrite vim rsyslog xfce4-terminal google-chrome-stable
```
## 2. What is a Desktop Environment? Install the following Desktop Environments: KDE Plasma, Cinnamon, Xfce.

* #### Desktop Environment , It is the graphical interface built on top of the core Linux engine. It turns lines of text into visual elements you can click with a mouse

1. ####  KDE Plasma (K Desktop Environment Plasma) , is where you can change the position of every single button and dial. By default, it looks like modern Windows, but you can customize it to look like anything one wants 

2. #### Cinnamon Desktop Environment ,It features a traditional "Start Menu" in the bottom-left corner, a taskbar along the bottom, and clear icons on the desktop. It is designed to make users coming from Windows feel instantly at home.

3. #### Xfce ( X Forms Common Environment ) , It removes flashy animations and heavy visual effects so it can run incredibly fast. It is perfect for old computers or making a new computer lightning fast because it uses very little computer memory (RAM).

### Step 1. Installing them 

* The softwares are organised in packages called Task Packages 

```bash
sudo apt update && sudo apt install -y task-kde-desktop task-cinnamon-desktop task-xfce-desktop
```
Explain ;

1. task-kde-desktop, task-cinnamon-desktop, task-xfce-desktop: These are the specific system names for the bundles. Using the task- prefix ensures you get all the wallpapers, login screens, and default applications made for that specific desktop style.

```bash
ssh pkinoti@test.traccar.quatrixglobal.com
```
2. Create the User Account for Zoe Doe 
 
```bash
sudo adduser zdoe
```
Explaining commands ;

1. Sudo , grands you administrator permission to make system changes 

2. adduser , builds a new user accounts an creates their own home directory

3. adoe , username for Zoe

### Step 2 ; Make zdoe a sudoer administrator

* Adding her to the sudo group so that she can run her own administrative commands .

```bash
sudo usermod -aG sudo zdoe
```

Explaining commands;

1. sudo: Grants you the admin rights needed to modify user accounts.

2. usermod: Short for user modify. This command changes existing user account settings.

     -aG , a means appen (add to) ,G group .Together, they add the user to a new group without removing them from any groups they are already in.

3. sudo , The name of the target group.Hence, anyone in the sudo group gets administrator rights.

4. zdoe: The username of the account we are modifying.

### Step 3: Generate an SSH Key Pair for Zoe using the ECDSA Protocol

```bash
ssh-keygen -t ecdsa -b 521 -C "zoe.doe@example.com"
```
Explaining the commands;

1. sh-keygen -t ecdsa -b 521 -C "..."

ssh-keygen: The tool that generate the keys

* -t ecdsa: Tells the tool to use the ECDSA protocol as requested.

* -b 521: Sets the bit size to 521, making it the strongest and most secure version of an ECDSA key possible.

* -C : "zoe.doe@example.com": Attaches a clear label tag to the key.

### Step 4 : Allow jdoe to access test.traccar.quatrixglobal.com server.

```bash
cat ~/.ssh/id_ecdsa.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```
Explaining the commands ; 

1. cat ~/.ssh/id_ecdsa.pub >> ~/.ssh/authorized_keys

* cat reads the newly created public key 

* (>>) the redirect tool , it copies the text and adds it to the end of a security file called the authorised_keys 

2. chmod 600 ~/.ssh/authorized_keys

* chmod , alters file security permissions 

* 600 Sets the permission level so that only Zoe can read and write to this 
file, and everyone else on the system is strictly blocked.

* why 600 ?. when you set a file to 600, you are breaking it down like this

1. 6 (4 + 2): The Owner (Zoe) has complete permission to Read and Write to the file.

2. 0: The system Group has absolutely no permissions to see or change it.

3. 0: Everyone Else on the computer has no permissions to see or change it.

* where by ; 

1. 4 points = Read permission (ability to open and view the file).

2. 2 points = Write permission (ability to edit or change the file).

3. 1 point = Execute permission (ability to run the file like a program).

4. 0 points = No access at all.1

* Log out of Zoe's profile 

```bash
exit
```
### Step 6: Create Zoe's Account on Your Local PC 

* Ensure youre in the pkinoti@gwekesa 

```bash
sudo adduser zdoe
```

### Step 7: Make Zoe a Sudoer on your Local PC

```bash
sudo usermod -aG sudo zdoe
```
### Step 8: Install the Xfce Desktop Package Locally

* From our profile 

```bash
sudo apt update && sudo apt install -y task-xfce-desktop
```
### Step 9 : Check the system logs and try and locate the login time for user jdoe. Capture the line showing the login action, as well as the 3 lines preceding and after that action.

```bash
sudo journalctl | grep -B 3 -A 3 "session opened for user zdoe"
```
Explain the command ;

1. journalctl: The modern administrator command used to output the system's central log journal database.

2. | (The Pipe): This character takes the massive output stream from journalctl and sends it directly into the next command as input.

3. grep -B 3 -A 3 "...": Sifts through the incoming stream to locate the phrase "session opened for user zdoe". Once found, it prints that line, along with the 3 lines before it and the 3 lines after it.

### Step 10 : Your supervisor has now informed you that Jane Doe is leaving the organization. Your supervisor insists that Jane Doe's account be deleted including her home directory on the local machine. On the test.traccar server, her home user account directory should be preserved, but she should no longer be able to ssh into the server.

* DELETING ZOE'S ACCOUNTS ;

In local PC

* Make sure your terminal prompt is pkinoti@gwekesa:~$

```bash
sudo deluser --remove-home zdoe
```
* In the Remote server 

```bash
ssh pkinoti@://quatrixglobal.com
```
the prompt should change to ; pkinoti@test-traccar:~$ 

```bash
sudo deluser zdoe
sudo passwd -l zdoe
```


Explain the commands ;

1. sudo deluser zdoe successfully detached her account from the server's user

registry.

2. sudo passwd -l zdoe completely locked out her account credentials,

ensuring that any future SSH connection attempts will be instantly blocked 

by the system

#### 10. Free Memory & Disk space:
* How can one check free and used memory (RAM) on a Linux PC? What is the 

status of memory of your Linux PC right now?

* How much used disk space do you have on your Linux PC?

* For the above two tasks, how can you view this information in Gigabytes as 

opposed to plain bytes?

#### 1. Checking RAM Usage

```bash
free
```
#### 2. Checking Disk Space Usage

```bash
df
```
* This lists all active, mounted storage pools, displaying their individual

 storage thresholds, utilized blocks, and overall capacity flags

#### 3. Viewing Information in Gigabytes

```bash
df -h
```
#### 12.

### Step 1: Install Nginx

```bash
sudo apt update && sudo apt install nginx -y
```
### Step 2: Create the Web Root Folder

```bash
sudo mkdir -p /var/www/html/pkinoti
```

### Step 3: Create the index.html File

* We will create a basic HTML file inside your new folder using the text 

editor nano

* Open the file editor 

```bash
sudo nano /var/www/html/pkinoti/index.html
```
inside the editor and this text

```bash
<html>
    This is my webpage.
</html>
```
### Step 4: Create the Nginx Configuration File

```bash
sudo nano /etc/nginx/sites-available/local.pkinoti.conf
```

```bash
server {
     server_name local.pkinoti;
     root /var/www/html/pkinoti;
     index index.html;

     access_log  /var/log/nginx/local.pkinoti.access.log;
     error_log  /var/log/nginx/local.pkinoti.error.log;

     location / {
         try_files $uri /index.html =404;
     }
}
```

### Step 5: Create a Symlink

* We will create a shortcut from the sites-available folder into the 

sites-enabled folder so Nginx actually reads your configuration.

```bash
sudo ln -s /etc/nginx/sites-available/local.pkinoti.conf /etc/nginx/sites-enabled/local.pkinoti.conf
```
Explain the command;

1. ln -s: Creates a symbolic link (a shortcut pointer)

2. The first path is the original source file.

3. The second path is where the shortcut will be placed

### Step 6: Update the Hosts File

* We will edit your computer's local "address book" (/etc/hosts) to point 

your domain name directly to your own machine (127.0.0.1).

* To open the hosts file ;

```bash
sudo nano /etc/hosts
```

```bash
127.0.0.1 local.pkinoti
```
#### ON YOUR WEB BROWER NOW TYPE 

* local.pkinoti 

### Step 7: Restart Nginx Service

* We need to restart Nginx so it reads our newly added configuration files.

```bash
sudo systemctl restart nginx
```

# QUESTIONS

## Question 1. What is Nginx

* It is a web server that listens to the user request which is (This is my  

  web page) and displays the right files back to them 

* It is a local web server for testing webs it runs directly on your pc as a

  local testing environment.

##  Question 2 ; Why is the purpose of the folder you created under /var/www...?

* #### You hit the nail on the head again! Because the server is constantly running and modifying data, /var is the dedicated, safe zone designed for files that change while the computer is active.

## Question 3: What do the two folders sites-available and sites-enabled help accomplish

* #### sites-available folder holds all your website configuration files. Even if a website is offline, broken, or under construction, its configuration file stays safe in here. It does nothing; Nginx ignores it.

* #### sites-enabled This folder only contains the websites you want to be live and active right now. Nginx only reads this folder.

## Question 4: What is a symlink?

* #### symlink (symbolic link) is a digital shortcut. It is just like a desktop shortcut on Windows . It is a tiny file that does not contain your actual configuration, but simply points directly to the real file located over in sites-available.


## Question 5: What is the hosts file used for? Name at least 2 uses.

* It helps the computer find the location of a domain right on your own PC   instead of looking on the internet.

 common uses ;

1. Local development , it lets you create fake webiste names so that we can 

   build and test website locally before launching them into the real world 

2. Blocking websites , it blockes harmful websites 

## Question 6: What is the difference between service and systemctl?

* systemctl the modern control tool used to manage background workers (called 

  "services") in Linux.

* service  This is an older tool used in older versions of Linux to start and 

  stop programs had fewer features.

## Question 7: What is the difference between restart and reload within the context of a service?

* #### restart (The hard reset): This completely shuts down the Nginx process and kills all current connections, then turns it back on from scratch. If a user is actively downloading a file on your website when you run this, their connection breaks and they see an error screen.

* #### reload (The live update): This does not shut down the server. Nginx stays online and keeps serving current users perfectly. It simply reads the new configuration file in the background and applies the changes instantly without any downtime.

## Question 8: If we edit the index.html file and add some content, do we need to restart, reload anything, or do something else to view the changes?

* #### Nginx only needs a reload or restart if you change its configuration rules (like changing the website name or switching folders) because it reads those rules only once when it boots up.So, if you edit the text in index.html, Nginx will automatically grab theupdated version the very next second someone loads the page or refeshes the page.

# 13. postgres - (On your local PC):

1. Install latest Postgres version supported by Debian (or Fedora).

2.  Explain the following:

* The purpose of pg_hba.conf file. Where is it located?

* Where are postgresql database server logs located?

* How many types of authentication methods does postgresql offer?

### Step 1: Install PostgreSQL

```bash
sudo apt update && sudo apt install postgresql postgresql-contrib -y
```
Explain the command;

1. postgresql: Installs the core PostgreSQL database server.

2. postgresql-contrib: Installs additional popular tools and extended functionalities for Postgres

## Question 1: What is the purpose of the pg_hba.conf file, and where is it located?

* The name pg_hba stands for PostgreSQL Host-Based Authentication.

* It acts as a firewall rulebook that decides who is allowed to connect to your database. Every time a program or a user tries to log in, Postgres checks this file to see:

## Question 2 ; Where is it located ?

```bash
sudo find /etc/postgresql/ -name pg_hba.conf
```
* its in the /etc because, /etc is the universal warehouse in Linux strictly reserved for configuration files and system settings.

* Since pg_hba.conf is a text file filled with security settings, rules, and instructions for how the PostgreSQL program should behave, the Linux operating system forces it to live inside /etc to keep everything perfectly organized.

## Question 3. Where are postgresql database server logs located?

* /var being the place for files that change constantly while the computer runs. Database logs are text files that record every single error, connection, and query live as they happen.

* Because logs change and grow every second, they live inside the /var/log directory.

```bash
ls /var/log/postgresql/
```
## Question 4: How many types of authentication methods does PostgreSQL offer?

## PEER AUTHENTIFICATION METHOD; 

* It looks at who you are logged into your computer as right now. If your Ubuntu username is pkinoti, Postgres will automatically let you into the database user named pkinoti without asking for a password, because the operating system already verified your identity.

## Step 1: Log Into PostgreSQL for the First Time

```bash
sudo -i -u postgres psql
```
Explain the command ; 

1. sudo -i -u postgres: Switches your terminal session to act as the postgres administrator user.

2. psql: Opens the interactive PostgreSQL terminal screen

## Step 2: See Your Database Version and Databases

* Type this exact command into your postgres=# prompt and hit

```bash
\l
```

* It prints out a table listing all the default databases currently created on your system (like postgres, template0) 

## Step 3: Exit the Postgres 

```bash
\q
```

## TRUST AUTHENTIFICATION 

* This means "no password required." PostgreSQL blindly trusts anyone who connects. This is highly dangerous and should only be used for quick local testing on your own PC.

```bash
sudo nano /etc/postgresql/*/main/pg_hba.conf
```

* CHANGE THIS TO ;

ALT + /  -  TO VIEW THE BOTTOM TEXT 


```bash
# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
```

THIS ;


```bash
host    all             all             127.0.0.1/32            trust
```

* To verify ; 

Tell Postgres to read the changes (Reload)

```bash
sudo systemctl reload postgresql
```
* Test the trust connection ;

```bash
psql -h 127.0.0.1 -U postgres
```
* postgres=# prompt immediately

# 14. ufw - (On your local PC):

* Install ufw

* Ensure that SSH, HTTP and HTTPS ports are accessible and NO others.

* Enable ufw

## Step 1: Install UFW

```bash
sudo apt update && sudo apt install ufw -y
```
* To enable the ufw 

```bash
sudo ufw enable
```
# 15. Fail2ban 

* Fail2ban acts like an automated security guard that reads your system logs and dynamically locks out malicious actors.

## Step 1: Install Fail2ban

```bash
sudo apt update && sudo apt install fail2ban -y
```
## Step 2: Create the jail.local Copy

* Now we need to make your personal scratchpad configuration file (jail.local) by copying the factory default file (jail.conf). This ensures system updates won't overwrite your custom settings later.

```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```
## Step 3: Open the File and Edit the SSH Section

* Now we will open your new jail.local file and change the default SSH settings to be highly aggressive against attackers.

```bash
sudo nano /etc/fail2ban/jail.local
```
After the text editor is open ;

1. Press CTRL + W 

2. Type [sshd] and press Enter.

3. Your cursor will jump directly to the SSH security block.

* Underneath sshd put this text ;

```bash
[sshd]

# To use more aggressive sshd modes set filter parameter "mode" in jail.local:
# normal (default), ddos, extra or aggressive (combines all).
# See "tests/files/logs/sshd" or "filter.d/sshd.conf" for usage example and details.
mode   = aggressive
maxretry = 2
findtime = 24h
bantime = 196h
port    = ssh
logpath = %(sshd_log)s
backend = %(sshd_backend)s
```

* Afterwards ;

1. ctrl + 0 then enter

2. ctrl + X

## Step 4: Create the Custom Website Filter File

* We will create a brand new file inside Fail2ban's filter.d folder specifically to define what a bad website visitor looks like.

```bash
sudo nano /etc/fail2ban/filter.d/nginx-brute.conf
```
* Inside the text editor ; 

```bash
[Definition]

failregex =  ^<HOST> .* "(GET|POST|PUT|POST) .*(\.env|xmlrpc|\.asp|ab2g|ab2h|\.yml|git).*$
             ^<HOST> .* "(GET|POST|PUT|POST) /(\.[a-zA-Z0-9]+|.*/\.[a-zA-Z0-9]+).*$
             ^<HOST> .* "(GET|POST) .*robot.*\ 404\ .*$

ignoreregex = .*\.well.*
              .*/wp-json/wc/v3/system_status.*
```

## Step 5: Add to the Website Jail Configuration 

* We will open your jail.local file again, jump right to the bottom, and drop in the instructions that tell Fail2ban to enforce bans for your custom website rules.

```bash
sudo nano /etc/fail2ban/jail.local
```
Inside the text editor do ;

1. alt + / to jump the cursor to the last line 

2. enter to create a clean empty space 

3. past this new config block at the bottom 

```bash
[nginx-brute]
enabled  = true
port     = http,https
logpath = %(nginx_access_log)s
bantime = 96h
maxretry = 2
findtime = 24h
```
## Step 6: Restart the Fail2ban Service

* After all the configuration file are ready , we just need to restart Fail2ban so it reads the brand-new settings and active filters.

```bash
sudo systemctl restart fail2ban
```
## Step 7: Watch the Fail2ban Logs Live

```bash
sudo tail -n 20 -f /var/log/fail2ban.log
```
## Step 8 :

```bash
sudo fail2ban-client status sshd
```
* To check who is trying to hack your web server or website

```bash
sudo fail2ban-client status nginx-brute
```
* To check who is trying to hack your admin command line SSH 

## Step 7 ; How to test the filter 

* Using .env file 



```bash
sudo fail2ban-regex '192.168.1.50 - - "GET /.env HTTP/1.1" 404' /etc/fail2ban/filter.d/nginx-brute.conf
```

1. sudo fail2ban-regex : This activates Fail2Ban's built-in testing tool

2. '192.168.1.50 - - "GET /.env HTTP/1.1" 404': This is a piece of fake log data that mimics a malicious request. It tells the simulator

3. /etc/fail2ban/filter.d/nginx-brute.conf: This points the simulator to the custom rules file we created

Expected Output ;

```bash
Running tests
=============

Use      filter file : nginx-brute, basedir: /etc/fail2ban
Use      single line : 192.168.1.50 - - "GET /.env HTTP/1.1" 404


Results
=======

Failregex: 2 total
|-  #) [# of hits] regular expression
|   1) [1] ^<HOST> .* "(GET|POST|PUT|POST) .*(\.env|xmlrpc|\.asp|ab2g|ab2h|\.yml|git).*$
|   2) [1] ^<HOST> .* "(GET|POST|PUT|POST) /(\.[a-zA-Z0-9]+|.*/\.[a-zA-Z0-9]+).*$
`-

Ignoreregex: 0 total

Date template hits:

Lines: 1 lines, 0 ignored, 1 matched, 0 missed
[processed in 0.01 sec]
```

Explanation ;

1. The Threat Matches (Failregex: 2 total)

* The first one spotted the forbidden word .env inisde the request and triggered the match 

* The second one recognizes that someeone wa trying to access the hidden files starting with a dot and triggered a match 

* 1 lines: The engine processed the 1 fake log line you provided.

* 1 matched: The security engine successfully isolated the attacker's IP address (192.168.1.50) and flagged it for a ban.

* 0 missed: The engine did not let the threat slip through undetected.

##### Other bad files 

1. .git/ — Exposes your entire source code history and secret access tokens.

2. config.php.bak / wp-config.php.old — Contains plain-text database usernames and passwords.

3. dump.sql / backup.zip / db.sql — Downloads your entire database structure and user data.