# Windows Server 2016 Home Lab

From small businesses to large enterprises, virtually every organization uses the Windows Server operating system and its Active Directory service and Exchange Server platform for centralized management of user authentication, email, security policies, and more. Windows Server _2016_ specifically is still one of the most used releases of the OS, so this lab directly translates to office environments today. 

## Technologies Used

- PowerShell
- Active Directory Domain Services (AD DS)
- Exchange Server 2016

## Walk-through

Google **Windows Server 2016 download**. The first result should be this: https://www.microsoft.com/en-us/evalcenter/download-windows-server-2016. Next to **English (United States)**, select **64-bit edition** to download the ISO file. 

Next, Google **Exchange Server 2016 download**. The first or second result should be: https://www.microsoft.com/en-us/download/details.aspx?id=104132. Click **Download**. 

You now have two ISO files, each of which you can [burn to a disc](https://www.wikihow.com/Burn-ISO-Files-to-DVD). Alternatively, you can create a [bootable USB drive](https://rufus.ie/en/) for each. However, if your Windows Server will be a virtual machine, then you only need to make sure your VM has a disc drive configured in the hypervisor to use the images (ISO files). I recommend at least 2 GB of RAM, two processor cores, and 50 GB of disk space for a long-term home lab project that will contain an increasing number of files. 

Boot your machine from the Windows Server installation media: 

<p align="center"><img alt="Language settings screen in Windows Setup" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/001-install-language.png" width="640"></p>

Leave the default language settings and select **Next** (from this point on, it will be implied to select **Next** or **OK**, if applicable). Select **Install now**. 

Choose the **Standard Evaluation (Desktop Experience)** version of Server 2016: 

<p align="center"><img alt="Selection of Server 2016 evaluation in Windows Setup" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/002-evaluation-version.png" width="640"></p>

Accept the license terms. Select **Custom: Install Windows only (advanced)**. Leave the default partition and format settings. Allow Windows to restart. You may disconnect the installation media now. 

Create a password—_Password123_ is sufficient for a home lab with no real-life security risks to mitigate. Log in. You can select **Yes** on the Networks popup to allow your machine to be discoverable on the network. If your system date and time are incorrect, change them in Settings > Time & language > Date & time. 

The default hostname in Windows Server is something like _WIN-BKU971JG9GM_. Go to File Explorer, right-click This PC, select Properties, and under **Computer name, domain, and workgroup settings**, select **Change settings** > **Computer Name** > **Change...** and enter a more readable name:

<p align="center"><img alt="Computer Name dialog box" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/003-computer-name.png" width="640"></p>

Apply the changes and restart the system. 

Open Internet Explorer, select the gear :gear: icon in the top-right corner > **Internet Options** > **Security** > **Internet** > **Custom level...** and scroll down to **Downloads** and enable file downloads:

<p align="center"><img alt="Security Settings - Internet Zone dialog box" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/004-internet-options.png" width="640"></p>

Back in the Internet Options dialog box, select the **Local Intranet** security zone > **Custom level...** and make sure file downloads are enabled there too. 

Still in the same Security tab, select the **Trusted sites** zone > **Sites** and add **https://\*.google.com** to your trusted sites. 

Google **Chrome**, download Chrome, run Chrome. Close IE for good. 

In Chrome, Google **Unified Communications Managed API 4.0**. The first link should be https://www.microsoft.com/en-us/download/details.aspx?id=34992. This is the first dependency of Exchange 2016. Download and run the setup program: 

<p align="center"><img alt="Unified Communications Managed API 4.0 Runtime installer" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/005-UCMA-setup.png" width="640"></p>

Accept the terms and install. 

Google **Visual C++ Redistributable 2013 download**. Click the first link: https://www.microsoft.com/en-us/download/details.aspx?id=40784. This is the second dependency of Exchange 2016, needed to prepare AD later. Click **Download** and select the 64-bit version. Run the download and install: 

<p align="center"><img alt="Visual C++ 2013 Redistributable setup program" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/006-vcredist.png" width="640"></p>

Next, we will install AD DS and its required features, such as Group Policy and Lightweight Directory Services (LDS). Go to Start > Server Manager > Manage > Add Roles and Features > Next. Use the default **Role-based** installation and server selection. Select **Active Directory Domain Services** > **Add Features** to add the AD DS role to the server. That's everything for now; proceed to install:

<p align="center"><img alt="Results screen of the Add Roles and Features Wizard" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/007-AD-DS-install.png" width="640"></p>

When you see _Installation succeeded_ (as in above image), select **Promote this server to a domain controller** > **Add a new forest** and enter a root domain name: 

<p align="center"><img alt="Deployment Configuration screen of the AD DS Configuration Wizard" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/008-domain-name.png" width="640"></p>

Enter a DSRM password and confirm. Leave DNS delegation off. Leave the default NetBIOS domain name and AD paths. Install and allow the system to reboot. 

<p align="center"><img alt="Server 2016 lock screen showing 'Other user'" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/009-domain-login.png" width="640"></p>

Tip: circled in red are two ways you can tell if you are now part of a domain as opposed to a workgroup, right from the lock screen: "...sign in to another domain" and "ROMANJM\Administrator" (given a domain name of _ROMANJM_, as an example). 

Go to **Start** > **Control Panel** > **Network and Sharing Center** (aka **View network status and tasks**) > **Change adapter settings**, right-click your adapter (usually named _Ethernet_ or _Ethernet0_), select **Properties**, double-click **Internet Protocol Version 4 (TCP/IPv4)**, and select **Obtain DNS server address automatically**. Repeat for **Internet Protocol Version 6 (TCP/IPv6)**: 

<p align="center"><img alt="IPv6 Properties dialog box showing DNS server address settings" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/010-DNS-address.png" width="640"></p>

If using a VM, reconfigure your disc drive to use the Exchange Server image downloaded at the beginning. Connect the Exchange Server installation media. It should show in File Explorer > This PC as the D: drive. 

Go to Start, right-click Windows PowerShell, and run it as Administrator. Run the `d:` command to change to the D: drive. Double-check the contents with `dir`: 

<p align="center"><img alt="Output of d: and dir commands in PowerShell" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/011-D-drive.png" width="640"></p>

Run `Install-WindowsFeature RSAT-ADDS` to install the Remote Tools Administration Pack. Then, run the following one-liner:

```PowerShell
Install-WindowsFeature NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS
``` 

Next, run `.\Setup /PrepareSchema /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF` to extend the AD schema for Exchange:

<p align="center"><img alt="PowerShell showing two successfully run commands and an error-throwing command" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/012-PS-installs.png" width="640"></p>

As you can see, the last command fails and throws a helpful error: "This computer requires .NET Framework 4.8 (https://support.microsoft.com/kb/4503548)." This is the third dependency of Exchange 2016, also needed in preparing AD. Open the link (highlighted in the above image) in Chrome and scroll down to **Download information**. Click **Download the Microsoft .NET Framework 4.8 offline installer package now.** Run the download and install:

<p align="center"><img alt=".NET Framework 4.8 installer" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/013-dotnet-framework.png" width="640"></p>

Restart the computer. Go back into PowerShell as an administrator, change to the D: drive, and run `.\setup /prepareschema /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF` again, successfully this time. Then, run `.\setup /preparead /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF /OrganizationName:"COMPANY"` to create the _Exchange organization_ in AD:

<p align="center"><img alt="Successful .\Setup /PrepareSchema and /PrepareAD commands in PowerShell" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/014-preparead.png" width="640"></p>

Finally, run `.\setup /preparedomain /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF` to prepare the AD domain where mail users will be located:

<p align="center"><img alt=".\Setup /PrepareDomain succeeding in PowerShell" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/015-preparedomain.png" width="640"></p>

Go back to File Explorer > This PC, right-click the D: drive, and select **Install or run program from your media**. Don't check for updates right now. Accept the license agreement. Use recommended settings for errors. Select the Mailbox role for the server. Use the default path for the Exchange Server installation. Leave malware scanning enabled. 

The prerequisite analysis step throws an error, giving us another opportunity to apply troubleshooting skills:

<p align="center"><img alt="Readiness Checks failing in the Exchange Server installation wizard" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/016-rewrite-lacking.png" width="640"></p>

The error reads: "The 'IIS URL rewrite module' isn't installed on this computer and needs to be installed before Exchange Setup can begin. For more information, visit: https://docs.microsoft.com/Exchange/plan-and-deploy/deployment-ref/ms-exch-setupreadiness-IISURLRewriteNotInstalled?view=exchserver-2016." This is the fourth and final dependency of Exchange 2016. Click the link in the error message and select **URL Rewrite Module version 2.1**. Next to **English**, select **x64 installer**. Run the download and install:

<p align="center"><img alt="IIS URL Rewrite Module 2.1 installer" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/017-url-rewrite.png" width="640"></p>

Back in the Exchange Server installation wizard, click **retry** on the Readiness Checks page and the checks should succeed. Select **install**. Wait about a half hour. Select **Launch Exchange Administration Center after finishing Exchange setup.** Click **finish**. The Exchange admin center should open in Chrome:

<p align="center"><img alt="EAC login page in Chrome" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/018-admin-center.png" width="640"></p>

If the page does not automatically open, then browse to **localhost/ecp** or, given a hostname of _AD-Exch-2016_, to **ad-exch-2016/ecp** in Chrome. (The "ecp" stands for "Exchange Control Panel," which is the name of the predecessor to the Exchange admin center. Microsoft didn't update "ecp" to "eac" I guess.) 

Enter your domain name and "administrator" username, delimited by a backslash as in the above image. Enter your password and sign in:

<p align="center"><img alt="EAC recipient mailboxes page in Chrome" src="https://github.com/romanjamesm/media/blob/main/Windows-Server-2016-Home-Lab/019-exchange-recipients.png" width="640"></p>

This is the current list of recipient mailboxes, only one at the moment. 

In Server Manager, practice creating users and organizational units (OUs) to organize the users. 

Back in the EAC, add some mailboxes and assign them to users. 

Next, we'll create network shares and security groups with different levels of permissions to access those shares. 

## Relevant Documentation

- For installing Exchange 2016 prerequisites: https://learn.microsoft.com/en-us/exchange/plan-and-deploy/prerequisites?view=exchserver-2016#exchange-2016-mailbox-servers-on-windows-server-2016
- Preparing AD and domain for Exchange 2016: https://learn.microsoft.com/en-us/exchange/plan-and-deploy/prepare-ad-and-domains?view=exchserver-2016
- Creating mail users in the EAC: https://learn.microsoft.com/en-us/exchange/recipients/mail-users?view=exchserver-2016

