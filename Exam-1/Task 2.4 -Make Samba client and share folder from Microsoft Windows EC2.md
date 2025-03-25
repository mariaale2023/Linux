Make Samba client and share folder from Microsoft Windows EC2 using Public IP to access from Linux instance. 

### 1) create 2 EC2 Instance
-  one Linux : public IP 3-25-107-75
- one Windows: public IP 3-25-110-1
![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314151726.png)

### 2) install Samba Package

```bash
#Install samba packege
sudo yum install samba 
```
![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314152150.png)

### 3) Where are Samba file located


`grep` (Global Regular Expression Print) is a **command-line tool** used in Linux and Unix-like systems to **search for a specific text pattern within files or command outputs**.


```bash

# basic syntax
grep [OPTIONS] "pattern" [file]

## example : searching for a Word in a File
grep "error" /var/log/syslog

# to found Samba 
Ls -l / | grep "samba"
```

![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314152941.png)

The `grep` command did not help so I can use `/usr/bin`, witch is a directory containing system binaries (executable files).
```bash
ls -l /usr/bin
```

![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314153133.png)

we found `-rwxr-xr-x  1 root root  70552 Oct 16  2023 smbcontrol`

| **Column**    | **Meaning**                                                                                      |
| ------------- | ------------------------------------------------------------------------------------------------ |
| `-rwxr-xr-x`  | **File permissions**: Read, write, and execute for owner; read and execute for group and others. |
| `1`           | **Number of links** (typically `1` for files).                                                   |
| `root`        | **Owner of the file** (user `root`).                                                             |
| `root`        | **Group that owns the file** (group `root`).                                                     |
| `70552`       | **File size in bytes** (e.g., `70552` bytes ≈ 70 KB).                                            |
| `Oct 16 2023` | **Last modified date**.                                                                          |
| `smbcontrol`  | **Filename (the actual binary executable)**.                                                     |
- **`smbcontrol`** - Sends control messages to the `smbd` daemon.
- **`smbpasswd`** - Used to change **Samba passwords**.
- **`smbstatus`** - Displays current Samba **connections and status**.


| `-`   | **File type** (`-` = regular file, `d` = directory, `l` = symbolic link, etc.) |
| ----- | ------------------------------------------------------------------------------ |
| `rwx` | **Owner permissions** (Read `r`, Write `w`, Execute `x`)                       |
| `r-x` | **Group permissions** (Read `r`, No write `-`, Execute `x`)                    |
| `r-x` | **Others (everyone else) permissions** (Read `r`, No write `-`, Execute `x`)   |
```bash
ls -l /usr/share

##prompt
drwxr-xr-x.  3 root root  20 Mar 10 22:54 samba

```

| **Field**      | **Meaning**                                                                               |
| -------------- | ----------------------------------------------------------------------------------------- |
| `d`            | **Directory** (not a file)                                                                |
| `rwxr-xr-x`    | **Permissions** (explained below)                                                         |
| `.`            | SELinux security context marker (optional)                                                |
| `3`            | Number of **hard links** (subdirectories inside)                                          |
| `root root`    | **Owner** and **group** (both `root`)                                                     |
| `20`           | **Size** in bytes (for directories, this doesn't represent actual size but metadata size) |
| `Mar 10 22:54` | **Last modified date**                                                                    |
| `samba`        | **Directory name**                                                                        |

Inside the /etc/samba/ directory, stores **Samba configuration files**.
![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314155524.png)

1. **`lmhosts`** (LAN Manager Hosts File)
    - Used for **NetBIOS name resolution** (similar to `/etc/hosts` but for Windows/Samba).
    - Not commonly used in modern setups.
    
2. **`smb.conf`** (Samba Configuration File)
    - **Main configuration file for Samba**.
    - Defines **shared folders, authentication, network settings**.
```bash
# Can be edited with
    sudo nano /etc/samba/smb.conf
    
# Restart Samba after editing:
    sudo systemctl restart smb nmb
```
        
3. **`smb.conf.example`**
    
    - **Example configuration file** with predefined settings.
    - Useful for reference when setting up Samba.

### 4)  Set User and Create Password

Is necessary to  adds ec2-user to the Samba user database and prompts it to set a Samba password for that user. This is necessary because Samba maintains its own password system, separate from Linux system users.

```bash
sudo smbpasswd -a ec2-user

# promopt to create a new password for user ec2-uer
```

![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314160723.png)

- **`sudo`** → Runs the command as **root (superuser)** because modifying Samba user accounts requires elevated privileges.
- **`smbpasswd`** → The **Samba password management tool** used to create, modify, or delete Samba user passwords.
- **`-a`** → **Add a new Samba user** (`ec2-user`) or enable an existing one.
- **`ec2-user`** → The **Linux user account** that is being added to Samba.


To verify that `ec2-user` was successfully added to Samba, use:

```bash
sudo pdbedit -L
```


This will list all Samba users.\

###  5) Configure Samba to Share `/home/ec2-user/share`**

1. Open Samba config:
```bash
sudo nano /etc/samba/smb.conf
```   
1. Add this at the end:
```bash

[SharedFolder] 
	path = /home/ec2-user/share 
	valid users = ec2-user 
	read only = no 
	browsable = yes`
```
![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314170704.png)

### 6) change ownership of share directory
A directory `/home/ec2-user/share`  has been created to be used for Samba sharing. Also I  added some files to the directory. When I created the `/home/ec2-user/share` directory, this automatically become owner by the root, as we can see in the image above. This mean that only the “root” user can modify/write the folder and ec2-user or any other samba user will not be able to add, delete or modify files inside 

![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314170835.png)

If ec2-user is allowed to access the share via Samba but **doesn’t have write permissions on the Linux system**, they will see an **access denied error** when trying to write files. We can change this by using the `chown` command.

![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314170901.png)

### 7) Restart samba server and check status.

Restarting the Samba service ensures that configuration changes take effect and that the service is running properly. After Adding a New Samba User, restart Samba to apply the new user authentication.

1. **After Changing Samba Configuration (`smb.conf`)**
    
    - If you modify `/etc/samba/smb.conf`, you **must restart Samba** for changes to apply.
    ```bash
    sudo systemctl restart smb
# or
     sudo service smb restart
```

2. **After Adding a New Samba User**
    
    - If you run:
```bash 
sudo smbpasswd -a ec2-user
```

Restart Samba to apply the new user authentication.

3. **If Samba Stops Working or Fails**

    - If `smbclient` cannot connect or file sharing fails, check if Samba is running:

        ```bash
sudo systemctl status smb
        ```
    
    - If it's **inactive** or crashed, restart it:

```bash
sudo systemctl restart smb
```

4. **After Updating Samba**
    
    - If you install or update Samba, restarting ensures you’re using the latest version.
    
    ![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314172512.png)

With command ‘_Testparm’_ we check that No syntax errors detected in the Samba configuration.
![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314181204.png)

The message “Weak crypto is allowed by GnuTLS (e.g. NTLM as a compatibility fallback)” mean that samba is allowed older NTLM authentication, if we want to connect with windows older Windows machine, probably we need to change this configuration. However for this exercise we are using a EC2 – MS Windows server 2025 base 64-bit

 
![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314173634.png)

### Access to the share file system from windows Ec2

Remote the windows EC2 by RDP and map the network `\\<private IP linux>\ec2-user\share`


![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314174521.png)

![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314174600.png)
![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314180911.png)


Get network error to connect. Check is the windows ec2 can ping the Linux

```bash
ping <IP public Linux machin>
```
![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314185549.png)

Troubleshooting protocol and noticed that I need to add SMB (port 445 protocol)
![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314185635.png)

Tried connect again to the share system from Windows EC2 >> successful
![](../IMG/IMG%20-%20Task%202.4%20-Make%20Samba%20client%20and%20share%20folder%20from%20Microsoft%20Windows%20EC2/Pasted%20image%2020250314185753.png)


## **Report: Configuring and Troubleshooting Samba on AWS EC2**

The goal of this exercise was to set up a Samba file-sharing service on a Linux EC2 instance and access it from a Windows EC2 instance within the same AWS VPC.

### **Steps Taken**

We started by ensuring that the Linux EC2 instance was running Amazon Linux 2023. After confirming this, we installed Samba, which is needed to enable file sharing between Linux and Windows. To create a shared directory, we made a new folder and modified its permissions so that the Windows EC2 user could access it. We then configured Samba by updating its settings file to define the shared folder and allow the appropriate user to connect. After making these changes, we restarted the Samba service so that the new settings would take effect.

To enable authentication, we added the `ec2-user` to Samba and set up a password specifically for Samba access. We then verified that the user was properly added to the system. Since we did not configure any firewalls, our focus remained on the security group settings in AWS. We ensured that the security group assigned to the Linux EC2 instance allowed traffic on TCP port 445, which is required for SMB file sharing. Additionally, we confirmed that the Windows EC2 instance could communicate with the Linux EC2 instance by testing network connectivity through ping commands.

From the Windows EC2 instance, we attempted to access the shared folder by connecting to the Linux EC2 instance using its private IP address. When prompted for credentials, we entered the Samba username and password. To make access easier, we also attempted to map the shared folder as a network drive. Initially, there were some authentication issues, which we resolved by resetting the Samba password and verifying that the service was running properly.

During troubleshooting, we checked whether the Samba service was active and reviewed the logs for any errors. We also tested access from the Linux EC2 instance itself to ensure that the Samba configuration was correct. After resolving authentication issues, we were finally able to access the shared folder from Windows without any problems.

### **Conclusion**

This exercise successfully established a Samba file-sharing service on a Linux EC2 instance, allowing access from a Windows EC2 instance. The main challenges we encountered were related to user authentication and security group configurations, but these were systematically resolved. The setup now enables seamless internal file sharing within the AWS environment. However, for production use, additional security measures should be implemented to protect shared data.