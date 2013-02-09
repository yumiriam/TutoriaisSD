# Install omniORB

1. Download omniORB

Grab a version of omniORB from omniORB's site an unpack it wherever you like (I like ~/src).

2. Configure, Compile and Install

	$ cd <omniORB-V.V.V> (referred to from here on as OMNIORB_TOP)
	$ ./configure
	$ make
	$ sudo make install
	
-where V.V.V is the version of omniORB that you downloaded

3. Edit omniORB Configuration

You will need to copy and edit as Root

	 cp $OMNIORB_TOP/sample.cfg /etc/omniORB.cfg

Edit the omniORB.cfg file and go to line 317 (or around there) and change the line:

	InitRef = NameService=corbaname::my.host.name
	to
	InitRef = NameService=corbaname::localhost

and make sure the line is uncommented.

4. Check for localhost resolution

Check that localhost resolves by pinging it:

	$ ping localhost

If it fails, as root, edit /etc/hosts and make sure 127.0.0.1 is set as localhost:

	127.0.0.1   localhost.localdomain   localhost
	
> Note: Alternatively, you can change line 317 in /etc/omniORB.cfg to

	InitRef = NameService=corbaname::127.0.0.1

5. Update Locations of Shared Libraries

Perform this step as root

Create a file /etc/ld.so.conf.d/omniORB.conf and add the line

	/usr/local/lib

Run /sbin/ldconfig as root.

6. omniNames Configuration

Make a directory named "logs" in the location of your choice

	$ mkdir /any/path/to/logs

You can put the log files anywhere you want to. Just make the appropriate changes to the below script file.

7. Create omniNames.sh

Create a file called omniNames.sh and put the following it:

	#!/bin/sh

	killall omniNames [omniEvents]
	rm /path/to/logs/omninames*

	omniNames -start -logdir /path/to/logs &

Now as root:

	chmod 755 omniNames.sh
	cp omniNames.sh /usr/local/bin
	
now this script (omniNames.sh) is accessible as your user from any shell.

8. Useful links

http://ossie.wireless.vt.edu/trac/wiki/InstallationGuide # this tutorial is fully based on this link
http://www.yolinux.com/TUTORIALS/CORBA.html
