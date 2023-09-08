### **How to SSH into your VM from your host and upload to github.**
GitHub primarily uses the Git version control system for managing and tracking changes to code repositories. Git is a distributed version control system that was originally developed by Linus Torvalds, the creator of Linux.

GitHub provides a web-based platform for hosting and collaborating on Git repositories. While Git is the underlying technology, GitHub adds a layer of features and functionality on top of Git. These include web-based repository management, code review tools, issue tracking, project management, and collaboration features.

To interact with GitHub repositories, you typically use Git commands on your local computer, such as **git clone**, **git pull**, **git push**, **git commit**, and **git merge**. These commands are part of the Git toolset, and GitHub provides a convenient hosting and collaboration platform for repositories managed with Git.

GitHub also provides an API that developers can use to interact with GitHub programmatically, allowing for automation and integration with other tools and services.

So, while GitHub itself is not a code or programming language, it is a web-based platform that facilitates code collaboration and project management, primarily using Git as the version control system.

### **Getting Started**

## **Step 1: Starting SSH Service from your VM**

To start the SSH service on a Linux-based Virtual Machine (VM), you'll need to use a command that's specific to the Linux distribution running on your VM. 
Below are examples for two common Linux distributions: 


Ubuntu (using systemctl) 
<pre>
sudo systemctl start ssh
</pre>

CentOS/Red Hat (using systemctl). 
<pre>sudo systemctl start sshd
</pre>
Please note that you'll need root or superuser privileges to perform these actions.

## **Step 2: Obtain VM IP Address**
You'll need the IP address of your VM to establish an SSH connection. You can usually find this information in your VM's settings or use a command like 
<pre>ifconfig</pre>or<pre>ip addr show</pre>within the VM to identify the IP address.

## **Step 3: Open a Terminal on Your Host**
On your host computer (the machine you're connecting from), open a terminal or command prompt.

## **Step 4: SSH into Your VM**
Use the ssh command to initiate an SSH connection to your VM. Replace username with your VM's **username** and **vm_ip_address** with the IP address of your VM:

<pre>
ssh username@vm_ip_address</pre>
Example:
<pre>
ssh blobphish@192.168.1.100</pre>
You'll be prompted to enter the password for your VM's user account.

## **Step 5: Navigate to Your Files**
Once connected to your VM via SSH, you can navigate to the directory where your files are located using standard Linux commands like <pre>cd</pre> 
and/or 
<pre>ls</pre>

## **Step 6: Generate a new private SSH key**
You must also add the public SSH key to your account on GitHub before you use the key to authenticate or sign commits.
Using the terminal that has been previously connected via SSH to your VM, Generate Secure Shell (SSH) Keys with the following command line:
<pre>ssh-keygen</pre>
Navigate to the key using the following command line in your terminal:
<pre>cd .ssh</pre>

You'll notice the following listed:
>id_rsa    id_rsa.pub    known_hosts    known_hosts.old

Use the following command line to see your **public** key.
<pre>cat id_rsa.pub </pre>

**It's important that you use the ".pub" file otherwise you're giving up your private key.**
The previous command will give you a series come letters and numbers that start with 'ssh-rsa'

## **Step 7: Add your _PUBLIC_ key to this repo**

#### **Remember not to add your private key** 
You'll set your private key later on your client to use to authenticate to github.

Make sure you create a new access token to authenticate. [Find this here.](https://github.com/settings/tokens)

When you first create the token the string will be shown but it won't be shown again. *Be sure to save this.*

#### **Run this command to set username and email:**
```
git config --global --edit
```
Uncomment the username and email lines.

#### **Create .git-credentials file in your home directory and add your token to this file.**

```
cd ~
```
```
nano .git-credentials
```
Example:
```
username:TOKEN@git@github.com:USERNAME/USERNAME.git
```

#### **Then, you need to clone a remote repository to your device.**
Example:
```
git clone git@github.com/USERNAME/USERNAME.git
```

**Once you have a local copy, we need to verify first that nothing is configured.**

```
git status

git remote -v

ssh -T git@github.com
```

#### **We should recieve responses here indicating nothing has been configured yet. Remember to always "check" yourself while on the terminal so you always know the current scenario.**

#### **We then need to add our SSH RSA private key to the ssh client.**

```
eval "$(ssh-agent -s)"
ssh-add -l
ssh-add ~/.ssh/privkey
ssh-add -l
ssh -T git@github.com
```
**This should ask you for your passphrase and log you in.**

#### ## **Step 7: Add the remote repository**

```
git remote -v
git status
```
#### **Note that you may have to run 'git remote set-url origin git@github.com:USERNAME/USERNAME.git' if the remote repo is set to HTTPS.**

#### **This should indicate that you have properly added the remote repository and are correctly configured to push changes.**

#### **Now we make changes to our directory and files, then push changes to our github.**

```
nano whatever.md
git add -A
git commit -am "whateveryouwant"
git push
```
note: you only have to run '--set-upstream origin main' once, and after that it isn't necessary but it will still work.

also note: don't run the git push command with sudo as it will break




































