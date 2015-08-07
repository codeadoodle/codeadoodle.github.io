---
layout: post
published: true
title: Getting started with Ubuntu using Vagrant on Windows
date: "2015-08-06 00:00:00"
categories: 
  - tutorials
---



Vagrant is a tool for building lightweight, reproducible, and portable development environment using configuration and provisioning script such as  [Varying Vagrant Vagrants](https://github.com/Varying-Vagrant-Vagrants/VVV). Although it is focused PHP and WordPress development, VVV also automatically provision major packages such as nginx, nodejs, and git. 

There're few things to take note if you're keen to use VVV on Windows 8.1:

1. VVV requires VirtualBox, thus you need to turn Hyper-V support off. Instead doing this manually, you can create new boot menu with a "No Hyper-V" entry using following tips by [Scott Hanselman](https://www.hanselman.com/blog/SwitchEasilyBetweenVirtualBoxAndHyperVWithABCDEditBootEntryInWindows81.aspx)
        
         - C:\>bcdedit /copy {current} /d "No Hyper-V"
    	 - C:\>bcdedit /set {ff-23-113-824e-5c5144ea} hypervisorlaunchtype off 
2. Hold down shift on the keyboard while clicking Windows `Restart` button
3. Follow VVV step-by-step installation guide
4. Update Windows host file with 
       
        
        192.168.50.4 vvv.dev local.wordpress.dev local.wordpress-trunk.dev src.wordpress-develop.dev build.wordpress-develop.dev
        
5. If you want to be able to use other devices (e.g. mobile phone) to access the virtual machine, you need to configure Vagrant with `config.vm.network :public_network`. Refer to webdevstudios's post on [How to View a Locally Developed Website on Other Devices](http://webdevstudios.com/2015/08/04/how-to-view-a-locally-developed-website-devices/).
6. You can now use the Vagrant environment with `vagrant up` and `vagrant halt`
7. Visit http://vvv.dev/ for accessing VVV default dashboard
8. You may also need to use [xip.io](http://xip.io/) to access virtual hosts from devices on your local network, like iPads, iPhones.

### Related Resources:
- [Vagrant shell provisioning](http://www.sitepoint.com/vagrantfile-explained-setting-provisioning-shell/)
- Articles [1](http://webdevstudios.com/2015/01/14/getting-started-vagrant-vvv-local-development/),[2](https://zach-adams.com/2014/09/ultimate-wordpress-development-workflow/),[3](https://wpbeaches.com/setting-up-a-wordpress-vvv-vagrant-workflow/) on using VVV Vagrant for WordPress local development workflow with [VV](https://github.com/bradp/vv) Variable and [VVV Dashboard](https://github.com/topdown/VVV-Dashboard)
- [StackOverflow](http://stackoverflow.com/questions/138162/wildcards-in-a-windows-hosts-file ) on Setting up DNS and [Wildcard Hostname](http://www.lavinski.me/wildcard-hostnames/) on Windows


