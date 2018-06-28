# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "centos7.2"
  config.ssh.insert_key = false

  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.56.88"
  # config.vm.network "public_network"
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end
  #
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  config.vm.provision "shell", inline: <<-SHELL
    yum update
    yum install -y zsh gcc git openssl-dev lua-devel ncurses-devel
    yum remove -y ruby vim-enhanced
    cd /usr/local/src/
    git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
    echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
    git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
    rbenv install 2.3.4
    rbenv global 2.3.4
    git clone https://github.com/vim/vim.git
    cd vim/
    git pull
    make distclean
    ./configure --prefix=/usr/local --with-features=huge --enable-multibyte --enable-rubyinterp --enable-luainterp --enable-cscope --enable-fail-if-missing --with-ruby-command=/home/vagrant/.rbenv/shims/ruby
    make
    make install
  SHELL
end
