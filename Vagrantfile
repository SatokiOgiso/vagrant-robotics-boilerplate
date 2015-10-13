# -*- mode: ruby -*-
# vi: set ft=ruby :

# This script will install hrpsys-base and choreonoid from ppa
$script = <<SCRIPT
echo "deb mirror://mirrors.ubuntu.com/mirrors.txt trusty main restricted universe multiverse
deb mirror://mirrors.ubuntu.com/mirrors.txt trusty-updates main restricted universe multiverse
deb mirror://mirrors.ubuntu.com/mirrors.txt trusty-backports main restricted universe multiverse
deb mirror://mirrors.ubuntu.com/mirrors.txt trusty-security main restricted universe multiverse
" > /etc/apt/sources.list
apt-get update
apt-get install -y software-properties-common
add-apt-repository ppa:cassou/emacs
add-apt-repository ppa:hrg/daily
echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list
wget http://packages.ros.org/ros.key -O - | apt-key add -
apt-get update
apt-get install -y xorg mesa-utils fluxbox openrtm-aist-dev omniorb-nameserver hrpsys-base choreonoid python-pip virtualbox-guest-x11 git pkg-config g++ libomniorb4-dev uuid-dev libopencv-dev python-dev libyaml-dev supervisor
pip install watchdog
cd /tmp
pip install rtctree
cd /tmp
pip install rtshell
echo "y\ny\ny" | rtshell_post_install
echo "export MANPATH=/usr/local/share/man:$MANPATH" >> /home/vagrant/.bashrc
echo "#!/bin/sh -e
startx 2> /dev/null &
exit 0
" > /etc/rc.local
echo "xhost +" > /etc/X11/Xsession.d/99localhost
echo "export DISPLAY=:0.0" > /etc/profile.d/display.sh
echo "[program:openhrp-model-loader]
command=/usr/bin/openhrp-model-loader -ORBInitRef NameService=corbaloc:iiop:localhost:2809/NameService -ORBgiopMaxMsgSize 20971520
user=vagrant
autostart=true
autorestart=true
" > /etc/supervisor/conf.d/openhrp-model-loader.conf
supervisorctl update
startx 2> /dev/null &
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.hostname = "box"
  config.vm.box = "ubuntu/trusty64"
  #config.vm.network :private_network, ip: "192.168.50.4"
  #config.vm.network :public_network

  config.vm.provider :virtualbox do |vb|
    vb.gui = true
    
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    vb.customize ["modifyvm", :id, "--graphicscontroller", "vboxvga"]
    vb.customize ["modifyvm", :id, "--accelerate3d", "on"]
    vb.customize ["modifyvm", :id, "--vram", "128"]
    vb.customize ["modifyvm", :id, "--hwvirtex", "on"]
  end
  
  config.vm.provision "shell", inline: $script
end
