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

While CentOS installs, you must setup a `Root Password`.

Once the install is done, you will be promted to `Reboot`.

