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

- Search up "Virtual Machines" and click on it, there you will discover your Virtual Machine.

![image](https://github.com/user-attachments/assets/d9c3f136-bea5-4c5f-91fe-9391d61a50ef)

Log into the VM with Remote Desktop
- On your PC, click the Windows 'start' icon to open up the menu and search up "Remote Desktop Connection".
- If using Mac, install Microsoft Remote Desktop.
- Copy windows VM Public IP address and paste it into the Remote Desktop Connection.
- Click 'Show Options' and put in the user name for the windows VM (labuser).
- Click 'connect'.
- Insert the password then click 'ok'.
- Click 'Yes' to continue.

![image](https://github.com/user-attachments/assets/fda72741-0438-4b5a-9d84-3124eb25398b)

- Within the VM (osticket-vm), open your browser and copy/paste the <a href="https://drive.usercontent.google.com/download?id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD&export=download&authuser=0">osTicket-Installation-Files.zip</a> link.

![image](https://github.com/user-attachments/assets/439c0d8f-8b91-4d25-b798-8e8af870439a)

- Click 'Download anyway' and when it has downloaded you can click on the folder icon and take you the file downloads folder section. The folder should be called “osTicket-Installation-Files”

![image](https://github.com/user-attachments/assets/72573046-d1f6-46a5-a4c5-c485834cd9f3)

- Drag the zip folder from the downloads section onto the VM desktop.
- We will use the files in this folder to install osTicket and some of the dependencies.

![image](https://github.com/user-attachments/assets/3a369161-cece-41e6-ad79-106d458a598d)

- Right click on the unzipped folder and and click Extract all.

![image](https://github.com/user-attachments/assets/d35670ca-428c-41d4-8fea-d780f29ba7f6)


- Make sure it is going to this folder and click 'Exrtract'.
- Once extraxted you can delete the original unzipped folder.

![image](https://github.com/user-attachments/assets/19a8c420-b097-46dd-8d22-c82cd8b5698c)

![image](https://github.com/user-attachments/assets/f0ee894b-4af1-4a7d-8efb-bcd1d9b83791)

Install / Enable IIS (Internet Information Services) in Windows WITH CGI
- To enable IIS on you VM windows search bar, type up and go to 'Control Panel'.

![image](https://github.com/user-attachments/assets/1072a94b-abf4-451c-be2e-8f418242392b)

- Under Programs click on 'Uninstall a program'.
- Click on 'Turn Windows features on or off'.

![image](https://github.com/user-attachments/assets/bd8e9ee8-cdf9-426a-bed6-e23bc4f83227)

- Tick the box 'Internet Information Services' and expand it.
- Expand World Wide Web Services and expand Application Development Features.
- Tick the box for 'CGI' and click OK.
- Once the message "Windows completed the requested changes" appears, close the window.

![image](https://github.com/user-attachments/assets/d0a501c7-ac86-4952-bc4e-090d962e0780)

- Open your web browser and type 127.0.0.1 into the address bar. You should see a page from IIS (Internet Information Services), which means your virtual machine is now working as a web server.

![image](https://github.com/user-attachments/assets/38b18df6-986a-43e3-8c95-2bd99e1a1aa8)

- Install PHP Manager for IIS (PHPManagerForIIS_V1.5.0).
- In your folder (Quick Access) you will observe the 'osTicket-Installation' and click on it.
- Open 'PHPManagerForIIS_V1.5.0.

![image](https://github.com/user-attachments/assets/d6584ea8-f91a-4335-993c-9759f0001256)

- Click 'Next' -> press 'I Agree' -> 'Next'. 
- When installation is complete you can close te window.

![image](https://github.com/user-attachments/assets/73ce697a-a298-4e25-9862-dc1843831f20)

 
- Install the Rewrite Module (rewrite_amd64_en-US).
- From winthin the same folder you're gonna install the Rewrite Module.
- Click 'I accept' -> 'Install'.
- Wait till intallation is complete and click 'Finish'.

![image](https://github.com/user-attachments/assets/4f109ec3-5cff-4fbf-bf4c-ee65b96870dd)

- Open a new File window.
- Click on 'This PC' to extend and go to 'Windows (C:)'.
- Make a new folder and call it 'PHP'.

![image](https://github.com/user-attachments/assets/b91933ac-560e-4bd2-a0f2-79267d0e0c39)

- From the “osTicket-Installation-Files” folder, unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into the “PHP” folder.
- Right click the (php-7.3.8-nts-Win32-VC15-x86.zip) folder and click 'Extract all'.
- Browse till you find the folder 'PHP' folder you just created and click 'Select Folder' -> 'Extract'.

![image](https://github.com/user-attachments/assets/9b336334-13a7-4ad8-b593-2efa018ea671)

- From the “osTicket-Installation-Files” folder, install (VC_redist.x86).
- Tick 'I agree' -> 'Install', then you can close the window.

![image](https://github.com/user-attachments/assets/3695d8b4-b757-4fb4-bd5f-b9fb8cfd03cb)

- From the “osTicket-Installation-Files” folder, install MySQL 5.5.62 (mysql-5.5.62-win32.)
- Click 'Next', tick 'I accept' -> 'Next'.
- For Setup Type click on Typical -> 'Install'.

![image](https://github.com/user-attachments/assets/19153721-1b90-433c-b21f-ed631af671d8)

- Launch Configuration Wizard (after install)
- When installation is complete click 'Finish' -> 'Next'.
- Choose 'Standard Configuration'.

![image](https://github.com/user-attachments/assets/391e2014-7096-49c8-ba83-defa2b289a74)

- 'Next' -> 'Next'
- Input the details as follows for MySQL Server:
- Password: root (do not get this wrong)

![image](https://github.com/user-attachments/assets/db7b4893-1f93-40f1-948b-314fd62bbdde)

- 'Next' -> 'Excecute'.
- Wait for configuration to process then click 'Finish'.

 ![image](https://github.com/user-attachments/assets/1cd2397f-2012-472e-a542-d7de7444668d)

Open IIS as an Admin  
- On your VM go to your windows search bar and type up "IIS" (Internet Information Services)
- Click 'Run as administrator'

![image](https://github.com/user-attachments/assets/c9dfdbd2-490d-43d1-94a8-1e58a93055f8)

![image](https://github.com/user-attachments/assets/8e752850-392b-4667-a748-ee0dcb21c49b)

-Register PHP from within IIS (PHP Manager -> Register new PHP version)  
C:\PHP\php-cgi.exe). 

![image](https://github.com/user-attachments/assets/04cb0c66-2378-4a22-9c42-f0be23e17726)

![image](https://github.com/user-attachments/assets/2065892f-95e6-4075-af7f-5c5749ad26eb)


- Then Reload IIS (Open IIS, Stop and Start the server. Under "Actions" on the right you can see the options to stop and start the server.)


-----------------------------------------------------------------------------
-----------------------------------------------------------------------------

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
