# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  config.vm.box = "hashicorp/precise64"

  config.vm.network "private_network", ip: "192.168.19.87"

  config.ssh.forward_agent = true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-shell

apt-get install python-software-properties

### 3rd party PPAs
add-apt-repository ppa:mapnik/boost
add-apt-repository ppa:ubuntu-toolchain-r/test

apt-get update

### Core dependencies
apt-get install -y git-core cmake g++ libmysqlclient-dev \
  libxml2-dev libmcrypt-dev libicu-dev openssl build-essential binutils-dev \
  libcap-dev libgd2-xpm-dev zlib1g-dev libtbb-dev libonig-dev libpcre3-dev \
  autoconf automake libtool libcurl4-openssl-dev \
  wget memcached libreadline-dev libncurses-dev libmemcached-dev libbz2-dev \
  libc-client2007e-dev php5-mcrypt php5-imagick libgoogle-perftools-dev \
  libcloog-ppl0 libelf-dev libdwarf-dev subversion \
  libmagickwand-dev libxslt1-dev ocaml-native-compilers libevent-dev \


### GCC 4.7
apt-get install -y gcc-4.7 g++-4.7
update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.7 60 \
                         --slave /usr/bin/g++ g++ /usr/bin/g++-4.7
update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.6 40 \
                         --slave /usr/bin/g++ g++ /usr/bin/g++-4.6
update-alternatives --set gcc /usr/bin/gcc-4.7

### Boost 1.49
apt-get install -y libboost1.49-dev libboost-regex1.49-dev \
  libboost-system1.49-dev libboost-program-options1.49-dev \
  libboost-filesystem1.49-dev libboost-thread1.49-dev

### HHVM Git repo
if [ ! -d /vagrant/hhvm/.git ]; then
  rm -rf /vagrant/hhvm
  sudo -u vagrant git clone --progress --recursive \
      git://github.com/facebook/hhvm.git /vagrant/hhvm
else
  echo "/vagrant/hhvm already a git repo, not checking out"
fi

  shell
end
