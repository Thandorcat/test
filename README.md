#  Task. Zabbix. Java Monitoring with Java

## Vagrantfile:

```ruby
Vagrant.configure("2") do |config|
  config.vm.define "zabbix" do |zabbix|
    zabbix.vm.box = "zabbix"
    zabbix.vm.hostname = 'zabbix'
    zabbix.vm.box_url = "sbeliakou-vagrant-centos-7.3-x86_64-minimal.box"
    zabbix.vm.network :forwarded_port, guest: 80, host: 8080, auto_correct: true
    zabbix.vm.network :private_network, ip: "192.168.56.101"
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
    agent.vm.network :private_network, ip: "192.168.56.111"
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
# 1. Configure Zabbix to examine Java parameters via Java Gateway

<img src="pictures/Screenshot from 2017-07-25 14-13-27.png">
Connecting via terminal


<img src="pictures/Screenshot from 2017-07-25 15-54-31.png">
Setting host


<img src="pictures/Screenshot from 2017-07-25 15-54-36.png">
Connected

Custom items:
<img src="pictures/Screenshot from 2017-07-25 15-54-50.png">

<img src="pictures/Screenshot from 2017-07-25 15-55-00.png">

<img src="pictures/Screenshot from 2017-07-25 16-00-56.png">

# 2. Configure triggers to alert once these parameters changed

<img src="pictures/Screenshot from 2017-07-25 16-09-56.png">
Creating trigger


<img src="pictures/Screenshot from 2017-07-25 16-11-18.png"
Warning after creating CPU load

## Create User group “Project Owners” 

<img src="pictures/Screenshot from 2017-07-24 13-44-24.png">

## Create User (example “Siarhei Beliakou”), assign user to “Project Owners”, set email

<img src="pictures/Screenshot from 2017-07-24 13-45-37.png">

<img src="pictures/Screenshot from 2017-07-24 13-47-28.png">


## Add 2nd VM to zabbix: create Host group (“Project Hosts”), create Host in this group, enable ZABBIX Agent monitoring

<img src="pictures/Screenshot from 2017-07-24 14-33-09.png">

<img src="pictures/Screenshot from 2017-07-24 14-38-20.png">

## Assign to this host template of Linux 

<img src="pictures/Screenshot from 2017-07-24 14-39-38.png">

<img src="pictures/Screenshot from 2017-07-24 14-42-48.png">

## Create custom checks (CPU Load, Memory load, Free space on file systems, Network load)

<img src="pictures/Screenshot from 2017-07-24 17-29-29.png">

<img src="pictures/Screenshot from 2017-07-24 17-31-57.png">

<img src="pictures/Screenshot from 2017-07-24 17-36-53.png">

<img src="pictures/Screenshot from 2017-07-24 18-39-45.png">

## Create trigger with Severity HIGH, check if it works (Problem/Recovery)

<img src="pictures/Screenshot from 2017-07-24 18-00-25.png">

<img src="pictures/Screenshot from 2017-07-24 15-33-49.png">

<img src="pictures/Screenshot from 2017-07-24 18-04-45.png">

<img src="pictures/Screenshot from 2017-07-24 18-04-45.png">

## Create Action to inform “Project Owners” if HIGH triggers happen

<img src="pictures/Screenshot from 2017-07-24 15-56-50.png">

<img src="pictures/Screenshot from 2017-07-24 15-56-04.png">

<img src="pictures/Screenshot from 2017-07-24 16-17-05.png">

<img src="pictures/Screenshot from 2017-07-24 18-26-38.png">

# 3. Task 2:

## Configure “Network discovery” so that, 2nd VM will be joined to Zabbix (group “Project Hosts”, Template “Template OS Linux”)

<img src="pictures/Screenshot from 2017-07-24 16-32-07.png">

<img src="pictures/Screenshot from 2017-07-24 16-48-05.png">

<img src="pictures/Screenshot from 2017-07-24 16-49-41.png">

<img src="pictures/Screenshot from 2017-07-24 16-51-36.png">

# 4. Task 3:

## Use zabbix_sender to send data to server manually (use zabbix_sender with key –vv for maximal verbosity).

<img src="pictures/Screenshot from 2017-07-24 18-59-26.png">

<img src="pictures/Screenshot from 2017-07-24 18-59-21.png">

## Use zabbix_get as data receiver.

<img src="pictures/Screenshot from 2017-07-24 19-15-23.png">

<img src="pictures/Screenshot from 2017-07-24 19-16-14.png">

<img src="pictures/Screenshot from 2017-07-24 19-16-06.png">
