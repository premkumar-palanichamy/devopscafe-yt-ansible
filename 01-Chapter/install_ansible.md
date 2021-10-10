# Getting Started with Ansible

Normal developers and sys. admin manage servers by logging into them via SSH, making changes, and logging off. Some of these changes would be documented, some would not. If an admin needed to make the same change to many servers (for example, changing one value in a config file), the admin would manually log into each server and repeatedly make this change.

<img src="https://miro.medium.com/max/900/0*puhBBlsbU0La3Yqm.jpg" align="center" height=250 width=1000>

### Other tools:
- CFEngine
- Puppet
- Chef

## Can Ansible be installed in all the OS system natively?

No, it is not possible to install ansible directly on windows but you can effectively manage them.

B'cuz ansible started as a Linux-based tool, and it uses the Secure Shell (SSH) protocol to communicate with the machines it manages. As most Linux hosts already have SSH installed, Ansible implementation in these environments is fairly straightforward.

But SSH is not installed on a Windows server in the same way, and it isn't available for production environments yet. Instead, Ansible uses PowerShell to push out and implement changes to Windows host machines. To use Ansible for Windows configuration management, run PowerShell version 3.0 or higher, as well as the .NET framework version 4.0 or higher, on managed systems.

So in short, in order to run ansible on Windows host natively, the admin must set it up under the Windows Subsystem for Linux (WSL).

## Installing Ansible

Ansible’s only real dependency is __*Python*__. Once Python is installed, the simplest way to get Ansible
running is to use pip, a simple package manager for Python.

> For MacOs:


```
1. Install Homebrew (brew install ansible).
2. Install Python 2.7.x (brew install python).
3. Install Ansible (sudo pip install ansible).
```

> For Linux:

```
There could be high chances for having Ansible’s dependencies installed already, if not follow below steps based on the OS specification.

Fedora/RHEL/CentOS:

$ sudo pip install ansible

Note: Using pip allows you to upgrade Ansible with pip install --upgrade ansible.

$ sudo yum install epel-release

$ sudo yum install -y ansible

Ubuntu/Debian:

$ sudo apt update -y

$ sudo apt install software-properties-common

$ sudo apt-add-repository ppa:ansible/ansible

$ sudo apt update

$ sudo apt install ansible
```

> For Windows:

```
There is no straight forward step for installation, some additional steps are needed.

1) Running ansible on Linux virtual machine on top of Virtual Box

2) Using WSL configuration
```

### Post-Installation Check:

Once Ansible is installed, make sure it’s working properly by entering ansible --version on the
command line.

```
$ ansible --version
```

### Create a basic Inventory file:

Inventory file - Used to commincate with the servers (like a index to the systems). Inventory file matches anything like IP addresses to domain names.

Default inventory file location:
``` 
/etc/ansible/hosts
```

### Run a Ad-hoc command:

$ ansible testservers -m ping

$ ansible -i hosts all -m ping -u prem
