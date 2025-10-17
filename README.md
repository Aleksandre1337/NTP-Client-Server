# NTP - Server and Client

## Description

This project sets up two virtual servers using Vagrant, VirtualBox, and Ansible. The main server node is equipped with Chrony, an open-source time synchronization server, and the client node is automatically configured to connect to it. This setup is ideal for testing and development environments where time synchronization between servers is required.

The client node will only be equipped with base ubuntu utilities, therefore, only timedatectl and timesyncd will be used for synchronization. This project was configured to be provisioned on a Windows machine via WSL. Feel free to switch to VMware Fusion and use the appropriate image from Vagrant Cloud.

## Dependencies

1. `Virtualbox (latest)`
2. `Vagrant (latest)`
3. `Ansible (latest)`
4. `Windows Subsystem for Linux (WSL) (latest)`
5. `VMware Fusion (optional)`

## Folder Structure

```
.
├── Vagrantfile
├── config.yml
├── ansible.cfg
├── inventory/
│   └── vagrant.ini
├── playbooks/
│   └── site.yml
├── roles/
│   ├── common/
│   │   └── tasks/
│   │       └── main.yml
│   ├── ntp-server/
│   │   └── tasks/
│   │       └── main.yml
│   └── ntp-client/
│       └── tasks/
│           └── main.yml
```

## Structure

- Modular Ansible roles for NTP server/client
- Centralized variables in `group_vars`
- Unified `site.yml` playbook
- Vagrantfile provisions VMs and delegates config to Ansible

## Usage

1. `vagrant up` to provision and configure.
2. Edit `config.yml` or inventory as needed for scaling or new environments.
