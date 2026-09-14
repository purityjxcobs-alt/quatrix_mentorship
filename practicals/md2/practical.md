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
# Question 3 : Creating a user (follow the steps in practical assessment one)

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

# CI/CD - Jenkins

## Question 1 : Install Jenkins 

#### * Jenkins is written in Java, so we must install the Java runtime environment first, then add the official Jenkins software repository to your Debian 13 (Trixie) system.

### Step 1 : Install Java version 21  

```bash
sudo apt update && sudo apt install -y openjdk-21-jre-headless
```
### Explain the commands :

#### 1. apt update: Refreshes your package index using your fixed Trixie repository lines.

#### 2. apt install -y: Installs Java automatically without stopping to ask you for confirmation.

#### 3. Openjdk - This is the open-source version of Java.

#### 4 . 21 - this is the version number

#### 5 . JRE VS JDK : JRE stands for Java Runtime Environment . it contains the only tools needed to run and existing java program like jenkins . JDK Or Development kit id for writing codes 

#### 6 . Headless : this means it does not include graphical user interface compenents like windows , buttons pr desktop wallapapers because our linux server has no screen we dont need to waste space or meomery graphic 


### * Check the version 

```bash
java -version
```

### Step 2 : Download and install the jenkins GPG key

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://jenkins.io
```
### Explain command:

#### 1. wget -O [path]: Downloads the official Jenkins encryption security key from their website and saves it directly to your shared system keyrings folder.

### Step 3 : Add the official Jenkins Reposiory link 

```bash
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://jenkins.io binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

### Explain the command :

#### 1. echo "...": Formats the exact repository configuration layout.

#### 2. tee: Creates a dedicated standalone package mirror list file named /etc/apt/sources.list.d/jenkins.list.


### Step 4 : Update the list and intasll jenkins 

```bash
sudo apt update && sudo apt install -y jenkins
```
## Veifications 

### Step 1 : Verify the Reposiroty Address file 

#### * We need to make sure the address book points to the official warehouse (pkg.jenkins.io) and not the homepage website.

```bash
cat /etc/apt/sources.list.d/jenkins.list
```
### Expected Output :

```bash
deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/

```

### Step 2 : Veify the security Key file 

```bash
file /usr/share/keyrings/jenkins-keyring.asc && wc -c /usr/share/keyrings/jenkins-keyring.asc
```

### Expected Output :

```bash
/usr/share/keyrings/jenkins-keyring.asc: PGP public key block Public-Key (old)
1680 /usr/share/keyrings/jenkins-keyring.asc
```
### Explain the output:

### /usr/share/keyrings/jenkins-keyring.asc: PGP public key block Public-Key (old)

#### 1 . The file command looks inside the document to see its format structure. Seeing PGP public key block proves this is a real, uncorrupted security credential certificate (not a human web page or a broken file).

### 1680 /usr/share/keyrings/jenkins-keyring.asc

#### 1. The wc -c (word count -bytes) command measures the exact data size. 1680 means the file contains exactly 1,680 characters. This matches the official 2026 Jenkins cryptographic signature length perfectly.

### Step 3 . Verifing the unaltered cryporaphic PGP signature file 

```bash
cat /usr/share/keyrings/jenkins-keyring.asc
```

# Question 2 . Configure nginx and certbot to use the domain name https://test.jenkins.quatrixglobal.com to access Jenkins installation (If an email address is requested during certificate creation, use support@quatrixglobal.com)

### Step 1 : Install Nginx 

```bash
sudo apt-get install -y nginx
```

### Verify the status 

```bash
sudo systemctl status nginx
```

### Step 2 : Linking the Nginx server blocks to activate the mapping path for our server .

#### Check nginx configuration file if it exists 

```bash
cat /etc/nginx/sites-available/test.jenkins.quatrixglobal.com
```

### If it does not  create one 


```bash
sudo nano /etc/nginx/sites-available/test.jenkins.quatrixglobal.com
```

### Write this inside the text editor

```bash
server {
    listen 80;
    server_name test.jenkins.quatrixglobal.com;

    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

```
### Step 3 : Check if the the domain name maps poperly to an ip address

```bash
host test.jenkins.quatrixglobal.com || ping -c 1 test.jenkins.quatrixglobal.com
```

### Expected Output :

```bash
test.jenkins.quatrixglobal.com has address 165.232.162.109
```

### Step 4 : Link the Route and Run Pre-Flight Syntax Tests

```bash
sudo ln -s /etc/nginx/sites-available/://quatrixglobal.com /etc/nginx/sites-enabled/
```
### To verify : 

```bash
ls -l /etc/nginx/sites-enabled/
```

### Expected Output :

```bash
total 0
lrwxrwxrwx 1 root root 34 Sep 14 09:19 default -> /etc/nginx/sites-available/default
lrwxrwxrwx 1 root root 57 Sep 14 10:05 test.jenkins.quatrixglobal.com -> /etc/nginx/sites-available/test.jenkins.quatrixglobal.com
```

### To check the active folder :

```bash
sudo nginx -t
```

### Step 5 : Install the Certbot

```bash
sudo apt-get install -y certbot python3-certbot-nginx
```
### Explain the command :

#### 1. certbot: The core application that handles requesting and renewing security certificates from Let's Encrypt

#### 2. python3-certbot-nginx: The plugin that allows Certbot to read your Nginx configurations and insert the encryption keys automatically.

### Step 6 : Verify the version 

```bash
certbot --version
```

### Step 7 : Run Certbot to encrpy the connection with out lets encrypt SSL certifacate 

```bash
sudo certbot --nginx -m support@quatrixglobal.com --agree-tos --no-eff-email -d ://quatrixglobal.com
```

### Explain the command :

#### 1. --nginx: Tells Certbot to automatically find your Nginx server block and upgrade it from insecure HTTP to secure HTTPS (port 443).

#### 2. -m support@quatrixglobal.com: Registers your tech support team address to receive urgent security updates or expiration reminders.

#### 3. --agree-tos: Automatically accepts Let's Encrypt's global subscriber terms of service agreement.

#### 4. -d ...: Specifies the exact domain name mapping route to encrypt.