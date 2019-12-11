README.md

#Headless Chrome Setup Instructions for Local Selenium Development/Scraping

Mac only instructions, however if VirtualBox and Vagrant are setup these exact steps should work the same on Windows.

=

1. On your host machine, install/update Homebrew, VirtualBox, Vagrant
	https://medium.com/@JohnFoderaro/macos-sierra-vagrant-quick-start-guide-2b8b78913be3
	
	```
	/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
	brew doctor
	brew update
	brew cask install virtualbox
	brew cask install vagrant
	```

2. Create a directory for storing your VMs/boxes (unless modifying this box beyond the built-in selenium and chrome combination, using the same shared box for multiple purposes is probably ok)

	e.g. `mkdir ~/vms`

3. Clone this repo with a basic Ubuntu vagrant box that installs selenium server, a version of Chrome supporting headless

	`git clone https://github.com/Anomen/vagrant-selenium`

4. Start the box

	`vagrant up`

5. After bootup, selenium hub service should be listening on port 4444 bound to localhost (it's bound to the same port internally in the VM, this can be seen in the Vagrantfile config) 

6. If you need to sign into a specific account in Chrome for automation, obviously that can be done automatically via selenium - or you can simply launch Chrome from cli in vm with `google-chrome` command, and perform actual login to service required using credentials and remember the password. Depends on your use-case.



# vagrant-selenium
Vagrant configuration base on ubuntu/trusty64, ready to be used with Selenium.

## Introduction

Selenium allows you to automate tests in Web Browsers. To do so, you need to have selenium webdriver installed for all the browsers that you want to run your test into.

## Installation

1. Install [Vagrant](https://www.vagrantup.com)
2. Clone this git repository
3. Run the command `vagrant up`

This vagrant works for *Virtualbox*, on a 64 bits machine.

## Browser support

- Firefox (latest version)
- Google Chrome (latest version)

The script also installs the latest version of selenium server, and google chrome webdriver.

## Why a VM for Selenium?

Installing selenium server and the webdrivers are easy on a machine. However, everytime that you want to run your tests, it opens the browser on top of the other windows, preventing you from doing something else. Unless you use phantomjs, it is not possible to run Chrome or Firefox hidden, without disturbing you on your work.

Thanks to this VM, you only need to start the VM, and all your tests will be run into the VM. You can continue developping in the meanwhile!

## How does it work?

When the VM starts, it automatically runs selenium server, along with the google-chrome webdriver. **You need to wait a few minutes** before running your tests.

On your host machine, you can send the tests on this address: **localhost:4444**, just as if you installed selenium on your host machine.

## How to access the host from the guest machine?

An alias already exists for your convenience: *http://host/* will target your host machine.
