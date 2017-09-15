CoreOs Static Routes
=========

A simple way to add Static Routes on CoreOS Machines

Requirements
------------

**None** (if you already has done the bootsrap on your coreos with python)  
If you need bootstrap your CoreOS and install python, run [coreos-bootstrap](https://galaxy.ansible.com/isca0/coreos-bootstrap/)
firstly... :smiley:

__This role will add static routes to CoreOS on file /etc/systemd/10-static.networks. If you already  
has a custom file with this same name, it will be backuped on the same directory, but this role only will deal with
routes.__


Role Variables
--------------

All you need to set routes is, the gateway and network addresses  
If you think as iproute way, the normal language syntax will be something like:  
 
10.0.0.0/8 via 172.17.12.1  
  
where 10.0.0.0/8 will be the network and 172.17.12.1 will be the gateway  
  
So the only variable you will need to set on this role is the routes variable.  
The syntax is that:  

```
  routes:
    - { network: 10.0.0.0/8, gateway: 172.17.12.1 }
```

You can also set multiple routes by dooing like this:
 
```
  routes:
    - { network: 10.0.0.0/8, gateway: 172.17.12.1 }
    - { network: 192.168.125.0/28, gateway: 10.12.13.1 }
  ...
```

You must remember to set your python interpreter path.  
if you have bootstrapped with **isca0.coreos-bootstrap**, set your inventory vars with this python path:  
[coreos:vars]  
ansible_python_interpreter="/opt/python/bin/python"  


Dependencies
------------

None

Example Playbook
----------------


```
---
  - name: "Adding Static Routes on CoreOS Machines"
    hosts: coreos
    remote_user: core
    become: true
    vars:
      routes:
        - { network: 10.0.0.0/8, gateway: 172.17.12.1 }
        - { network: 192.168.125.0/28, gateway: 10.12.13.1 }
    roles:
      - coreos-StaticRoutes
```

License
-------

BSD

Author Information
------------------

This role was create in 2017 by [Isca](https://isca.space)

