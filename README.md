Objective / Background
======================

While learning Chef and Berkshelf I was bombarded with too much information and wondered what the bare minimum was, to get it up and running. For instance, when I did `berks cookbook appname` I ended up with a nice (but scary) template and did not really know what was required and what was not.
This demo is the result of my trial and error; about 18 hours of googling, destorying VMs and generally being a slow-learner.

Here is what I wanted to achieve: Provision an ubuntu VM on vagrant with nginx and mysql. In simple english, I wanted to create a virtual machine running ubuntu, install nginx and mysql automatically.

Warning
=======

This is not the standard way of creating Chef cookbooks. Check out http://www.youtube.com/watch?v=hYt0E84kYUI for the correct way.

Pre-Requisites
==============

* osx
* git
* vagrant
* Plugins for vagrant `vagrant plugin install vagrant-berkshelf` and `vagrant plugin install vagrant-omnibus`
* rbenv with ruby 1.9.3-p385 (You can also use rvm)

Description of Contents
=======================

* Berksfile - This defines the cookbooks you want. In my case I wanted nginx and mysql. Note that I have also included apt which is required to update ubuntu, instead of manually doing something like `sudo apt-get update -y`
* Gemfile - This defines the Gems (ruby apps) I want to use. I can manually do `gem install berkshelf` and do away with a Gemfile
* Vagrantfile - This defines the kind of VM I want. I am creating a VM called "ubuntu" running ubuntu-raring-64-bit, with IP set to 192.168.12.34, with 2GB RAM, with berkshelf, with omnibus (to install chef on this VM) and the items I want to install (mysql, nginx after doing an update). Note that I have some lines commented out because I am using run.list. You may remove runlist and uncomment these lines to get the same result.
* .lock files - These are to ensure we all will use the same versions of all dependencies

Run
===

* `git clone git@github.com:sajnikanth/berksdemo.git && cd berksdemo`
* `bundle install`
* `berks install` - Cookbooks get downloaded to `~/.berkshelf/`
* `vagrant up` - This is where magic happens. If you are using vagrant for the first time it will take a while to download the ubuntu "box". After VM is created it will update and install nginx, mysql.
* Open the browser on your host (osx) and hit 192.168.12.34; You should see a 404 from nginx (this means it is installed)
* `vagrant ssh` to login to your new VM to check if mysql is installed correctly
