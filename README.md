## Vagrantfile:

```ruby
Vagrant.configure("2") do |config|
  config.vm.define "zabbix" do |zabbix|
    zabbix.vm.box = "zabbix"
    zabbix.vm.hostname = 'zabbix'
    zabbix.vm.box_url = "sbeliakou-vagrant-centos-7.3-x86_64-minimal.box"
    zabbix.vm.network :forwarded_port, guest: 80, host: 8080
    zabbix.vm.network :private_network, ip: "192.168.56.10"
    zabbix.vm.synced_folder "share/", "/share"
    zabbix.vm.provider :virtualbox do |v|
      v.memory = "4096"
      v.name = "zabbixVM"
    end
    zabbix.vm.provision "shell", inline: <<-SHELL
    sudo su
    chmod +x /share/scripts/server.sh
    /share/scripts/server.sh
    SHELL
  end

  config.vm.define "agent" do |agent|
    agent.vm.box = "agent"
    agent.vm.hostname = 'agent'
    agent.vm.box_url = "sbeliakou-vagrant-centos-7.3-x86_64-minimal.box"
    agent.vm.network :private_network, ip: "192.168.56.11"
    agent.vm.synced_folder "share/", "/share"
    agent.vm.provider :virtualbox do |v|
      v.memory = "2048"
      v.name = "agent"
    end
    agent.vm.provision "shell", inline: <<-SHELL
    sudo su
    chmod +x /share/scripts/agent.sh
    /share/scripts/agent.sh
    SHELL
  end

end
```
#  Task. Zabbix. Items

# 1. Simple checks:

Zabbix Server WEB availability

<img src="pictures/Screenshot from 2017-07-26 13-24-32.png">

Zabbix DB is available

<img src="pictures/Screenshot from 2017-07-26 17-40-17.png">

Tomcat availability

<img src="pictures/Screenshot from 2017-07-26 13-28-00.png">

<img src="pictures/Screenshot from 2017-07-26 17-40-44.png">

Tomcat Server is available by ssh

<img src="pictures/Screenshot from 2017-07-26 17-43-33.png">

# 2. Calculated Checks:

<img src="pictures/Screenshot from 2017-07-26 15-14-19.png">

<img src="pictures/Screenshot from 2017-07-26 15-14-27.png">

CPU Load per Core (1min)

<img src="pictures/Screenshot from 2017-07-26 15-14-13.png">

CPU Load per Core (5min)

<img src="pictures/Screenshot from 2017-07-26 15-17-14.png">

CPU Load per Core (15min)

<img src="pictures/Screenshot from 2017-07-26 15-18-59.png">
