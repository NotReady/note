# Ansible #

## プロビジョニング要件 ##
---

* AmazonLinux2
    * RHEL7 / CentOS7
* PHP 5.6
* MySQL 5.7
* Phalcon 2.3
* Apache 2.4
* memcached
* 

## 手順 ##
---
* まずは同一ホスト内でテストしてみる
* pip入れるのは面倒なので、パッケージマネージャでインストールする

### ansibleインストール ###
---
```
sudo yum install -y ansible

...

[vagrant@localhost ~]$ ansible --version
ansible 2.4.2.0
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/home/vagrant/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.5 (default, Apr  9 2019, 14:30:50) [GCC 4.8.5 20150623 (Red Hat 4.8.5-36)]
```
