
1) Armaan connect to the EC2 Linux instance
![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226180349.png)![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226180411.png)

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226181146.png)
![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226181103.png)![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226181241.png)![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226181446.png)

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226181610.png)![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226181801.png)

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226181927.png)

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226182010.png)

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226182040.png) 

```
man ln
ln fisrtfile.txt fun
ls
```

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226182407.png)

## FIND:

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226182531.png)

man find
![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226182512.png)

```
find . -name "*.txt"
find /home . -name "*.txt"
find /usrhome . -name "*.bin"
```

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226182545.png)![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226182702.png)

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226182914.png)

```sudo mkdir -p abc/def/pqr/lmn/xyz```

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226183040.png) 

## Chmod

```
chmod 777 newfile.txt
ls -l n*


#other way:
chmod u-rwx newfile.txt
ls -l n*

#other way:
chmod u+r,g-w newfile.txt
ls -l n*

#other way:
chmod u+r,g+w newfile.txt
ls -l n*


#other way:
chmod u-r+w,g+w newfile.txt
ls -l n*

#other way:
chmod ugw-rwx newfile.txt
ls -l n*

#other way:
chmod ugw+rwx newfile.txt
ls -l n*
```

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226183952.png)
Let's break down each of these `chmod` commands and the resulting `ls -l n*` output.

**Understanding `chmod`**

`chmod` stands for "change mode." It's used to modify the permissions of files and directories in Unix-like systems (like Linux and macOS). Permissions control who can read, write, and execute a file.

- **Symbolic Mode:** This is the format used in your examples (e.g., `u+r`, `g-w`). It's more human-readable.
    
    - **`u` (user):** Refers to the file's owner.
    - **`g` (group):** Refers to the group that owns the file.
    - **`o` (others):** Refers to everyone else.
    - **`a` (all):** Applies the change to user, group, and others.
    - **`+`:** Adds a permission.
    - **`-`:** Removes a permission.
    - **`=`:** Sets permissions exactly (overwrites existing ones).
    - **`r` (read):** Allows viewing the file's contents.
    - **`w` (write):** Allows modifying the file's contents.
    - **`x` (execute):** Allows running the file (if it's a program or script).
- **Numeric Mode:** Uses octal numbers (e.g., `777`). Each digit represents permissions for user, group, and others, respectively.
    
    - `4`: Read permission
    - `2`: Write permission
    - `1`: Execute permission
    - To get the numeric value, add the permissions together. For example:
        - `7` (4+2+1) means read, write, and execute.
        - `6` (4+2) means read and write.
        - `5` (4+1) means read and execute.

**Understanding `ls -l n*`**

- `ls` lists directory contents.
- `-l` provides a long listing format, showing detailed information including permissions.
- `n*` lists files that start with "n" (in this case, "newfile.txt").

**Let's analyze each sequence:**

**1. `chmod 777 newfile.txt`**

- **Command:** Sets read, write, and execute permissions for everyone (user, group, others).
- **`ls -l n*` Output:** `-rwxrwxrwx. 1 ec2-user ec2-user 78 Feb 26 05:19 newfile.txt` (All permissions are granted).

**2. `chmod u-rwx newfile.txt`**

- **Command:** Removes read, write, and execute permissions for the file's owner (user).
- **`ls -l n*` Output:** `-----rwxrwx. 1 ec2-user ec2-user 78 Feb 26 05:19 newfile.txt` (Only group and others have full permissions).

**3. `chmod u+r,g-w newfile.txt`**

- **Command:** Adds read permission for the user and removes write permission for the group.
- **`ls -l n*` Output:** `-r--r-xrwx. 1 ec2-user ec2-user 78 Feb 26 05:19 newfile.txt` (User has read, group has read and execute, others have all).

**4. `chmod u+r,g+w newfile.txt`**

- **Command:** Adds read permission for the user and adds write permission for the group.
- **`ls -l n*` Output:** `-rw-rwxrwx. 1 ec2-user ec2-user 78 Feb 26 05:19 newfile.txt` (User has read and write, group has all, others have all).

**5. `chmod u-r+w,g+w newfile.txt`**

- **Command:** Removes read permission for the user, adds write permission for the user, and adds write permission for the group.
- **`ls -l n*` Output:** `--w-rwxrwx. 1 ec2-user ec2-user 78 Feb 26 05:19 newfile.txt` (User has write, group has all, others have all).

**6. `chmod ugw-rwx newfile.txt`**

- **Command:** Removes read, write, and execute permissions for both the user and the group.
- **`ls -l n*` Output:** `----------rwx. 1 ec2-user ec2-user 78 Feb 26 05:19 newfile.txt` (Only others have full permissions).

**7. `chmod ugw+rwx newfile.txt`**

- **Command:** Adds read, write, and execute permissions for both the user and the group.
- **`ls -l n*` Output:** `-rwxrwxrwx. 1 ec2-user ec2-user 78 Feb 26 05:19 newfile.txt` (All permissions are granted for everyone).

**Key Takeaways**

- `chmod` is a powerful tool for controlling file access.
- Symbolic mode offers a more readable way to modify permissions.
- The `ls -l` command is essential for viewing permission changes.
- Understanding the user, group, and others categories is crucial for effective permission management.

## UNIQ:


```
cat fisrtfile.txt
uniq fisrtfile.txt

```
![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226184701.png)

```
# this comand show the one that is repeat
UNIQ -D FIRSTFILE.TXT
```
![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226184827.png)


The `uniq` command in Unix-like operating systems (like Linux and macOS) is used to **filter out adjacent duplicate lines** from a file or standard input.

Here's a breakdown:

- **Purpose:** It's designed to make a list unique by **removing repeated lines**.1
- **Key Feature: Adjacent Duplicates:** `uniq` only removes duplicates that are next to each other. If the same line appears non-consecutively, `uniq` will not remove them.
- **Typical Usage:**
    - `uniq filename`: Reads from "filename" and outputs unique lines to standard output.
    - `uniq inputfile outputfile`: Reads from "inputfile" and writes unique lines to "outputfile".
    - `command | uniq`: Takes the output of another command and filters it.
- **Options:**
    - `-c`: Prefixes each line with the number of times it occurred.
    - `-d`: Only prints duplicate lines.
    - `-u`: Only prints unique lines (non-duplicates).
    - `-i`: Ignores case when comparing lines.
    - `-f n`: Ignores the first 'n' fields of a line.
    - `-s n`: Ignores the first 'n' characters of a line.

**In essence, `uniq` is a tool for cleaning up lists by removing adjacent repetitions.**2

## GREP

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226184943.png)![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226185211.png)

```

## CAT is from print

cat fun | grep "Linux" | wc -c
 cat fun | grep "Linux" | sort
  cat fun | grep "Linux" | sort -r

## to update or write more over the link
 nano fun 
 cat fun
  cat fun | grep -i "Linux" | sort -r
```

na

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226185459.png)

print exactat it match
![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226185747.png)

## DEV
![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226190129.png)



![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226190401.png)


**The Big Picture: `/dev` is a Special Directory**

- Imagine your computer has a bunch of hardware: a keyboard, a mouse, a hard drive, etc.
- The `/dev` directory (short for "devices") is where your computer keeps special files that represent these hardware pieces.
- Instead of dealing with the hardware directly, programs talk to these special files.

**What You Did: `ls -l /dev`**

- `ls` is a command to list files and directories.
- `-l` means "long listing," which gives you a lot of details about each item.
- `/dev` is the directory you asked to list.

**Understanding the Output: Each Line Explained**

Each line describes a file or directory within `/dev`. Let's look at the important parts:

1. **File Type:**
    
    - `d` at the very beginning means it's a directory (like a folder).
    - `c` means it's a "character device" (used for things like keyboards, terminals).
    - `b` means it's a "block device" (used for things like hard drives).
    - `l` means it is a symbolic link (a shortcut to another file or directory).
2. **Permissions:**
    
    - Like `rwxr-xr-x`, these letters tell you who can read, write, or execute the file.
    - `r` means "read," `w` means "write," `x` means "execute."
    - The letters are grouped into three sets: owner, group, and everyone else.
3. **Owner and Group:**
    
    - `root root` means the owner and group are both "root" (the system administrator).
    - `root disk` means the owner is root, and the group is "disk".
    - `root tty` means the owner is root, and the group is "tty".
    - `root dialout` means the owner is root, and the group is "dialout".
    - `root kvm` means the owner is root, and the group is "kvm".
4. **Major and Minor Numbers:**
    
    - These numbers (like `10, 235`) are unique identifiers for the device.
    - They help the computer know which hardware it's dealing with.
5. **Date and Time:**
    
    - Shows when the file was last modified.
6. **Name:**
    
    - The name of the file or directory (e.g., `autofs`, `console`, `sda`).

**Key Device Types:**

- **`tty`:** These are terminals (like the command-line interface you're using).
- **`sda`, `xvda`:** These represent your hard drive. (sda is the general name, xvda is the virtualized name used on aws.)
- **`null`, `zero`, `random`, `urandom`:** Special files used for various purposes (e.g., discarding data, generating random numbers).
- **`console`:** Represents the system console.
- **`loop`:** Represents loopback devices, which allow you to mount files as if they were disk partitions.
- **Links:** Files that point to other locations. For example `fd -> /proc/self/fd` means the fd file is simply a shortcut to the location `/proc/self/fd`.

**In Simple Terms:**

The `/dev` directory is like a phone book for your computer's hardware. It lists all the devices and gives your computer the information it needs to communicate with them.

## group the items in the `/dev` listing and explain each group's general purpose:

**1. Core System Devices and Processes:**

- **`autofs`, `btrfs-control`, `cpu`, `cpu_dma_latency`, `cuse`, `fd`, `initctl`, `kmsg`, `log`, `mqueue`, `net`, `null`, `nvram`, `ptmx`, `pts`, `random`, `rtc`, `rtc0`, `shm`, `snapshot`, `stderr`, `stdin`, `stdout`, `urandom`, `userfaultfd`, `vfio`:**
    - These are fundamental to how the Linux system operates.
    - They handle things like:
        - File systems (`autofs`, `btrfs-control`).
        - CPU and memory management (`cpu`, `cpu_dma_latency`).
        - Inter-process communication (`mqueue`).
        - Networking (`net`).
        - Random number generation (`random`, `urandom`).
        - System logging (`log`, `kmsg`)
        - Virtualization support (`vfio`).
        - Standard input and output (`stdin`, `stdout`, `stderr`).
        - Shared memory (`shm`).
        - Real time clock (`rtc`).
        - Null device for discarding data (`null`).

**2. Terminal and Console Devices:**

- **`console`, `tty`, `tty0`, `tty1`, ..., `tty63`, `ttyS0`, `ttyS1`, `ttyS2`, `ttyS3`, `vcs`, `vcs1`, ..., `vcs6`, `vcsa`, `vcsa1`, ..., `vcsa6`, `vcsu`, `vcsu1`, ..., `vcsu6`:**
    - These handle user interaction through the command line or virtual consoles.
    - `tty` represents the current terminal. `tty0`, `tty1`, etc., are virtual terminals.
    - `ttyS` are serial ports.
    - `vcs` and `vcsa` relate to virtual console screens.

**3. Block Devices (Storage):**

- **`block`, `disk`, `loop-control`, `loop0`, `loop1`, ..., `loop7`, `mapper`, `sda`, `sda1`, `sda127`, `sda128`, `xvda`, `xvda1`, `xvda127`, `xvda128`:**
    - These represent storage devices like hard drives, partitions, and loopback devices.
    - `sda` and `xvda` are your main disk drives.
    - `loop` devices let you mount files as if they were disks.
    - `mapper` is used for logical volume management (LVM).

**4. Character Devices (Other Hardware):**

- **`char`, `fuse`, `hpet`, `input`, `uhid`, `uinput`:**
    - These represent various hardware components that communicate character by character.
    - `input` handles input devices like keyboards and mice.
    - `fuse` allows user-space file systems.
    - `hpet` is a high precision event timer.
    - `uhid` and `uinput` are used for user-space HID (Human Interface Device) drivers.

**5. Virtualization and Kernel Modules:**

- **`hugepages`, `xen`, `vhost-net`, `vhost-vsock`:**
    - These are related to virtualization and kernel modules.
    - `hugepages` are used for large memory pages.
    - `xen` is related to the Xen hypervisor.
    - `vhost-net` and `vhost-vsock` accelerate network and socket communication in virtual machines.

**6. Special Files:**

- **`core`, `full`, `zero`:**
    - `core` is a file that contains a memory image of a crashed process.
    - `full` always returns an "out of space" error when written to.
    - `zero` provides a stream of null bytes (zeros).

**7. Symbolic Links:**

- Many of the entries are symbolic links. Those are shortcuts to the real files. These are used to provide convenient access points. For example, `sda` -> `xvda` means that the file named `sda` points to the file named `xvda`.

**Key takeaways:**

- `/dev` is the interface between software and hardware.
- The file types and permissions give clues about how each device is used.
- Understanding these groups helps you understand how your Linux system interacts with its hardware and software components.

## Create link 

```
ln -s <name file> <name link>
ln -s newfile.txt maria
cat maria
```

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226191333.png)

## FREE

```
man free

free -h
```

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226191941.png)

## UPTIME
```
man uptime

uptime
 uptime -p
```

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226192130.png)

## LSCPU

- **Displays CPU architecture information:** It provides details about your computer's central processing unit (CPU).
- **Shows key CPU characteristics:** This includes information like the number of CPUs, cores, threads, sockets, and cache sizes.
- **Helps with system analysis:** It's a valuable tool for system administrators and developers to understand CPU capabilities and optimize performance.

Essentially, `lscpu` gives you a detailed report on your CPU's specifications.

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226192146.png)

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226192317.png)

## IFCONFIG

```
man ifconfig

inconfig

ping
```



![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226192539.png)

It's important to note that while `ifconfig` has been historically used, the `ip` command is now generally preferred in modern Linux distributions. However, understanding both is still valuable. Here's a breakdown:

**ifconfig (interface configuration)**

- **Purpose:**
    - `ifconfig` is a command-line utility used to configure and display network interface parameters in Unix-like operating systems.
    - It allows you to assign IP addresses, netmasks, and other network settings to network interfaces.1
    - It also displays information about the current status of network interfaces.2
- **Key Functions:**
    - Displaying network interface information (IP address, MAC address, etc.).3
    - Enabling or disabling network interfaces.4
    - Assigning IP addresses and network masks.5
- **Note:**
    - `ifconfig` is considered legacy, and the `ip` command is now the recommended tool for network configuration in most modern Linux distributions.

**ping (Packet Internet Groper)**

- **Purpose:**
    - `ping` is a network utility used to test the reachability of a host on an Internet Protocol (IP) network.
    - It sends Internet Control Message Protocol (ICMP)6 echo request packets to the target host and waits for ICMP echo reply packets.7
    - It measures the round-trip time (RTT) of the packets, which indicates the latency of the connection.8
- **Key Functions:**
    - Verifying network connectivity between two hosts.9
    - Measuring network latency.10
    - Troubleshooting network problems.11
- **In essence:**
    - `ifconfig` is for configuring your network interfaces.
    - `ping` is for testing if you can reach other devices on a network.
## NETSTAT
 show just the stats that are listening at the moment
![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226192638.png)


## SS
 desplay the sockets
![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226192803.png)

**netstat (network statistics)**

- **Purpose:**
    - `netstat` is a command-line tool that provides information about network connections, routing tables, interface statistics,1 and multicast memberships.
    - It's a traditional tool used for network troubleshooting and monitoring.2
- **Key Functions:**
    - Displaying active network connections (TCP, UDP, etc.).3
    - Showing listening ports.4
    - Displaying routing tables.5
    - Providing network interface statistics.6
- **Status:**
    - `netstat` is considered obsolete in many modern Linux distributions. The `ss` command is its recommended replacement.

**ss (socket statistics)**

- **Purpose:**
    - `ss` is a command-line utility used to display socket statistics.
    - It's designed to be faster and more efficient than `netstat`.
- **Key Functions:**
    - Displaying socket information (TCP, UDP, UNIX domain sockets).7
    - Providing detailed information about TCP states.8
    - Filtering socket information based on various criteria.9
    - It is much faster than netstat.10
- **Advantages over netstat:**
    - **Speed:** `ss` is significantly faster, especially when dealing with a large number of sockets.
    - **Efficiency:** It retrieves information directly from the kernel, making it more efficient.
    - **Filtering:** `ss` provides more powerful filtering options.
- **In essence:**
    - `netstat` was the older, more traditional tool.
    - `ss` is the modern, faster, and more efficient replacement.

Therefore, while you might still encounter `netstat`, it's generally recommended to use `ss` for network connection analysis on modern Linux systems.

## SSH

```
ssh username@<ip>
```

to connect by SSH whith a server/device/machine that has an IP

## WGET

```
 wget http://google.com
 
 ls -l

 cat index.html
```

`wget http://google.com` downloads the HTML content of Google's homepage and saves it as "index.html" in your current directory. It's a command-line way to grab a webpage's basic code.

![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226193508.png)
![](../IMG/IMG-%20Class%203%20-%2026.02.2025%20-%20Linux%20Internal%20Commands%20-class%20II/Pasted%20image%2020250226193538.png)