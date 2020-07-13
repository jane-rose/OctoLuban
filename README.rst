OctoLuban
======





Where to get it?
----------------

Download the latest stable build via this button:



How to use it?
--------------

#. Unzip the image and install it to an sd card `like any other Raspberry Pi image <https://www.raspberrypi.org/documentation/installation/installing-images/README.md>`_
#. Configure your WiFi by editing ``octopi-wpa-supplicant.txt`` on the root of the flashed card when using it like a thumb drive
#. Boot the Pi from the card
#. Log into your Pi via SSH (it is located at ``octopi.local`` `if your computer supports bonjour <https://learn.adafruit.com/bonjour-zeroconf-networking-for-windows-and-linux/overview>`_ or the IP address assigned by your router), default username is "pi", default password is "raspberry". Run ``sudo raspi-config``. Once that is open:

   a. Change the password via "Change User Password"
   b. Optionally: Change the configured timezone via "Localization Options" > "Timezone".
   c. Optionally: Change the hostname via "Network Options" > "Hostname". Your OctoPi instance will then no longer be reachable under ``octopi.local`` but rather the hostname you chose postfixed with ``.local``, so keep that in mind.

   You can navigate in the menus using the arrow keys and Enter. To switch to selecting the buttons at the bottom use Tab.

   You do not need to expand the filesystem, current versions of OctoPi do this automatically.


Features
--------

* `mjpg-streamer with RaspiCam support <https://github.com/jacksonliam/mjpg-streamer>`_ for live viewing of prints and timelapse video creation.

Developing
----------

Requirements
~~~~~~~~~~~~

#. `qemu-arm-static <http://packages.debian.org/sid/qemu-user-static>`_
#. `CustomPiOS <https://github.com/guysoft/CustomPiOS>`_
#. Downloaded `Raspbian <http://www.raspbian.org/>`_ image.
#. root privileges for chroot
#. Bash
#. git
#. sudo (the script itself calls it, running as root without sudo won't work)

Build OctoLuban From within OctoPi / Raspbian / Debian / Ubuntu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

OctoLuban can be built from Debian, Ubuntu, Raspbian, or even OctoPi.
Build requires about 2.5 GB of free space available.
You can build it by issuing the following commands::

    sudo apt-get install gawk util-linux qemu-user-static git p7zip-full python3

    git clone https://github.com/jiantaolovebingbing/OctoLuban.git
    cd OctoLuban/dependencies
    git clone https://github.com/guysoft/CustomPiOS.git
    git clone https://github.com/guysoft/OctoPi.git
    cd ../src/image
    wget -c --trust-server-names 'https://downloads.raspberrypi.org/raspbian_lite_latest'
    cd ..
    ../dependencies/CustomPiOS/src/update-custompios-paths
    sudo modprobe loop
    sudo bash -x ./build_dist

Also, you can just download Luban using npm. If you're going to use sudo or root to install Luban, you need to specify the `--unsafe-perm` option to run npm as the root account.
install npm::
    cd /usr/local/lib/
    sudo mkdir nodejs
    wget https://nodejs.org/dist/v10.16.0/node-v10.16.0-linux-armv7l.tar.xz
    sudo tar -xJvf node-v10.16.0-linux-armv7l.tar.xz -C /usr/local/lib/nodejs
    sudo ln -s /usr/local/lib/nodejs/node-v10.16.0-linux-armv7l/bin/node /usr/bin/node
    sudo ln -s /usr/local/lib/nodejs/node-v10.16.0-linux-armv7l/bin/npm /usr/bin/npm
    npm -v

install Luban::
    sudo npm install --unsafe-perm -g snapmaker-luban
    luban
