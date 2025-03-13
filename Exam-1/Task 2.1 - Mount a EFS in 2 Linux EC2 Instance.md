CREATE TWO LINUX EC2 INSTANCE USING COMMON SECURITY GROUP AND DEPLOY BOTH INSTANCES AS WEB SERVERS. 

CONFIGURE SHARED STORAGE USING EFS SERVICE WITH SECURITY GROUP OUTBOUND ANY AND INBOUND NFS TCP 2049 ONLY RULE TO SHARE WEBSITE CONTENT BETWEEN MULTIPLE LINUX INSTANCES TO IMPLEMENT WEB SERVER SECURITY. (DO NOT USE DEFAULT WEB PAGE DESIGN SAMPLE WEB SITE USING ANY CONVENIENT SCRIPTING LANGUAGE)
### 1) Create 2 EC2 Linux as web server

1. **Log in to AWS Management Console.**
2. Navigate to **EC2 Dashboard** → Click **Launch Instance**.
3. Choose **Amazon Linux 2** or **Ubuntu** as the OS.
4. Select an **instance type** (e.g., t2.micro for free-tier or t3.small for better performance).
5. In **Network Settings**, choose:
    - **VPC:** Select an existing VPC or create a new one.
    - **Security Group:** Create a new security group named `WebServerSG` with:
        - **Inbound Rule:** Allow HTTP (port 80) from anywhere.
        - **Outbound Rule:** Allow all traffic.
6. **Launch two instances** with the same settings.
7
![](../IMG/IMG-%20Task%202%20.1-%20Mount%20a%20EFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250312221400.png)

### 2) Create security group

In the same VPC I create two different security groups. One for the EC2 instance allow protocol SSH (port 22) and HTTP (port 80)  to display the webserver. And s second one just for the EFS share system that allow protocol NFS (port 2049)
![](../IMG/IMG-%20Task%202%20.1-%20Mount%20a%20EFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250312221319.png)
![](../IMG/IMG-%20Task%202%20.1-%20Mount%20a%20EFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250312221330.png)

### 3) Create and Mount EFS

Create a Shared EFS Storage on Aws console, and assign the SG-EFS-Sydney security group that already allow  NFS protocols (port 2049). The new DNS for the EFS is _fs-07be93bf88c0684f8.efs.ap-southeast-2.amazonaws.com_
![](../IMG/IMG-%20Task%202%20.1-%20Mount%20a%20EFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250312221554.png)


open your WLS /Linux console and connect wit  you EC2 instance via SSH


```bash
# 3 check if key is save it
ls -l
```


![](../IMG/IMG-%20Task%202%20.1-%20Mount%20a%20EFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250312213619.png)

```bash
# connect with the instance
ssh -i "key_task2.pem" ec2-user@ec2-3-27-231-169.ap-southeast-2.compute.amazonaws.com
```

```bash

#install EFS utilities
sudo yum install -y amazon-efs-utils

#create directory
sudo mkdir -p /var/www/html

# Mount EFS
sudo mount -t efs -o tls your-efs-dns:/ /var/www/

# Ensure the mount persists after reboot:
echo "your-efs-dns:/ /var/www/html efs defaults,_netdev 0 0" | sudo tee -a /etc/fstab

```
![](../IMG/IMG-%20Task%202%20.1-%20Mount%20a%20EFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250312214147.png)
![](../IMG/IMG-%20Task%202%20.1-%20Mount%20a%20EFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250312220924.png)
```bash
#restart the web server
sudo systemctl restart httpd  # Amazon Linux
sudo systemctl restart apache2  # Ubuntu

```

```bash

### **How to Create `mariafile.html` in `/var/www/html/`**

#Connect to your EC2 instance via SSH:**
ssh -i your-key.pem ec2-user@your-instance-ip
    
# Navigate to the web directory:**

cd /var/www/html

#Create `mariafile.html` with sample content:**
echo "This is Maria's extra file for testing." | sudo tee /var/www/html/mariafile.html
 
# Verify the file exists:**
ls -l /var/www/html/
    
# View the content of `mariafile.html` in your second instance Linux 2
cat /var/www/html/mariafile.html

```

![](../IMG/IMG-%20Task%202%20.1-%20Mount%20a%20EFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250312221041.png)

```
# Open your browser and visit both IP puublic

http://<your-ec2-public-ip>/mariafile.html

```
![](../IMG/IMG-%20Task%202%20.1-%20Mount%20a%20EFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250312221154.png)
----------------

In resume:

Here's how you can achieve this step-by-step:

---

## **Step 1: Launch Two Linux EC2 Instances**

1. **Log in to AWS Management Console.**
2. Navigate to **EC2 Dashboard** → Click **Launch Instance**.
3. Choose **Amazon Linux 2** or **Ubuntu** as the OS.
4. Select an **instance type** (e.g., t2.micro for free-tier or t3.small for better performance).
5. In **Network Settings**, choose:
    - **VPC:** Select an existing VPC or create a new one.
    - **Security Group:** Create a new security group named `WebServerSG` with:
        - **Inbound Rule:** Allow HTTP (port 80) from anywhere.
        - **Outbound Rule:** Allow all traffic.
6. **Launch two instances** with the same settings.

---

## **Step 2: Create a Shared EFS Storage**

1. **Navigate to the EFS Service in AWS Console.**
2. Click **Create file system**.
3. Choose the same **VPC** as the EC2 instances.
4. Under **Network Access**, configure:
    - **Mount Targets:** Select the subnets where the EC2 instances exist.
    - **Security Group:** Create `EFS-SG` with:
        - **Inbound Rule:** Allow **NFS (port 2049, TCP)** from `WebServerSG`.
        - **Outbound Rule:** Allow all traffic.
5. Complete the setup and note down the **EFS DNS name**.

---

## **Step 3: Mount EFS on Both Instances**

1. Connect to each instance via SSH:
    
    ```sh
    ssh -i your-key.pem ec2-user@your-instance-ip
    ```
    
2. Install **NFS utilities**:
    
    ```sh
    sudo yum install -y amazon-efs-utils  # For Amazon Linux
    sudo apt update && sudo apt install -y nfs-common  # For Ubuntu
    ```
    
3. Create a mount directory:
    
    ```sh
    sudo mkdir -p /var/www/html
    ```
    
4. Mount the EFS storage:
    
    ```sh
    sudo mount -t efs your-efs-dns:/ /var/www/html
    ```
    
    _(Replace `your-efs-dns` with the actual EFS DNS name)_
5. Ensure the mount persists after reboot:
    
    ```sh
    echo "your-efs-dns:/ /var/www/html efs defaults,_netdev 0 0" | sudo tee -a /etc/fstab
    ```
    

---

## **Step 4: Install Web Server and Deploy Website**

1. Install Apache (or Nginx):
    
    ```sh
    sudo yum install -y httpd  # For Amazon Linux
    sudo apt install -y apache2  # For Ubuntu
    ```
    
2. Start and enable the web server:
    
    ```sh
    sudo systemctl start httpd
    sudo systemctl enable httpd
    ```
    
3. Set proper permissions on EFS storage:
    
    ```sh
    sudo chown -R apache:apache /var/www/html  # For Apache
    sudo chmod -R 755 /var/www/html
    ```
    
4. Create a sample **PHP-based website**:
    
    ```sh
    echo "<?php echo '<h1>Welcome to My Web Server</h1>'; ?>" | sudo tee /var/www/html/index.php
    ```
    
5. Restart Apache:
    
    ```sh
    sudo systemctl restart httpd
    ```
    

---

## **Step 5: Test the Setup**

1. Open a browser and visit:
    
    ```
    http://<your-instance-public-ip>/index.php
    ```
    
2. Repeat for both instances – the shared EFS storage should serve the same content.

---

## **Step 6: Security Enhancements**

- Use **firewall rules** (`iptables` or `firewalld`) to restrict access.
- Implement **SSL (HTTPS)** using **Let's Encrypt**.
- Configure **IAM roles** for secure EFS access.

This setup ensures **high availability, scalability, and shared content management** across multiple web servers. 🚀

## Note : you can save some step if you use User data when you create the webserver

```bash
#!/bin/bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
echo "<h1>Welcome to the task - $(hostname -f)</h1>" | sudo tee /var/www/html/index.html
sudo systemctl restart httpd

```