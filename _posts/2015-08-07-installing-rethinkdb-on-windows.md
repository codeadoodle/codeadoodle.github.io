---
layout: post
published: false
title: Installing RethinkDB on Windows
date: "2015-07-08 10:30:00"
categories: 
  - tutorials
---


### Install RethinkDB
Ensure you have setup and start Ubuntu VM before following RethinkDB [Installation Script](http://www.rethinkdb.com/docs/install/ubuntu/):  
- source /etc/lsb-release && echo "deb http://download.rethinkdb.com/apt $DISTRIB_CODENAME main" | sudo tee /etc/apt/sources.list.d/rethinkdb.list
- wget -qO- http://download.rethinkdb.com/apt/pubkey.gpg | sudo apt-key add -
- sudo apt-get update
- sudo apt-get install rethinkdb

### Start RethinkDB at system startup
You’ll need to add a config file to /etc/rethinkdb/instances.d/ to automatically run RethinkDB on system startup.

- sudo cp /etc/rethinkdb/default.conf.sample /etc/rethinkdb/instances.d/instance1.conf
- sudo vim /etc/rethinkdb/instances.d/instance1.conf
- sudo /etc/init.d/rethinkdb restart

### Vim Editing Tips
Quick Tips on [vim editing](http://www.howtogeek.com/102468/a-beginners-guide-to-editing-text-files-with-vi/)
- Press `i` to enter insert mode
- Press `esc` to enter command mode
- Type `:wq` to save and quit vim editing

