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

## 6. Develop a playbook (name: tomcat_provision.yml) which is supposed to run against any host (specified in inventory)
### Use following modules (at least):
#### - copy
#### - file
#### - get_url
#### - group
#### - service
#### - shell
#### - unarchive
#### - user
#### - yum
### Define play variables (at least):
#### - tomcat_version
#### - java_version
### Every task should have a name section with details of task purpose.
### Examples:
#### - name: Ensure user student exists
#### - name: Fetch artifact form the Shared repository
### Ensure tomcat is up and running properly with module “shell” (at least 3 different checks).
### Second (and other) run(s) of playbook shouldn’t interrupt the service – one of checks should show tomcat uptime.

```yaml
- name: Tomcat provision
  hosts: all
  become: true
  become_user: root

  vars:
    tomcat_version: 8.0.35
    java_version: 1.8
  tasks:

  - name: Install Java {{java_version}}
    yum:
      name: java-devel

  - name: Creating tomcat group
    group:
      name: tomcat_as_group

  - name: Creating tomcat user
    user:
      name: tomcat_as
      group: tomcat_as_group

  - name: Download Tomcat
    get_url:
      url: http://archive.apache.org/dist/tomcat/tomcat-8/v{{tomcat_version}}/bin/apache-tomcat-{{tomcat_version}}.tar.gz
      dest: ./
 
  - name: Unpack Tomcat
    unarchive:
      remote_src: true
      src: apache-tomcat-{{tomcat_version}}.tar.gz
      dest: ./

  - name: Creating directory
    file:
      path: /opt/tomcat/{{tomcat_version}}
      state: directory

  - name: Copy Tomcat
    shell: cp -R apache-tomcat-{{tomcat_version}}/* /opt/tomcat/{{tomcat_version}}/

  - name: Setting permitions
    file:
      recurse: true
      path: /opt/tomcat/{{tomcat_version}}/
      owner: tomcat_as
      group: tomcat_as_group

  - name: Copy Tomcat Service file
    copy:
      src: tomcat.service
      dest: /etc/systemd/system/tomcat.service

  - name: Fix Tomcat Service file
    replace:
      path: /etc/systemd/system/tomcat.service
      regexp: '{version}'
      replace: '{{tomcat_version}}'

  - name: Start Tomcat
    service:
      state: started
      enabled: true
      name: tomcat

  - name: Check via curl
    shell: if [[ $(curl -IL localhost:8080 | grep "200 OK" )  > 0 ]] ; then echo Success! ; else echo Failed! ; fi

  - name: Check via pgrep
    shell: if [[ $(pgrep java)  > 0 ]] ; then echo Success! ; else echo Failed! ; fi

  - name: Check service
    shell: if [[ $(systemctl status tomcat | grep "active (running)" )  > 0 ]] ; then echo $(systemctl status tomcat | grep active) ; else echo "Service not active" ; fi
```

