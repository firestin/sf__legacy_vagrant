Vagrant.configure("2") do |config|
  config.vm.box = "mrlesmithjr/precise64"
  config.vm.box_version = "1574746203"

# Настраиваем VM
  config.vm.network "private_network", type: "dhcp"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  # Сценарий для установки PostgreSQL 8.4
  config.vm.provision "shell", inline: <<-SHELL
    # Добавляем репозиторий
    sudo apt-get update
    sudo apt-get install -y wget
    echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
    sudo apt-get update

    # Устанавливаем PostgreSQL 8.4
    sudo apt-get install -y postgresql-8.4 postgresql-contrib-8.4

    # Запускаем и проверяем
    sudo service postgresql start
    psql --version
  SHELL
end