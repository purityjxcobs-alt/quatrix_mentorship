# Practical Assessment #1 - Test Traccar

* This is a hands-on practical assessment where you work on one of our test servers: test.traccar.quatrixglobal.com

# Basic Linux Administration

### Step 1 : Set Up Mobile SSH Emergency Access

* Downloaded Terminus on my mobile phone

* Inside the app settings, look for Connections or Keys and select Generate New Key

* Copy that long string of text (the public key) from your phone screen.

```bash
vi ~/.ssh/authorized_keys
```
Then press ;
1. Uppercase letter G to jump the cursore to the bottom line 

2. Press the lowercase letter o on your keyboard. This creates a fresh new line 

```bash
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIGQ9BJUp7l4vdy0T5v4RHA7XuRyNccdf78tjKLAco4zv pkinoti-iphone-termius
```
4. Save and exit 

1. ESC
2. :wq
3. enter

### Step 5: Check System Versions Using cat

```bash
cat /etc/os-release
```
Expected Output :


```bash
PRETTY_NAME="Debian GNU/Linux 13 (trixie)"
NAME="Debian GNU/Linux"
VERSION_ID="13"
VERSION="13 (trixie)"
VERSION_CODENAME=trixie
DEBIAN_VERSION_FULL=13.6
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
```

* The Linux Part: The underlying engine (the kernel) running your system is Linux.

* The Debian Part: The user interface, package tools, and system setup are built by Debian.

* so, your system version can be accurately summarized as Debian GNU/Linux 13 (Trixie).

* The GNU is the body interior the tools , like cat , grep ,sed ,vi and the bash terminal itself however , they were missing the engine to make it all run

* Linux is the engine (kernel) , that talks directly to your computer hardware , memory and cpu 

* When they combine they create a complete OS hence Debian GNU/LINUX

### Step 6 : Fully Upgrade the Debian Packages

```bash
sudo apt update && sudo apt full-upgrade -y
```
### Step 7 : Update the hostname so that it reads test-traccar

```bash
hostname
```
# Step 8 : Fail2ban updating : 
### Step 8 a) . Check the nginx logs for potential intrusion attacks. Usually requests that end in 404 are potential attacks

* We will use grep to search the live Nginx access log file for failed requests resulting in a 404 Not Found status error code.

```bash
sudo grep " 404 " /var/log/nginx/access.log | tail -n 20
```
* It reads the Nginx log, filters out lines containing a 404 error code using grep, and shows you the last 20 records using tail to earn you full methodology marks.

Expected Output ; 

```bash
20.91.226.158 - ```bash
sudo grep " 404 " /var/log/nginx/access.log | tail -n 20
```- [04/Aug/2026:00:30:37 +0000] "GET /wp-content/plugins/hellopress/wp_filemanager.php HTTP/1.1" 404 460 "-"```bash
sudo grep " 404 " /var/log/nginx/access.log | tail -n 20
``` "-"
34.106.32.153 - - [04/Aug/2026:02:28:05 +0000] "GET /htdocs/.git/config HTTP/1.1" 404 430 "-" "crusader-worker/1.0"
34.106.32.153 - ```bash
sudo grep " 404 " /var/log/nginx/access.log | tail -n 20
```- [04/Aug/2026:02:28:05 +0000] "GET /backend/.git/config HTTP/1.1" 404 431 "-" "crusader-worker/1.0"
34.106.32.153 - - [04/Aug/2026:02:28:05 +0000] "GET /.git/config HTTP/1.1" 404 423 "-" "crusader-worker/1.0"
34.106.32.153 - - [04/Aug/2026:02:28:05 +0000] "GET /app/.git/config HTTP/1.1" 404 427 "-" "crusader-worker/1.0"
136.109.219.64 - - [04/Aug/2026:02:50:26 +0000] "GET /site/.git/config HTTP/1.1" 404 428 "-" "crusader-worker/1.0"
136.109.219.64 - - [04/Aug/2026:02:50:26 +0000] "GET /var/www/.git/config HTTP/1.1" 404 431 "-" "crusader-worker/1.0"
136.109.219.64 - - [04/Aug/2026:02:50:26 +0000] "GET /app/.git/config HTTP/1.1" 404 427 "-" "crusader-worker/1.0"
136.109.219.64 - - [04/Aug/2026:02:50:26 +0000] "GET /public/.git/config HTTP/1.1" 404 430 "-" "crusader-worker/1.0"
136.109.219.64 - - [04/Aug/2026:02:50:26 +0000] "GET /backend/.git/config HTTP/1.1" 404 431 "-" "crusader-worker/1.0"
136.109.219.64 - - [04/Aug/2026:02:50:26 +0000] "GET /.git/config HTTP/1.1" 404 423 "-" "crusader-worker/1.0"
136.109.219.64 - - [04/Aug/2026:02:50:26 +0000] "GET /wordpress/.git/config HTTP/1.1" 404 433 "-" "crusader-worker/1.0"
136.109.219.64 - - [04/Aug/2026:02:50:26 +0000] "GET /htdocs/.git/config HTTP/1.1" 404 430 "-" "crusader-worker/1.0"
136.109.219.64 - - [04/Aug/2026:02:50:26 +0000] "GET /html/.git/config HTTP/1.1" 404 428 "-" "crusader-worker/1.0"
136.109.219.64 - - [04/Aug/2026:02:50:26 +0000] "GET /www/.git/config HTTP/1.1" 404 427 "-" "crusader-worker/1.0"
136.109.219.64 - - [04/Aug/2026:02:50:26 +0000] "GET /src/.git/config HTTP/1.1" 404 427 "-" "crusader-worker/1.0"
136.109.219.64 - - [04/Aug/2026:02:50:26 +0000] "GET /api/.git/config HTTP/1.1" 404 4492 "-" "crusader-worker/1.0"
66.249.71.69 - - [04/Aug/2026:05:32:14 +0000] "GET /robots.txt HTTP/1.1" 404 94 "-" "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
66.249.64.230 - - [04/Aug/2026:06:47:14 +0000] "GET /robots.txt HTTP/1.1" 404 118 "-" "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
66.249.64.231 - - [04/Aug/2026:06:47:15 +0000] "GET / HTTP/1.1" 404 181 "-" "Mozilla/5.0 (Linux; Android 6.0.1; Nexus 5X Build/MMB29P) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/150.0.7871.186 Mobile Safari/537.36 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
```
* This log file shows clear evidence of automated malicious scanning combined with normal search engine indexing.

Explanation of one line ; 

```bash
34.106.32.153 - - [04/Aug/2026:02:28:05 +0000] "GET /htdocs/.git/config HTTP/1.1" 404 430 "-" "crusader-worker/1.0"
```
1. 34.106.32.153 (Client IP Address): The network address of the computer making the request.

2. 04/Aug/2026:02:28:05 +0000] (Timestamp): The exact date, time, and timezone tracking when the packet hit your Nginx web proxy.

3. "GET /htdocs/.git/config HTTP/1.1" (HTTP Request):

* GET means the client is trying to pull down or read a file.

* /htdocs/.git/config is the target directory path.

* HTTP/1.1 is the web communication protocol standard used.

4. 404 (HTTP Status Code): "Not Found." The server tells the client that this target path does not exist.

5. 430 (Data Size): The payload response size returned to the client in bytes.

6. Crusader-worker/1.0" (User Agent): The identification signature of the software making the request. Real humans browsing websites use agents like Chrome or Safari. crusader-worker is a known automated vulnerability scanning script.

### Step 8 b). If you find credible new threats, add them to the nginx-brute filter if it exists. If it doesn't exist, create one.

*  Create or Update the nginx-brute Filter 

```bash
sudo vi /etc/fail2ban/filter.d/nginx-brute.conf
```
Explaining the command ; 

1. sudo: Runs the operation with superuser (administrator) privileges. This is mandatory because system security configuration files inside /etc/ are locked down and cannot be modified by standard users.

2. vi:  visual text editor 

3. /etc/fail2ban/filter.d/: This is the specific system directory where Fail2ban stores its application filter definitions.

4. nginx-brute.conf: The specific configuration file name
