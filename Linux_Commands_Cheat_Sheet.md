# Linux Commands Cheat Sheet

**I'm not responsible for any disaster you may cause. Use at your own risk!**

- [Linux Commands Cheat Sheet](#linux-commands-cheat-sheet)
  - [Most common commands](#most-common-commands)
    - [Getting help](#getting-help)
      - [Viewing help](#viewing-help)
      - [Viewing help for a command](#viewing-help-for-a-command)
      - [Viewing the manual of a command](#viewing-the-manual-of-a-command)
    - [Logout](#logout)
    - [Exit](#exit)
    - [Shutdown and reboot](#shutdown-and-reboot)
      - [Shutdown](#shutdown)
      - [Reboot](#reboot)
      - [Cancel scheduled shutdown or reboot](#cancel-scheduled-shutdown-or-reboot)
    - [Print working directory](#print-working-directory)
    - [Go to directory](#go-to-directory)
    - [List files](#list-files)
    - [Create file](#create-file)
    - [Edit file](#edit-file)
    - [Print file](#print-file)
    - [Create directory](#create-directory)
    - [Remove file](#remove-file)
    - [Remove directory](#remove-directory)
    - [Remove directory and its content](#remove-directory-and-its-content)
    - [Change password](#change-password)
    - [Run as Super-User](#run-as-super-user)
    - [Switch to Super-User](#switch-to-super-user)
    - [Update and upgrade packages](#update-and-upgrade-packages)
    - [Find files and commands](#find-files-and-commands)
      - [Update file indexing database](#update-file-indexing-database)
      - [Using "locate" command](#using-locate-command)
      - [Using "which" command](#using-which-command)
      - [Using "find" command](#using-find-command)
    - [List processes](#list-processes)
    - [Kill process](#kill-process)
  - [Connect to SSH [with PKA]](#connect-to-ssh-with-pka)
  - [Set up public key authentication](#set-up-public-key-authentication)
    - [Check if there is already a key pair](#check-if-there-is-already-a-key-pair)
    - [Delete old pair and generate new pair](#delete-old-pair-and-generate-new-pair)
    - [Generate new key pair](#generate-new-key-pair)
    - [Copy public key](#copy-public-key)
    - [Secure the key pair](#secure-the-key-pair)
    - [Add your public key to server, service or application](#add-your-public-key-to-server-service-or-application)
      - [Add to SSH](#add-to-ssh)
      - [Add to GitHub](#add-to-github)
    - [Fix Kali Linux APT (Virtual Box)](#fix-kali-linux-apt-virtual-box)
  - [About](#about)

## Most common commands

### Getting help

#### Viewing help

```help```

#### Viewing help for a command

```COMMAND --help```

```apt --help```

#### Viewing the manual of a command

```man COMMAND```

```man apt```

### Logout

```logout```

### Exit

```exit```

### Shutdown and reboot

#### Shutdown

```shutdown TIME```

```shutdown now```

```shutdown 11:00```

#### Reboot

```shutdown -r TIME```

```shutdown -r now```

```shutdown -r 23:00```

#### Cancel scheduled shutdown or reboot

```shutdown -c [MESSAGE]```

```shutdown -c```

```shutdown -c "Cancelled scheduled shutdown"```

### Print working directory

```pwd```

### Go to directory

"**~/**" is used instead of user's home directory (*/home/user*)
```~/.ssh/id_rsa``` = ```/home/user/id_rsa```

"**/**" is used instead of root directory (*/*)
```/.ssh``` != ```.ssh``` unless working directory is root (*/*)

```cd PATH```

```cd /mnt/c```

To go back to previous directory:

```cd ..```

### List files

```ls -hal [PATH]```

```ls -hal /mnt/c```

### Create file

```touch PATH```

### Edit file

```nano PATH```

### Print file

```cat PATH```

### Create directory

```mkdir PATH```

### Remove file

```rm PATH [PATH] [...PATH]```

```rm /abc/test.txt```

```rm /abc/text.txt test.txt app.zip```

### Remove directory

```rmdir PATH [PATH] [...PATH]```

### Remove directory and its content

```rm -rf PATH [PATH] [...PATH]```

### Change password

```passwd [USERNAME]```

### Run as Super-User

```sudo COMMAND```

```sudo touch test.txt```

### Switch to Super-User

```su```

### Update and upgrade packages

```sudo apt-get update && sudo apt upgrade```

### Find files and commands

#### Update file indexing database

For the ```locate``` command to work correctly, you will first need to update the file indexing database using the command:

```updatedb```

#### Using "locate" command

```locate``` command is used for finding files.

```locate FILENAME```

```locate abc.txt```

#### Using "which" command

```which``` command is used for finding command files/links, or checking whether a command exists in PATH.

```which COMMAND```

#### Using "find" command

```find``` command is used for finding directories.

```find DIRECTORY```

### List processes

Use these commands to get the PID (process ID) of a process, so that you can kill/restart the process.

```ps -A```

If there are too many processes, use the following command to scroll at your own pace:

```ps -A | less```

If you want to find a process by name:

```ps -A | grep firefox```

### Kill process

```kill PID```

```pkill PID```

To kill a process tree:

```killall PID```

To kill a graphical process:

```xkill PID```

## Connect to SSH [with PKA]

*If you don't use ```[-p PORT]``` option, the default SSH port is used: **22***

*If you don't use ```[-i PRIVATE_KEY_FILE]``` option, the default key file is used (assuming it exists): ```~/.ssh/id_rsa```*

You must set up PKA (Public Key Authentication) before these commands

```ssh [-p PORT] [-i PRIVATE_KEY_FILE] USERNAME@SERVER_IP```

```ssh -p 2222 -i ~/.ssh/server-a-key my_user@192.168.2.25```

## Set up public key authentication

You can use this highly secure method to connect to GitHub or SSH.

**DO NOT LEAVE YOUR PRIVATE KEY ```id_rsa``` IN THE DEVICE YOU WOULD LIKE TO CONNECT TO. PRIVATE KEY IS YOUR HOUSE KEY, DO NOT LEAVE ANY COPIES OR ITSELF AT HOME!**

### Check if there is already a key pair

```ls -la ~/.ssh```

If you see a pair of files named like: ```something``` and ```something.pub```, then that means there is already a key pair.

Most commonly found as: ```id_rsa``` and ```id_rsa.pub```.

### Delete old pair and generate new pair

**Make sure you are not using the current key pair in any application/service etc. If you complete this step, THERE IS NO GOING BACK. If you think this key pair is still safe to use, please skip this step.**

```rm id_rsa id_rsa.pub```

### Generate new key pair

```ssh-keygen```

Follow the steps. I will be using the default values, and maybe a passphrase.

### Copy public key

```cat ~/.ssh/id_rsa.pub```

Select and copy the output.

### Secure the key pair

```bash
chmod 600 ~/.ssh/id_rsa
chmod 600 ~/.ssh/id_rsa.pub
```

You can skip this step, however if you see "Insecure Key" error, please complete this step.

### Add your public key to server, service or application

#### Add to SSH

1. On the device which you would like to connect to (server etc.), create a file named ```authorized_keys``` and open for editing; using the command:
```nano ~/.ssh/authorized_keys```

2. Paste the public key you copied in step 4. Press ```Ctrl + X```, then ```Y```, and lastly press ```ENTER``` to save.

#### Add to GitHub

1. Open GitHub on your browser
2. Click on your profile picture on top right corner
3. Click on **Settings**
4. Go to **SSH and GPG keys** tab
5. Click **New SSH key** button, name your key and paste the public key you copied in step 4
6. Save by clicking **Add SSH key**
7. Now you can try connecting to ```git@github.com``` using [[#Connect to SSH with PKA]] method. You must have your private key to be able to do this step. You should see:

```txt
Hi USER! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```

### Fix Kali Linux APT (Virtual Box)

For some reason, whenever ```sudo apt-get update && sudo apt upgrade``` command to update the packages is run, it gives ```E: Failed to fetch store:/var/lib/apt/lists/partial/http.kali.org_kali_dists_kali-rolling_main_binary-amd64_Packages.gz  Hash Sum mismatch``` and ```E: Some index files failed to download. They have been ignored, or old ones used instead.``` errors. To fix this, you need to execute the following commands:

```bash
sudo bash
mkdir /etc/gcrypt
echo all >> /etc/gcrypt/hwf.deny
sudo apt-get update
```

## About

Made by Adil Atalay Hamamcioglu, after failing to memorize even the simplest, shortest commands ;_; .
