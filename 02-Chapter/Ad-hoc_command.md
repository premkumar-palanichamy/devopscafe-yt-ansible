# Ad-Hoc commands

In this chapter, you will learn how to manage static inventory in Ansible and will explore few Ansible inbuilt modules. We shall also get our hands dirty by running some Anisble Ad-Hoc commands

<img src ="https://opensourcegeeks.net/wp-content/uploads/2019/01/Ansible-Ad-Hoc-Commands.jpg" align="center" height=300 width=1000>



## Basic Inventory file

We will see what is Inventories in more details in the upcoming chapter, but for now remember, Ansible uses an inventory file to communicate with your servers.

Inventories = List of servers

|| The default location for Ansible inventory file => `/etc/ansible/hosts`

By default ansible communicates to its nodes via ssh port 22, in case if you are using any customport for ssh then do mention this one explicity as ansible wont get this value by default

Edit the inventory file and add you server details

```
vi /etc/ansible/hosts

[web]
192.0.1.0

[db]
192.0.2.0 2222
```

## Running Ad-Hoc commands

Once the entire setup is done, you can do your first dry ad-hoc run by refering one simple inbuilt module of ansible

```
$ ansible all --list hosts

Note: if you are using custom name and location for the hostfile/inventory file then use "-i" to refer the file

$ ansible all -i host.ini --list hosts

$ ansible web -m ping

$ ansible db -a "free -m" -u prem
```

By default, ansible will go with passwordless login incase of using username and password, one have to mention it explicitly.

### Security tip

> Even though you can use the root user in Ansible to run Ad-Hoc commands and
playbooks, it’s definitely not recommended and is not considered best practice due
to the security risks that can arise by allowing root user ssh access.

So it is highly recommended to have a dedicated user for anisble user with sudo privileges

```
* Create user

[root@ansible-server ~]# useradd -m ansible

* Grant sudo privileges without password

[root@ansible-server  ~]# echo "ansible ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

* Login with new user and generate a ssh-key pair

[ansible@ansible-server ~]$ ssh-keygen

* copy the key on all the node host

[ansible@ansible-server ~]$ ssh-copy-id ansible-worker-1
```

### Additional inventory tip

* all --> refers to all the host in the inventory
* host group --> grouping host which shares the same role
* subgroup --> grouping host which shares the same role and same scope
* ungrouped --> the orphan hosts