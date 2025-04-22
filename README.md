<p align="center">
  <img src="https://github.com/user-attachments/assets/f708ec8e-ae0a-4d4f-8e42-fe84f594fba4"/>
</p>

<h1>osTicket - Prerequisites and Installation<h1>  
In this lab, I install osTicket from the ground up using the necessary installation files. There are a few steps to take before the installation of the ticketing system. This lab is done using a Windows 10 Pro VM made on Azure.
<br />

<h2>Environment and Technologies Used</h2>

- <b>Microsoft Azure (Virtual Machines)</b> 
- <b>Remote Desktop Connection</b>
- <b>Internet Information Services (IIS)</b>
- <b>MySQL)</b>

<h2>Environment and Technologies Used</h2>

- <b>Windows 10 Pro</b> 

<h2>Installation Steps</h2>

Before installing any files, Internet Information Services (IIS) needs to be enabled. We are installing osTicket locally and it needs IIS in order to function. To turn on IIS, open the Control Panel. From the Control Panel, open Programs and and Turn Windows Features On or Off. Within this menu, expand Internet Information Services, expand Web Management Tools and enable IIS Management Console. Click and expand World Wide Web Services and expand Application Development Features. In Application Development Features, enable CGI and click ok to confirm.

![iis](https://github.com/user-attachments/assets/8c48c067-9e9f-48bb-a31e-e3011c0c9524)

After enabling IIS, download and install PHP Manager for IIS (PHPManagerforIIS_V1.5.0.msi) from the installtion files folder. Download and install the Rewrite Module (rewrite_amd64_en-US.msi) after installing PHP Manager for IIS.

![iis2](https://github.com/user-attachments/assets/facec482-6708-460d-93f1-83a93afd6be2)

After installing the Rewrite Module, create a new folder/directory called C:\PHP on the Windows (C:) drive. This new folder will be used to unzip the contents from the PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) zip folder downloaded from the installation files. Extract all contents from the zip folder into the C:\PHP folder.

![cphp](https://github.com/user-attachments/assets/bef6430d-93e8-4fa1-b5b0-b0008d461856)

Next, download and install VC_redist.x86.exe from the installation files.

![redist](https://github.com/user-attachments/assets/65de48e2-3124-4fa0-897c-eb88106d3f61)

Next, download and install MySQL 5.5.62 (mysql-5.5.62-win32.msi) from the installation files. Within the MySQL setup wizard, click "I agree" and select a Typical install and Install. Launch the Configuration Wizard after the installation. Select Standard Configuration and select Install As Windows Service and make sure Launch the MySQL Server automatically is checked. For credentials, the username will be root and the password is Password1. In a practical setting, the credentials will be basic to where they can be easily guessed. For the purposes of this lab, the standard credentials root and Password1 will do.

![mysql](https://github.com/user-attachments/assets/2bbc1b0c-c9a8-4825-a6bb-8b07efa967a8)

Before installing osTicket, configurations need to be made within IIS. Open IIS as an admin and select PHP Manager. Within PHP Manager, select Register new PHP version. Select Browse and select the PHP CGI executable file (php-cgi.exe) within the PHP folder created earlier in the lab. After registering the PHP version, reload the IIS server within the management console.

![php](https://github.com/user-attachments/assets/c553778c-7226-4ec8-849d-180b3dd1b3cc)
![php2](https://github.com/user-attachments/assets/48cc091d-be7f-4985-a24e-6f8110a1416c)

From the installation files, download osTicket v1.15.8. Extract and copy the "upload" folder to the following path: c:\inetpub\wwwroot. Within the c:\inetpub\wwwroot folder, rename "upload" to "osTicket." Reload the IIS server afterwards.

![wwwroot](https://github.com/user-attachments/assets/7a4be366-b230-481c-be4c-172d6851601f)

Within the IIS console, browse to Sites -> Default -> osTicket. Click "Browse *:80" and the installation page for osTicket will now show up. Some extensions are not enabled and they will be enabled with the IIS console before installing osTicket. To do so, click on PHP Manager while in the osTicket menu in IIS. Click on "Enable or disable an extension." Enable the following extentions: php_imap.dll, php_intl.dll, php_opcache.dll.

![install1](https://github.com/user-attachments/assets/796a96c1-578b-4045-ad6f-2bcbb3d91533)
![install2](https://github.com/user-attachments/assets/5bf62574-0e8e-40db-bed3-9f1f0ff6ac26)
![install3](https://github.com/user-attachments/assets/db4eed66-4fe3-44fc-a6ac-92ec5df0289e)

Before continuing to install osTicket, a file needs to be renamed as well as have its permissions changed. From C:\inetpub\wwwroot\osTicket\include, rename ost-sampleconfig.php to ost-config.php. The newly named ost-config.php will have its permissions changed. Open its Properties and change the following permissions: Disable inheritence -> Remove All and New Permissions -> Everyone -> All.

![ostsample](https://github.com/user-attachments/assets/87aaf969-5497-4f59-a4eb-2aab1169e37d)
![ostconfig](https://github.com/user-attachments/assets/92769f26-119a-4a7d-84c0-0ca3a5292cf6)

From the installation files, download and install HeidiSQL. Create a new session with HeidiSQL and enter the password used in the installation of MySQL earlier. Within the new session, right-click on Unnamed and create a new database named osTicket.

![hedisql](https://github.com/user-attachments/assets/87756bb5-bd2a-421b-b1e9-43257300cb91)
![heidisql2](https://github.com/user-attachments/assets/17818137-1e07-419b-b3eb-6ad8626cc8d7)

Within osTicket browser window, enter the necessary details to set up osTicket. For the MySQL database, use the credentials used for MySQL and HeidiSQL.

![databaeinstall](https://github.com/user-attachments/assets/d3d5b290-9573-4294-82cb-a83d7e9e4643)

After everything is done, osTicket should now be installed! Before continuing to use osTicket, some clean up has to be done. First, delete the setup folder found in C:\inetpub\wwwroot\osTicket. Next, return to C:\inetpub\wwwroot\osTicket\include and change the permissions of the ost-config.php file. The file should no longer have full access to Everyone. Revert the permissions to "Read" only.

![osinstall](https://github.com/user-attachments/assets/3f1d334f-995e-448e-8428-718a1e07cecb)

<h2>osTicket Installed!</h2>

osTicket is now installed and ready to be used. I used osTicket to understand how ticketing systems work and how to resolve tickets. In IT Support, I have to work with a team to solve a person's IT related issues through the use of a ticketing system. I used this lab as a means to set up a ticketing system from the ground up and lay the grounds for what I will do in the future.
