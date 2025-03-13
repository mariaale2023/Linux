
```
alias ll="ls -la --color=auto"

ll
```
This command creates a shortcut (alias) called `ll`. When you type `ll` in the terminal, it will run `ls -la --color=auto-------
![](../IMG/IMG-%20Class%206%20-%2005.03.2025%20-%20Linux%20-%20Bash%20Scripting%20-%20Conditional%20Loops%20-%20Class%20III/Pasted%20image%2020250305181438.png)

![](../IMG/IMG-%20Class%206%20-%2005.03.2025%20-%20Linux%20-%20Bash%20Scripting%20-%20Conditional%20Loops%20-%20Class%20III/Pasted%20image%2020250305181416.png)

## SLEEP
The `sleep` command pauses the execution of a script or command for a specified amount of time.
### Usage:

```bash
sleep 5  # Pauses for 5 seconds
sleep 2m # Pauses for 2 minutes
sleep 1h # Pauses for 1 hour
```

### Simple Explanation:

It makes the terminal **"wait"** before running the next command. Useful for delays in scripts or scheduling tasks. ⏳

![](../IMG/IMG-%20Class%206%20-%2005.03.2025%20-%20Linux%20-%20Bash%20Scripting%20-%20Conditional%20Loops%20-%20Class%20III/Pasted%20image%2020250305181843.png)

## TAR

The `tar` command is used to **archive** (combine multiple files into one) and optionally **compress** them in Linux.

### Basic Usage:

1. **Create an archive:**
    
    ```bash
    tar -cvf archive.tar file1 file2 folder/
    ```
    
    - `c` → Create a new archive
    - `v` → Verbose (show progress)
    - `f` → Specify the file name (`archive.tar`)
2. **Extract an archive:**
    
    ```bash
    tar -xvf archive.tar
    ```
    
    - `x` → Extract files
3. **Create a compressed archive (gzip):**
    
    ```bash
    tar -cvzf archive.tar.gz file1 file2 folder/
    ```
    
    - `z` → Compress with gzip
4. **Extract a compressed archive:**
    
    ```bash
    tar -xvzf archive.tar.gz
    ```
    

### Simple Explanation:

- `tar` is like **putting multiple files in a box** 📦
- Adding `z` compresses it, making the box **smaller** 🎈
- You can **open (extract) the box** later to get the files back 🎁

## GZIP

The `gzip` command is used to **compress files** in Linux, reducing their size. It replaces the original file with a compressed `.gz` version.

### Basic Usage:

1. **Compress a file:**
    
    ```bash
    gzip file.txt
    ```
    
    - This creates `file.txt.gz` and removes `file.txt`
2. **Decompress a file:**
    
    ```bash
    gunzip file.txt.gz
    ```
    
    - This restores `file.txt`
3. **Keep the original file while compressing:**
    
    ```bash
    gzip -c file.txt > file.txt.gz
    ```
    
    - `-c` → Outputs compressed data to a new file instead of replacing the original.
4. **Compress multiple files:**
    
    ```bash
    gzip file1.txt file2.txt file3.txt
    ```
    
    - Each file gets compressed separately into `file1.txt.gz`, `file2.txt.gz`, etc.
5. **Check compression details:**
    
    ```bash
    gzip -l file.txt.gz
    ```
    
    - Shows original and compressed sizes.

### Simple Explanation:

- `gzip` **shrinks files** 📉
- `gunzip` brings them **back to normal** 🔄
- Useful for **saving space** and **speeding up file transfers** 🚀
---
![](../IMG/IMG-%20Class%206%20-%2005.03.2025%20-%20Linux%20-%20Bash%20Scripting%20-%20Conditional%20Loops%20-%20Class%20III/Pasted%20image%2020250305183151.png)
## KILL

!!!! Never use Kill, at least you know what you are doing >> kill process, 
![](../IMG/IMG-%20Class%206%20-%2005.03.2025%20-%20Linux%20-%20Bash%20Scripting%20-%20Conditional%20Loops%20-%20Class%20III/Pasted%20image%2020250305183429.png)


## HISTORY

return the history list of all command tat you already wrote

![](../IMG/IMG-%20Class%206%20-%2005.03.2025%20-%20Linux%20-%20Bash%20Scripting%20-%20Conditional%20Loops%20-%20Class%20III/Pasted%20image%2020250305184017.png)


## LESS and MORE

## WC

![](../IMG/IMG-%20Class%206%20-%2005.03.2025%20-%20Linux%20-%20Bash%20Scripting%20-%20Conditional%20Loops%20-%20Class%20III/Pasted%20image%2020250305184932.png)

## UNAME
to get info about the system

![](../IMG/IMG-%20Class%206%20-%2005.03.2025%20-%20Linux%20-%20Bash%20Scripting%20-%20Conditional%20Loops%20-%20Class%20III/Pasted%20image%2020250305185340.png)

