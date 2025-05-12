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

- From the “osTicket-Installation-Files” folder, install MySQL 5.5.62 (mysql-5.5.62-win32).
- Click 'Next', tick 'I accept' -> 'Next'.
- For Setup Type click on Typical -> 'Install'.

![image](https://github.com/user-attachments/assets/19153721-1b90-433c-b21f-ed631af671d8)

- Launch Configuration Wizard (after install).
- When installation is complete click 'Finish' -> 'Next'.
- Choose 'Standard Configuration'.

![image](https://github.com/user-attachments/assets/391e2014-7096-49c8-ba83-defa2b289a74)

- 'Next' -> 'Next'.
- Input the details as follows for MySQL Server:
- Password: root (do not get this wrong).

![image](https://github.com/user-attachments/assets/db7b4893-1f93-40f1-948b-314fd62bbdde)

- 'Next' -> 'Excecute'.
- Wait for configuration to process then click 'Finish'.

 ![image](https://github.com/user-attachments/assets/1cd2397f-2012-472e-a542-d7de7444668d)

Open IIS as an Admin  
- On your VM go to your windows search bar and type up "IIS" (Internet Information Services).
- Click 'Run as administrator'.

![image](https://github.com/user-attachments/assets/c9dfdbd2-490d-43d1-94a8-1e58a93055f8)

![image](https://github.com/user-attachments/assets/8e752850-392b-4667-a748-ee0dcb21c49b)

- Register PHP from within IIS (PHP Manager -> Register new PHP version).

![image](https://github.com/user-attachments/assets/04cb0c66-2378-4a22-9c42-f0be23e17726)

![image](https://github.com/user-attachments/assets/2065892f-95e6-4075-af7f-5c5749ad26eb)

- Browse till you find (C:\PHP\php-cgi.exe). 

![image](https://github.com/user-attachments/assets/67279400-8ab7-465b-9ded-cb9847354330)

![image](https://github.com/user-attachments/assets/524a7c71-4fb8-4372-98ed-c76ddefd988f)

- Click 'OK'.

![image](https://github.com/user-attachments/assets/f0e454e8-f49e-475d-a4d4-d417918d083b)

- Then Reload IIS (Open IIS, Stop and Start the server. Under "Actions" on the right you can see the options to stop and start the server).

![image](https://github.com/user-attachments/assets/4d02b1d4-7aa1-441d-a3b7-1be2085c7390)

- Back in the “osTicket-Installation-Files” folder, unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into the “C:\PHP” folder.

![image](https://github.com/user-attachments/assets/c255fe8c-0db0-498e-9149-e341c7e3a1aa)

- Extract in this following Folder (osTicket-V1.15.8).

![image](https://github.com/user-attachments/assets/1e0e33b6-aa74-4b6b-b523-03f110300def)

- Open a new file folder.
- Within “c:\inetpub\wwwroot”

![image](https://github.com/user-attachments/assets/9bc4414f-dc24-4295-8b97-2798965e79fd)

![image](https://github.com/user-attachments/assets/0efd4466-9b25-4f37-a4e3-58b09fe7adc0)

- Copy/Paste the 'upload' folder from "osTicket-v1.15.8" into “c:\inetpub\wwwroot”

![image](https://github.com/user-attachments/assets/6f452871-997a-49b3-baf3-fece6ff9efb7)

![image](https://github.com/user-attachments/assets/33733c6c-2baf-4490-a558-b5124832e55a)

- Within “c:\inetpub\wwwroot”, Rename “upload” to “osTicket”. You can delete the old "upload" folder on "osTicket-v1.15.8".

![image](https://github.com/user-attachments/assets/11875bed-1524-49cc-84c6-d1212a6a2ddb)

- Reload IIS (Open IIS, Stop and Start the server)

![image](https://github.com/user-attachments/assets/4a1f82c9-14f2-4369-a388-c6e48ff4ed02)

- Go to sites -> Default -> osTicket

![image](https://github.com/user-attachments/assets/a1ff657b-15d2-492f-aaba-c7aaf6b1adaa)

![image](https://github.com/user-attachments/assets/9838ee5f-777f-42dd-ae31-68bbe0587309)

- On the right, click “Browse *:80”

![image](https://github.com/user-attachments/assets/ee849ce9-e150-4682-84b9-99359fef1ea8)

- Opening a new browser, some required extensions are currently disabled.

![image](https://github.com/user-attachments/assets/dd036dcd-8cdb-4aaa-9e6e-2c0d6ae5b478)

- Go back to IIS, sites -> Default -> osTicket

![image](https://github.com/user-attachments/assets/0ce83150-ad8d-4c05-b249-a1ebc670b149)

- Double-click PHP Manager

![image](https://github.com/user-attachments/assets/7f6115ca-41b6-421c-9b30-61c4dcd249f2)

- Click “Enable or disable an extension”

![image](https://github.com/user-attachments/assets/25983f0e-1bfd-4395-a7e7-265f5a5e69e3)

- Enable: php_imap.dll
- Enable: php_intl.dll
- Enable: php_opcache.dll

![image](https://github.com/user-attachments/assets/9bb5ee0b-6441-4319-8831-41e9b981eec6)

![image](https://github.com/user-attachments/assets/1d2bdfa5-d487-4ff5-be46-89abd831c457)

![image](https://github.com/user-attachments/assets/a65f8873-f887-42e2-8c31-21144f27af16)

- Refresh the osTicket site in your browser, observe the changes

![image](https://github.com/user-attachments/assets/f3c8f06c-d30c-4aeb-af6d-b387ec4ecc49)

Rename: ost-config.php
- From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
- To: C:\inetpub\wwwroot\osTicket\include\ost-config.php

![image](https://github.com/user-attachments/assets/1a228b6e-ec2a-45cc-8404-056b568f30dc)

![image](https://github.com/user-attachments/assets/7d9fa9f9-b4c3-4c06-a0c1-ae905ae4c3fa)

![image](https://github.com/user-attachments/assets/f6a07607-2147-499d-8788-25540bd1a522)

- From: ost-sampleconfig.php
- To: ost-config.php

![image](https://github.com/user-attachments/assets/9835a55f-6ea4-4070-915b-2e6e7df57d3d)

Assign Permissions: ost-config.php
- Right click 'ost-config.php' and go to Properties.

![image](https://github.com/user-attachments/assets/4ddcf136-0d12-4d1b-a354-481cb0605922)

- On the tabs, go to Security and click on 'Advanced'.

![image](https://github.com/user-attachments/assets/02aa4127-7b51-4a9b-bf34-2117c3055aef)

- Click 'Disable inheritance' -> 'Remove all inherited permissions from this object'.

![image](https://github.com/user-attachments/assets/63f99eb6-4055-496e-907a-4526f6d3bcbe)

![image](https://github.com/user-attachments/assets/c84b4775-62fc-4464-aca7-949831a4eabe)

- 'Add' new permissions.

![image](https://github.com/user-attachments/assets/b40e6484-3760-4f4b-8f66-7b200a822e6c)

- Click on 'Select a principal'

![Screenshot 2025-05-12 133655](https://github.com/user-attachments/assets/fd5b418d-45ff-4e36-9b44-085ed2c0ba7b)

- In the box to enter object names, type "everyone" and click 'Check Names'.
- Click 'OK'.

![image](https://github.com/user-attachments/assets/5fabd0a8-7f02-4cb5-b034-8c0eaadedfab)

- Under Basic permissions, tick 'Full control'.
- Click 'OK'.

![image](https://github.com/user-attachments/assets/791790bf-7b6d-46a7-b637-d1d59902f539)

- Everyone should have Full control.
- Click 'Apply' -> 'OK'.

![image](https://github.com/user-attachments/assets/caf8e58c-22f3-44d0-bd47-efabf87e05f6)

- You will observe under Security Permissions for Everyone has been allowed.
- Click 'OK'.

![image](https://github.com/user-attachments/assets/3890ae32-290b-48f9-801a-13547125ca58)

From the “osTicket-Installation-Files” folder, install HeidiSQL.
- Open Heidi SQL

![image](https://github.com/user-attachments/assets/dea7486d-68d6-45c3-9114-22f0ef6ecce4)


- Click 'I accept the agreement' then 'Next' -> 'Next' -> 'Next' -> 'Next' -> 'Install' -> 'Finish'.

![image](https://github.com/user-attachments/assets/4d0fc58b-ee51-472f-a328-c168a5421bde)

![image](https://github.com/user-attachments/assets/3367b3b4-97de-4beb-a8e1-cb233e944ca1)

![image](https://github.com/user-attachments/assets/f1548fd4-67a7-4b22-8bef-9c0cd2a208cd)

- Skip here.

![image](https://github.com/user-attachments/assets/90d90418-377e-47af-af2c-aa718cabc0b3)

- With this HeidiSQL page, we're gonna make a connection to our database and with the database for osTicket to use.
- Click 'New'.

![image](https://github.com/user-attachments/assets/f9f1b9b9-c9e3-45e8-bda6-31430f0c04f9)

MySQL Server:
- User: root
- Password: root
- Click 'Open'.
- This will open the connection to the database.

![image](https://github.com/user-attachments/assets/168c1377-4115-4b91-abfe-f18bb961b3ed)

- Create a database called “osTicket”
- Right click on 'Unamed', click 'Create new' -> 'Database.

![image](https://github.com/user-attachments/assets/efe32fdf-912d-4432-bcae-b674c6b12fd8)

- Name: "osTicket".
- Click 'OK'.

![image](https://github.com/user-attachments/assets/5484bf5a-a027-4e2e-a8e5-0316e75c6a82)

- You can observe that 'osTicket' is in the database.

![image](https://github.com/user-attachments/assets/12769aca-66b8-44ea-88b7-16245557d04f)




- Continue Setting up osTicket in the browser (click Continue)

![image](https://github.com/user-attachments/assets/d27ec0dc-a21b-485c-a2a9-8e528eaef6a8)

- In System Settings, create your Helpdesk Name. Mine will be "Nathan's Help Desk"
- Make a email. e.g, (nathan.butler.it@gmail.com)

![image](https://github.com/user-attachments/assets/b2ae5583-dec4-4a10-9e4a-74168c9ae5db)

- Under Admin User, you can just put your name and last name.
- Make a different email from the one you put in System Settings. mine is "me@nathanbutler.tech
- For osTicket Admin use:
- Username: adminuser 
- Password: Password1

![image](https://github.com/user-attachments/assets/affa9a8c-be1e-4c5c-a0ce-354b6e253814)

- With this HeidiSQL page, we're gonna make a connection to our database and with the database for osTicket to use.
- Click 'New'.

![image](https://github.com/user-attachments/assets/f9f1b9b9-c9e3-45e8-bda6-31430f0c04f9)

MySQL Server:
- User: root
- Password: root
- Click 'Open'.
- This will open the connection to the database.

![image](https://github.com/user-attachments/assets/168c1377-4115-4b91-abfe-f18bb961b3ed)

- Create a database called “osTicket”
- Right click on 'Unamed', click 'Create new' -> 'Database.

![image](https://github.com/user-attachments/assets/efe32fdf-912d-4432-bcae-b674c6b12fd8)

- Name: "osTicket".
- Click 'OK'.

![image](https://github.com/user-attachments/assets/5484bf5a-a027-4e2e-a8e5-0316e75c6a82)

- You can observe that 'osTicket' is in the database.

![image](https://github.com/user-attachments/assets/12769aca-66b8-44ea-88b7-16245557d04f)



-----------------------------------------------------------------------------
-----------------------------------------------------------------------------

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
