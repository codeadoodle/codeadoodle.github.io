---
published: false
---


## Getting started with Ubuntu using Vagrant VVV on Windows

Vagrant is a tool for building lightweight, reproducible, and portable development environment using configuration and provisioning script such as  [Varying Vagrant Vagrants](https://github.com/Varying-Vagrant-Vagrants/VVV). Although it is focused PHP and WordPress development, VVV also automatically provision major packages such as nginx, nodejs, and git. 

There're few things to take note if you're keen to use VVV on Windows 8.1
1. VVV requires VirtualBox, thus you need to turn Hyper-V support off. Instead doing this manually, you can create new boot menu with a "No Hyper-V" entry, following tips from [Hanselman](https://www.hanselman.com/blog/SwitchEasilyBetweenVirtualBoxAndHyperVWithABCDEditBootEntryInWindows81.aspx)
	C:\>bcdedit /copy {current} /d "No Hyper-V" 
	The entry was successfully copied to {ff-23-113-824e-5c5144ea}. 
	C:\>bcdedit /set {ff-23-113-824e-5c5144ea} hypervisorlaunchtype off 
	The operation completed successfully.
2. Hold down shift on the keyboard while clicking Restart with the mouse
3. Follow VVV recommended installation step-by-step
4. Edit Windows host file: 
	`192.168.50.4 vvv.dev local.wordpress.dev local.wordpress-trunk.dev src.wordpress-develop.dev build.wordpress-develop.dev`
