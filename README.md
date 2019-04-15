[![Build Status](https://travis-ci.org/zaxos/lvm-ansible-role.svg?branch=master)](https://travis-ci.org/zaxos/lvm-ansible-role)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-_zaxos.lvm--ansible--role-blue.svg)](https://galaxy.ansible.com/zaxos/lvm-ansible-role/)

lvm-ansible-role
================

Ansible role to create and mount single lvm volumes.

Requirements
------------
* centos/rhel 7
* ansible >= 2.5

Installation
------------
```
$ ansible-galaxy install zaxos.lvm-ansible-role
```

Example Playbook
----------------
```yaml
- hosts: servers
  vars:
    lvm_volumes:
    - vg_name: vg_data
      lv_name: lv_data
      disk: sdb
      filesystem: xfs
      mount: /mnt
            
  roles:
    - role: zaxos.lvm-ansible-role
```

Example volume
--------------
```yaml
- vg_name: vg_data  # required, volume group name #
  lv_name: lv_data  # required, logical volume name #
  disk: sdb  # required #
  filesystem: xfs  # optional, default is 'xfs' #
  filesystem_mkfs_opts: "-n ftype=1"  # optional #
  mount: /mnt  # required #
  state: present/absent  # optional, default is 'present', set to 'absent' for removal #
  lv_size: 100%VG  # optional, default is '100%VG' #
  create_partition: False  # optional, default is 'False', set to 'True' to create gpt partition before vg creation #
  mounted: True  # optional, default is 'True', set to 'False' to unmount #
  owner: "root"  # optional, default is "root" #
  group: "root"  # optional, default is "root" #
  mode: "0644"  # optional, default is "0755" #
  mount_options: defaults  # optional, default is 'defaults' #
```

Role Variables
--------------
Some variables that require review::
- `lvm_volumes`: List of volumes.
- `lvm_auto_remount`: Default value is "True". If set to "True", when the mount path of a volume is changed, the old mount path will be automatically unmounted and removed from fstab.
