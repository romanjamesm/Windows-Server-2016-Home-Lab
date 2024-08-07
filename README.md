# Windows Server 2016 Home Lab

From small businesses to large enterprises, virtually every organization uses the Windows Server operating system and its Active Directory service and Exchange Server platform for centralized management of user authentication, email, security policies, and more. Windows Server 2016 specifically is still one of the most used versions of the OS, so this lab directly translates to office environments today. 

## Technologies Used

- PowerShell
- Active Directory Domain Services (AD DS)
- Exchange Server 2016

## Walk-through

Google **Windows Server 2016 evaluation download**. The first or second result should be this: https://www.microsoft.com/en-us/evalcenter/download-windows-server-2016. Next to **English (United States)**, select **64-bit edition** to download the ISO file. 

Next, you can [burn the ISO to a disc](https://www.wikihow.com/Burn-ISO-Files-to-DVD), create a [bootable USB drive](https://rufus.ie/en/), or create a virtual machine in your favorite hypervisor—I recommend at least 2 GB of RAM, two processor cores, and 50 GB of disk space for a long-term home lab project that will contain an increasing number of files. 

Boot your machine from the installation media: 

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/001-install-language.png" width="640"></p>

Leave the default language settings and select **Next** (from this point on, it will be implied to select **Next** or **OK**, if applicable). Select **Install now**. 

Choose the **Standard Evaluation (Desktop Experience)** version of Server 2016: 

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/002-evaluation-version.png" width="640"></p>

Accept the license terms. Select **Custom: Install Windows only (advanced)**. Leave the default partition and format settings. Allow Windows to restart. You may disconnect the installation media now. 

Create a password and confirm—_Password123_ is sufficient for a home lab with no real-life security risks to mitigate—and log in. You can select **Yes** on the Networks popup to allow your machine to be discoverable on the network. 

If your system date and time are incorrect, change them in Settings > Time & language > Date & time. 

The default computer name in Windows Server is something like _WIN-BKU971JG9GM_. Go to File Explorer, right-click **This PC**, select **Properties**, and under **Computer name, domain, and workgroup settings**, select **Change settings** > **Computer Name** > **Change...** and enter a more readable name:

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/003-computer-name.png" width="640"></p>

Apply the changes and restart the system. 

Open Internet Explorer, select the gear :gear: icon in the top-right corner > **Internet Options** > **Security** > **Internet** > **Custom level...** and scroll down to **Downloads** and enable file downloads:

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/004-internet-options.png" width="640"></p>

Back in Internet Options > Security, select **Local Intranet** > **Custom level...** and make sure file downloads are enabled there too. 

Finally, in the same Internet Options > Security tab, select Trusted sites > Sites, and add **https://\*.google.com** to the zone. 

Search Google for **Chrome**, download Chrome, and run Chrome. Close IE for good. 

In Chrome, Google **Unified Communications Managed API 4.0**. The first link should be https://www.microsoft.com/en-us/download/details.aspx?id=34992. Download and run the setup program: 

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/005-UCMA-setup.png" width="640"></p>

Accept the terms and install. 

Google **Visual C++ Redistributable 2013 download**. Click the first link: https://www.microsoft.com/en-us/download/details.aspx?id=40784. Click **Download** and select the 64-bit version. Run the download: 

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/006-vcredist.png" width="640"></p>

Next, we will install the required features for AD DS, such as Group Policy and Lightweight Directory Services (LDS). Go to Start > Server Manager > Manage > Add Roles and Features > Next. Use the default **Role-based** installation and server selection. Select **Active Directory Domain Services** > **Add Features** to add the AD DS role to the server. Those are the only tools and features needed; proceed to install. 

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/007-AD-DS-install.png" width="640"></p>

When you see _Installation succeeded_ (as in above image), select **Promote this server to a domain controller** > **Add a new forest** and enter a root domain name: 

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/008-domain-name.png" width="640"></p>

Enter a DSRM password and confirm. Leave DNS delegation off. Leave the default NetBIOS domain name and AD paths. Install. 








