Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.disksize.size = "20GB"
  # ネットワークの設定
  config.vm.network "private_network", ip: "192.168.31.31"
  # VirtualBoxの設定
  config.vm.provider "virtualbox" do |vm|
    vm.customize ["modifyvm", :id, "--ostype", "RedHat_64"]
    vm.name = "amoungus-automuteus"
    vm.cpus = 2
    vm.memory = 2048
  end
  # dockerのインストール
  config.vm.provision "docker"
  config.vm.provision :docker_compose, compose_version: "1.27.4"
  # シェルでゲストOSの初期設定
  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    # パッケージの更新
    sudo yum update -y
    # タイムゾーン設定
    sudo timedatectl set-timezone Asia/Tokyo
    sudo yum install -y tzdata
    # docker-composeの権限設定
    sudo chmod 777 /usr/local/bin/docker-compose-1.27.4
  SHELL
  # automuteusの同期
  config.vm.synced_folder ".", "/vagrant", type:"rsync"
end
