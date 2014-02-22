vagrant-robotics-boilerplate
============================

Instant robotics middleware development environment using Vagrant.

Install
-------

Vagrant works on Windows, OSX, and Linux.

1. Download & install Vagrant: http://vagrantup.com/

2. Download & install VirtualBox: https://www.virtualbox.org/

3. Download & install git and ssh client:

- on Windows msysgit is recommended (will installs both git and ssh): https://code.google.com/p/msysgit/

- on OSX you may want to install git using Homebrew ("brew install git"): http://brew.sh/

- on Linux (Ubuntu) it is as simple as "sudo apt-get install git"

Checkout the repository
-----------------------

Open the terminal window (on Windows use "Git Bash") and type:

~~~bash
$ git clone git://github.com/devrt/vagrant-robotics-boilerplate.git
~~~

Vagrant UP!
-----------

Now, we run vagrant:

~~~bash
$ cd vagrant-robotics-boilderplate
$ vagrant up
~~~

When you first run vagrant, it may take long time to actually startup.
What happen behind is:

1. Download the base ubuntu image for virtualbox (called "box").

2. Install robotics related middleware (this process is called "provision").

3. Configure the virtualbox to enable 3D acceleration (for better simulation experience).

> At the very first time when you run vagrant, virtualbox opened in separate window ask you for some decisions and provisioning process will be stopped. Select your preference to let it continue.

At the second time you run vagrant, all the above process will be skiped.

These are the commands you may want to remember:

`vagrant up` start the vagrant.

`vagrant halt` stop the vagrant.

`vagrant destroy` delete the virtualbox image.


Software installed at the beginning
-----------------------------------

This is the list of software installed so far at the beginning:

- OpenRTM-aist: Middleware framework.
- ROS: Universe of the robot middleware.
- OpenHRP: Set of high precision simulation servers.
- OpenRAVE: Collection of motion planning algorithms.
- hrpsys-base: Command-line oriented simulation runner.
- rtshell: Command-line oriented system composer.

ROS packages can be installed additionally by "sudo apt-get [package]" command.


Example use
-----------

~~~bash
$ vagrant ssh
(login to vagrant box)
$ xterm -e openhrp-model-loader &
$ hrpsys-simulator /usr/share/hrpsys/samples/PA10/PA10simulation.xml
~~~

PA10 robot simulator will be started on separate virtualbox window.

Tips for using Vagrant
----------------------

You can always reset your environment by "vagrant destroy" command.

Keep your important files under "/vagrant" folder. This folder is connected to your host computer and not be deleted with "vagrant destroy" command.


How to contribute
-----------------

Send me a pull request.


Author
------

Yosuke Matsusaka
