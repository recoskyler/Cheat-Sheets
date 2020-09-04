# Linux Commands Cheat Sheet

**I'm not responsible for any disaster you may cause. Use at your own risk!**

- [Linux Commands Cheat Sheet](#linux-commands-cheat-sheet)
  - [Most common commands](#most-common-commands)
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
    - [Update packages](#update-packages)
  - [Connect to SSH with PKA](#connect-to-ssh-with-pka)
  - [Set up public key authentication](#set-up-public-key-authentication)
    - [Check if there is already a key pair](#check-if-there-is-already-a-key-pair)
    - [Delete old pair and generate new pair](#delete-old-pair-and-generate-new-pair)
    - [Generate new key pair](#generate-new-key-pair)
    - [Copy public key](#copy-public-key)
    - [Secure the key pair](#secure-the-key-pair)
    - [Add your public key to server, service or application](#add-your-public-key-to-server-service-or-application)
      - [Add to SSH](#add-to-ssh)
      - [Add to GitHub](#add-to-github)
  - [About](#about)

## Most common commands

### Print working directory

```bash
pwd
```

### Go to directory

```bash
cd PATH
```

```bash
cd /mnt/c
```

To go back to previous directory:

```bash
cd ..
```

### List files

```bash
ls -hal [PATH]
```

```bash
ls -hal /mnt/c
```

### Create file

```bash
touch PATH
```

### Edit file

```bash
nano PATH
```

### Print file

```bash
cat PATH
```

### Create directory

```bash
mkdir PATH
```

### Remove file

```bash
rm PATH [PATH] [...PATH]
```

```bash
rm /abc/test.txt
```

```bash
rm /abc/text.txt test.txt app.zip
```

### Remove directory

```bash
rmdir PATH [PATH] [...PATH]
```

### Remove directory and its content

```bash
rm -rf PATH [PATH] [...PATH]
```

### Change password

```bash
passwd [USERNAME]
```

### Run as Super-User

```bash
sudo COMMAND
```

```bash
sudo touch test.txt
```

### Switch to Super-User

```bash
su
```

### Update packages

```bash
sudo apt-get update || sudo apt upgrade
```

## Connect to SSH with PKA

*If you don't use ```[-p PORT]``` option, the default SSH port is used: **22***

*If you don't use ```[-i PRIVATE_KEY_FILE]``` option, the default key file is used (assuming it exists): ```~/.ssh/id_rsa```*

> **You must set up PKA (Public Key Authentication)**

```bash
ssh [-p PORT] [-i PRIVATE_KEY_FILE] USERNAME@SERVER_IP
```

```bash
ssh -p 2222 -i ~/.ssh/server-a-key my_user@192.168.2.25
```

## Set up public key authentication

You can use this highly secure method to connect to GitHub or SSH.

**DO NOT LEAVE YOUR PRIVATE KEY ```id_rsa``` IN THE DEVICE YOU WOULD LIKE TO CONNECT TO. PRIVATE KEY IS YOUR HOUSE KEY, DO NOT LEAVE ANY COPIES OR ITSELF AT HOME!**

### Check if there is already a key pair

```bash
ls -la ~/.ssh
```

If you see a pair of files named like: ```something``` and ```something.pub```, then that means there is already a key pair. 

Most commonly found as: ```id_rsa``` and ```id_rsa.pub```.

### Delete old pair and generate new pair

**Make sure you are not using the current key pair in any application/service etc. If you complete this step, THERE IS NO GOING BACK. If you think this key pair is still safe to use, please skip this step.**

```bash
rm id_rsa id_rsa.pub
```

### Generate new key pair

```bash
ssh-keygen
```

Follow the steps. I will be using the default values, and maybe a passphrase.

### Copy public key

```bash
cat ~/.ssh/id_rsa.pub
```

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

    ```bash
    nano ~/.ssh/authorized_keys
    ```

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

## About

Made by Adil Atalay Hamamcioglu, after failing to memorize even the simplest, shortest commands ;_; .
