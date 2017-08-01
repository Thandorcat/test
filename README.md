## Vagrantfile:

```ruby

Vagrant.configure("2") do |config|

  config.vm.box = "sbeliakou/centos-7.3-x86_64-minimal"
  config.vm.network "forwarded_port", guest: 8080, host: 8080

end

```
#  Lab Work Task. Tomcat AS Provisioning

## 1. Install Ansible v2.3.1 with python pip. Report details where ansible has been installed.


<img src="pictures/Screenshot from 2017-08-01 12-19-43.png">

## 2. Create folder ~/cm/ansible/day-1. All working files are supposed to be placed right there.

## 3. Spin up clear CentOS6 VM using vagrant (“vagrant init sbeliakou/centos-7.3-minimal”). Verify connectivity to the host using ssh keys (user: vagrant)

<img src="pictures/Screenshot from 2017-08-01 12-40-21.png">

## 4. Create ansible inventory file (name: inventory) with remote host connection details:
### - Remote VM hostname/ip/port
### - Remote ssh login username
### - Connection type
```
[all]
127.0.0.1 ansible_ssh_port=2222 ansible_ssh_user=vagrant ansible_connection=ssh
ansible_ssh_private_key_file=.vagrant/machines/default/virtualbox/private_key
```

## 5. Test ansible connectivity to the VM with ad-hoc command: 

<img src="pictures/Screenshot from 2017-08-01 13-25-47.png">

### Find out host details:

### - Number of CPUs

<img src="pictures/Screenshot from 2017-08-01 13-35-52.png">

### - Host name

<img src="pictures/Screenshot from 2017-08-01 13-38-20.png">

### - Host IP(s)

<img src="pictures/Screenshot from 2017-08-01 13-55-36.png">

### - Total RAM

<img src="pictures/Screenshot from 2017-08-01 14-00-11.png">

