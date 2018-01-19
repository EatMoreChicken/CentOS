## Downloading and Installing CentOS 
### Contact
- Slack: @vcharly
- Email: emlincharly@gmail.com

### Table

1. [Downloading and First Startup of CentOS](#id-link-to-section)

## Downloading and First Startup of CentOS
First, download the CentOS ISO. It can be found [here](https://www.centos.org/download/)

I'm going to be using the CentOS Minimal ISO and install everything we need.

Once the ISO is done downloading, proceed to create a new virtual machine inside VMWare
or Virtual Box using the downloaded ISO. Use the recommended settings for the allocated ram, storage, and cpu cores.
And when asked for network adapter, allow CentOS to access the Host-Only, DMZ adapter.

Boot the CentOS vm to proceed with the installation.

Once booted, choose the `Install CentOS 7` option.

Now you will be greeted with a `Welcome to CentOS 7` screen.

Choose your prefered language and procced to the `Installation Summary` screen.

Before the installation can begin, you must choose the installation destination. Click on `Installation Destination` and choose the virtual 
hard drive you created for the vm.

Click `Done` and `Begin Installation`.

While CentOS installs, you must setup a `Root Password` and create a `New User`.

Once the install is done, you will be promted to `Reboot`.

The reboot process shouldn't need any user input. But, once it has booted up, login with the new user you created while CentOS was installing.

If you successfully logged in, Congragulations! You have installed CentOS. If you couldn't login, try login in with `localhost login: root`
and `Password: (The root password you set)`. Once you login with root, **BE SURE YOU CREATE A NEW USER**. If that didn't work, try reinstalling CentOS from the beginning.

## Setting up CentOS

Execute `ip a` and take note of your network adapter. It should be something along the lines of `enp0s3` for Virtual Box vms and `ens33` for 
VMWare vms.

Type `su root` to obtain root

And now `vi /etc/sysconfig/network-scripts/ifcfg-enp0s3`. (If you are using a VMWare vm, use `vi /etc/sysconfig/network-scripts/ifcfg-ens33`)

To edit text in `vi`, you must click `i` to enter "insert mode" and once you are done editing, click `ESC` to exit insert mode, now click `SHIFT` and `:` at the same time and enter `wq`. `wq` means write to the file and quit the file. The same cam be done by doing `x` instead of `wq`. Refer to [this website](https://www.cs.colostate.edu/helpdocs/vi.html) to learn more about vi.

Change `BOOTROTO=dhcp` to `BOOTROTO=static` and `ONBOOT=no` to `ONBOOT=yes`

Add these lines to the end of the document
```
IPADDR=172.20.240.11
NETMASK=255.255.255.0
GATEWAY=172.20.240.254
DNS1=8.8.8.8
NM_CONTROLLED=no
```

Now execute the command `ifdown enp0s3` and then `ifup enp0s3`. (Again, if you are VMWare, your adapter is most likely ens33 or something similar.)

Lets varify everything worked by doing `ping 8.8.8.8` and `ping wwww.google.com` and making sure both responds.


