---
layout: post
published: false
title: Installing Jekyll on Windows
date: "2015-08-10 00:00:00"
categories: 
  - tutorials
---


Julian Thilo has written comprehensive guide to get [Jekyll running on Windows](http://jekyll-windows.juthilo.com/). This article highlights some of the errors that you might encounter and how to resolve them. 

Windows users must have [Ruby installed](http://rubyinstaller.org/downloads/archives) and the recommended working version is [2.0.0 p576](http://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-2.0.0-p576-x64.exe) (not the latest). You will also need to install the [Ruby Development Kit](http://dl.bintray.com/oneclick/rubyinstaller/DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe), which is also available on the Ruby Installer downloads page. Without DevKit, you'll likely encounter following error:

```
ERROR:  Error installing jekyll:
The 'yajl-ruby' native gem requires installed build tools.
```

Double-click the self-extracting executable (SFX) downloaded and choose a directory (without spaces) to install the DevKit artifacts into
e.g. `C:\RubyDevKit`. Then, enable Rubies to use DevKit by running following commands:
```
cd C:\RubyDevKit
ruby dk.rb init
ruby dk.rb install
```
If you encounter 
```
Invalid configuration or no Rubies listed. Please fix 'config.yml' and rerun 'ruby dk.rb install'
```
when running `ruby dk.rb install` - check the `config.yml` and add path to your ruby installation manually, i.e. `- C:/ruby200` (include the dash), then re-run the command as following:
```
c:\RubyDevKit>ruby dk.rb install
[INFO] Installing 'C:/ruby200/lib/ruby/site_ruby/2.0.0/rubygems/defaults/operating_system.rb'
[INFO] Installing 'C:/ruby200/lib/ruby/site_ruby/devkit.rb'
```
Refer to  http://github.com/oneclick/rubyinstaller/wiki/Development-Kit for more details .

Finally, you can run `gem install jekyll`. In the event you encounter SSL error when trying to pull updates from RubyGems:


```console
ERROR:  Could not find a valid gem 'jekyll' (>= 0), here is why:
Unable to download data from https://rubygems.org/ - SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://rubygems.org/latest_specs.4.8.gz)
```
You can resolve this by downloading and updating your ruby gems into version 2.0.15 using this workaround highlighted in https://gist.github.com/luislavena/f064211759ee0f806c88:

```
D:\>gem install --local D:\rubygems-update-2.0.15.gem
update_rubygems --no-ri --no-rdoc
gem uninstall rubygems-update -x
gem install jekyll
```
Now you should be able to clone your Jekyll theme and run `jekyll serve` to build your site.