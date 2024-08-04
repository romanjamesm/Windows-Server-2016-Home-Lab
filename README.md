# Windows Server 2016 Home Lab

From small businesses to large enterprises, virtually every organization uses the Windows Server operating system and its Active Directory and Exchange Server services for centralized management of authentication, email, policies, and more. Windows Server 2016 specifically (and its associated Exchange Server 2016) is still one of the most used versions of the OS, which means this lab translates directly to office environments today. 

## Technologies Used

- PowerShell
- Windows Server 2016
- Active Directory Domain Services
- Exchange Server 2016

## Walk-through

Google _**Windows Server 2016 evaluation download**_. The first or second result should be this: https://www.microsoft.com/en-us/evalcenter/download-windows-server-2016. Next to _**English (United States)**_, select _**64-bit edition**_ to download the ISO file. 

Next, you can [burn the ISO to a disc](https://www.wikihow.com/Burn-ISO-Files-to-DVD), create a [bootable USB flash drive](https://rufus.ie/en/), or create a virtual machine in your favorite hypervisor—I recommend at least 2 GB of RAM, two processor cores, and 50 GB of disk space for a long-term home lab project that will contain an increasing amount of files. 

Boot your machine from the installation media: 

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/001-install-language.png" width="640"></p>

Select **_Next_** to use the default English (United States) settings. On the next screen, select **_Install now_**. Choose the **_Windows Server 2016 Standard Evaluation (Desktop Experience)_** as the OS version: 

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/002-evaluation-version.png" width="640"></p>

On the next page, accept the license terms and click **_Next_**. Select **_Custom: Install Windows only (advanced)_**. Leave the default partition and format settings and click **_Next_**. Allow Windows to restart. You may disconnect the installation media now. Enter a password and confirm—**_Password123_** is sufficient for a home lab with no real-life security risks to mitigate. Select **_Finish_**, press **_Ctrl+Alt+Delete_** to unlock, and log in. You can select **_Yes_** on the Networks popup to allow your machine to be discoverable on the network. If your OS date and time are incorrect, change them in Settings > Time & language > Date & time. Open File Explorer, right-click **_This PC_**, select **_Properties_**, and under **_Computer name, domain, and workgroup settings_**, select **_Change settings_**. Under the default Computer Name tab, select **_Change..._** and enter a more suitable computer name:

<p align="center"><img alt="" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/003-computer-name.png" width="640"></p>












