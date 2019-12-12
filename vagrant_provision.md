# Vagrant

## 動作環境
---
>  MacOS 10.12.6

> ### Virtual Box
```
jpnotready:~ notready$ VBoxManage -v
6.0.8r130520
```
> ### vagrant
```
jpnotready:~ notready$ vagrant --version
Vagrant 2.2.6
```

## 構築
---

```
# dir作成
mkdir path/to/vagrant.d

# Boxを指定してVagrantファイル作成
cd path/to/vagrant.d
vagrant init centos/7

# vmを起動する
vagrant up

# vmにsshログインする
vagrant ssh
```