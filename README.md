# Vagrant (MacOS) + Ansible + Wordpress

### This is a basic Vagrant file to setup 3 hosts:

- ansible
- mysql (mariadb)
- apache (httpd)

The Vagrant is installed in Mac OS and it's running with CentOS7

You need manually to copy the ssh keys from ansible host to apache and mysql
(I know I can automate this, but for now, this is manual).

### Tech

* [Vagrant] - Up the VMs with VirtualBox!
* [Ansible] - Provisioning Everything! Oh Yeah!
* [MariaDB] - Database! And that's all!
* [Apache HTTPD] - WebServer

### Installation

Ok, first thing, from your Vagrant host, let's up the 3 nodes...

```sh
$ cd ansible-wordpress
$ vagrant up
# output expected:
# ... looooot of stuff.... then:
==> ansible: Machine 'ansible' has a post `vagrant up` message. This is a message
==> ansible: from the creator of the Vagrantfile, and not from Vagrant itself:
==> ansible: 
==> ansible: Provision finished. :)

==> apache: Machine 'apache' has a post `vagrant up` message. This is a message
==> apache: from the creator of the Vagrantfile, and not from Vagrant itself:
==> apache: 
==> apache: Provision finished. :)

==> mysql: Machine 'mysql' has a post `vagrant up` message. This is a message
==> mysql: from the creator of the Vagrantfile, and not from Vagrant itself:
==> mysql: 
==> mysql: Provision finished. :)
```

When this step finishes, you need to connect to ansible host and copy the ssh key to apache and mysql (password for vagrant user is vagrant)

```sh
$ vagrant ssh ansible
[vagrant@ansible ~]$ ssh-copy-id apache
...
[vagrant@ansible ~]$ ssh-copy-id mysql
```

now run the playbook:

```sh
[vagrant@ansible ~]$ ansible-playbook -i ansible/files/hosts -u vagrant ansible/provisioning.yml 
...
PLAY RECAP ****************************************************************
10.0.11.11                 : ok=7    changed=7    unreachable=0    failed=0   
10.0.11.12                 : ok=6    changed=6    unreachable=0    failed=0   
```

you can now access your host (http://localhost:8082/wordpress/) and create your site. easy, no? :)

### General Information

this is a basic install, config for vagrant, ansible, apache and mariadb. Of course you can get this, improve and do whatever changes for your need. :)


[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [Ansible]: <http://ansible.com>
   [Vagrant]: <http://vagrantup.com>
   [MariaDB]: <http://mariadb.com>
   [Apache HTTPD]: <https://httpd.apache.org>
