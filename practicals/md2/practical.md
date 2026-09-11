# Practical Assessment #2 - Test Jenkins

### * This is a hands-on practical assessment where you work on one of our test jenkins servers: test.jenkins.quatrixglobal.com

# Pre-Requisites

### * Created your quatrix-mentorship repo and added a folder called practicals

### * Completion of following modules:

1. #### Bash

2. #### Git

3. #### Linux Sys Admin module 


# Instructions:

### * We will be using the following server: test.jenkins.quatrixglobal.com

### * Jenkins Forums and Google in general.

### * If making changes to sshd, ufw or fail2ban, make sure to always have an extra ssh session open so that if you misconfigure either of them, you don’t lock yourself out. Having an extra ssh session is an insurance that allows you to correct the error.

# Basic Linux Administration

## Question 1 . Update Debian to version 13.0 Trixie

```bash
cat /etc/os-release
```
## Question 2 . Update the hostname so that it reads test-jenins and not just test 

### Step 1 : Verify the current static name 

```bash
hostnamectl
```
### Expected Output ;

```bash
Static hostname: test-traccar
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: 26f89979ac0f4b4da717c7b918c8476e
         Boot ID: 6c72e1b1ddf74a2f94af72a2d4895269
  Virtualization: kvm
Operating System: Debian GNU/Linux 13 (trixie)    
          Kernel: Linux 6.1.0-31-amd64
    Architecture: x86-64
 Hardware Vendor: DigitalOcean
  Hardware Model: Droplet
Firmware Version: 20171212
```

### Step 2 : Change the static name to test-jenkins 

```bash
sudo hostnamectl set-hostname test-jenkins
```
### Step 3 : Update the /etc/host file on the server 

```bash
sudo vi /etc/hosts
```

### Step 4 : Look for the line containg the old hostname test

```bash
127.0.0.1       test.traccar.quatrixglobal.com test-traccar
```
### Step 5 : Change the test-traccar to test-jenkins

```bash
127.0.0.1       test.jenkins.quatrixglobal.com test-jenkins
```
### Step 6 : Save and exit 

#### * CTRL + O

#### * ENTER

#### * CRTL + X

### Step 7 : Verify the change 

```bash
hostnamectl
```

### Step 8 : To view the host file

```bash
cat /etc/hosts
```
!!!!!!

# Networking & Security

# Question 1 : Ensure sshd (OpenSSH) on the server is configured such that

### a. Users can only authenticate using an ssh key

### b.The root user is blocked from accessing ssh access remotely.

### Step 1 : Opening the SSH configuration file 

```bash
sudo nano /etc/ssh/sshd_config
```

### Step 2 : Disable password authentication

### * find the line matching PasswordAuthentication. If it has a hashtag # in front of it, remove the hashtag to uncomment it, and set it to no

```bash
PasswordAuthentication no
```
### Step 3 : Add this lines 

```bash
PubkeyAuthentication yes
KbdInteractiveAuthentication no
```

# Question 1b . The root user is blocked from accessing ssh access remotely.

### Step 1 : Block remote root access

#### * To block the root user from accessing the server remotely, find the PermitRootLogin line, uncomment it if necessary, and change its value to no

```bash
PermitRootLogin no
```
### Step 2 : Test and restart the SSH service

#### * Test the configuration file for syntax errors before applying it

```bash
sudo sshd -t
```
### Step 3 : Restart the ssh deamon to apply the changes 

```bash
sudo systemctl restart sshd
```
### Step 4 : To verify all the changes made in the ssh config file 

```bash
cat /etc/ssh/sshd_config | grep -v '^[[:space:]]*#' | grep -v '^[[:space:]]*$'
```
### Explain the command :

#### 1. cat /etc/ssh/sshd_config – Reads and outputs the entire file.

#### 2. grep -v '^[[:space:]]*#' – Inverts the match (-v) to exclude any lines starting with # (comments).

#### 3. grep -v '^[[:space:]]*$' – Inverts the match to exclude entirely blank lines.

### OR ?


```bash
sudo sshd -T | grep -E "passwordauthentication|permitrootlogin|pubkeyauthentication"
```

### Expected output :


```bash
permitrootlogin no
pubkeyauthentication yes
passwordauthentication no
```
# Question 2 : Install ufw (uncomplicated Firewall) and enable:

# Question 2 a : OpenSSH

### Step 1 : Install UFW

```bash
sudo apt update && sudo apt install ufw -y
```
### Step 2 . Allow OpenSSH 


```bash
sudo ufw allow OpenSSH
```

# Question 2 b : Allow HTTP

### Step 3 

```bash
sudo ufw allow 80/tcp
```
# Question 2 c : Allow HTTPS

### Step 4 
```bash
sudo ufw allow 443/tcp
```
### Step 5 

### To verify that the rules have been added 

```bash
sudo ufw show added
```

### Step 6 : Enable the firewall 

```bash
sudo ufw enable
```
### Step 7 : Check the final active status

```bash
sudo ufw status verbose
```
### Expected output :

```bash
pkinoti@test-jenkins:~$ sudo ufw status verbose
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp (OpenSSH)           ALLOW IN    Anywhere                  
80,443/tcp (Nginx Full)    ALLOW IN    Anywhere                  
5055                       ALLOW IN    Anywhere                  
80/tcp                     ALLOW IN    Anywhere                  
443/tcp                    ALLOW IN    Anywhere                  
22/tcp (OpenSSH (v6))      ALLOW IN    Anywhere (v6)             
80,443/tcp (Nginx Full (v6)) ALLOW IN    Anywhere (v6)             
5055 (v6)                  ALLOW IN    Anywhere (v6)             
80/tcp (v6)                ALLOW IN    Anywhere (v6)             
443/tcp (v6)               ALLOW IN    Anywhere (v6)   
```
# Question 3 : Install fail2ban and configure it to prevent
# a . Brute force ssh authentication attacks
# b . Exempt Applewood, Yard and Trio from sshd bans. For remote Quatrix interns, exempt your home network from fail2ban rules.

### Step 1 : Install Fail2ban 

```bash
sudo apt update && sudo apt install fail2ban -y
```

### Step 2 : Create a local configuration file 

```bash
sudo nano /etc/fail2ban/jail.d/sshd.local
```
### Step 3 : Add the custom configration file 

```bash
[sshd]
enabled = true
port = ssh
filter = sshd
maxretry = 5
findtime = 10m
bantime = 1h

# Whitelist local machine, Yard, Applewood/QX, Trio, and your home network
ignoreip = 127.0.0.1/8 ::1 102.215.13.6 41.90.10.170 197.232.110.49 41.139.233.235 197.248.171.13 YOUR_HOME_IP_HERE
```

### Step 4 : Enable and start the service 

```bash
sudo systemctl enable fail2ban --now
```

### Step 5 : Reload it t apply the new configuration

```bash
sudo fail2ban-client reload
```
### Step 6 : Verify the setup SSH jail is active 


```bash
sudo fail2ban-client status sshd
```

### Step 7 : Check the Fail2ban is successfully reading the new ips 

```bash
sudo fail2ban-client get sshd ignoreip
```

