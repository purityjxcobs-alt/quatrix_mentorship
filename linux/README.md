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

* Using .env file - It stands for Environment , this file contains your private database passwords and secret encryption keys and the only people typing ://yourwebsite.com into a browser are automated hacker bots. They are fishing for misconfigured servers where the administrator accidentally left this file publicly downloadable 

* To view the ngnix log file for .env 

```bash
sudo grep ".env" /var/log/nginx/access.log
```

```bash
sudo fail2ban-regex '192.168.1.50 - - "GET /.env HTTP/1.1" 404' /etc/fail2ban/filter.d/nginx-brute.conf
```

1. sudo fail2ban-regex : This activates Fail2Ban's built-in testing tool

2. '192.168.1.50 - - "GET /.env HTTP/1.1" 404': This is a piece of fake log data that mimics a malicious request. It tells the simulator

3. /etc/fail2ban/filter.d/nginx-brute.conf: This points the simulator to the custom rules file we created

4. - - "GET /.env : This is the malicious action the bot actively requesting to view and download your secrect file

5. 404 : This is the web defense web servers defence . it means the server responsed with a not found error code 

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


# NOTES 


##  8. Linux System Administration & Configuration

This section covers core Linux administrative procedures, including package management variations, user authorization policies, system architecture diagnostic utilities, and network debugging tools.


###  Repository & Package Management

Linux distributions handle software maintenance through standardized command-line tools. The command structures differ based on the underlying operating system family tree:

#### **Debian / Ubuntu Systems (`apt`)**
*   **Command:** `sudo apt update`
    *   *Explanation:* Connects to remote repositories and pulls down the **latest indexed list** of available packages and versions. It does not upgrade software; it updates the local index database.
*   **Command:** `sudo apt full-upgrade`
    *   *Explanation:* Downloads and installs available package updates. It handles changing system dependencies intelligently, removing obsolete packages or installing new ones if required.
*   **Command:** `sudo apt install <package_name>`
    *   *Explanation:* Downloads, resolves dependencies for, and installs a specific software package (e.g., `sudo apt install vim tree curl`).

#### **Fedora / RHEL / CentOS Systems (`dnf`)**
*   **Command:** `sudo dnf check-update`
    *   *Explanation:* Scans remote Red Hat or Fedora repositories to check for available software upgrades.
*   **Command:** `sudo dnf upgrade`
    *   *Explanation:* Downloads and installs all system and software upgrades across the operating system environment.
*   **Command:** `sudo dnf install <package_name>`
    *   *Explanation:* Installs targeted application packages via Red Hat repository mirrors.

---

###  B. Advanced User Management & Security

#### **1. Creating User Profiles**
*   **Command:** `sudo adduser jdoe`
    *   *Explanation:* Creates a new user profile on the system. It handles several background administrative steps automatically: adding a home directory at `/home/jdoe`, creating a matching user group, and prompting for account password configuration.

#### **2. Mandatory Password Expiration Policy**
*   **Command:** `sudo chage -d 0 jdoe`
    *   *Explanation:* Modifies the password aging data for the user. Setting the date of the last password change to zero (`-d 0`) tricks the security engine into evaluating the password as immediately expired. **This forces the user to choose a new password on their very next terminal or SSH login.**

#### **3. Escalating Sudo Privileges**
*   **Command:** `sudo usermod -aG sudo jdoe`
    *   *Explanation:* Modifies user attributes. The `-aG` flags mean **Append to Group**. This appends user `jdoe` to the system's `sudo` group, granting them administrative execution rights without stripping them of existing group permissions.

---

###  C. Hardware & File System Diagnostics

#### **1. Verifying Connected Disk Hardware**
*   **Command:** `lsblk`
    *   *Explanation:* **List Block Devices.** Outputs a visual tree chart showing all active hard drives, solid-state drives, partitions, USB flash nodes, and optical ROM devices connected to the computer, along with their size and system mount points.
*   **Command:** `dmesg`
    *   *Explanation:* **Display Message.** Dumps the kernel's internal ring buffer log messages. It is highly valuable for real-time hardware diagnostics; plugging in a USB drive or an external disk will immediately print physical connection logs and error warnings to the bottom of this text log stream.

#### **2. Synchronizing Written Data Blocks**
*   **Command:** `sync`
    *   *Explanation:* Forces the operating system to flush all cached data currently residing in temporary system RAM straight down onto physical storage hard drives or flash layers. **Always run this command after using disk-writing utilities like `cp` or `dd` to build bootable media before safely removing a USB stick.**

---

###  D. Network Configuration & Diagnostics

#### **1. Downloading Web Files and API Auditing**
*   **Command:** `wget -c <URL>`
    *   *Explanation:* A dedicated file downloading engine. The `-c` flag enforces a **continue/resume** protocol; if the network connection breaks mid-download, re-running the command picks up exactly where it failed instead of starting over.
*   **Command:** `curl -fsSL <URL> | sh`
    *   *Explanation:* A multi-protocol data delivery agent. The flags specify: fail silently on server errors (`-f`), hide progress bars (`-s`), show error text if failure occurs (`-S`), and follow web redirects (`-L`). This command pulls an install script down from the internet and passes it via a pipe (`|`) to `sh` to execute the code instantly.

#### **2. Interactive Service Selection Configurator**
*   **Command:** `sudo update-alternatives --config editor`
    *   *Explanation:* On systems containing multiple software options serving the same role (e.g., having `nano`, `vi`, and `vim` installed simultaneously), this opens an interactive console selection menu. It allows administrators to define which program opens as the default global choice when applications trigger standard utility routines.

---

## 9. Linux File System Hierarchy & Essential Commands

###  Directory Structures Explained

*   **`/` (Root):** The foundational top-level directory containing all files, folders, and mounted devices.
*   **`/etc`:** Houses host-specific, system-wide configuration files and startup scripts.
*   **`/tmp`:** Stores volatile temporary files that are wiped automatically upon system reboot.
*   **`/var`:** Contains variable, changing data files such as logs (`/var/log`) and transient web application data.
*   **`/bin` & `/sbin`:** `/bin` holds essential user binaries for system boot/repair, while `/sbin` holds vital system administration tools requiring root access.
*   **`/usr` & `/usr_local`:** `/usr` holds OS-distributed resources and read-only data, whereas `/usr/local` is reserved for manually installed local applications.
*   **`/home` & `/root`:** `/home` contains isolated storage directories for standard users, while `/root` is the exclusive home directory for the superuser.
*   **`/srv`, `/opt`, `/run`, `/mnt`:** Respectively used for site service operational data (`/srv`), optional third-party software (`/opt`), volatile runtime process data (`/run`), and temporary manual mount points (`/mnt`).

---

### Operational Matrix & Privilege Escalation

*   **`/usr` vs `/usr/local`:** `/usr` is managed entirely by official system package managers, whereas `/usr/local` is safe from package manager overwrites and used for manual compiling.
*   **`bin` vs `sbin` distinctions:** Standard binaries versus system maintenance binaries.
*   **Root User & Commands:** The root user is the absolute superuser. `sudo` temporarily elevates standard users to execute administrative commands, while `su` switches the shell context to a different user or root.

---

##  10. Application & User Account Infrastructure Workflow

###  Debian Application Management & Offboarding

*   **Application Installation & Removal:** Managed via `apt update` and `apt install` for packages like `gedit`, `kwrite`, `vim`, `rsyslog`, and `xfce4-terminal`. External repositories like Google Chrome require manual key and source list setup. Applications are removed via `sudo apt remove` or fully purged via `sudo apt purge`.
*   **Desktop Environments:** Graphical interface suites like KDE Plasma, Cinnamon, and Xfce can be installed via package tasks.
*   **User Provisioning (`jdoe`):** Created with `sudo adduser`, added to sudoers, and configured with local ECDSA keys via `ssh-keygen -t ecdsa`. Terminal customization uses Oh-My-Zsh and Powerlevel9k themes.
*   **Auditing & Offboarding:** Login times are traced via `sudo grep` on `/var/log/auth.log`. For offboarding, local accounts are removed with `sudo deluser --remove-home jdoe`, while remote server accounts are locked and restricted using `passwd -l` and `chsh -s /usr/sbin/nologin`.


##  11. Debian Repository Configuration (`sources.list`)

###  Concept Breakdown

#### **The `/etc/apt/sources.list` File**
This configuration file serves as the **central repository index** for the `apt` package manager. It tells your operating system exactly where to fetch software, dependencies, and system security fixes over the web.

#### **Structural Line Syntax**
Every configuration row inside the file is mapped out into four essential fields:
`[Type] [Repository URL] [Distribution Release Name] [Component Categories]`

*   **Type:** 
    *   `deb`: Pre-compiled binary installation packages.
    *   `deb-src`: Raw, uncompiled package source code files.
*   **Repository URL:** The host mirror address holding the software database.
*   **Distribution:** Matches your operating system release code name (e.g., `bookworm` for Debian 12, `trixie` for Debian 13).
*   **Component Categories:**
    *   `main`: Completely free, officially supported open-source software.
    *   `contrib`: Free software requiring non-free components to compile or run.
    *   `non-free`: Proprietary software.
    *   `non-free-firmware`: Proprietary device drivers needed to support physical hardware components.

#### **Repository Segregation (The Different Lines)**
*   **Base:** Contains core stable packages frozen at the release date of the operating system version.
*   **Security (`-security`):** Delivers rapid mitigation patches for severe security threats and software vulnerabilities.
*   **Updates (`-updates`):** Distributes non-critical stability adjustments for long-term production setups.
*   **Backports (`-backports`):** Introduces modern package features ported from testing branches onto current production systems.

#### **The `/etc/apt/sources.list.d/` Directory**
A modular extension workspace. Rather than altering your primary system file, standalone custom source files (terminating in `.list`) are placed inside this folder to safely configure third-party software platforms (e.g., Google Chrome, Docker, Nginx).



---

##  12. Task Automation using Cronjobs

###  Concept Breakdown

#### **What is a Cronjob?**
A **cronjob** is an automated task scheduled to run in the background at fixed intervals or specific times. The service is managed by the system's `cron` daemon, making it highly effective for recurring tasks like backups, system cleanups, and log generation.

#### **Managing Crontabs**
*   **View current user cronjobs:**
    ```bash
    crontab -l
    ```
*   **Edit current user cronjobs:**
    ```bash
    crontab -e
    ```
*   **View another user's cronjobs (Administrative):**
    ```bash
    sudo crontab -u username -l
    ```

---

###  Practice Exercise Solution

**Objective:** Automatically generate a log message in `/tmp` every single morning at 9:00 AM.

**Crontab Configuration Line:**
```text
0 9 * * * echo "Good morning, Systems are up and running! - $(date)" >> /tmp/systems_status.log
```

#### **Execution Schedule Analysis:**
*   **`0`**: Minute field (00)
*   **`9`**: Hour field (9:00 AM using 24-hour formatting)
*   **`*`**: Day of Month field (Every single day)
*   **`*`**: Month field (Every month of the year)
*   **`*`**: Day of Week field (Every day from Sunday through Saturday)
*   **`>>`**: The **append operator** ensures that new morning messages are written to the bottom of the log file without destroying historical tracking entries.


# Notes 

# Linux Module — Complete Study Guide

> A full walkthrough of the Linux module as a subject: concepts, architecture, filesystem, commands, and administration.
> Copy into VS Code or GitHub as your notes.

---

## Table of Contents

1. [What is Linux?](#1-what-is-linux)
2. [Linux Architecture](#2-linux-architecture)
3. [Linux Distributions](#3-linux-distributions)
4. [The Shell](#4-the-shell)
5. [Filesystem Hierarchy Standard (FHS)](#5-filesystem-hierarchy-standard-fhs)
6. [File Types in Linux](#6-file-types-in-linux)
7. [File & Directory Commands](#7-file--directory-commands)
8. [File Permissions](#8-file-permissions)
9. [Users and Groups](#9-users-and-groups)
10. [Process Management](#10-process-management)
11. [Package Management](#11-package-management)
12. [Disk & Filesystem Management](#12-disk--filesystem-management)
13. [Networking Basics](#13-networking-basics)
14. [System Information Commands](#14-system-information-commands)
15. [Text Editors](#15-text-editors)
16. [Environment Variables & Shell Configuration](#16-environment-variables--shell-configuration)
17. [Archiving & Compression](#17-archiving--compression)
18. [Boot Process](#18-boot-process)
19. [Systemd & Services](#19-systemd--services)
20. [Scheduling (cron/at)](#20-scheduling-cronat)
21. [Logging & Monitoring](#21-logging--monitoring)
22. [Links: Hard vs Symbolic](#22-links-hard-vs-symbolic)
23. [Security Basics](#23-security-basics)
24. [Scenario-Based Questions](#24-scenario-based-questions)
25. [Quick Reference Cheat Sheet](#25-quick-reference-cheat-sheet)

---

## 1. What is Linux?

**Linux** is a free, open-source, Unix-like operating system kernel created by **Linus Torvalds** in 1991.

**Key points:**

- Linux is **not** a full OS by itself — it's a **kernel**.
- A full OS using Linux = **GNU/Linux** (kernel + GNU tools + utilities + package manager + shell).
- It is **multi-user**, **multitasking**, **portable**, and **secure**.
- Source code is freely available under the **GPL** license.
- Runs on servers, desktops, mobile (Android), embedded devices, supercomputers.

**Q: Who created Linux and when?**
Linus Torvalds, 1991.

**Q: What does "open source" mean?**
The source code is freely available to view, modify, and redistribute.

**Q: What does "multi-user" mean?**
Multiple users can log in and use the system at the same time.

**Q: What does "multitasking" mean?**
Multiple processes can run simultaneously.

---

## 2. Linux Architecture

Linux is layered:

```
+-------------------------------------+
|          User Applications          |   ← browsers, editors, etc.
+-------------------------------------+
|       Shell (bash, zsh, sh)         |   ← interprets user commands
+-------------------------------------+
|    System Libraries (glibc, etc.)   |   ← APIs for programs
+-------------------------------------+
|        System Call Interface        |   ← bridge user ↔ kernel
+-------------------------------------+
|             Kernel                  |   ← core: memory, CPU, devices
+-------------------------------------+
|             Hardware                |   ← CPU, RAM, disks, NIC
+-------------------------------------+
```

**Layers explained:**

| Layer | Role |
|-------|------|
| Hardware | Physical components (CPU, RAM, disk, network) |
| Kernel | Manages hardware, memory, processes, filesystems, devices |
| System calls | Interface programs use to ask the kernel to do something |
| Libraries | Ready-made functions (glibc, libc) |
| Shell | Command interpreter (bash, sh, zsh) |
| Applications | Programs the user runs (vim, firefox, python) |

**Kernel responsibilities:**

- Process management (scheduling, creation, termination)
- Memory management (RAM, virtual memory, swap)
- Device management (drivers)
- File system management
- Networking
- Security (users, permissions)

**Q: What are the main components of Linux?**
Kernel, shell, filesystem, utilities, applications.

**Q: What is the difference between kernel and shell?**

| Kernel | Shell |
|--------|-------|
| Core of the OS | User interface to the OS |
| Runs in kernel space | Runs in user space |
| Manages hardware | Interprets user commands |
| Invisible to user | Visible (terminal prompt) |

---

## 3. Linux Distributions

A **distribution (distro)** = Linux kernel + GNU tools + package manager + desktop environment + applications.

**Common families:**

| Family | Base | Package Manager | Examples |
|--------|------|-----------------|----------|
| Debian | Debian | `apt`, `dpkg` | Ubuntu, Mint, Kali |
| Red Hat | RHEL | `yum`, `dnf`, `rpm` | Fedora, CentOS, Alma |
| Arch | Arch | `pacman` | Manjaro, EndeavourOS |
| SUSE | SUSE | `zypper` | openSUSE |
| Gentoo | Gentoo | `portage` | Gentoo |

**Q: What is the difference between a distro and the kernel?**
The kernel is the core; a distro bundles the kernel with tools, package managers, and apps.

**Q: Which distro is most common on servers?**
Ubuntu Server, Debian, RHEL/CentOS.

**Q: Which distro is common for penetration testing?**
Kali Linux, Parrot OS.

---

## 4. The Shell

The **shell** is a program that reads commands from the user and passes them to the kernel.

**Common shells:**

| Shell | Path | Description |
|-------|------|-------------|
| `sh` | `/bin/sh` | Original Bourne shell |
| `bash` | `/bin/bash` | Bourne Again Shell (default on most Linux) |
| `zsh` | `/bin/zsh` | Extended, popular with developers |
| `ksh` | `/bin/ksh` | Korn shell |
| `csh`/`tcsh` | `/bin/csh` | C shell |

**Check your shell:**

```bash
echo $SHELL
```

**Change shell:**

```bash
chsh -s /bin/zsh
```

**Shell prompt** usually shows: `username@hostname:current_directory$`

- `$` = normal user
- `#` = root user

**Shell types:**

- **Login shell** — opened when you log in
- **Interactive shell** — accepts typed commands
- **Non-interactive shell** — runs scripts

**Q: What is a shell?**
A command interpreter that reads commands and executes them via the kernel.

**Q: Which shell is default on most Linux?**
Bash.

---

## 5. Filesystem Hierarchy Standard (FHS)

Linux organizes files in a single tree starting from **`/`** (root).

| Directory | Purpose |
|-----------|---------|
| `/` | Root of the filesystem |
| `/bin` | Essential user binaries (`ls`, `cp`, `mv`) |
| `/sbin` | System binaries (`fdisk`, `mkfs`) |
| `/etc` | Configuration files |
| `/home` | User home directories (`/home/alice`) |
| `/root` | Root user's home directory |
| `/tmp` | Temporary files (cleared on reboot) |
| `/var` | Variable data (logs, spool, cache) |
| `/usr` | User programs, libraries, docs |
| `/lib` | Shared libraries |
| `/opt` | Optional add-on software |
| `/mnt` | Temporary mount points |
| `/media` | Removable media (USB, DVD) |
| `/dev` | Device files (`/dev/sda`, `/dev/null`) |
| `/proc` | Process & kernel info (virtual) |
| `/sys` | Kernel & hardware info (virtual) |
| `/boot` | Bootloader files (kernel, initrd) |
| `/srv` | Data served by system (web, ftp) |

**Q: What is `/etc` for?**
System-wide configuration files.

**Q: Where are user home directories stored?**
`/home/<username>` (except root, which is `/root`).

**Q: Difference between `/bin` and `/usr/bin`?**
Traditionally `/bin` had essential boot binaries; `/usr/bin` had user programs. On modern systems they're often merged.

**Q: What is `/proc`?**
A virtual filesystem exposing kernel and process info.

```bash
cat /proc/cpuinfo
cat /proc/meminfo
```

**Q: What is `/dev/null`?**
A special file that discards everything written to it ("bit bucket").

---

## 6. File Types in Linux

Everything in Linux is a file. There are **7 types**:

| Type | Symbol (in `ls -l`) | Example |
|------|---------------------|---------|
| Regular file | `-` | `notes.txt`, `script.sh` |
| Directory | `d` | `/home`, `/etc` |
| Symbolic link | `l` | `mylink -> /etc/passwd` |
| Character device | `c` | `/dev/tty`, `/dev/null` |
| Block device | `b` | `/dev/sda`, `/dev/sdb1` |
| Named pipe (FIFO) | `p` | created with `mkfifo` |
| Socket | `s` | created by processes |

**Check file type:**

```bash
ls -l
file myfile
stat myfile
```

**Q: How do you know a file is a directory from `ls -l`?**
The first character is `d`.

**Q: What is a device file?**
A file that represents a hardware device.

---

## 7. File & Directory Commands

### 7.1 Navigation

| Command | Purpose |
|---------|---------|
| `pwd` | Print working directory |
| `cd /path` | Change directory |
| `cd ~` | Go home |
| `cd -` | Previous directory |
| `cd ..` | Parent directory |
| `ls` | List files |
| `ls -la` | Long format, all files |

### 7.2 Creating

| Command | Purpose |
|---------|---------|
| `touch file.txt` | Create empty file / update timestamp |
| `mkdir folder` | Create directory |
| `mkdir -p a/b/c` | Create parent directories |

### 7.3 Copying, moving, deleting

| Command | Purpose |
|---------|---------|
| `cp src dst` | Copy file |
| `cp -r src dst` | Copy directory |
| `cp -v` | Verbose |
| `cp -i` | Interactive |
| `cp -p` | Preserve permissions |
| `mv src dst` | Move or rename |
| `rm file` | Delete file |
| `rm -r folder` | Delete directory |
| `rm -rf folder` | Force delete (no prompt) |
| `rmdir folder` | Delete **empty** directory |

### 7.4 Viewing files

| Command | Purpose |
|---------|---------|
| `cat file` | Print entire file |
| `less file` | Scrollable view |
| `more file` | Older pager |
| `head file` | First 10 lines |
| `head -n 5 file` | First 5 lines |
| `tail file` | Last 10 lines |
| `tail -f log` | Follow a growing file |
| `wc file` | Count lines, words, chars |
| `file name` | Show file type |
| `stat file` | Detailed file info |

### 7.5 Searching inside files

| Command | Purpose |
|---------|---------|
| `grep "pattern" file` | Search text |
| `grep -i` | Case-insensitive |
| `grep -r` | Recursive |
| `grep -v` | Invert |
| `grep -n` | Line numbers |
| `grep -c` | Count |

### 7.6 Locating files

| Command | Purpose |
|---------|---------|
| `find / -name "file"` | Search by name |
| `find . -iname "*.txt"` | Case-insensitive |
| `find . -type f -size +1M` | By size |
| `which ls` | Path of a command |
| `whereis ls` | Binary + man + source |
| `locate file` | Fast DB-based search |
| `updatedb` | Update locate DB |

**Q: Difference between `find` and `locate`?**
`find` searches in real time; `locate` uses a prebuilt database (faster but can be stale).

---

## 8. File Permissions

Every file has **three permission groups** and **three permission types**.

### Groups

| Group | Who |
|-------|-----|
| `u` | Owner |
| `g` | Group |
| `o` | Others |
| `a` | All |

### Types

| Symbol | Meaning | Value |
|--------|---------|-------|
| `r` | Read | 4 |
| `w` | Write | 2 |
| `x` | Execute | 1 |
| `-` | None | 0 |

### Example

```
-rwxr-xr--
 │└┬┘└┬┘└┬┘
 │ │  │  └── others: r--  (4)
 │ │  └───── group:  r-x  (5)
 │ └──────── owner:  rwx  (7)
 └────────── type:   regular file
```

Octal: `754`.

### Changing permissions

```bash
chmod 755 file.sh         # rwxr-xr-x
chmod 644 file.txt        # rw-r--r--
chmod +x script.sh        # add execute
chmod -w file.txt         # remove write
chmod u+x,g+r file.txt    # symbolic
```

### Changing ownership

```bash
chown user file.txt
chown user:group file.txt
chown -R user:group folder/
```

### `umask`

Default permissions are calculated by removing `umask` bits.

- Default umask: `022`
- Files: `666 - 022 = 644`
- Directories: `777 - 022 = 755`

```bash
umask
umask 027
```

**Q: What does `chmod 777` do?**
Gives read, write, execute to everyone (rarely safe).

**Q: Difference between `chmod` and `chown`?**
`chmod` changes permissions; `chown` changes ownership.

**Q: Why can't a normal user write to `/etc`?**
Because `/etc` is owned by root and permissions deny write access to others.

---

## 9. Users and Groups

Linux is **multi-user**: each user has an account with a UID, home directory, and shell.

### User files

| File | Purpose |
|------|---------|
| `/etc/passwd` | Usernames, UIDs, homes, shells |
| `/etc/shadow` | Encrypted passwords (root only) |
| `/etc/group` | Group definitions |
| `/etc/sudoers` | Who can use `sudo` |

### User management

| Command | Purpose |
|---------|---------|
| `useradd john` | Create user |
| `useradd -m -s /bin/bash john` | Create with home + shell |
| `passwd john` | Set password |
| `usermod -aG sudo john` | Add to group |
| `userdel john` | Delete user |
| `userdel -r john` | Delete user + home |
| `id john` | Show UID, GID, groups |
| `groups john` | Show groups |
| `whoami` | Current user |
| `who` | Logged-in users |
| `w` | Logged-in users + activity |
| `last` | Login history |
| `su - john` | Switch user |
| `sudo command` | Run as root |

### Group management

| Command | Purpose |
|---------|---------|
| `groupadd devs` | Create group |
| `groupdel devs` | Delete group |
| `gpasswd -a john devs` | Add user to group |
| `gpasswd -d john devs` | Remove user |
| `newgrp devs` | Switch primary group |

### Types of users

| Type | UID range | Description |
|------|-----------|-------------|
| Root | 0 | Superuser |
| System users | 1–999 | Services (www-data, mysql) |
| Regular users | 1000+ | Human accounts |

**Q: What is the UID of root?**
0.

**Q: What's the difference between `su` and `sudo`?**

| `su` | `sudo` |
|------|--------|
| Switch to root shell | Run one command as root |
| Needs root's password | Uses your password |
| Full session | Per-command |

**Q: Why is `/etc/shadow` more secure than `/etc/passwd`?**
It's readable only by root, so password hashes are protected.

---

## 10. Process Management

A **process** is a running instance of a program. Each has a **PID**.

### Viewing processes

| Command | Purpose |
|---------|---------|
| `ps` | Current shell processes |
| `ps aux` | All processes, detailed |
| `ps -ef` | All processes, full format |
| `top` | Live process viewer |
| `htop` | Improved interactive viewer |
| `pstree` | Tree of processes |
| `pgrep firefox` | PID by name |

### Signals and killing

| Signal | Number | Meaning |
|--------|--------|---------|
| SIGHUP | 1 | Hangup |
| SIGINT | 2 | Interrupt (Ctrl+C) |
| SIGKILL | 9 | Force kill (cannot be ignored) |
| SIGTERM | 15 | Terminate (default, graceful) |
| SIGSTOP | 19 | Pause |
| SIGCONT | 18 | Resume |

```bash
kill PID
kill -9 PID
kill -15 PID
pkill firefox
killall firefox
```

### Foreground vs background

```bash
sleep 100 &        # run in background
jobs               # list jobs
fg %1              # bring job 1 to foreground
bg %1              # resume job 1 in background
Ctrl+Z             # suspend current process
Ctrl+C             # terminate
```

### Process priority

```bash
nice -n 10 command
renice -n 5 -p PID
```

Nice values: **-20 (highest priority) to 19 (lowest)**.

### Long-running detached processes

```bash
nohup ./script.sh &
disown
```

**Q: What is a PID?**
Process ID — a unique number assigned to each running process.

**Q: What is PID 1?**
`init` or `systemd` — the first process started by the kernel.

**Q: Difference between SIGTERM and SIGKILL?**
SIGTERM asks the process to stop gracefully; SIGKILL forces immediate termination.

**Q: What is a zombie process?**
A process that has finished but whose parent hasn't read its exit status.

**Q: What is a daemon?**
A background process not attached to a terminal (e.g., `sshd`, `cron`).

---

## 11. Package Management

A **package** bundles software with metadata. A **package manager** installs, updates, and removes packages.

### Debian/Ubuntu — `apt` / `dpkg`

```bash
sudo apt update                # refresh package list
sudo apt upgrade               # upgrade installed
sudo apt full-upgrade          # upgrade + dependencies
sudo apt install nginx
sudo apt remove nginx
sudo apt purge nginx           # remove + config
sudo apt autoremove            # remove unneeded deps
apt search nginx
apt show nginx
apt list --installed

sudo dpkg -i package.deb       # install local .deb
dpkg -l                        # list installed
```

### Red Hat/CentOS — `yum` / `dnf` / `rpm`

```bash
sudo dnf install nginx
sudo dnf remove nginx
sudo dnf update
sudo rpm -ivh package.rpm
rpm -qa
```

### Arch — `pacman`

```bash
sudo pacman -S nginx
sudo pacman -R nginx
sudo pacman -Syu
```

**Q: Difference between `apt` and `apt-get`?**
`apt` is user-friendly; `apt-get` is stable for scripts.

**Q: What is a repository?**
A server hosting packages that the package manager downloads from.

**Q: Difference between `.deb` and `.rpm`?**
`.deb` for Debian-based; `.rpm` for Red Hat-based.

---

## 12. Disk & Filesystem Management

### Viewing disk usage

| Command | Purpose |
|---------|---------|
| `df -h` | Disk space by filesystem |
| `du -sh folder/` | Size of folder |
| `du -h --max-depth=1` | Sizes at depth 1 |
| `lsblk` | Block devices tree |
| `blkid` | UUIDs of devices |
| `fdisk -l` | Partition table |
| `free -h` | RAM usage |

### Mounting filesystems

```bash
mount
sudo mount /dev/sdb1 /mnt
sudo umount /mnt
```

Mount point must exist (`mkdir /mnt/usb`).

### Filesystem types

| FS | Description |
|----|-------------|
| ext4 | Default Linux filesystem |
| xfs | High performance, RHEL default |
| btrfs | Modern, snapshots, CoW |
| vfat/FAT32 | USB drives |
| ntfs | Windows |
| tmpfs | RAM-backed |

### Formatting and creating filesystems

```bash
sudo mkfs.ext4 /dev/sdb1
sudo mkfs.xfs /dev/sdb1
```

### Checking & repairing

```bash
sudo fsck /dev/sdb1
```

### Partitioning

```bash
sudo fdisk /dev/sdb
sudo parted /dev/sdb
```

**Q: What is a filesystem?**
The method an OS uses to store and retrieve files on disk.

**Q: What is mounting?**
Attaching a filesystem to a directory in the tree.

**Q: What is swap?**
Disk space used as virtual memory when RAM is full.

```bash
swapon --show
free -h
```

---

## 13. Networking Basics

### Viewing network info

| Command | Purpose |
|---------|---------|
| `ip a` / `ip addr` | Show interfaces |
| `ip route` | Routing table |
| `ifconfig` | Older interface info |
| `hostname -I` | Local IP |
| `ping host` | Test reachability |
| `traceroute host` | Path to host |
| `ss -tuln` | Listening ports |
| `netstat -tuln` | Older equivalent |
| `dig domain` | DNS lookup |
| `nslookup domain` | DNS lookup |
| `curl URL` | HTTP request |
| `wget URL` | Download file |
| `ssh user@host` | Remote login |
| `scp file user@host:/path` | Copy over SSH |
| `rsync -av src/ dst/` | Sync files |

### Common network files

| File | Purpose |
|------|---------|
| `/etc/hosts` | Local hostname → IP map |
| `/etc/resolv.conf` | DNS servers |
| `/etc/network/interfaces` | Interface config (Debian) |
| `/etc/hostname` | Local hostname |

**Q: Difference between TCP and UDP?**
TCP is connection-oriented (reliable); UDP is connectionless (fast, no guarantee).

**Q: What is a port?**
A number identifying a service on a machine (0–65535).

**Q: Common ports?**

| Port | Service |
|------|---------|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 21 | FTP |
| 25 | SMTP |
| 53 | DNS |
| 3306 | MySQL |
| 5432 | PostgreSQL |

**Q: What does `ping` do?**
Sends ICMP echo requests to test if a host is reachable.

---

## 14. System Information Commands

| Command | Purpose |
|---------|---------|
| `uname -a` | Kernel, hostname, architecture |
| `uname -r` | Kernel version |
| `hostname` | System hostname |
| `hostnamectl` | Detailed hostname info |
| `uptime` | How long system has been up |
| `date` | Current date/time |
| `cal` | Calendar |
| `whoami` | Current user |
| `who` | Logged-in users |
| `w` | Who + what they're doing |
| `last` | Last logins |
| `top` | Processes + load |
| `free -h` | RAM + swap |
| `df -h` | Disk usage |
| `du -sh` | Folder size |
| `lscpu` | CPU info |
| `lsmem` | Memory info |
| `lsblk` | Block devices |
| `lspci` | PCI devices |
| `lsusb` | USB devices |
| `dmidecode` | Hardware info (root) |
| `cat /proc/cpuinfo` | CPU details |
| `cat /proc/meminfo` | Memory details |
| `cat /etc/os-release` | Distro info |

**Q: How do you find the kernel version?**

```bash
uname -r
cat /proc/version
```

**Q: How do you check memory usage?**

```bash
free -h
cat /proc/meminfo
```

---

## 15. Text Editors

### nano (beginner-friendly)

```bash
nano file.txt
```

| Key | Action |
|-----|--------|
| `Ctrl+O` | Save |
| `Ctrl+X` | Exit |
| `Ctrl+W` | Search |
| `Ctrl+K` | Cut line |
| `Ctrl+U` | Paste |

### vim (powerful)

```bash
vim file.txt
```

**Modes:**

| Mode | Enter with | Purpose |
|------|------------|---------|
| Normal | `Esc` | Navigate, delete, copy |
| Insert | `i`, `a`, `o` | Type text |
| Command | `:` | Save, quit, search |

**Common commands:**

| Command | Action |
|---------|--------|
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and quit |
| `:q!` | Quit without saving |
| `dd` | Delete line |
| `yy` | Copy line |
| `p` | Paste |
| `/word` | Search |

### emacs

```bash
emacs file.txt
```

**Q: How do you save and exit in vim?**
`Esc` then `:wq`.

**Q: How do you exit vim without saving?**
`Esc` then `:q!`.

---

## 16. Environment Variables & Shell Configuration

**Environment variables** store values used by shells and programs.

```bash
echo $HOME
echo $PATH
echo $USER
echo $SHELL
```

### Setting variables

```bash
MYVAR="hello"          # shell variable (current session)
export MYVAR="hello"   # environment variable (inherited by children)
```

### Viewing all

```bash
env
printenv
set
```

### Important variables

| Variable | Meaning |
|----------|---------|
| `$HOME` | User home |
| `$PATH` | Command search path |
| `$USER` | Username |
| `$SHELL` | Current shell |
| `$PWD` | Current directory |
| `$OLDPWD` | Previous directory |
| `$PS1` | Primary prompt |
| `$EDITOR` | Default editor |

### Making variables permanent

Add to `~/.bashrc` or `~/.profile`:

```bash
echo 'export MYVAR="hello"' >> ~/.bashrc
source ~/.bashrc
```

### Startup files

| File | When run |
|------|----------|
| `/etc/profile` | Login, system-wide |
| `/etc/bash.bashrc` | Interactive, system-wide |
| `~/.bash_profile` | Login, user |
| `~/.bashrc` | Interactive non-login, user |
| `~/.profile` | Login (fallback) |

**Q: Difference between `~/.bashrc` and `~/.bash_profile`?**
`.bashrc` for interactive shells; `.bash_profile` for login shells.

**Q: What is `$PATH`?**
A colon-separated list of directories the shell searches for commands.

---

## 17. Archiving & Compression

### tar

```bash
tar -cvf archive.tar folder/              # create
tar -xvf archive.tar                      # extract
tar -tvf archive.tar                      # list
tar -czvf archive.tar.gz folder/          # create gzip
tar -xzvf archive.tar.gz -C /target/      # extract gzip into folder
tar -cjvf archive.tar.bz2 folder/         # bzip2
tar -xJvf archive.tar.xz                  # xz
tar -xzf archive.tar.gz --strip-components=1
```

| Flag | Meaning |
|------|---------|
| `-c` | Create |
| `-x` | Extract |
| `-t` | List |
| `-v` | Verbose |
| `-f` | File (must be last) |
| `-z` | gzip |
| `-j` | bzip2 |
| `-J` | xz |
| `-C` | Change directory |

### gzip / gunzip

```bash
gzip file.txt
gunzip file.txt.gz
```

### zip / unzip

```bash
zip archive.zip file1 file2
zip -r archive.zip folder/
unzip archive.zip
unzip archive.zip -d target/
```

### Other tools

```bash
bzip2 file.txt
xz file.txt
zstd file.txt
```

**Q: Difference between `tar` and `gzip`?**
`tar` bundles many files; `gzip` compresses one file.

**Q: What is `.tar.gz`?**
A tar archive compressed with gzip.

---

## 18. Boot Process

When you press power, Linux boots in this order:

1. **BIOS/UEFI** — hardware check, finds boot device
2. **Bootloader (GRUB)** — loads kernel
3. **Kernel** — initializes hardware, mounts initrd/initramfs
4. **init / systemd** — first process (PID 1)
5. **Services** — started by systemd in parallel
6. **Login prompt / GUI**

### GRUB

- Configuration: `/boot/grub/grub.cfg`
- Editable at boot with `e`
- Regenerate:

```bash
sudo update-grub
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### Init systems

| Init | Description |
|------|-------------|
| SysVinit | Older, sequential |
| Upstart | Transitional |
| systemd | Modern, parallel, default on most distros |

**Q: What is the first process started on Linux?**
`systemd` (or `init`), PID 1.

**Q: What is GRUB?**
GRand Unified Bootloader — loads the kernel.

**Q: What is the kernel ring buffer?**

```bash
dmesg
```

---

## 19. Systemd & Services

**systemd** manages services, mounts, timers, sockets, and more.

### Managing services

```bash
systemctl status nginx
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
sudo systemctl enable nginx     # start at boot
sudo systemctl disable nginx
systemctl is-active nginx
systemctl is-enabled nginx
```

### Listing

```bash
systemctl list-units --type=service
systemctl --failed
```

### Targets (like runlevels)

```bash
systemctl get-default
sudo systemctl set-default multi-user.target
sudo systemctl isolate rescue.target
```

| Target | Runlevel | Meaning |
|--------|----------|---------|
| poweroff | 0 | Shut down |
| rescue | 1 | Single-user |
| multi-user | 3 | Multi-user, no GUI |
| graphical | 5 | Multi-user + GUI |
| reboot | 6 | Reboot |

### Unit files

Located at:

- `/etc/systemd/system/` — custom
- `/lib/systemd/system/` — package-installed

Reload after changes:

```bash
sudo systemctl daemon-reload
```

**Q: What is `systemd`?**
The init system and service manager used by most modern Linux distros.

**Q: Difference between `start` and `enable`?**
`start` runs now; `enable` makes it start at boot.

---

## 20. Scheduling (cron/at)

### cron — recurring jobs

```bash
crontab -e          # edit
crontab -l          # list
crontab -r          # remove all
```

**Cron syntax:**

```
* * * * * command
│ │ │ │ │
│ │ │ │ └── day of week (0–7, 0=Sun)
│ │ │ └──── month (1–12)
│ │ └────── day of month (1–31)
│ └──────── hour (0–23)
└────────── minute (0–59)
```

**Examples:**

```
0 2 * * *        # daily at 2:00 AM
*/5 * * * *      # every 5 minutes
0 0 * * 0        # Sundays at midnight
0 9 1 * *        # 1st of every month at 9 AM
```

**Cron directories:**

- `/etc/crontab` — system crontab
- `/etc/cron.d/` — individual jobs
- `/etc/cron.daily/`, `/etc/cron.hourly/`, etc.

### at — one-time jobs

```bash
at 10:00 PM
at now + 1 hour
atq
atrm 3
```

**Q: Difference between `cron` and `at`?**
`cron` repeats; `at` runs once.

**Q: What user can schedule cron jobs?**
Any user (for their own crontab); root can schedule system-wide.

---

## 21. Logging & Monitoring

### Log locations

| Path | Purpose |
|------|---------|
| `/var/log/` | All logs |
| `/var/log/syslog` | General (Debian) |
| `/var/log/messages` | General (RHEL) |
| `/var/log/auth.log` | Auth attempts |
| `/var/log/kern.log` | Kernel |
| `/var/log/dmesg` | Boot messages |
| `/var/log/apache2/` | Web logs |

### journalctl (systemd logs)

```bash
journalctl
journalctl -u nginx
journalctl -f
journalctl --since "1 hour ago"
journalctl -b
journalctl -p err
```

### dmesg

```bash
dmesg
dmesg | tail
```

### Monitoring tools

| Command | Purpose |
|---------|---------|
| `top` | Real-time process view |
| `htop` | Improved top |
| `iotop` | Disk I/O |
| `iftop` | Network |
| `vmstat` | VM stats |
| `iostat` | I/O stats |
| `sar` | Historical stats |
| `netstat` / `ss` | Network connections |

**Q: Where are Linux logs stored?**
`/var/log/`.

**Q: What replaces `tail -f /var/log/syslog` in systemd?**
`journalctl -f`.

---

## 22. Links: Hard vs Symbolic

### Hard link

```bash
ln target link
```

- Points to the **same inode** as the target.
- Cannot cross filesystems.
- Cannot link to a directory.
- Deleting the original does **not** delete the data — it's still reachable via other hard links.
- The file is only removed when **all** hard links are deleted.

### Symbolic (soft) link

```bash
ln -s target link
```

- Points to a **path**.
- Can cross filesystems.
- Can point to directories.
- If target is deleted, the symlink becomes **broken**.
- `ls -l` shows `l` as the first character.

**Comparison:**

| Feature | Hard link | Symlink |
|---------|-----------|---------|
| Same inode | Yes | No |
| Cross filesystem | No | Yes |
| Link directories | No | Yes |
| Survives target deletion | Yes | No |
| Shows as | Regular file | `l` type |

**Q: What happens if you delete the original file when a hard link exists?**
The data stays reachable via the hard link.

**Q: What happens if you delete the original file when a symlink exists?**
The symlink becomes broken.

---

## 23. Security Basics

### Permissions recap

- File permissions: `rwx` for user/group/others.
- Root can do anything.
- `sudo` allows temporary privilege escalation.

### Common practices

- Use strong passwords.
- Use SSH keys instead of passwords.
- Keep system updated.
- Limit `sudo` to trusted users.
- Disable root SSH login.
- Use a firewall (`ufw`, `firewalld`, `iptables`).

### Firewall tools

```bash
sudo ufw enable
sudo ufw allow 22
sudo ufw status

sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --reload
```

### SSH keys

```bash
ssh-keygen -t ed25519
ssh-copy-id user@host
```

### File access control

```bash
getfacl file
setfacl -m u:john:rw file
```

### File integrity / hashing

```bash
md5sum file
sha256sum file
```

### Sensitive files

| File | Why |
|------|-----|
| `/etc/shadow` | Password hashes |
| `/etc/sudoers` | sudo rules |
| `/root/` | Root home |
| `~/.ssh/` | SSH keys |

**Q: Why is `/etc/shadow` restricted?**
It contains password hashes; only root should read it.

**Q: What is the principle of least privilege?**
Users should only have the minimum access they need.

---

## 24. Scenario-Based Questions

**Q1.** Your disk is full. How do you find the largest files?

```bash
df -h
du -sh /* 2>/dev/null | sort -h
du -ah / 2>/dev/null | sort -h | tail -20
find / -type f -size +100M 2>/dev/null
```

**Q2.** You deleted a file but the disk space hasn't freed. Why?

The file is still open by a running process. Check with:

```bash
lsof | grep deleted
```

**Q3.** A process is using 100% CPU. How do you find and kill it?

```bash
top
ps aux --sort=-%cpu | head
kill -9 PID
```

**Q4.** You want to monitor a log file in real time.

```bash
tail -f /var/log/syslog
journalctl -f
```

**Q5.** You need to copy a directory to a remote server.

```bash
scp -r folder/ user@host:/path/
rsync -avz folder/ user@host:/path/
```

**Q6.** A script must run every day at 3 AM.

```bash
crontab -e
0 3 * * * /home/user/backup.sh
```

**Q7.** A user can't `sudo`. How do you fix it?

```bash
sudo usermod -aG sudo username
```

**Q8.** You need to find which process uses port 80.

```bash
sudo lsof -i :80
sudo ss -tulpn | grep :80
```

**Q9.** Your service isn't starting at boot.

```bash
sudo systemctl enable myservice
systemctl is-enabled myservice
```

**Q10.** You need to change the owner of a directory tree.

```bash
sudo chown -R user:group folder/
```

**Q11.** A file is "Permission denied" when you try to run it.

```bash
chmod +x file
./file
```

**Q12.** You need to find all `.log` files older than 30 days and delete them.

```bash
find /var/log -name "*.log" -mtime +30 -delete
```

**Q13.** Compare two files to see differences.

```bash
diff file1.txt file2.txt
```

**Q14.** You want to test a destructive command safely.

```bash
mkdir -p ~/Documents/sandbox
cd ~/Documents/sandbox
# test here
```

**Q15.** You need to change the hostname.

```bash
sudo hostnamectl set-hostname newname
```

**Q16.** You want to know which kernel version is running.

```bash
uname -r
```

**Q17.** A file is not visible in `ls`. What could be wrong?

It starts with `.` (hidden). Use `ls -a`.

**Q18.** You want to know how much space a folder uses.

```bash
du -sh folder/
```

**Q19.** You want to shut down / reboot the system.

```bash
sudo shutdown -h now       # power off
sudo shutdown -r now       # reboot
sudo reboot
sudo poweroff
```

**Q20.** You want to see all users on the system.

```bash
cut -d: -f1 /etc/passwd
```

**Q21.** You want to add a user and give them sudo.

```bash
sudo useradd -m -s /bin/bash john
sudo passwd john
sudo usermod -aG sudo john
```

**Q22.** You want to disable SSH root login.

Edit `/etc/ssh/sshd_config`:

```
PermitRootLogin no
```

Then:

```bash
sudo systemctl restart sshd
```

**Q23.** Check if a service is running.

```bash
systemctl status nginx
```

**Q24.** Find the PID of a process by name.

```bash
pgrep firefox
pidof firefox
```

**Q25.** See disk usage sorted by size.

```bash
du -sh * | sort -h
```

---

## 25. Quick Reference Cheat Sheet

| Task | Command |
|------|---------|
| Show kernel version | `uname -r` |
| System info | `uname -a` |
| Current user | `whoami` |
| Hostname | `hostname` / `hostnamectl` |
| Date | `date` |
| Uptime | `uptime` |
| Show PATH | `echo $PATH` |
| List files | `ls -la` |
| Change directory | `cd /path` |
| Current directory | `pwd` |
| Create file | `touch file` |
| Create folder | `mkdir -p a/b/c` |
| Copy | `cp src dst` |
| Copy folder | `cp -r src dst` |
| Move/rename | `mv src dst` |
| Delete file | `rm file` |
| Delete folder | `rm -rf folder` |
| View file | `cat` / `less` / `head` / `tail` |
| Follow log | `tail -f log` |
| Search text | `grep "x" file` |
| Case-insensitive grep | `grep -i "x" file` |
| Find file | `find / -name "file"` |
| Locate | `locate file` |
| Permissions | `chmod 755 file` |
| Owner | `chown user:group file` |
| umask | `umask` |
| Create user | `useradd -m user` |
| Set password | `passwd user` |
| Add to group | `usermod -aG group user` |
| Switch user | `su - user` |
| Run as root | `sudo cmd` |
| Processes | `ps aux` / `top` / `htop` |
| Kill process | `kill -9 PID` |
| Kill by name | `pkill name` |
| Background job | `cmd &` |
| List jobs | `jobs` |
| Bring to foreground | `fg %1` |
| Nice | `nice -n 10 cmd` |
| Package update | `sudo apt update` |
| Package upgrade | `sudo apt upgrade` |
| Install | `sudo apt install pkg` |
| Remove | `sudo apt remove pkg` |
| Disk usage | `df -h` |
| Folder size | `du -sh folder` |
| RAM | `free -h` |
| Block devices | `lsblk` |
| Mount | `sudo mount /dev/sdb1 /mnt` |
| IP addresses | `ip a` |
| Routes | `ip route` |
| Ping | `ping host` |
| Open ports | `ss -tuln` |
| SSH | `ssh user@host` |
| Copy over SSH | `scp file user@host:/path` |
| Sync | `rsync -av src/ dst/` |
| Download | `wget URL` |
| HTTP request | `curl URL` |
| Archive | `tar -czf a.tar.gz folder/` |
| Extract | `tar -xzf a.tar.gz -C dir` |
| Zip | `zip -r a.zip folder/` |
| Unzip | `unzip a.zip -d dir` |
| Service status | `systemctl status svc` |
| Start service | `sudo systemctl start svc` |
| Enable at boot | `sudo systemctl enable svc` |
| View logs | `journalctl -u svc` |
| Boot messages | `dmesg` |
| Cron edit | `crontab -e` |
| Cron list | `crontab -l` |
| One-time job | `at 10:00 PM` |
| Symlink | `ln -s target link` |
| Hard link | `ln target link` |
| Shutdown | `sudo shutdown -h now` |
| Reboot | `sudo reboot` |
| Firewall (ufw) | `sudo ufw allow 22` |
| Firewall (firewalld) | `firewall-cmd --add-port=80/tcp` |
| SSH key | `ssh-keygen -t ed25519` |
| Hash | `sha256sum file` |
| Manual | `man cmd` |
| Quick help | `cmd --help` |

---

# ```markdown
# Linux Module — Practice Question Set (Same Style as Bash)

> Questions and answers structured the same way as the Bash re-take guide.
> Each section explains the concept, gives practice questions, and shows step-by-step answers.
> Copy this into VS Code or GitHub.

---

## Table of Contents

1. [Test Commands in the Terminal First](#1-test-commands-in-the-terminal-first)
2. [Leverage the Man Pages](#2-leverage-the-man-pages)
3. [Create Test Files for Verification](#3-create-test-files-for-verification)
4. [Understand sudo Before Using It](#4-understand-sudo-before-using-it)
5. [Stop Using Your Home Directory for Testing](#5-stop-using-your-home-directory-for-testing)
6. [Watch Your Spacing and Formatting](#6-watch-your-spacing-and-formatting)
7. [Practice wget Scenarios & Shell History](#7-practice-wget-scenarios--shell-history)
8. [Filesystem & File Management Questions](#8-filesystem--file-management-questions)
9. [Permissions & Ownership Questions](#9-permissions--ownership-questions)
10. [Users & Groups Questions](#10-users--groups-questions)
11. [Process Management Questions](#11-process-management-questions)
12. [Package Management Questions](#12-package-management-questions)
13. [Disk & Filesystem Questions](#13-disk--filesystem-questions)
14. [Networking Questions](#14-networking-questions)
15. [Systemd & Services Questions](#15-systemd--services-questions)
16. [Cron & Scheduling Questions](#16-cron--scheduling-questions)
17. [Logging & Monitoring Questions](#17-logging--monitoring-questions)
18. [Links — Hard vs Symbolic Questions](#18-links--hard-vs-symbolic-questions)
19. [Boot Process Questions](#19-boot-process-questions)
20. [Security Basics Questions](#20-security-basics-questions)
21. [Mixed Test-Style Questions](#21-mixed-test-style-questions)
22. [Quick Reference Sheet](#22-quick-reference-sheet)

---

## 1. Test Commands in the Terminal First

**Concept:** Always verify your command in a safe directory before writing the final answer. If a question uses a restricted folder like `/etc` or `/usr/bin`, replicate the structure in a folder you own.

**Q1.** You need to find all `.conf` files in `/etc` and copy them to `/etc/backup`. Why can't you test this directly in `/etc`?

<details>
<summary>Answer</summary>

Because `/etc` is owned by `root`. A normal user does not have write permission there. Test in a folder you own first.

```bash
mkdir -p ~/Documents/practice/etc
cd ~/Documents/practice/etc
touch a.conf b.conf c.txt
mkdir backup
find . -name "*.conf" -exec cp {} backup/ \;
ls backup/
```

Final answer:

```bash
sudo mkdir -p /etc/backup
sudo find /etc -maxdepth 1 -name "*.conf" -exec cp {} /etc/backup/ \;
```
</details>

**Q2.** Test this in `~/Documents/practice` before submitting: *Find all files ending in `.log` in `/var/log` and move them to `/var/log/old`.*

<details>
<summary>Answer</summary>

```bash
mkdir -p ~/Documents/practice/var_log/old
cd ~/Documents/practice/var_log
touch a.log b.log c.txt d.log
find . -name "*.log" -exec mv {} old/ \;
ls old/
```

Final answer:

```bash
sudo mkdir -p /var/log/old
sudo find /var/log -maxdepth 1 -name "*.log" -exec mv {} /var/log/old/ \;
```
</details>

---

## 2. Leverage the Man Pages

**Concept:** `man <command>` opens the manual. Use `/word` to search, `n` for next match, `q` to quit.

**Q3.** What command opens the manual page for `chmod`?

<details>
<summary>Answer</summary>

```bash
man chmod
```
</details>

**Q4.** Inside a man page, how do you search for the word "recursive"?

<details>
<summary>Answer</summary>

Type `/recursive` and press Enter. Press `n` for the next match, `N` for the previous match.
</details>

**Q5.** How do you open section 5 of the `passwd` man page?

<details>
<summary>Answer</summary>

```bash
man 5 passwd
```

Section 5 is for file formats. Section 1 is user commands, section 8 is admin commands.
</details>

**Q6.** What command gives a one-line description of `systemctl` without opening the full manual?

<details>
<summary>Answer</summary>

```bash
whatis systemctl
# or
man -f systemctl
```
</details>

**Q7.** How do you search all man pages for the keyword "permission"?

<details>
<summary>Answer</summary>

```bash
man -k permission
# or
apropos permission
```
</details>

**Q8.** What are the 8 man page sections?

<details>
<summary>Answer</summary>

| Section | Meaning |
|---------|---------|
| 1 | User commands |
| 2 | System calls |
| 3 | Library functions |
| 4 | Devices |
| 5 | File formats |
| 6 | Games |
| 7 | Miscellaneous |
| 8 | System administration |
</details>

---

## 3. Create Test Files for Verification

**Concept:** When a question asks you to find or list files matching a pattern, create dummy files and test your glob.

**Q9.** You need to list all files ending in `.conf`. Create test files and verify.

<details>
<summary>Answer</summary>

```bash
mkdir -p ~/Documents/practice/globtest
cd ~/Documents/practice/globtest
touch app.conf db.conf readme.txt notes.md
ls *.conf
```

Output:

```
app.conf  db.conf
```

Final answer:

```bash
ls *.conf
```
</details>

**Q10.** List all files whose names are exactly 5 characters long.

<details>
<summary>Answer</summary>

```bash
cd ~/Documents/practice/globtest
touch 12345 abcde short longername
ls -d ????? 2>/dev/null
```

Output:

```
12345  abcde
```

Final answer:

```bash
ls -d ????? 2>/dev/null
```

Remember: `?` = exactly one character. Five `?` = five characters.
</details>

**Q11.** List files that start with `log` and end with `.txt`.

<details>
<summary>Answer</summary>

```bash
touch log1.txt log2.txt log3.log other.txt
ls log*.txt
```

Final answer:

```bash
ls log*.txt
```
</details>

**Q12.** Create test files to verify a permission change.

<details>
<summary>Answer</summary>

```bash
cd ~/Documents/practice
touch test.sh
ls -l test.sh         # -rw-r--r--
chmod +x test.sh
ls -l test.sh         # -rwxr-xr-x
```
</details>

---

## 4. Understand sudo Before Using It

**Concept:** `sudo` gives root privileges. Only use it when the task actually requires writing to system folders or managing system resources.

**Q13.** Which of these needs `sudo`?

a) `ls /etc`  
b) `cp file.txt /etc/`  
c) `cat /etc/hostname`  
d) `mkdir /etc/newfolder`

<details>
<summary>Answer</summary>

- a) **No** — reading is allowed for everyone.
- b) **Yes** — writing to `/etc` requires root.
- c) **No** — `/etc/hostname` is world-readable.
- d) **Yes** — creating a folder in `/etc` requires root.

```bash
sudo cp file.txt /etc/
sudo mkdir /etc/newfolder
```
</details>

**Q14.** You want to copy a file from your home directory to `~/Documents`. Do you need `sudo`?

<details>
<summary>Answer</summary>

No. You own your home directory, so standard permissions are enough:

```bash
cp file.txt ~/Documents/
```
</details>

**Q15.** Why does `sudo cat /etc/shadow` work but `cat /etc/shadow` fails?

<details>
<summary>Answer</summary>

`/etc/shadow` has permissions like `-rw-r-----` — only root and the shadow group can read it. `sudo` temporarily gives you root privileges, so `sudo cat /etc/shadow` works.
</details>

**Q16.** What is the difference between `sudo` and `su`?

<details>
<summary>Answer</summary>

| `sudo` | `su` |
|--------|------|
| Runs one command as root | Switches to root shell |
| Uses your own password | Uses root's password |
| Logged by default | Not always logged |
| Configurable per user in `/etc/sudoers` | Root password required |

```bash
sudo apt update          # one command
su -                     # full root shell
```
</details>

**Q17.** What file controls who can use `sudo`?

<details>
<summary>Answer</summary>

`/etc/sudoers`. Always edit with `visudo`:

```bash
sudo visudo
```
</details>

---

## 5. Stop Using Your Home Directory for Testing

**Concept:** Always create a dedicated sandbox folder. Don't clutter `~` or risk deleting important files.

**Q18.** What's wrong with running this in your home directory?

```bash
rm -rf *
```

<details>
<summary>Answer</summary>

It deletes **everything** in your current directory. If you're in `~`, it wipes your entire home folder. Always `mkdir` a sandbox first:

```bash
mkdir -p ~/Documents/sandbox
cd ~/Documents/sandbox
touch test1 test2
rm -rf *
```
</details>

**Q19.** Write the commands to create a safe sandbox, add test files, and clean up afterward.

<details>
<summary>Answer</summary>

```bash
mkdir -p ~/Documents/sandbox
cd ~/Documents/sandbox
touch a.txt b.txt c.log
ls
cd ~
rm -rf ~/Documents/sandbox
```
</details>

**Q20.** How do you keep your current directory clean while testing?

<details>
<summary>Answer</summary>

- Subshell: `(cd /tmp && command)`
- `pushd` / `popd`
- `cd -`
- `mktemp -d` + `trap 'rm -rf $tmp' EXIT`
- Dedicated sandbox: `mkdir -p ~/Documents/sandbox`
</details>

---

## 6. Watch Your Spacing and Formatting

**Concept:** Automated grading is strict. Extra spaces, missing spaces, or repeating parts of the command will fail.

**Q21.** The question asks: *Make a script executable: `chmod ___ script.sh`* — what goes in the blank?

<details>
<summary>Answer</summary>

```
+x
```

Just `+x`. Not `chmod +x`.
</details>

**Q22.** Is `ls-la` valid?

<details>
<summary>Answer</summary>

No. Missing space. Correct:

```bash
ls -la
```
</details>

**Q23.** Is `ls ` (with a trailing space) the same as `ls`?

<details>
<summary>Answer</summary>

Functionally yes in a terminal, but automated grading may mark `ls ` wrong because of the trailing space. Always write it clean:

```bash
ls
```
</details>

**Q24.** Fill in the blank: *Move all `.log` files to `/tmp`: `mv ___ /tmp`*

<details>
<summary>Answer</summary>

```
*.log
```

Just `*.log`. Not `mv *.log`.
</details>

**Q25.** Fill in the blank: *Find all `.txt` files: `find . -name ___`*

<details>
<summary>Answer</summary>

```
"*.txt"
```

Just `"*.txt"`. Not `find . -name "*.txt"`.
</details>

**Q26.** Which is correct?

a) `tar -xzf file.tar.gz -C myfolder`  
b) `tar-xzf file.tar.gz -C myfolder`  
c) `tar -xzf file.tar.gz -C  myfolder`  
d) `tar -xzf file.tar.gz -C myfolder `/b (trailing space)

<details>
<summary>Answer</summary>

Only **a)** is correct.

- b) missing space after `tar`
- c) double space after `-C`
- d) trailing space
</details>

**Q27.** Fill in the blank: *Create a folder and its parents: `mkdir ___ a/c`*

<details>
<summary>Answer</summary>

```
-p
```

Just `-p`. Not `mkdir -p`.
</details>

---

## 7. Practice wget Scenarios & Shell History

**Concept:** Practice real `wget` downloads. Use `history` or `Ctrl+R` to recall verified commands.

**Q28.** Download `https://example.com/file.zip` and save it as `myfile.zip`.

<details>
<summary>Answer</summary>

```bash
wget -O myfile.zip "https://example.com/file.zip"
```

`-O` = capital letter O = output filename.
</details>

**Q29.** Download and extract a `.tar.gz` file into a folder called `myfolder`.

<details>
<summary>Answer</summary>

```bash
mkdir -p myfolder
wget -O myfile.tar.gz "https://example.com/somefile.tar.gz" && tar -xzf myfile.tar.gz -C myfolder
```

`&&` means run `tar` only if `wget` succeeds.
</details>

**Q30.** What's the difference between `wget -O` and `wget -o`?

<details>
<summary>Answer</summary>

- `wget -O` (capital O) = save the downloaded file with this name.
- `wget -o` (lowercase o) = write the log output to this file.

```bash
wget -O myfile.zip "https://example.com/file.zip"    # saves the file as myfile.zip
wget -o log.txt "https://example.com/file.zip"       # saves download log to log.txt
```
</details>

**Q31.** You downloaded a file earlier and want to rerun the exact command. How do you find it quickly?

<details>
<summary>Answer</summary>

Use `history`:

```bash
history | grep wget
```

Then rerun by number:

```bash
!123
```

Or just press **Ctrl+R** and type `wget`.
</details>

**Q32.** Download a file, then extract it into a folder, and show the files inside — all in one line.

<details>
<summary>Answer</summary>

```bash
mkdir -p myfolder && wget -O myfile.tar.gz "https://example.com/somefile.tar.gz" && tar -xzf myfile.tar.gz -C myfolder && ls myfolder
```
</details>

**Q33.** Alternatives to `history` for recalling commands.

<details>
<summary>Answer</summary>

| Method | How to use |
|--------|-----------|
| **Up arrow** | Press `↑` repeatedly |
| **Ctrl + R** | Reverse search — fastest |
| **`!!`** | Run last command |
| **`!n`** | Run command number n |
| **`!wget`** | Last command starting with wget |
| **`!?tar?`** | Last command containing tar |
| **`fc -l`** | List recent |
| **`alias`** | Create shortcuts |
</details>

---

## 8. Filesystem & File Management Questions

**Q34.** What does `pwd` do?

<details>
<summary>Answer</summary>

Prints the current working directory.

```bash
pwd
```
</details>

**Q35.** What does `cd` do? Give 4 examples.

<details>
<summary>Answer</summary>

Changes the current directory.

```bash
cd /home/user          # absolute path
cd Documents           # relative path
cd ~                   # home directory
cd -                   # previous directory
cd ..                  # parent directory
```
</details>

**Q36.** What is the difference between `cd` and `cd -`?

<details>
<summary>Answer</summary>

- `cd` — changes to a directory
- `cd -` — toggles between the current and previous directory
</details>

**Q37.** How do you create a file with no content?

<details>
<summary>Answer</summary>

```bash
touch file.txt
```
</details>

**Q38.** How do you create a directory and its parents in one command?

<details>
<summary>Answer</summary>

```bash
mkdir -p a/b/c
```
</details>

**Q39.** Difference between `cp` and `mv`?

<details>
<summary>Answer</summary>

| `cp` | `mv` |
|------|------|
| Copies | Moves or renames |
| Original stays | Original is removed |
| `cp -r` for directories | Works on directories without `-r` |
</details>

**Q40.** Difference between `rm` and `rmdir`?

<details>
<summary>Answer</summary>

- `rm` — removes files (and directories with `-r`)
- `rmdir` — removes only **empty** directories

```bash
rm file.txt
rmdir emptydir/
rm -r fulldir/
```
</details>

**Q41.** What is the difference between `rm -r` and `rm -rf`?

<details>
<summary>Answer</summary>

- `rm -r` — recursive, may prompt for protected files
- `rm -rf` — recursive + force, no prompts, ignores missing files
</details>

**Q42.** How do you view a large file one screen at a time?

<details>
<summary>Answer</summary>

```bash
less bigfile.log
```

- `Space` — next page
- `b` — previous page
- `/word` — search
- `q` — quit
</details>

**Q43.** What does `head` do? What does `tail -f` do?

<details>
<summary>Answer</summary>

```bash
head file.txt             # first 10 lines
head -n 5 file.txt        # first 5 lines
tail file.txt             # last 10 lines
tail -f /var/log/syslog   # follow growing file
```
</details>

**Q44.** Difference between `cat` and `less`?

<details>
<summary>Answer</summary>

| `cat` | `less` |
|-------|--------|
| Prints whole file | Page-by-page |
| No navigation | Navigate and search |
| Good for small files | Good for large files |
</details>

**Q45.** What does `file` command do?

<details>
<summary>Answer</summary>

Identifies the file type:

```bash
file document.pdf     # PDF document
file image.png        # PNG image
file script.sh        # ASCII text, executable
```
</details>

**Q46.** What does `stat` show that `ls -l` doesn't?

<details>
<summary>Answer</summary>

Detailed file info: inode number, access/modify/change times, block count, and full permissions.

```bash
stat file.txt
```
</details>

**Q47.** How do you find all `.conf` files in the current directory?

<details>
<summary>Answer</summary>

```bash
find . -maxdepth 1 -name "*.conf"
```
</details>

**Q48.** Difference between `find` and `locate`?

<details>
<summary>Answer</summary>

| `find` | `locate` |
|--------|----------|
| Real-time search | Database-based |
| Slower | Faster |
| More options | Fewer options |
| Always current | May be stale |

```bash
sudo updatedb
locate file.conf
```
</details>

**Q49.** Difference between `which`, `whereis`, and `type`?

<details>
<summary>Answer</summary>

| Command | What it shows |
|---------|---------------|
| `which ls` | Path of executable |
| `whereis ls` | Binary, source, man page |
| `type ls` | Builtin, alias, function, or executable |
</details>

**Q50.** What is the Filesystem Hierarchy Standard? List 5 important directories.

<details>
<summary>Answer</summary>

The standard that defines Linux directory structure.

| Directory | Purpose |
|-----------|---------|
| `/` | Root |
| `/etc` | Config files |
| `/home` | User homes |
| `/var` | Variable data (logs) |
| `/usr` | User programs |
| `/bin` | Essential binaries |
| `/tmp` | Temporary files |

```bash
ls /
```
</details>

**Q51.** Where are system logs stored?

<details>
<summary>Answer</summary>

`/var/log/`.

```bash
ls /var/log/
```
</details>

**Q52.** Where are user home directories stored?

<details>
<summary>Answer</summary>

`/home/<username>` (except root, which is `/root`).

```bash
ls /home/
```
</details>

---

## 9. Permissions & Ownership Questions

**Q53.** What do the `rwx` letters mean?

<details>
<summary>Answer</summary>

| Letter | Meaning | Value |
|--------|---------|-------|
| `r` | Read | 4 |
| `w` | Write | 2 |
| `x` | Execute | 1 |
| `-` | None | 0 |
</details>

**Q54.** What does `-rwxr-xr--` mean in octal?

<details>
<summary>Answer</summary>

- Owner: `rwx` = 7
- Group: `r-x` = 5
- Others: `r--` = 4
- Octal: **754**
</details>

**Q55.** How do you make a file executable?

<details>
<summary>Answer</summary>

```bash
chmod +x script.sh
# or
chmod 755 script.sh
```
</details>

**Q56.** How do you give read and write to owner, read to group, none to others?

<details>
<summary>Answer</summary>

```bash
chmod 640 file.txt
```
</details>

**Q57.** Difference between `chmod` and `chown`?

<details>
<summary>Answer</summary>

| `chmod` | `chown` |
|---------|---------|
| Changes permissions | Changes owner |
| `chmod 755 file` | `chown user:group file` |
| Works with rwx values | Works with user/group names |

```bash
chmod 755 file.txt
chown john:devs file.txt
chown -R john:devs folder/
```
</details>

**Q58.** What is `umask`?

<details>
<summary>Answer</summary>

Default permission mask. New files/dirs have permissions reduced by the umask value.

- Default umask: `022`
- File: `666 - 022 = 644`
- Directory: `777 - 022 = 755`

```bash
umask
umask 027
```
</details>

**Q59.** Why can a normal user not write to `/etc`?

<details>
<summary>Answer</summary>

Because `/etc` is owned by `root` with permissions `drwxr-xr-x` — others can only read and execute, not write.

```bash
ls -ld /etc
```
</details>

**Q60.** How do you make a directory writable only by the owner?

<details>
<summary>Answer</summary>

```bash
chmod 700 myfolder
```
</details>

**Q61.** What does `chmod 777` do?

<details>
<summary>Answer</summary>

Gives read, write, execute to everyone. Usually unsafe for anything but temporary testing.
</details>

**Q62.** How do you change ownership of a directory tree?

<details>
<summary>Answer</summary>

```bash
sudo chown -R user:group folder/
```
</details>

---

## 10. Users & Groups Questions

**Q63.** How do you create a new user?

<details>
<summary>Answer</summary>

```bash
sudo useradd -m -s /bin/bash john
sudo passwd.

 john
```
</details>

**Q64.** How do you``` delete a user and their home directory?

<details>
<bashsummary>Answer</
summary>

```bash
sudo userdel -nr john
```
oh</details>

**Q65.** How do you add a user to the `sudo` group?

<details>
<summary>Answer</summary>

```bash
sudo usermod -aG sudo john
```

The `-aG` means append to supplementary groups.
</details>

**Q66.** What is the UID of root?

<details>
<summary>Answer</summary>

`0`.
</details>

**Q67.** Where are user accounts stored?

<details>
<summary>Answer</summary>

| File | Contents |
|------|----------|
| `/etc/passwd` | Usernames, UIDs, GIDs, homes, shells |
| `/etc/shadow` | Encrypted passwords (root only) |
| `/etc/group` | Groups |

```bash
cat /etc/passwd
sudo cat /etc/shadow
cat /etc/group
```
</details>

**Q68.** What is the difference between `sudo` and `su`?

<details>
<summary>Answer</summary>

| `sudo` | `su` |
|--------|------|
| Runs one command as root | Opens a root shell |
| Uses your password | Uses root's password |
| Logged | Not always |
| Configurable in `/etc/sudoers` | Requires root password |

```bash
sudo apt update
su - 
```
</details>

**Q69.** How do you list all users on the system?

<details>
<summary>Answer</summary>

```bash
cut -d: -f1 /etc/passwd
```
</details>

**Q70.** How do you see which groups a user belongs to?

<details>
<summary>Answer</summary>

```bash
groups john
id john
```
</details>

**Q71.** How do you switch to another user?

<details>
<summary>Answer</summary>

```bash
su - john
sudo -i          # root shell
```
</details>

---

## 11. Process Management Questions

**Q72.** What is a process? What is a PID?

<details>
<summary>Answer</summary>

- Process: a running instance of a program.
- PID: unique Process ID assigned by the kernel.

```bash
ps aux
```
</details>

**Q73.** What is PID 1?

<details>
<summary>Answer</summary>

The first process started by the kernel — usually `systemd` (or `init`). It manages all other processes.

```bash
ps -p 1
```
</details>

**Q74.** How do you list all running processes?

<details>
<summary>Answer</summary>

```bash
ps aux
ps -ef
top
htop
```
</details>

**Q75.** How do you kill a process by PID?

<details>
<summary>Answer</summary>

```bash
kill PID
kill -9 PID        # force
kill -15 PID       # graceful (SIGTERM)
```
</details>

**Q76.** What is the difference between SIGTERM and SIGKILL?

<details>
<summary>Answer</summary>

| SIGTERM (15) | SIGKILL (9) |
|--------------|-------------|
| Graceful termination | Forces termination |
| Process can clean up | Cannot be caught/ignored |
| Default `kill` | `kill -9` |
</details>

**Q77.** What does `Ctrl+C` do? What does `Ctrl+Z` do?

<details>
<summary>Answer</summary>

- `Ctrl+C` → sends SIGINT, terminates process.
- `Ctrl+Z` → sends SIGTSTP, suspends process.
</details>

**Q78.** What does `&` at the end of a command do?

<details>
<summary>Answer</summary>

Runs the command in the background.

```bash
sleep 100 &
```
</details>

**Q79.** What do `jobs`, `fg`, and `bg` do?

<details>
<summary>Answer</summary>

- `jobs` — lists background jobs
- `fg %1` — brings job 1 to foreground
- `bg %1` — resumes job 1 in background

```bash
sleep 100 &
jobs
fg %1
```
</details>

**Q80.** What does `nohup` do?

<details>
<summary>Answer</summary>

Runs a command that ignores hangup signals — it keeps running after logoutup ./script.sh &
```
</details>

**Q81.** How do you find a process by name?

<details>
<summary>Answer</summary>

```bash
pgrep firefox
pidof firefox
```
</details>

**Q82.** How do you change a process's priority?

<details>
<summary>Answer</summary>

```bash
nice -n 10 command
renice -n 5 -p PID
```

Nice values range from -20 (highest) to 19 (lowest).
</details>

**Q83.** What is a zombie process?

<details>
<summary>Answer</summary>

A process that has finished but whose parent hasn't read its exit status. It stays in the process table.

```bash
ps aux | grep Z
```
</details>

**Q84.** What is a daemon?

<details>
<summary>Answer</summary>

A background process not attached to a terminal (e.g., `sshd`, `cron`, `systemd`).
</details>

---

## 12. Package Management Questions

**Q85.** What is a package manager?

<details>
<summary>Answer</summary>

A tool that installs, updates, and removes software, handling dependencies.

| Distro Family | Package Manager |
|---------------|-----------------|
| Debian/Ubuntu | `apt`, `dpkg` |
| RHEL/CentOS | `yum`, `dnf`, `rpm` |
| Arch | `pacman` |
| SUSE | `zypper` |
</details>

**Q86.** How do you update the package list and upgrade installed packages?

<details>
<summary>Answer</summary>

```bash
sudo apt update
sudo apt upgrade
```
</details>

**Q87.** How do you install and remove a package?

<details>
<summary>Answer</summary>

```bash
sudo apt install nginx
sudo apt remove nginx
sudo apt purge nginx       # also removes config
sudo apt autoremove        # remove unneeded deps
```
</details>

**Q88.** Difference between `apt` and `apt-get`?

<details>
<summary>Answer</summary>

- `apt` — user-friendly output, progress bars.
- `apt-get` — script-friendly, stable interface.

Both work; scripts usually use `apt-get`.
</details>

**Q89.** Difference between `.deb` and `.rpm`?

<details>
<summary>Answer</summary>

- `.deb` — Debian/Ubuntu packages, installed with `dpkg -i`.
- `.rpm` — Red Hat/CentOS packages, installed with `rpm -ivh` or `dnf install`.

```bash
sudo dpkg -i package.deb
sudo rpm -ivh package.rpm
```
</details>

**Q90.** How do you list installed packages?

<details>
<summary>Answer</summary>

```bash
apt list --installed
dpkg -l
rpm -qa
```
</details>

**Q91.** What is a repository?

<details>
<summary>Answer</summary>

A server hosting packages the package manager downloads from. Defined in `/etc/apt/sources.list` (Debian/Ubuntu).
</details>

---

## 13. Disk & Filesystem Questions

**Q92.** How do you check disk space usage?

<details>
<summary>Answer</summary>

```bash
df -h
```
</details>

**Q93.** How do you check how much space a folder uses?

<details>
<summary>Answer</summary>

```bash
du -sh folder/
du -h --max-depth=1
```
</details>

**Q94.** How do you check RAM usage?

<details>
<summary>Answer</summary>

```bash
free -h
cat /proc/meminfo
```
</details>

**Q95.** What does `lsblk` show?

<details>
<summary>Answer</summary>

Block devices (disks, partitions) in a tree view.

```bash
lsblk
```
</details>

**Q96.** What does `mount` do? What is a mount point?

<details>
<summary>Answer</summary>

Attaches a filesystem to a directory in the tree.

```bash
sudo mount /dev/sdb1 /mnt
sudo umount /mnt
```

The directory (`/mnt`) is the mount point.
</details>

**Q97.** What is a filesystem? Name 4 types.

<details>
<summary>Answer</summary>

The method of storing/retrieving files on disk.

| FS | Notes |
|----|-------|
| ext4 | Linux default |
| xfs | High performance |
| btrfs | Snapshots, CoW |
| vfat | USB drives |
| ntfs | Windows |
</details>

**Q98.** How do you format a partition with ext4?

<details>
<summary>Answer</summary>

```bash
sudo mkfs.ext4 /dev/sdb1
```
</details>

**Q99.** What is swap?

<details>
<summary>Answer</summary>

Disk space used as virtual memory when RAM fills up.

```bash
swapon --show
free -h
```
</details>

**Q100.** What does `fdisk -l` show?

<details>
<summary>Answer</summary>

Partition tables of all disks.

```bash
sudo fdisk -l
```
</details>

---

## 14. Networking Questions

**Q101.** How do you see your IP addresses?

<details>
<summary>Answer</summary>

```bash
ip a
ip addr
hostname -I
```
</details>

**Q102.** What does `ping` do?

<details>
<summary>Answer</summary>

Sends ICMP echo requests to test if a host is reachable.

```bash
ping google.com
ping -c 4 google.com
```
</details>

**Q103.** How do you see listening ports?

<details>
<summary>Answer</summary>

```bash
ss -tuln
netstat -tuln
sudo lsof -i :80
```
</details>

**Q104.** What is the difference between TCP and UDP?

<details>
<summary>Answer</summary>

| TCP | UDP |
|-----|-----|
| Connection-oriented | Connectionless |
| Reliable | No guarantee |
| Slower | Faster |
| HTTP, SSH, FTP | DNS, video, games |
</details>

**Q105.** Name 5 common ports and their services.

<details>
<summary>Answer</summary>

| Port | Service |
|------|---------|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 53 | DNS |
| 3306 | MySQL |
</details>

**Q106.** Difference between `ssh` and `scp`?

<details>
<summary>Answer</summary>

| `ssh` | `scp` |
|-------|-------|
| Remote login | Copy files over SSH |
| `ssh user@host` | `scp file user@host:/path` |
</details>

**Q107.** What does `rsync` do?

<details>
<summary>Answer</summary>

Syncs files efficiently (only copies changes).

```bash
rsync -av source/ dest/
rsync -av source/ user@host:/dest/
```
</details>

**Q108.** What does `dig` do?

<details>
<summary>Answer</summary>

DNS lookup tool.

```bash
dig google.com
nslookup google.com
```
</details>

**Q109.** What does `traceroute` do?

<details>
<summary>Answer</summary>

Shows the path packets take to reach a host.

```bash
traceroute google.com
```
</details>

**Q110.** Where do you define local hostname mappings?

<details>
<summary>Answer</summary>

`/etc/hosts`.

```bash
cat /etc/hosts
```
</details>

---

## 15. Systemd & Services Questions

**Q111.** What is systemd?

<details>
<summary>Answer</summary>

The init system and service manager used by most modern Linux distributions. PID 1.
</details>

**Q112.** How do you check if a service is running?

<details>
<summary>Answer</summary>

```bash
systemctl status nginx
```
</details>

**Q113.** How do you start, stop, and restart a service?

<details>
<summary>Answer</summary>

```bash
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
```
</details>

**Q114.** Difference between `start` and `enable`?

<details>
<summary>Answer</summary>

- `start` — runs now
- `enable` — starts at boot

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```
</details>

**Q115.** How do you see failed services?

<details>
<summary>Answer</summary>

```bash
systemctl --failed
```
</details>

**Q116.** What are systemd targets? Name 3.

<details>
<summary>Answer</summary>

Replacement for runlevels.

| Target | Meaning |
|--------|---------|
| multi-user.target | Multi-user, no GUI |
| graphical.target | Multi-user + GUI |
| rescue.target | Single-user |
| poweroff.target | Shutdown |

```bash
systemctl get-default
sudo systemctl set-default multi-user.target
```
</details>

**Q117.** How do you reload systemd after editing a unit file?

<details>
<summary>Answer</summary>

```bash
sudo systemctl daemon-reload
```
</details>

**Q118.** Where are unit files stored?

<details>
<summary>Answer</summary>

- `/etc/systemd/system/` — custom
- `/lib/systemd/system/` — package-installed
</details>

---

## 16. Cron & Scheduling Questions

**Q119.** What is `cron`?

<details>
<summary>Answer</summary>

A scheduler for recurring tasks.
</details>

**Q120.** How do you edit your crontab?

<details>
<summary>Answer</summary>

```bash
crontab -e
crontab -l      # list
crontab -r      # remove
```
</details>

**Q121.** What is the crontab syntax?

<details>
<summary>Answer</summary>

```
* * * * * command
│ │ │ │ │
│ │ │ │ └── day of week (0-7)
│ │ │ └──── month (1-12)
│ │ └────── day of month (1-31)
│ └──────── hour (0-23)
└────────── minute (0-59)
```
</details>

**Q122.** Give an example of a daily cron job at 2 AM.

<details>
<summary>Answer</summary>

```bash
0 2 * * * /home/user/backup.sh
```
</details>

**Q123.** What is the difference between `cron` and `at`?

<details>
<summary>Answer</summary>

| `cron` | `at` |
|--------|------|
| Recurring jobs | One-time job |
| `crontab -e` | `at 10:00 PM` |
| `crontab -l` | `atq` |
</details>

**Q124.** How do you schedule a one-time job at 10 PM?

<details>
<summary>Answer</summary>

```bash
at 10:00 PM
# type command, then Ctrl+D
atq          # list
atrm 3       # remove job 3
```
</details>

**Q125.** Where are system cron jobs stored?

<details>
<summary>Answer</summary>

- `/etc/crontab`
- `/etc/cron.d/`
- `/etc/cron.daily/`, `/etc/cron.hourly/`, `/etc/cron.weekly/`, `/etc/cron.monthly/`
</details>

---

## 17. Logging & Monitoring Questions

**Q126.** Where are Linux logs stored?

<details>
<summary>Answer</summary>

`/var/log/`.
</details>

**Q127.** What is `journalctl`?

<details>
<summary>Answer</summary>

The log viewer for systemd.

```bash
journalctl
journalctl -u nginx
journalctl -f
journalctl --since "1 hour ago"
journalctl -p err
```
</details>

**Q128.** How do you monitor a log file in real time?

<details>
<summary>Answer</summary>

```bash
tail -f /var/log/syslog
journalctl -f
```
</details>

**Q129.** What does `dmesg` show?

<details>
<summary>Answer</summary>

Kernel ring buffer — boot messages, hardware events.

```bash
dmesg | tail
```
</details>

**Q130.** Name 4 monitoring tools.

<details>
<summary>Answer</summary>

| Tool | Purpose |
|------|---------|
| `top` | Real-time process view |
| `htop` | Improved top |
| `iotop` | Disk I/O |
| `iftop` | Network |
| `vmstat` | VM stats |
| `iostat` | I/O stats |
</details>

**Q131.** Which log contains authentication attempts?

<details>
<summary>Answer</summary>

`/var/log/auth.log` (Debian) or `/var/log/secure` (RHEL).

```bash
sudo cat /var/log/auth.log
```
</details>

---

## 18. Links — Hard vs Symbolic Questions

**Q132.** Difference between a hard link and a symbolic link?

<details>
<summary>Answer</summary>

| Hard link | Symlink |
|-----------|---------|
| Same inode | Points to path |
| Cannot cross FS | Can cross FS |
| Cannot link directories | Can link directories |
| `ln file link` | `ln -s target link` |
| Survives target deletion | Broken if target deleted |
</details>

**Q133.** How do you create a symlink?

<details>
<summary>Answer</summary>

```bash
ln -s /path/to/target linkname
```
</details>

**Q134.** How do you create a hard link?

<details>
<summary>Answer</summary>

```bash
ln file.txt hardlink.txt
```
</details>

**Q135.** What happens if you delete the original of a symlink?

<details>
<summary>Answer</summary>

The symlink becomes **broken** (dangling). `ls -l` shows it pointing to a nonexistent path.
</details>

**Q136.** What happens if you delete the original of a hard link?

<details>
<summary>Answer</summary>

The file still exists — the data is only removed when **all** hard links are deleted.
</details>

**Q137.** How do you identify a symlink from `ls -l`?

<details>
<summary>Answer</summary>

First character is `l`:

```
lrwxrwxrwx 1 user user 10 Jan 1 12:00 mylink -> /etc/passwd
```
</details>

---

## 19. Boot Process Questions

**Q138.** What is the Linux boot order?

<details>
<summary>Answer</summary>

1. BIOS/UEFI
2. Bootloader (GRUB)
3. Kernel
4. init / systemd (PID 1)
5. Services
6. Login prompt / GUI
</details>

**Q139.** What is GRUB?

<details>
<summary>Answer</summary>

The GRand Unified Bootloader — loads the kernel.

Config: `/boot/grub/grub.cfg`.

```bash
sudo update-grub
```
</details>

**Q140.** What is PID 1?

<details>
<summary>Answer</summary>

`systemd` (or `init`) — the first process started by the kernel.

```bash
ps -p 1
```
</details>

**Q141.** Difference between BIOS and UEFI?

<details>
<summary>Answer</summary>

| BIOS | UEFI |
|------|------|
| Legacy | Modern |
| MBR partitions | GPT partitions |
| 2 TB limit | Larger disks |
| Slower | Faster boot |
</details>

**Q142.** What is the kernel ring buffer?

<details>
<summary>Answer</summary>

Boot and kernel messages, viewable with `dmesg`.
</details>

---

## 20. Security Basics Questions

**Q143.** What is the principle of least privilege?

<details>
<summary>Answer</summary>

Users should only have the minimum access needed to do their jobs. Applies to files, sudo, services.
</details>

**Q144.** Why is `/etc/shadow` more restricted than `/etc/passwd`?

<details>
<summary>Answer</summary>

`/etc/passwd` is world-readable (usernames, UIDs). `/etc/shadow` stores password hashes and is readable only by root.
</details>

**Q145.** How do you enable a firewall with UFW?

<details>
<summary>Answer</summary>

```bash
sudo ufw enable
sudo ufw allow 22
sudo ufw allow 80
sudo ufw status
```
</details>

**Q146.** How do you create an SSH key?

<details>
<summary>Answer</summary>

```bash
ssh-keygen -t ed25519
ssh-copy-id user@host
```
</details>

**Q147.** How do you hash a file?

<details>
<summary>Answer</summary>

```bash
sha256sum file.txt
md5sum file.txt
```
</details>

**Q148.** What is `setfacl` / `getfacl`?

<details>
<summary>Answer</summary>

Tools for extended ACLs (Access Control Lists) — per-user permissions.

```bash
getfacl file.txt
setfacl -m u:john:rw file.txt
```
</details>

**Q149.** How do you disable root SSH login?

<details>
<summary>Answer</summary>

Edit `/etc/ssh/sshd_config`:

```
PermitRootLogin no
```

Then:

```bash
sudo systemctl restart sshd
```
</details>

**Q150.** What is a firewall and what does it do?

<details>
<summary>Answer</summary>

A network filter controlling incoming/outgoing traffic. Common tools: `ufw`, `firewalld`, `iptables`, `nftables`.
</details>

---

## 21. Mixed Test-Style Questions

**Q151.** List all files in your home directory with exactly 14 characters, including hidden files.

<details>
<summary>Answer</summary>

`ls` won't match hidden files with `?`. Use `find`:

```bash
find ~ -maxdepth 1 -type f -name '??????????????' -printf '%f\n'
```

14 question marks = 14 characters.
</details>

**Q152.** Copy all `.conf` files from `/etc` to a backup folder in your home directory. Do you need `sudo`?

<details>
<summary>Answer</summary>

No, because you're **reading** from `/etc` (world-readable) and **writing** to your home directory.

```bash
mkdir -p ~/backup_conf
cp /etc/*.conf ~/backup_conf/
```

You would need `sudo` only if you were writing **into** `/etc`.
</details>

**Q153.** What does this command do?

```bash
wget -O data.tar.gz "https://example.com/data.tar.gz" && tar -xzf data.tar.gz -C ~/Documents/sandbox
```

<details>
<summary>Answer</summary>

1. Downloads `data.tar.gz` and saves it as `data.tar.gz`.
2. If the download succeeds, extracts it into `~/Documents/sandbox`.
3. `-O` = output filename, `-xzf` = extract gzip tar, `-C` = change to directory.

Note: `~/Documents/sandbox` must already exist, or `tar` will fail.
</details>

**Q154.** A user reports their disk is full. What commands do you use to investigate?

<details>
<summary>Answer</summary>

```bash
df -h
du -sh /* 2>/dev/null | sort -h
du -ah / 2>/dev/null | sort -h | tail -20
find / -type f -size +100M 2>/dev/null
lsof | grep deleted
```
</details>

**Q155.** A process is using 100% CPU. How do you find and kill it?

<details>
<summary>Answer</summary>

```bash
top
ps aux --sort=-%cpu | head
kill -9 PID
```
</details>

**Q156.** A user can't run `sudo`. How do you fix it?

<details>
<summary>Answer</summary>

```bash
sudo usermod -aG sudo username
```

Then log out and back in for the group change to apply.
</details>

**Q157.** A service won't start at boot. How do you check?

<details>
<summary>Answer</summary>

```bash
systemctl is-enabled myservice
systemctl status myservice
sudo systemctl enable myservice
```
</details>

**Q158.** You need to find which process uses port 80.

<details>
<summary>Answer</summary>

```bash
sudo lsof -i :80
sudo ss -tulpn | grep :80
sudo netstat -tulpn | grep :80
```
</details>

**Q159.** A file is "Permission denied" when you try to run it. Fix it.

<details>
<summary>Answer</summary>

```bash
chmod +x file
./file
```
</details>

**Q160.** Compare two files to see differences.

<details>
<summary>Answer</summary>

```bash
diff file1.txt file2.txt
```
</details>

**Q161.** Find all `.log` files older than 30 days and delete them.

<details>
<summary>Answer</summary>

```bash
find /var/log -name "*.log" -mtime +30 -delete
```
</details>

**Q162.** You need to rename a folder tree safely. Test first.

<details>
<summary>Answer</summary>

```bash
mkdir -p ~/Documents/sandbox
cd ~/Documents/sandbox
mkdir -p a/b/c
mv a renamed_a
ls renamed_a/b/c
```
</details>

**Q163.** Change the system hostname.

<details>
<summary>Answer</summary>

```bash
sudo hostnamectl set-hostname newname
hostnamectl
```
</details>

**Q164.** Find the kernel version and full system info.

<details>
<summary>Answer</summary>

```bash
uname -r
uname -a
cat /etc/os-release
```
</details>

**Q165.** A file is not visible in `ls`. What could be wrong?

<details>
<summary>Answer</summary>

It starts with `.` (hidden). Use `ls -a`.
</details>

**Q166.** Schedule a backup every day at 3 AM.

<details>
<summary>Answer</summary>

```bash
crontab -e
0 3 * * * /home/user/backup.sh
```
</details>

**Q167.** Create a symbolic link to `/etc/passwd` called `mypasswd`.

<details>
<summary>Answer</summary>

```bash
ln -s /etc/passwd mypasswd
ls -l mypasswd
```
</details>

**Q168.** Shut down and reboot the system.

<details>
<summary>Answer</summary>

```bash
sudo shutdown -h now
sudo shutdown -r now
sudo reboot
sudo poweroff
```
</details>

**Q169.** Add a new user with sudo privileges.

<details>
<summary>Answer</summary>

```bash
sudo useradd -m -s /bin/bash john
sudo passwd john
sudo usermod -aG sudo john
```
</details>

**Q170.** List all environment variables.

<details>
<summary>Answer</summary>

```bash
env
printenv
set
```
</details>

**Q171.** What is the difference between `>` and `>>`?

<details>
<summary>Answer</summary>

- `>` — overwrites the file
- `>>` — appends to the file

```bash
ls > out.txt
echo "new line" >> out.txt
```
</details>

**Q172.** What does `2>/dev/null` do?

<details>
<summary>Answer</summary>

Discards error output (stderr) so it doesn't show on screen.

```bash
find / -name "*.txt" 2>/dev/null
```
</details>

**Q173.** What does `$( )` do?

<details>
<summary>Answer</summary>

Command substitution — runs a command and inserts its output.

```bash
today=$(date +%Y-%m-%d)
echo "Today is $today"
```
</details>

**Q174.** What does `&&` do? What does `||` do?

<details>
<summary>Answer</summary>

- `&&` — run next command only if the first succeeds
- `||` — run next command only if the first fails

```bash
wget -O file.zip "URL" && unzip file.zip
cp file.txt /backup/ || echo "Copy failed"
```
</details>

**Q175.** What is the difference between `/etc/passwd` and `/etc/shadow`?

<details>
<summary>Answer</summary>

| File | Contents | Access |
|------|----------|--------|
| `/etc/passwd` | User info | World-readable |
| `/etc/shadow` | Password hashes | Root only |
</details>

---

## 22. Quick Reference Sheet

| Task | Command |
|------|---------|
| Show working directory | `pwd` |
| Change directory | `cd /path` |
| List files | `ls -la` |
| Create file | `touch file` |
| Create folder | `mkdir -p a/b/c` |
| Copy | `cp src dst` |
| Copy folder | `cp -r src dst` |
| Move/rename | `mv src dst` |
| Delete file | `rm file` |
| Delete folder | `rm -rf folder` |
| View file | `cat` / `less` / `head` / `tail` |
| Follow log | `tail -f log` |
| Search text | `grep "x" file` |
| Case-insensitive grep | `grep -i "x" file` |
| Find files | `find . -name "*.txt"` |
| Case-insensitive find | `find . -iname "*.txt"` |
| Permissions | `chmod 755 file` |
| Owner | `chown user:group file` |
| umask | `umask` |
| Create user | `useradd -m user` |
| Set password | `passwd user` |
| Add to sudo | `usermod -aG sudo user` |
| Switch user | `su - user` |
| Run as root | `sudo cmd` |
| Processes | `ps aux` / `top` / `htop` |
| Kill process | `kill -9 PID` |
| Kill by name | `pkill name` |
| Background | `cmd &` |
| List jobs | `jobs` |
| Bring to foreground | `fg %1` |
| Nice | `nice -n 10 cmd` |
| Package update | `sudo apt update` |
| Install | `sudo apt install pkg` |
| Remove | `sudo apt remove pkg` |
| Disk usage | `df -h` |
| Folder size | `du -sh folder` |
| RAM | `free -h` |
| Block devices | `lsblk` |
| Mount | `sudo mount /dev/sdb1 /mnt` |
| IP addresses | `ip a` |
| Routes | `ip route` |
| Ping | `ping host` |
| Open ports | `ss -tuln` |
| SSH | `ssh user@host` |
| Copy over SSH | `scp file user@host:/path` |
| Sync | `rsync -av src/ dst/` |
| Download | `wget -O name URL` |
| Download + extract | `wget -O f.tar.gz URL && tar -xzf f.tar.gz -C dir` |
| HTTP request | `curl URL` |
| Archive | `tar -czf a.tar.gz folder/` |
| Extract | `tar -xzf a.tar.gz -C dir` |
| Zip | `zip -r a.zip folder/` |
| Unzip | `unzip a.zip -d dir` |
| Service status | `systemctl status svc` |
| Start service | `sudo systemctl start svc` |
| Enable at boot | `sudo systemctl enable svc` |
| View logs | `journalctl -u svc` |
| Boot messages | `dmesg` |
| Cron edit | `crontab -e` |
| Cron list | `crontab -l` |
| One-time job | `at 10:00 PM` |
| Symlink | `ln -s target link` |
| Hard link | `ln target link` |
| Shutdown | `sudo shutdown -h now` |
| Reboot | `sudo reboot` |
| Firewall (ufw) | `sudo ufw allow 22` |
| Firewall (firewalld) | `firewall-cmd --add-port=80/tcp` |
| SSH key | `ssh-keygen -t ed25519` |
| Hash | `sha256sum file` |
| Manual | `man cmd` |
| Quick help | `cmd --help` |
| Sandbox | `mkdir -p ~/Documents/sandbox` |
| Subshell | `(cd /tmp && cmd)` |
| Auto-cleanup | `tmp=$(mktemp -d); trap 'rm -rf $tmp' EXIT` |
| Reverse search | `Ctrl+R` |
| Rerun last | `!!` |

# # Linux Module — Important Commands & Kernel Version

> Complete reference guide based on the "Important Commands" screenshot and question 6.
> Copy this into VS Code or GitHub as your notes.

---

## Table of Contents

1. [Answer to Question 6: Linux Kernel Version](#1-answer-to-question-6-linux-kernel-version)
2. [Important Commands (1-27)](#2-important-commands-1-27)
3. [Quick Reference Cheat Sheet](#3-quick-reference-cheat-sheet)

---

## 1. Answer to Question 6: Linux Kernel Version

**Q: How does one tell the Linux kernel version on a Linux PC/Server?**

You can use the `uname` command. Specifically, `uname -r` shows the kernel release, and `uname -a` shows all system information. Alternatively, you can use `cat /proc/version`.

**Examples:**

```bash
uname -r                  # Show kernel release (e.g., 6.8.0-31-generic)
uname -a                  # Show all system info (kernel, hostname, arch)
cat /proc/version         # Show kernel version and build info
hostnamectl               # Shows kernel version among other system info
```

---

## 2. Important Commands (1-27)

### 1. `ps`

**Meaning:** Report a snapshot of the current running processes.

| Flag | Meaning |
|------|---------|
| `-a` | Show processes for all users |
| `-u` | Display user-oriented format |
| `-x` | Show processes not attached to a terminal |
| `-e` | Show all processes |
| `-f` | Full-format listing |

**Examples:**

```bash
ps                     # Current shell processes
ps aux                 # All processes, detailed (BSD style)
ps -ef                 # All processes, full format (UNIX style)
ps -u username         # Processes by user
```

---

### 2. `apt`

**Meaning:** Advanced Package Tool; the package manager used for installing, updating, and removing software on Debian/Ubuntu systems.

| Command | Purpose |
|---------|---------|
| `apt install` | Install a package |
| `apt remove` | Remove a package |
| `apt purge` | Remove package + config |
| `apt search` | Search for a package |
| `apt show` | Show package details |
| `apt list --installed` | List installed packages |

**Examples:**

```bash
sudo apt install nginx
sudo apt remove nginx
apt search nginx
apt show nginx
```

---

### 3. `uname`

**Meaning:** Print system information (kernel name, version, architecture, etc.).

| Flag | Meaning |
|------|---------|
| `-a` | All information |
| `-r` | Kernel release |
| `-s` | Kernel name |
| `-m` | Machine hardware (architecture) |
| `-n` | Hostname |

**Examples:**

```bash
uname              # Linux
uname -r           # 6.8.0-31-generic
uname -a           # Full system info
uname -m           # x86_64
```

---

### 4. `du`

**Meaning:** Estimate file space usage (Disk Usage). Shows how much space directories and files take up.

| Flag | Meaning |
|------|---------|
| `-h` | Human-readable (KB, MB, GB) |
| `-s` | Summary only (total per argument) |
| `-a` | All files, not just directories |
| `--max-depth=N` | Limit recursion depth |

**Examples:**

```bash
du -sh folder/                   # Total size of folder
du -h --max-depth=1              # Sizes at depth 1
du -ah /var/log | sort -h        # Sorted sizes
```

---

### 5. `df`

**Meaning:** Report file system disk space usage (Disk Free). Shows available and used space on mounted drives.

| Flag | Meaning |
|------|---------|
| `-h` | Human-readable |
| `-T` | Show filesystem type |
| `-i` | Show inode usage |
| `-a` | Include pseudo filesystems |

**Examples:**

```bash
df -h
df -hT
df -i
```

---

### 6. `top`

**Meaning:** Display a dynamic, real-time view of running processes, CPU, and memory usage.

| Key | Action |
|-----|--------|
| `q` | Quit |
| `k` | Kill a process |
| `M` | Sort by memory |
| `P` | Sort by CPU |
| `1` | Show CPU cores individually |

**Examples:**

```bash
top
top -u username         # Processes for a specific user
top -p PID              # Monitor a specific PID
```

---

### 7. `kill`

**Meaning:** Send a signal to a process by its PID (Process ID), typically to terminate it.

| Signal | Number | Meaning |
|--------|--------|---------|
| SIGHUP | 1 | Hangup |
| SIGINT | 2 | Interrupt (Ctrl+C) |
| SIGKILL | 9 | Force kill |
| SIGTERM | 15 | Graceful terminate (default) |
| SIGSTOP | 19 | Pause |

**Examples:**

```bash
kill PID
kill -9 PID             # Force kill
kill -15 PID            # Graceful (default)
kill -l                 # List all signals
```

---

### 8. `pkill`

**Meaning:** Kill processes by name or other attributes instead of PID.

| Flag | Meaning |
|------|---------|
| `-f` | Match full command line |
| `-u` | Match by user |
| `-9` | Force kill |

**Examples:**

```bash
pkill firefox
pkill -f "python script.py"
pkill -9 -u john
```

---

### 9. `adduser`

**Meaning:** Add a user to the system (a friendlier wrapper around `useradd` that also creates the home directory and prompts for a password).

**Examples:**

```bash
sudo adduser john
sudo adduser john sudo        # Add user to sudo group
```

---

### 10. `usermod`

**Meaning:** Modify a user account (e.g., change groups, home directory, shell, or login name).

| Flag | Meaning |
|------|---------|
| `-aG` | Append user to supplementary groups |
| `-d` | Change home directory |
| `-s` | Change shell |
| `-l` | Change username |
| `-L` | Lock account |
| `-U` | Unlock account |

**Examples:**

```bash
sudo usermod -aG sudo john
sudo usermod -s /bin/zsh john
sudo usermod -L john             # Lock account
sudo usermod -U john             # Unlock
```

---

### 11. `ln`

**Meaning:** Make links between files. By default creates hard links; with `-s`, creates symbolic (soft) links.

| Flag | Meaning |
|------|---------|
| `-s` | Symbolic link |
| `-f` | Force (overwrite existing) |
| `-v` | Verbose |

**Examples:**

```bash
ln file.txt hardlink.txt         # Hard link
ln -s /etc/passwd mypasswd       # Symlink
ln -sf /new/target link          # Force symlink
```

---

### 12. `chmod`

**Meaning:** Change file mode bits (permissions) for users, groups, and others.

| Value | Meaning |
| r-------|---------|
| 7 | rwx |
w| 6 | rw- |
|-r 5 | r-x |
| 4-- | r-- |
| 0 | --- |

**Examples:**

```bash
chmod 755 script.sh              # rwxr-xr-x
chmod 644 file.txt               #r--
chmod +x script.sh               # Add execute
chmod -w file.txt                # Remove write
chmod u+x,g+r file.txt           # Symbolic mode
```

---

### 13. `chown`

**Meaning:** Change file owner and group.

| Flag | Meaning |
|------|---------|
| `-R` | Recursive |
| `-v` | Verbose |
| `user:group` | Change both owner and group |

**Examples:**

```bash
chown user file.txt
chown user:group file.txt
sudo chown -R user:group folder/
```

---

### 14. `apt update`

**Meaning:** Update the list of available packages and their versions (refreshes the package index). Does **not** install or upgrade anything.

**Examples:**

```bash
sudo apt update
```

---

### 15. `apt upgrade`

**Meaning:** Install newer versions of all packages currently installed on the system. It does **not** remove packages or change dependencies.

**Examples:**

```bash
sudo apt upgrade
sudo apt upgrade -y              # Auto-confirm
```

---

### 16. `apt dist-upgrade`

**Meaning:** Upgrade the system, intelligently handling changing dependencies (may remove obsolete packages). It can install new packages and remove old ones as needed.

**Examples:**

```bash
sudo apt dist-upgrade
```

---

### 17. `apt full-upgrade`

**Meaning:** Similar to `dist-upgrade`, performs a complete system upgrade and handles dependencies. In newer versions of `apt`, `full-upgrade` is an alias for `dist-upgrade`.

**Examples:**

```bash
sudo apt full-upgrade
```

---

### 18. `apt autoremove`

**Meaning:** Remove packages that were automatically installed to satisfy dependencies for other packages and are now no longer needed.

**Examples:**

```bash
sudo apt autoremove
sudo apt autoremove --purge      # Also remove config files
```

---

### 19. `ssh-keygen`

**Meaning:** Generate, manage, and convert authentication keys for SSH (Secure Shell).

| Flag | Meaning |
|------|---------|
| `-t` | Key type (rsa, ed25519, ecdsa) |
| `-b` | Key size (bits) |
| `-f` | Output file |
| `-C` | Comment |

**Examples:**

```bash
ssh-keygen -t ed25519
ssh-keygen -t rsa -b 4096
ssh-keygen -t ed25519 -C "john@example.com"
ssh-copy-id user@host            # Copy public key to server
```

---

### 20. `systemd`

**Meaning:** The system and service manager (init system) for Linux. It is PID 1 and manages services, mounts, timers, sockets, etc.

> **Note:** You usually interact with it via `systemctl`, not by running `systemd` directly.

**Examples:**

```bash
ps -p 1                          # Show systemd as PID 1
systemctl --version
```

---

### 21. `service`

**Meaning:** Run a System V init script (legacy command used to start/stop services; often redirects to `systemctl` on modern systems).

**Examples:**

```bash
sudo service nginx start
sudo service nginx stop
sudo service nginx restart
sudo service nginx status
```

---

### 22. `systemctl`

**Meaning:** Control the systemd system and service manager (e.g., start, stop, restart, enable, or check the status of services).

| Command | Purpose |
|---------|---------|
| `start` | Start now |
| `stop` | Stop now |
| `restart` | Restart |
| `reload` | Reload config |
| `enable` | Start at boot |
| `disable` | Do not start at boot |
| `status` | Show status |

**Examples:**

```bash
systemctl status nginx
sudo systemctl start nginx
sudo systemctl enable nginx
systemctl --failed
systemctl list-units --type=service
```

---

### 23. `crontab`

**Meaning:** Maintain crontab files for individual users, used to schedule recurring tasks (cron jobs).

| Flag | Meaning |
|------|---------|
| `-e` | Edit crontab |
| `-l` | List crontab |
| `-r` | Remove crontab |
| `-u user` | Specify user |

**Cron syntax:**

```
* * * * * command
│ │ │ │ │
│ │ │ │ └── day of week (0-7)
│ │ │ └──── month (1-12)
│ │ └────── day of month (1-31)
│ └──────── hour (0-23)
└────────── minute (0-59)
```

**Examples:**

```bash
crontab -e
crontab -l
0 3 * * * /home/user/backup.sh   # Daily at 3 AM
```

---

### 24. `ufw`

**Meaning:** Uncomplicated Firewall; a user-friendly frontend for managing iptables/netfilter firewall rules.

| Command | Purpose |
|---------|---------|
| `enable` | Enable firewall |
| `disable` | Disable firewall |
| `allow` | Allow a port/service |
| `deny` | Deny a port/service |
| `status` | Show rules |

**Examples:**

```bash
sudo ufw enable
sudo ufw allow 22
sudo ufw allow 80/tcp
sudo ufw deny 23
sudo ufw status verbose
```

---

### 25. `sudo`

**Meaning:** Execute a command as another user, typically the superuser (root). Uses your own password.

| Flag | Meaning |
|------|---------|
| `-i` | Root shell |
| `-u user` | Run as another user |
| `-l` | List allowed commands |

**Examples:**

```bash
sudo apt update
sudo -i                          # Root shell
sudo -u john whoami
sudo -l                          # What can I sudo?
```

---

### 26. `su`

**Meaning:** Substitute user identity; switch to another user account (usually root). Requires the target user's password.

| Flag | Meaning |
|------|---------|
| `-` | Load target's environment |
| `-c` | Run a single command |

**Examples:**

```bash
su -                             # Switch to root shell
su - john                        # Switch to john
su -c "whoami" john              # Run one command as john
```

---

### 27. `rsyslog`

**Meaning:** The rocket-fast system for log processing. It is the primary logging daemon on many Linux distributions, responsible for collecting and storing system logs (usually found in `/var/log/`).

**Examples:**

```bash
systemctl status rsyslog
cat /etc/rsyslog.conf
ls /var/log/
journalctl -u rsyslog
```

**Common log files managed by rsyslog:**

| Path | Purpose |
|------|---------|
| `/var/log/syslog` | General system logs |
| `/var/log/auth.log` | Authentication |
| `/var/log/kern.log` | Kernel |
| `/var/log/mail.log` | Mail |

---

## 3. Quick Reference Cheat Sheet

| Command | Purpose |
|---------|---------|
| `ps aux` | List all processes |
| `apt install pkg` | Install package |
| `uname -r` | Kernel version |
| `du -sh folder` | Folder size |
| `df -h` | Disk space |
| `top` | Live process view |
| `kill -9 PID` | Force kill |
| `pkill name` | Kill by name |
| `adduser user` | Add user |
| `usermod -aG sudo user` | Add user to sudo |
| `ln -s target link` | Symlink |
| `chmod 755 file` | Change permissions |
| `chown user:group file` | Change owner |
| `apt update` | Refresh package list |
| `apt upgrade` | Upgrade packages |
| `apt dist-upgrade` | Smart upgrade |
| `apt full-upgrade` | Full upgrade |
| `apt autoremove` | Remove unneeded |
| `ssh-keygen -t ed25519` | SSH key |
| `systemd` | Init system (PID 1) |
| `service nginx start` | Legacy service |
| `systemctl start nginx` | Start service |
| `crontab -e` | Edit cron jobs |
| `ufw allow 22` | Firewall rule |
| `sudo cmd` | Run as root |
| `su -` | Switch to root |
| `rsyslog` | Logging daemon |

---

**End of Notes.**
