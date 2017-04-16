Role Name
=========

An [Ansible] role to install/configure [KeepAliveD]

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-keepalived
config_keepalived: false
keepalived_router_info:
  - name: vrrp_1
    check_script:
      - name: chk_haproxy
        script: 'killall -0 haproxy'
        interval: 2
        weight: 2
    # Define inventory_hostname of node to be considered Master
    master_node: node0
    router_id: 50
    router_pri_backup: 100
    router_pri_master: 150
    vip_int: '{{ ansible_eth1.device }}'
    vip_addresses:
      - 192.168.202.100
      - 192.168.202.101
  - name: vrrp_2
    check_script:
      - name: chk_nginx
        script: 'pidof nginx'
        interval: 2
        weight: 2
    master_node: node1
    router_id: 51
    router_pri_backup: 100
    router_pri_master: 150
    vip_int: '{{ ansible_eth1.device }}'
    vip_addresses:
      - 192.168.202.102
```

Dependencies
------------

None...unless using GlusterFS


Example Playbook
----------------

```
---
- hosts: load_balancers
  become: true
  vars:
  roles:
    - role: ansible-keepalived
  tasks:
```

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com

[Ansible]: <https://www.ansible.com>
[KeepAliveD]: <http://www.keepalived.org/>
