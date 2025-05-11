<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Setup a Resource Group and a Virtual Machine in Azure.
- Install the osTicket requirements.
- Install osTicket itself.

<h2>Installation Steps</h2>

1. Creating Resource Groups and Virtual Machines

Resource Group:

- To create a Resource Group, go to the Azure Portal. In the middle of the homepage under 'Azure Services', click on 'Resource groups' and then select 'Create' to begin the process'.

![Screenshot 2025-05-02 161517](https://github.com/user-attachments/assets/ec12459d-cb6b-48e2-9c15-cbb380493b23)

- All rescources in a subsciption are billed together so leave that as default.
- Resource group name can be named to your desire. I will call mine "osTicket".
- When selecting a resource group region, it's recommended that you select a location close to where your control operations originate.
- Click 'Review + create' -> 'Create'.

![image](https://github.com/user-attachments/assets/50d8efe0-d58b-460b-b8d8-05b296ef5a42)

Virtual Machines:

- In the Azure Portal, use the search bar at the top os search for 'Virtual Machines" and select it.
- In the display area, click 'Create' -> 'Azure virtual machine'.

![Screenshot 2025-05-02 225357](https://github.com/user-attachments/assets/c78dd6c5-e884-40fe-83ac-4b2933348372)

- Under 'Project details', assign your new resource group you just created (osTicket).
- Give your Virtual Machine name "osticket-vm".
- Select the resource region the same as the Resource groups ((Asia Pacific) Australia East).

![image](https://github.com/user-attachments/assets/a45acb8c-7570-42aa-847b-aee985598bc4)

- For Image, select 'Windows 10 Pro version 22H2 - x64 Gen2'.
- Recommended for 'Size' you utilise "Standard_D2s_v5 - 2 vcpus, 8 GiB memory".
- For 'Administrator Account' create your Username "labuser" and password can be anything. e.g; "osTicketPassword1!".

![image](https://github.com/user-attachments/assets/5e8854b0-2b7d-4056-bad0-81824d17ef5b)

- Be sure to tick the box for eligibily of a windows liscence.
- Click 'Review + Create'.

![image](https://github.com/user-attachments/assets/7f996f2b-c763-4ba2-bbfd-08d8fe10973e)

- Wait for the VM to process till you see "Validation passed" on the top of the page.

![Screenshot 2025-05-06 141709](https://github.com/user-attachments/assets/03ba5cf9-cf60-4dba-9bc6-3b7ded00c07e)

- Then click 'Create'.
- You have successfully created a Windows Virtual Machine.

![Screenshot 2025-05-06 141743](https://github.com/user-attachments/assets/461d94d0-4c8e-4888-b191-f1aa8dbedd03)

Observing ICMP Traffic
- On your PC, click the Windows 'start' icon to open up the menu and search up "Remote Desktop Connection".
- If using Mac, install Microsoft Remote Desktop.
- Copy windows VM Public IP address and paste it into the Remote Desktop Connection.
- Click 'Show Options' and put in the user name for the windows VM (labuser).
- Click 'connect'.


-----------------------------------------------------------------------------
-----------------------------------------------------------------------------





Log into the VM with Remote Desktop

Within the VM (osticket-vm), download the osTicket-Installation-Files.zip and unzip it onto your desktop. The folder should be called “osTicket-Installation-Files”
- We will use the files in this folder to install osTicket and some of the dependencies.

Install / Enable IIS in Windows WITH CGI
- World Wide Web Services -> Application Development Features -> [X] CGI

From the “osTicket-Installation-Files” folder, install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)

From the “osTicket-Installation-Files” folder install the Rewrite Module (rewrite_amd64_en-US.msi)

Create the directory C:\PHP

From the “osTicket-Installation-Files” folder, unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into the “C:\PHP” folder

From the “osTicket-Installation-Files” folder, install VC_redist.x86.exe.

From the “osTicket-Installation-Files” folder, install MySQL 5.5.62 (mysql-5.5.62-win32.msi)
- Typical Setup ->
- Launch Configuration Wizard (after install) ->
- Standard Configuration ->
- Username: root
- Password: root

Open IIS as an Admin

Register PHP from within IIS (PHP Manager -> C:\PHP\php-cgi.exe)

Reload IIS (Open IIS, Stop and Start the server)

Install osTicket v1.15.8
- From the “osTicket-Installation-Files” folder, unzip “osTicket-v1.15.8.zip” and copy the “upload” folder into “c:\inetpub\wwwroot”
- Within “c:\inetpub\wwwroot”, Rename “upload” to “osTicket”

Reload IIS (Open IIS, Stop and Start the server)

Go to sites -> Default -> osTicket
- On the right, click “Browse *:80”

Note that some extensions are not enabled
- Go back to IIS, sites -> Default -> osTicket
- Double-click PHP Manager
- Click “Enable or disable an extension”
- Enable: php_imap.dll
- Enable: php_intl.dll
- Enable: php_opcache.dll
- Refresh the osTicket site in your browser, observe the changes

Rename: ost-config.php
- From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
- To: C:\inetpub\wwwroot\osTicket\include\ost-config.php

Assign Permissions: ost-config.php
- Disable inheritance -> Remove All
- New Permissions -> Everyone -> All

Continue Setting up osTicket in the browser (click Continue)
- Name Helpdesk
- Default email (receives email from customers)

From the “osTicket-Installation-Files” folder, install HeidiSQL.
- Open Heidi SQL
- Create a new session, root/root
- Connect to the session
- Create a database called “osTicket”

Continue Setting up osTicket in the browser
- MySQL Database: osTicket
- MySQL Username: root
- MySQL Password: root
- Click “Install Now!”

Congratulations, hopefully it is installed with no errors!
- Browse to your help desk login page: http://localhost/osTicket/scp/login.php

End Users osTicket URL:
- http://localhost/osTicket/ 

Clean up
- Delete: C:\inetpub\wwwroot\osTicket\setup
- Set Permissions to “Read” only: C:\inetpub\wwwroot\osTicket\include\ost-config.php
