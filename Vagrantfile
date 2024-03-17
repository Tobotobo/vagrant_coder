# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/alpine319"
  config.vm.box_version = "4.3.12"

  config.vm.synced_folder ".", "/vagrant"

  # config.vm.network "private_network", type: "dhcp"
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provider "virtualbox" do |vb|
    vb.cpus = "2"
    vb.memory = "4096"
  end

  # Alpine はサポート対象外
  # config.vm.provision "docker"

  config.vm.provision "shell", inline: <<-SHELL
    # タイムゾーンの設定
    apk --no-cache add tzdata
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
    apk del tzdata

    # Docker 関連のインストール
    apk add --no-cache docker docker-cli-compose
    addgroup vagrant docker
    rc-update add docker default
    service docker start
  SHELL

end
