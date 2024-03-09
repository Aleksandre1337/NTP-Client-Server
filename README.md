# NTP - Server and Client

## Description

This project sets up two virtual servers using Vagrant, VirtualBox, and Ansible. The main server node is equipped with Chrony, an open-source time synchronization server, and the client node is automatically configured to connect to it. This setup is ideal for testing and development environments where time synchronization between servers is required.

The client node will only be equipped with base ubuntu utilities, therefore, only timedatectl and timesyncd will be used for synchronization. This project was configured to be provisioned on a Windows machine via WSL. Feel free to switch to VMware Fusion and use the appropriate box from Vagrant Cloud.

## Dependencies

1. `Virtualbox (latest)`
2. `Vagrant (latest)`
3. `Ansible (latest)`
4. `Windows Subsystem for Linux (WSL) (latest)`
5. `VMware Fusion (optional)`

## Configuration variables explained

```
memory: 2048                  # ram for each vm
cpus: 2                       # cpus for each vm

nodes: 2                      # number of vms
box: generic/ubuntu2204       # vagrant box for each vm
playbook: config.yml         # playbook used to run role(s)
```
**Note:** vagrant automatically assigns VM hostnames and private IPs in the following manner:
```
ntp-server - 192.168.56.20
ntp-client - 192.168.56.21
```

## Usage

1. Create role and put it in `roles/` or the main directory.
2. Create custom playbook (e.g. `example.yml`) to test your role.
3. Change `config.yml` variables for your needs.
4. Run command `vagrant up` and wait for provisioning.

**Note:** Feel free to modify the `Vagrantfile` as per your host machine and other requirements.
