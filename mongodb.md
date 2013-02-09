1. Build Prerequisites

> Boost

http://www.boost.org/users/history/version_1_52_0.html
http://www.boost.org/doc/libs/1_52_0/more/getting_started/unix-variants.html

http://www.linuxfromscratch.org/blfs/view/svn/general/boost.html

sudo ./bootstrap.sh --prefix=PREFIX where PREFIX is the directory where you want Boost.Build to be installed
sudo ./bjam
sudo ./bjam install link=shared --prefix=PREFIX --with-date_time --with-filesystem --with-program_options --with-system --with-thread
sudo ./bjam install link=shared --prefix=PREFIX --layout=tagged --with-date_time --with-filesystem --with-program_options --with-system --with-thread
	--layout=tagged # configure to build multithreaded
PREFIX=/usr/local
Add PREFIX/bin to your PATH environment variable.

sudo ldconfig

> You'll need SCons, the gnu C++ toolchain, and glibc-devel. To get the code from github, you'll probably also want git.

sudo aptitude install git-core build-essential scons

2. Building

> Get the source code
git clone git://github.com/mongodb/mongo.git
cd mongo

> Pick a version to build (only use "master" if you're doing development work).
git tag -l # List all tagged versions

> Check out a tagged release, e.g. 2.0.4 (stable have even-numbered minor version)
git checkout r2.0.4

> Compile
scons all

> Install. Use --prefix to specify where you want to install your binaries. Defaults to /usr/local.
scons --prefix=/opt/mongo  install

3. Installing Database Source Driver

> Download the driver
http://dl.mongodb.org/dl/cxx-driver
cd mongo-cxx-driver-vX.X where X.X is te version
> Install
sudo scons install --prefix=PREFIX


http://www.mongodb.org/display/DOCS/Building+for+Linux     # build
http://docs.mongodb.org/manual/installation/               # install
http://docs.mongodb.org/manual/tutorial/getting-started/   # mongodb tutorial
http://www.mongodb.org/pages/viewpage.action?pageId=133415 # c++ tutorial
http://www.mongodb.org/pages/viewpage.action?pageId=133409 # c++ language center
http://www.mongodb.org/pages/viewpage.action?pageId=16646453 # bson library

http://www.mongodb.org/display/DOCS/Java+Tutorial          # java tutorial
http://www.mongodb.org/display/DOCS/Java+Language+Center   # java language center

4. Enable connection by remote hosts

Lastest MongoDb package on debian is bind to 127.0.0.1, this address doesn’t allow the connection by remote hosts, to change it u must set bind to 0.0.0.0 for eg

nano /etc/mongodb.conf

bind_ip = 0.0.0.0
port = 27017

service mongodb restart

Done! Remember to secure the connection by password in production mode.

http://blog.aeonmedia.eu/2011/04/mongodb-setup-config-to-connect-by-remote-hosts-debian/

http://docs.mongodb.org/manual/administration/security/#SecurityandAuthentication-Ports # security
