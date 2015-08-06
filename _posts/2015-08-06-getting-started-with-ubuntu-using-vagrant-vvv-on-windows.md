---
published: true
---


## Getting started with Ubuntu using vagrant VVV on Windows

[Vagrant](https://www.vagrantup.com/) is a tool for building lightweight, reproducible, and portable development environment using configuration and provisioning script such as  [Varying Vagrant Vagrants](https://github.com/Varying-Vagrant-Vagrants/VVV). Although it is focused PHP and WordPress development, VVV also automatically provision major packages such as nginx, nodejs, and git. 

There're few things to take note if you're keen to use VVV on Windows 8.1:
1. VVV requires VirtualBox, thus you need to turn Hyper-V support off. Instead doing this manually, you can create new boot menu with a "No Hyper-V" entry using following tips by [Scott Hanselman](https://www.hanselman.com/blog/SwitchEasilyBetweenVirtualBoxAndHyperVWithABCDEditBootEntryInWindows81.aspx)
     C:\>bcdedit /copy {current} /d "No Hyper-V" 
     The entry was successfully copied to {ff-23-113-824e-5c5144ea}. 
     C:\>bcdedit /set {ff-23-113-824e-5c5144ea} hypervisorlaunchtype off 
     The operation completed successfully.
2. Hold down shift on the keyboard while clicking Windows `Restart` button
3. Follow VVV step-by-step installation guide
4. Edit Windows host file `192.168.50.4 vvv.dev local.wordpress.dev local.wordpress-trunk.dev src.wordpress-develop.dev build.wordpress-develop.dev`
5. If you want to be able to use other devices (e.g. mobile phone) to access the virtual machine, you need to configure Vagrant with `config.vm.network :public_network`. Refer to this post by [webdevstudios](http://webdevstudios.com/2015/08/04/how-to-view-a-locally-developed-website-devices/).
6. You can now use the Vagrant environment with `vagrant up` and `vagrant halt`
7. Visit [http://vvv.dev/](http://vvv.dev/) for accessing VVV default dashboard
8. You may also need to use [xip.io](http://xip.io/) to access virtual hosts from devices on your local network, like iPads, iPhones.
