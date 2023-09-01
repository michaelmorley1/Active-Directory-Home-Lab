<h1>Setting Up a Home Lab Running Active Directory</h1>

This repository contains steps on how I set up a basic home lab running Active Directory on Oracle VirtualBox whilst also 
adding users to it via a PowerShell script. 

In order to complete this lab three tools need to be downloaded.

- Oracle VirtualBox (Virtual Machine): https://www.virtualbox.org/wiki/Downloads
- Windows Server 2019 ISO (Domain Controller): https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019
- Windows 10 Pro Edition ISO (Domain Client): https://www.microsoft.com/en-ca/software-download/windows10ISO

Oracle VirtualBox will be used to create the VM, Windows Server 2019 will be used as the domain controller and Windows 10 is the client.

<h2>Virtual Machine Network Diagram</h2>

<p align="center">
<img src="https://i.imgur.com/P7uGl4T.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>

This diagram represents how the Virtual Machine Network will be set up. The Domain Controller will have two Network Interface Cards. One will give access to the internet via the SOHO router and the second will connect the two VMs( DC and client).

Nat is configured so our internal private VMs are able to reach the internet and the DHCP server is configured so clients will automatically be assigned a default gateway, IP address and subnet mask once they log in.


<h2> Windows Server 2019 Setup</h2>
The Domain Controller will have two Network Interface Cards. One will give access to the internet via the router and the second will connect the two VMs( DC and client). 

<p align="center">
<img src="https://i.imgur.com/4HBESwx.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>

The network adaptor is used for connection to the internet whilst the second network adaptor named X_INTERNAL_X is used for the private network.

<p align="center">
<img src="https://i.imgur.com/i2myDfC.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>

The internal network adaptor is configured so that it is assigned DNS and an IP address. The DNS was set to the loopback address because the active directory automatically installs DNS, meaning that the server itself acts as the DNS.

<h2> Install Active Directory</h2>

Active directory domain services are enabled through the server manager. Choose the "Add roles and features" option, select "Active Directory Domain Services" and complete the setup.

<p align="center">
<img src="https://i.imgur.com/01ECgNF.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>

Once the active directory is set up we create a new domain admin account so that it can act as the central authority to control services.

<p align="center">
<img src="https://i.imgur.com/dBlASoK.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>



<h2>Configure NAT/RAS</h2>

Setting up NAT/RAS allows clients connected to the domain controller to be able to access the internet.

<p align="center">
<img src="https://i.imgur.com/KoD9wU2.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>



<p align="center">
<img src="https://i.imgur.com/XzbAJuu.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>

<h2>Setup DHCP on domain controller</h2>

Setting up DHCP enables clients who connect to the domain controller are lease an IP address.

<p align="center">
<img src="https://i.imgur.com/JFMoZ9s.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>

<p align="center">
<img src="https://i.imgur.com/XA7EHZd.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>


<h2>Powershell script to create users</h2>

We ran a Powershell script to create 1000 users. The script automated the creation of 1,000 user accounts using a list of names on a text file. 

<p align="center">
<img src="https://i.imgur.com/G7EeKLL.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>

The script set a default password, created an organisational unit and assigned first name, last name, username and password policy


<p align="center">
<img src="https://i.imgur.com/MfmIzNX.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>

<h2>Windows Client</h2>

A new VM "Client1" was created and Windows 10 was installed on it. The VM was then assigned an IP address as per the DHCP scope of the domain controller. The client is successfully running and connected to the domain controller.

<p align="center">
<img src="https://i.imgur.com/K1sWrc1.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>

Successfully able to log into the client machine with a domain account taken from the Powershell script that was run.
<p align="center">
<img src="https://i.imgur.com/CCCKitM.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>

<p align="center">
<img src="https://i.imgur.com/kByZcQw.png" height="50%" width="50%" alt="Image Analysis Dataflow"/>
</p>

That completes the setup of an Active Directory home lab. This lab helped me gain a greater understanding of the following:
- Active Directory
- PowerShell
- Windows Server
- Virtualization (Oracle VirtualBox)

