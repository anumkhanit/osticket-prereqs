<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation (Part 1)</h1>
<p>In this installation tutorial, I will walk you through what you need and how to set up osTicket, an open-source help desk ticketing system. With some notes and screenshots to give you a quick peek at the important stuff.</p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines: Windows 10 recommend for this guide)
- MacBook Air
- RD Client
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10 Pro

<h2>Files to use for installation</h2>

- https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6

-----

<h1>Part 1: Setting Up Your Azure Virtual Machine</h1>

<h2>1) Create a Resource Group</h2>

- Start by logging into your Azure portal.

- Click on "Create a resource" and choose "Resource group."

- Name your resource group, and select a region. Click "Review + create" and then "Create."

<h2>2) Create a Windows 10 Virtual Machine</h2>

- In the Azure portal, select your newly created resource group.

- Click on "Add" and search for "Windows 10 Pro." Choose an appropriate image.
  
- Configure your VM with 2-4 virtual CPUs and memory as needed.
  
- Allow the creation of a new Virtual Network (VNet) during VM setup.

-----

<h1>Part 2: Installation</h1>

<h3>1) Azure Virtual Machine Configuration</h3>

- Name your VM (e.g., "Vm-osticket").
  
- Set a username (e.g., "labuser").
  
- Choose a strong password (e.g., "osTicketPassword1!").
  
<h3>2) Download Installation Files</h3>

- Open your RD Client and within the VM, you can you copy and paste it through the search bar and download the installation files: https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6

<h3>3.1) Install Within Windows VM & Enable IIS with CGI and Common HTTP Features</h3>

- Open "Server Manager" on your VM.
  
- Go to "Manage" and select "Add roles and features."

- Go to "World Wide Web Services" to "Application Development Features"
    - CGI
    - Common HTTP Features

<h3>3.2) ALONG with IIS Management Console</h3>

- Go to "Internet Information Services" to "Web Management Tools" to "IIS Management Console"
    - IIS Management Console

<p align="center">
<img src="https://i.imgur.com/MUljPsb.png" height="50%" width="50%" />
</p>

<h3>4) Install PHP Manager for IIS</h3>

- Download and install "[PHP Manager for IIS](https://drive.google.com/file/d/1RHsNd4eWIOwaNpj3JW4vzzmzNUH86wY_/view?usp=share_link)" (PHPManagerForIIS_V1.5.0.msi) from your installation files.

<h3>5) Install the Rewrite Module</h3>

- Download and install the "[Rewrite Module](https://drive.google.com/file/d/1tIK9GZBKj1JyUP87eewxgdNqn9pZmVmY/view?usp=share_link)" (rewrite_amd64_en-US.msi) from your installation files.

<h3>6) Create the C:\PHP Directory or Folder</h3>

- Find "Windows Files Explorer" and head to "The PC" and create a folder of "PHP".

<h3>7) Install PHP 7.3.8</h3>

- Download [PHP 7.3.8](https://drive.google.com/file/d/1snNMtLdCOpMtkCyD4mvl9yOOmvVIp9fP/view?usp=share_link) (php-7.3.8-nts-Win32-VC15-x86.zip) from your installation files. (Note: if you see a warning icon, ignore it and keep it!)

<p align="center">
<img src="https://i.imgur.com/MpP1vqT.jpg" height="50%" width="50%" />
</p>

<p align="center">
<img src="https://i.imgur.com/nClDfL8.jpg" height="30%" width="50%" />
</p>

- After downloading the content, first move the content and unzip it into the "PHP folder.

<h3>8) Install VC_redist.x86.exe</h3>

- Download and install "[VC_redist.x86.exe](https://drive.google.com/file/d/1s1OsGF3-ioO0_9LYizPRiVuIkb3lFJgH/view?usp=share_link)" from your installation files.

<h3>9) Install MySQL 5.5.62</h3>

- Download and install "[MySQL 5.5.62](https://drive.google.com/file/d/1_OWh9p7VQLcrB0q_V7qT8yHl0xo5gv7z/view?usp=share_link)" (mysql-5.5.62-win32.msi) from your installation files.
  
- During installation, select "Typical Setup" and configure with the password "Password1."

<h3>10) Register PHP in IIS</h3>

- Open IIS as an administrator.
  
- Register PHP from within IIS.
  
<h3>11) Reload IIS</h3>

- Open IIS, stop and start the server.
  
<h3>12) Install osTicket v1.15.8</h3>

- Download osTicket from the Installation Files Folder.
  
- Extract and copy the "upload" folder to "c:\inetpub\wwwroot."
  
- Rename the "upload" folder to "osTicket" within "c:\inetpub\wwwroot."

<h3>13) Reload IIS Again</h3>

- Open IIS, stop and start the server.
  
<h3>14) Configure osTicket</h3>

- Go to sites -> Default -> osTicket.
  
- Click "Browse *:80." and note any missing extensions.
  
<h3>15) Enable PHP Extensions</h3>

- Go back to IIS, sites -> Default -> osTicket.
  
- Double-click PHP Manager.
  
- Click "Enable or disable an extension."

- Enable:
    - php_imap.dll
    - php_intl.dll
    - php_opcache.dll
      
- Refresh the osTicket site in your browser and observe the changes.

<h3>16) Rename ost-config.php</h3>

- Rename "ost-sampleconfig.php" to "ost-config.php" within "C:\inetpub\wwwroot\osTicket\include."
  
<h3>17) Assign Permissions to ost-config.php</h3>

- Disable inheritance and remove all permissions.
  
- Add new permissions for "Everyone" with "All" access.
  
<h3>18) Continue Setting up osTicket in the Browser</h3>

- Visit the osTicket setup page in your browser and follow the on-screen instructions. Name your helpdesk and set the default email.

<h3>19) Install HeidiSQL</h3>

- Download and install "[HeidiSQL](https://www.heidisql.com/installers/HeidiSQL_12.3.0.6589_Setup.exe)" from your installation files.
  
- Open HeidiSQL and create a new session using "root" and the password "Password1."

<h3>20) Create a Database</h3>

- Connect to the session and create a database called "osTicket."

<h3>21) Complete osTicket Setup</h3>

- Continue setting up osTicket in the browser, providing the following details:
    - MySQL Database: osTicket
    - MySQL Username: root
    - MySQL Password: Password1

- Click "Install Now!"

<h1>Clean Up</h1>

<h3>1) Delete Setup Files</h3>

- Delete the "C:\inetpub\wwwroot\osTicket\setup" folder.

<h3>2) Set Permissions</h3>
Set the permissions of "C:\inetpub\wwwroot\osTicket\include\ost-config.php" to "Read" only.

-----
<h1>Conclusion</h1>

Congratulations! You've made it through a tedious process of installing a help desk software by scratch! Now that the osTicket is installed with no errors. You can access your help desk login page at http://localhost/osTicket/scp/login.php. Along with the End Users osTicket URL: http://localhost/osTicket/ you will use for another lesson.

-----

# [Next: osTicket - Post Installation Setup (Part 2)](https://github.com/anumkhanit/post-install-config)
