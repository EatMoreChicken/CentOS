# Setting up CentOS with Wordpress
## Downloading and installing CentOS 

First, download the CentOS ISO. It can be found [here](https://www.centos.org/download/)

I'm going to be using the CentOS Minimal ISO and we will install everything we need.

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

