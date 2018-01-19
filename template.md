## Downloading and Installing CentOS 
### Contact
- Slack: @vcharly
- Email: emlincharly@gmail.com

### Table

1. [Downloading and First-Time Startup of CentOS](#id-link-to-section)
2. [Setting up CentOS](#id-link-to-section)

## Downloading and First-Time Startup of CentOS <a id="id-link-to-section"></a>
1. First, download the CentOS ISO. It can be found [here](https://www.centos.org/download/)

    I'm going to be using the CentOS Minimal ISO and install everything we need.

    Once the ISO is done downloading, proceed to create a new virtual machine inside VMWare
or Virtual Box using the downloaded ISO. Use the recommended settings for the allocated ram, storage, and cpu cores.
And when asked for network adapter, allow CentOS to access the Host-Only, DMZ adapter.

    Boot the CentOS vm to proceed with the installation.

2. Once booted, choose the `Install CentOS 7` option.

    Now you will be greeted with a `Welcome to CentOS 7` screen.

    Choose your prefered language and procced to the `Installation Summary` screen.

    Before the installation can begin, you must choose the installation destination. Click on `Installation Destination` and choose the virtual 
hard drive you created for the vm.

    Click `Done` and `Begin Installation`.

3. While CentOS installs, you must setup a `Root Password` and create a `New User`.

    Once the install is done, you will be promted to `Reboot`.

4. The reboot process shouldn't need any user input. But, once it has booted up, login with the new user you created while CentOS was installing.

    If you successfully logged in, Congragulations! You have installed CentOS. If you couldn't login, try login in with `localhost login: root`
and `Password: (The root password you set)`. Once you login with root, **BE SURE YOU CREATE A NEW USER**. If that didn't work, try reinstalling CentOS from the beginning.

## Setting up CentOS <a id="id-link-to-section"></a>

1. Execute `ip a` and take note of your network adapter. It should be something along the lines of `enp0s3` for Virtual Box vms and `ens33` for 
VMWare vms.

2. Type `su root` to obtain root

3. And then, `vi /etc/sysconfig/network-scripts/ifcfg-enp0s3`. (If you are using a VMWare vm, use `vi /etc/sysconfig/network-scripts/ifcfg-ens33`)

    To edit text in `vi`, you must click `i` to enter "insert mode" and once you are done editing, click `ESC` to exit insert mode, now click `SHIFT` and `:` at the same time and enter `wq`. `wq` means write to the file and quit the file. The same cam be done by doing `x` instead of `wq`. Refer to [this website](https://www.cs.colostate.edu/helpdocs/vi.html) to learn more about vi.

    You need to change the configuration from
    ``` bash
    BOOTROTO=dhcp
    ONBOOT=no
    ```
    to
    ``` bash
    BOOTROTO=static
    ONBOOT=yes
    ```
    Once that has been added, add these lines to the end of the configuration document
    ``` bash
    IPADDR=172.20.240.11
    NETMASK=255.255.255.0
    GATEWAY=172.20.240.254
    DNS1=172.20.240.23
    NM_CONTROLLED=no
    ```
    `DNS1=172.20.240.23` will make sure that DNS requests will be passed through the Ubuntu DNS.
    
4. Now to ensure that CentOS has an IP address, execute these commands (Again, if you are VMWare, your adapter is most likely ens33 or something similar).
    - `sudo ifdown enp0s3`
    - `sudo ifup enp0s3`
    - `ip a`

    Lets varify everything worked by doing `ping 8.8.8.8` and `ping wwww.google.com` and making sure both responds.
    
## Installing Apachce
Install Apachce using the following commands:
1. `sudo yum update` will ensure that the next lines will run smoothly.
2. `sudo yum install httpd`
    Next, `sudo iptables -F` needs to be run to flush the iptables.
    
    Now, you can restart the service by running `sudo systemctl start httpd.service`
    
    We want Apache to start on boot, so we can run `sudo systemctl enable httpd.service` to enable that. (At this point you can visit `172.20.240.11` from the Windows 10 machine to ensure everything is running properly.
    
## Installing the Database
Install the database using the following commands:
1. `sudo yum install mariadb-server mariadb`
2. `sudo systemctl start mariadb`
3. `sudo systemctl status mariadb` will ensure that MariaDB is installed and started.
4. `sudo mysql_secure_installation` is used to secure the database.

## Install PHP
Install PHP using the following commands:
1. `sudo yum install php php-mysql`
2. `sudo yum install nano` installs nano. Nano will be used to edit `.php` files that will be later created.
3. `sudo nano /var/www/html/info.php` will create and open a new `.php` file in that directory.
    Add `<?php phpinfo(); ?>` to the file. This will be used to display general information about PHP later on.
4. `sudo systemctl restart httpd.service` restarts the service.
    Run `sudo systemctl status httpd.service` to verify that the service is back up and running.
5. Now you can visit `172.20.240.11/info.php` from the Windows 10 machine and it will now display information about PHP that is created in step 3.
## Adding a User to the Database
1. `mysql -u root –p` to login as root

    After entering MYSQL, the terminal should look something like this:
    ```bash
    mysql>
    ```


    
