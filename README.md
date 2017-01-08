Role Name
=========
ansible-rabbitmq 
the role install rabbitmq or rabbitmq cluster

Requirements
------------
ansible > 1.8

Role Variables
--------------
```
# defaults file for ansible-rabbitmq
rabbitmq_cluster: true
firewall_config_enabled: false
#package location
#download erlang_rpm from https://github.com/rabbitmq/erlang-rpm/releases
#download rabbitmq_rpm from https://www.rabbitmq.com/install-rpm.html
erlang_rpm: /rabbitmq/rpm/erlang-19.2.0-1.el6.x86_64.rpm
rabbitmq_rpm: /rabbitmq/rpm/rabbitmq-server-3.6.6-1.el6.noarch.rpm

#rabbitmq plugins to install
rabbitmq_plugins:
  - rabbitmq_management
  - rabbitmq_shovel
  - rabbitmq_shovel_management

# firewall ports
rabbitmq_ports:
  - 5671
  - 5672
  - 15672
  - 4369
  - 25672

#rabbitmq users
rabbitmq_users:  #define admin user to create in order to login to WebUI
  - name: 'admin'
    password: 'rabbitmqadmin'
    vhost: '/'
    configure_priv: '.*'
    read_priv: '.*'
    write_priv: '.*'
    tags: 'administrator'  #define comma separated list of tags to assign to user....management,policymaker,monitoring,administrator...required for management plugin. https://www.rabbitmq.com/management.html

#the cookie
rabbitmq_erlang_cookie: LVYQXSYSINTEXAHGHIHU
rabbitmq_erlang_cookie_file: /var/lib/rabbitmq/.erlang.cookie
```

Dependencies
------------
centos6&7

rhel6&7

Example Playbook
----------------
```
---
- hosts: all
  remote_user: root
  roles:
  - { role: firxiao.ansible-rabbitmq, when: "ansible_os_family == 'RedHat'" }
```

License
-------

BSD

Author Information
------------------
Firxiao
