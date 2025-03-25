## Implement NFS server in one instance and configure shared storage between multiple Linux (10 Marks)

## 1) Create 2 EC2 Linux as web server

2. **Log in to AWS Management Console.**
3. Navigate to **EC2 Dashboard** → Click **Launch Instance**.
4. Choose **Amazon Linux 2** or **Ubuntu** as the OS.
5. Select an **instance type** (e.g., t2.micro for free-tier or t3.small for better performance).
6. In **Network Settings**, choose:
    - **VPC:** Select an existing VPC or create a new one.
    - **Security Group:** Create a new security group named `WebServerSG` with:
        - **Inbound Rule:** Allow HTTP (port 80) from anywhere.
        - **Outbound Rule:** Allow all traffic.
7. **Launch two instances** with the same settings.


###  Create 2 new Linux instance      
- Linux1-2:
	- IP Public: 3.27.206.222
	- IP Priv: 10.0.1.65
- Linux2-2:
	- IP Public: 3 52.63.213.252
	- IP Priv: 10.0.1.107

![](../IMG/IMG%20-%20Task%202.2%20-%20Mount%20a%20NFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250313204908.png)

### 2)  Create security group

In the same VPC I create two different security groups. One for the EC2 instance allow protocol SSH (port 22) and HTTP (port 80)  to display the webserver. And s second one just for the EFS share system that allow protocol NFS (port 2049)  
![](app://afc3e0d9ff4c14df6b8f19c52fb404d4fb00/C:/Users/aleja/OneDrive/PERSONAL/ObsidianNotes/Linux/IMG/IMG-%20Task%202%20.1-%20Mount%20a%20EFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250312221319.png?1741770799077)  
![](app://afc3e0d9ff4c14df6b8f19c52fb404d4fb00/C:/Users/aleja/OneDrive/PERSONAL/ObsidianNotes/Linux/IMG/IMG-%20Task%202%20.1-%20Mount%20a%20EFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250312221330.png?1741770810073)

## 2) Create and Mount EF

Create a Shared EFS Storage on Aws console, and assign the SG-EFS-Sydney security group that already allow  NFS protocols (port 2049). The new DNS for the EFS is _fs-07be93bf88c0684f8.efs.ap-southeast-2.amazonaws.com_
The EFS file system is created on the same VPC in where the EC2 are created with and enable encryption. As a good practice is good to enable automatic backups, but for effects of this report is not necessary.

![](../IMG/IMG%20-%20Task%202.2%20-%20Mount%20a%20NFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250313204718.png)
![](../IMG/IMG%20-%20Task%202.2%20-%20Mount%20a%20NFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250313205256.png)

## 3) Connect to the FIRST instance   via SSH on your WSL (Windows subsystem for Linux)  and install NFS utilities

```bash
ssh -i "<key-file-name>" ec2-user@ec2-<IP-public>.ap-southeast-2.compute.amazonaws.com

#example
ssh -i "key_task2.pem" ec2-user@ec2-52-63-213-252.ap-southeast-2.compute.amazonaws.com
```

```bash

#install NFS utilities
sudo yum install -y nfs-utils

#create directory
sudo mkdir -p /var/www/html

# Mount NFS
sudo mount -t nfs -o tls your-efs-dns:/ /<path>
## example
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-07be93bf88c0684f8.efs.ap-southeast-2.amazonaws.com:/ /var/www/html

```

![](../IMG/IMG%20-%20Task%202.2%20-%20Mount%20a%20NFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250313222432.png)

```bash
# Ensure the mount persists after reboot:
df -hT
```
![](../IMG/IMG%20-%20Task%202.2%20-%20Mount%20a%20NFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250313222544.png)



```bash
#  create manauelly a file on directory that you create
echo "your-efs-dns:/ /var/www/html efs defaults,_netdev 0 0" | sudo tee -a /etc/fstab

## example
echo "<h1>HELLO WORLD. I AM MARIA</h1><h2>Welcome to the Task 2.2 of the
 Term 3 in the Cloud Computing Program - $(hostname -f)</h2>" | sudo tee /var/www/html/index.html

# check if was created
ls -la <path>
##example
ls -la /var/www/html
```

![](../IMG/IMG%20-%20Task%202.2%20-%20Mount%20a%20NFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250313222624.png)

How you file is a index.html, you can check the IP public on the web browser
![](../IMG/IMG%20-%20Task%202.2%20-%20Mount%20a%20NFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250313222749.png)

## 4) Connect to the SECOND instance   via SSH on your WSL (Windows subsystem for Linux)  and install NFS utilities

Log in to **second instance**  (10.0.1.65) via SSH and install the NFS utilities and create the same directory (/var/www/html) on before instance to mount the share file system then repeat the same command to mount the NFS that we run in previous Linux instance. 

![](../IMG/IMG%20-%20Task%202.2%20-%20Mount%20a%20NFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250313223419.png)


 With the command “CAT” we can check the file that was previous created on first Linux (10.0.1.107)
 
```bash
ls -la /var/www/html

cat /var/www/html/index.html
```

![](../IMG/IMG%20-%20Task%202.2%20-%20Mount%20a%20NFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250313223445.png)

Check on the web browser the IP public of the second Linux
![](../IMG/IMG%20-%20Task%202.2%20-%20Mount%20a%20NFS%20in%202%20Linux%20EC2%20Instance/Pasted%20image%2020250313223625.png)

--END--

#Note: for more information check  AWs NFs documentation  https://docs.aws.amazon.com/efs/latest/ug/mounting-fs-install-nfsclient.html

hello