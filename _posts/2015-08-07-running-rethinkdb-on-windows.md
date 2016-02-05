---
layout: post
published: true
title: Running RethinkDB on Windows
date: "2015-08-07 00:00:00"
categories: 
  - tutorials
---



[RethinkDB](http://rethinkdb.com/) is an open-source NoSQL JSON database with an innovative push architecture that can be used to continuously send updated query results to applications in realtime instead of polling for changes. It supports relationships using joins, geospatial query,  as well as analytics using aggregation and map/reduce. In short, it could dramatically reduces the time and effort necessary to build scalable realtime apps.

### Install RethinkDB
Since RethinkDB requires Linux or OS X, you'll need to [setup and start Ubuntu VM](/posts/getting-started-with-ubuntu-using-vagrant-vvv-on-windows) using VirtualBox before following RethinkDB [Installation Script](http://www.rethinkdb.com/docs/install/ubuntu/) on Windows. Use WinSCP, SSH into the VM then run following commands:  

{% highlight bash %}
- source /etc/lsb-release && echo "deb http://download.rethinkdb.com/apt $DISTRIB_CODENAME main" | sudo tee /etc/apt/sources.list.d/rethinkdb.list
- wget -qO- http://download.rethinkdb.com/apt/pubkey.gpg | sudo apt-key add -
- sudo apt-get update
- sudo apt-get install rethinkdb
{% endhighlight %}

### Start RethinkDB at system startup
You’ll need to add a config file to `/etc/rethinkdb/instances.d/` to automatically run RethinkDB on system startup.  

{% highlight bash %}
- sudo cp /etc/rethinkdb/default.conf.sample /etc/rethinkdb/instances.d/instance1.conf
- sudo vim /etc/rethinkdb/instances.d/instance1.conf
{% endhighlight %}

Update RethinkDB binding with `bind=all` and optionally, give a server name, then restart the service using:

{% highlight bash %}
- sudo /etc/init.d/rethinkdb restart
{% endhighlight %}

### Vim Editing Tips
If you're using Vagrant VVV, you may need to use vim to edit since you may not have root access. Some quick reference on [vim editing](http://www.howtogeek.com/102468/a-beginners-guide-to-editing-text-files-with-vi/)

{% highlight bash %}
- Press `i` to enter insert mode
- Press `esc` to enter command mode
- Type `:wq` to save and quit vim editing
{% endhighlight %}
