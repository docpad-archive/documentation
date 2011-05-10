This guide will run you through installing Node.js on your computer.

- ### On OSX
	
	1. [Install Git](http://git-scm.com/download)

	2. [Install Xcode](http://itunes.apple.com/us/app/xcode/id422352214?mt=12&ls=1)

	3. Run the following in terminal
		
		``` bash
		sudo chown -R $USER /usr/local
		git clone https://github.com/joyent/node.git && cd node && git checkout v0.4.7 && ./configure && make && sudo make install && cd .. && rm -Rf node
		curl http://npmjs.org/install.sh | sh
		```

- ### On Apt Linux (e.g. Ubuntu)

	``` bash
	sudo chown -R $USER /usr/local
	sudo apt-get update && sudo apt-get install curl build-essential openssl libssl-dev git
	git clone https://github.com/joyent/node.git && cd node && git checkout v0.4.7 && ./configure && make && sudo make install && cd .. && rm -Rf node
	curl http://npmjs.org/install.sh | sh
	```

- ### On Yum Linux (e.g. Fedora)
	
	``` bash
	sudo chown -R $USER /usr/local
	sudo yum -y install tcsh scons gcc-c++ glibc-devel openssl-devel git
	git clone https://github.com/joyent/node.git && cd node && git checkout v0.4.7 && ./configure && make && sudo make install && cd .. && rm -Rf node
	curl http://npmjs.org/install.sh | sh
	```

- ### On Windows

	Node.js is not currently available for direct stable use on Windows; the following instructions will run you through setting up a Ubuntu (Apt Linux) Virtual Machine allowing you to run Node.js stably (albeit indirectly) on Windows.

	1. [Download Ubuntu Disk Image](http://d235whtva55mz9.cloudfront.net/ubuntu-11.04-desktop-i386.iso)

	2. [Download & Install VMWare Player](http://www.vmware.com/products/player/overview.html)

	3. Open VMWare Player and Create/Install a Virtual Machine using the Ubuntu Disk Image as the Install Media

	4. With the new Ubuntu Virtual Machine, follow the Apt Linux instructions.
