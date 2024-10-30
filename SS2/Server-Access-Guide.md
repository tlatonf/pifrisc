# SERVER DOCUMENTATION: SETUP AND ACCESS GUIDE

*Last updated: 03/10/2024*

***NOTICE:**
\- This guide is for Windows operating system users. For other operating systems (Linux/Mac OS), please contact the administrator for support.
\- Please contact the administrator to receive **your account** and **vpn configuration file**.
\- This is an internal document, please do not share it with others.
\- This is an internal document, please do not share it with others.
\- This is an internal document, please do not share it with others.*

## 1. Install & configure Wireguard (skip if you don't need remote external access)

* **WireGuard** is a straightforward VPN solution for secure and fast remote access. It allows you to create a virtual private network (VPN) to access the system from anywhere in the world.
* Download and install: https://www.wireguard.com/install/.

* Import configuration file:

  * Open the *WireGuard* app.
  * From the **Add Tunnel** drop-down *(located at the bottom left of the window)*, select Import tunnel(s) from file... or press **Ctrl+O**.
  * Then, select the provided config file.

* Connect to VPN: In the **Tunnels** tab, select the tunnel you just imported and click **Activate**.

* Check connection:

  * After connecting, if the **Transfer** section shows received data, it means you have successfully connected.

  * Another way to confirm your connection is by pinging a host. To do this, open *Terminal (or Windows PowerShell)* and running the command below. If you see similar results, your connection is successful.

    ```bash
    Windows PowerShell
    Copyright (C) Microsoft Corporation. All rights reserved.
    
    Install the latest PowerShell for new features and improvements! https://aka.ms/PSWindows
    
    PS C:\Windows\system32> ping eda.pifclub.site
    Pinging eda.pifclub.site [192.168.10.200] with 32 bytes of data:
    Reply from 192.168.10.200: bytes=32 time=2ms TTL=64
    Reply from 192.168.10.200: bytes=32 time=2ms TTL=64
    Reply from 192.168.10.200: bytes=32 time=2ms TTL=64
    Reply from 192.168.10.200: bytes=32 time=2ms TTL=64
    Ping statistics for 192.168.10.200:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
    Approximate round trip times in milli-seconds:
    Minimum = 2ms, Maximum = 2ms, Average = 2ms
    ```

**NOTE:** 

* *When you are in the lab, please turn off WireGuard when accessing the server to avoid any unwanted errors.*

## 2. Change default password (mandatory)

* Run *Terminal (or Windows PowerShell)* on your computer.

* Login into the server via Secure Shell Protocol (SSH):

  ```bash
  $ ssh <your-username>@<hostname>
  ```

  *Example: User named **tlatonf** wants to login to the host **eda.pifclub.site**, so he needs to execute the following command:*

  ```bash
  $ ssh tlatonf@eda.pifclub.site
  ```

* Below is the notification that appears when you connect via SSH to a server that you have never connected to from your device before. Enter ***yes*** to continue.

  ```bash
  The authenticity of host 'eda.pifclub.site (192.168.10.242)' can't be established.
  ECDSA key fingerprint is SHA256:
  Are you sure you want to continue connecting (yes/no/[fingerprint])?
  ```

* Enter your old password *(the password provided to you)*.

  ```bash
  You are required to change your password immediately (root enforced)
  Last failed login: Mon Jan 01 00:00:00 EDT 2024 from 192.168.10.242 on ssh:notty
  There was 1 failed login attempt since the last successful login.
  WARNING: Your password has expired.
  You must change your password now and login again!
  Changing password for user tlatonf.
  Changing password for tlatonf.
  (current) UNIX password:
  ```

* Enter and confirm the new password. If the console screen appears as shown below, it means you have successfully changed your password.

  ```bash
  New password:
  Retype new password:
  passwd: all authentication tokens updated successfully.
  Connection to eda.pifclub.site closed.
  ```

**NOTE:** 

* *At the console screen, it will not display anything as you enter your password.*

## 3. Install & configure FileZilla (skip if you don't need to transfer files with the server)

* **FileZilla** is a free and open-source FTP *(File Transfer Protocol)* software used to manage and transfer files between computers and servers.

* Download and install: https://filezilla-project.org/download.php?show_all=1.

* Configure:

  * Run *FileZilla*, it has just been installed.

  * Login with the following information:

    ```
        Host: eda.pifclub.site
    Username: <your-username>
    Password: <your-password>
        Port: 22
    ```

* The user transfers files between the server and the computer by drag-and-drop.

**NOTE:** 

* *You should install the **Windows (32-bit x86)** version to minimize unexpected errors.*

## 4. Access the server

* Run *Remote Desktop Connection*, it comes pre-installed in Windows.

* In your **Remote Desktop Connection** Options, go to the **Display** tab. Set the color depth of the remote session to **True color (24bit)**.

* Login with the following information:

  ```
      Host: eda.pifclub.site
  Username: <your-username>
  Password: <your-password>
  ```