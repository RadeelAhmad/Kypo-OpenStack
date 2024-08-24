# OpenStack

I will provide a detailed method for deploying **OpenStack** on **CentOS 8**.

## Requirement

- CentOS 8
- VMware
- [Configuration file](https://github.com/RadeelAhmad/OpenStack/tree/main/yum.repos.d)

## Let’s Start…
First of all, you need to configure your VMware according to the following screenshot.

<p align="center">
    <img src="Images/Screenshot202-08-12231805.png" alt="image1">
</p>


I set RAM to 32 GB but you set it to 8 GB minimum, depending upon your RAM size, and Processor set to 32.

Add 5 hard drives, 100 GB for CentOS, which is already available starting from 20 GB. Additionally, we need 4 local hard drives for installing various VMs on Open Stack. The sizes of these local hard drives range from 30 GB to 50 GB.

Add 3 network adapters to the CentOS VM configuration in VMware settings. One adapter is already available, and you need to add 2 more.

Your cent OS Network Adapter should be at **NAT** settings
- The second network adapter will be a **HOST-only** setting.
- The third network adapter will be a **bridged** connection.

Make sure to match the configuration with the first screenshot at the top of this article. Name your VM and set the username and password for your CentOS login screen. Leave the other settings as they are. Close the settings and then turn on your VM. The installation process of CentOS is fully automated.

Please ensure that your internet is working properly and that all adapters are functioning correctly. You can check them from the VMware Status bar or the Network panel of CentOS. Currently, ens224 is turned off.

<p align="center">
    <img src="Images/Screenshot202-08-12231720.png" alt="image1">
</p>


## CentOS

On your terminal, and get root access. Now use this Command for OpenStack local hostname.

```bash
su
hostnamectl set-hostname openstackio --static
```
`openstackio` is the name. You can use any name of your choice. This execution of the command will set the local hostname only.

<p align="center">
    <img src="Images/a.png" alt="image1">
</p>

To configure your IP with your local host. I use an ens160 IP address. Use the command to map your IP to the local host. The name for the local host should be the same as set in the previous command. Then use the cat command with directories to verify your mapping:
```bash
echo "192.168.186.131 openstackio" >> /etc/hosts
cat /etc/hosts
```

<p align="center">
    <img src="Images/b.png" alt="image1">
</p>

Now use these Commands:
```bash
setenforce 0 
sed -i 's/^SELINUX=.*/SELINUX=disabled/g' /etc/selinux/config
```

<p align="center">
    <img src="Images/c.png" alt="image1">
</p>

Now use following command the following command to install network
```bash
scripts dnf install network-scripts -y
```

<p align="center">
    <img src="Images/1.png" alt="image1">
</p>

Upon completing this, the following output will be displayed.

<p align="center">
    <img src="Images/1.1.png" alt="image1">
</p>

Now use the following back-to-back commands.
```bash
systemctl disable - now firewalld NetworkManager 
systemctl enable - now network 
dnf -y install lvm2
```

<p align="center">
    <img src="Images/d.png" alt="image1">
</p>

<p align="center">
    <img src="Images/2.png" alt="image1">
</p>

Upon completing this, the following output will be displayed.

<p align="center">
    <img src="Images/2.1.png" alt="image1">
</p>
