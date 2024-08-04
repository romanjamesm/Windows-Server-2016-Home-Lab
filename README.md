# Windows Server 2016 Home Lab

From small businesses to large enterprises, virtually every organization uses the Windows Server operating system and its Active Directory and Exchange Server services for centralized management of user authentication, email, security policies, and more. Windows Server 2016 specifically (and its associated Exchange Server 2016) is still one of the most used versions of the OS, which means this lab translates directly to office environments today. 

## Technologies Used

- PowerShell
- Windows Server 2016
- Active Directory Domain Services
- Exchange Server 2016

## Walk-through

Google **Windows Server 2016 evaluation download**. The first or second result should be this: https://www.microsoft.com/en-us/evalcenter/download-windows-server-2016. Next to **English (United States)**, select **64-bit edition** to download the ISO file. 

Next, you can [burn the ISO to a disc](https://www.wikihow.com/Burn-ISO-Files-to-DVD), create a [bootable USB flash drive](https://rufus.ie/en/), or create a virtual machine in your favorite hypervisor—I recommend at least 2 GB of RAM, two processor cores, and 50 GB of disk space for a long-term home lab project that will contain an increasing number of files. 

Boot your machine from the installation media: 

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/001-install-language.png" width="640"></p>

Leave the default language settings and select **Next** (from this point on, it will be implied to select the **Next** or **OK** button, if applicable). Select **Install now**. 

Choose **Windows Server 2016 Standard Evaluation (Desktop Experience)** as the OS version: 

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/002-evaluation-version.png" width="640"></p>

Accept the license terms. Select **Custom: Install Windows only (advanced)**. Leave the default partition and format settings. Allow Windows to restart. You may disconnect the installation media now. 

Create a password and confirm—_Password123_ is sufficient for a home lab with no real-life security risks to mitigate—and log in. You can select **Yes** on the Networks popup to allow your machine to be discoverable on the network. 

If your OS date and time are incorrect, change them in Settings > Time & language > Date & time. 

Open File Explorer, right-click **This PC**, select **Properties**, and under **Computer name, domain, and workgroup settings**, select **Change settings** > **Computer Name** > **Change...** and enter a more suitable computer name:

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/003-computer-name.png" width="640"></p>

Apply the changes and restart the system. 

Open Internet Explorer, select the gear :gear: icon in the top-right corner > Internet Options > Security > Internet > Custom level... and scroll down to Downloads and enable file downloads:

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/004-internet-options.png" width="640"></p>

Back in Internet Options > Security, select Local Intranet > Custom level... and make sure file downloads are enabled there too. 

Finally, in the same Internet Options > Security tab, select Trusted sites > Sites, add **https://\*.google.com** to the zone. 

Search Google for **Chrome**, download Chrome, and run Chrome. Close IE for good. 

In Chrome, Google **Unified Communications Managed API 4.0**. The first link should be https://www.microsoft.com/en-us/download/details.aspx?id=34992. Download and run the setup program: 

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/005-UCMA-setup.png" width="640"></p>

Accept the terms and install. 
