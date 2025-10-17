# 🕓 NTP - Server and Client

## 🧩 Description

This project sets up two virtual servers using **Vagrant**, **VirtualBox**, and **Ansible**.
The **server node** is configured with **Chrony**, an open-source time synchronization service, and the **client node** automatically syncs its clock with it ⏱️.

This setup is ideal for **testing** and **development environments** where consistent time synchronization between servers is required.

💡 The **client node** uses base Ubuntu tools (`timedatectl` and `timesyncd`) instead of Chrony.
This project is configured to be provisioned on **Windows (via WSL)** — though you can switch to **VMware Fusion** and use a compatible image from [Vagrant Cloud](https://app.vagrantup.com/).

---

## ⚙️ Dependencies

You’ll need the following installed on your system:

1. 🧱 **VirtualBox** (latest)
2. 📦 **Vagrant** (latest)
3. 🧠 **Ansible** (latest)
4. 💻 **Windows Subsystem for Linux (WSL)** (latest)
5. 🌀 **VMware Fusion** *(optional)*

---

## 📁 Folder Structure

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

---

## 🧱 Structure Overview

* 🧩 **Modular Ansible roles** for NTP server/client separation
* ⚙️ **Centralized configuration** in `group_vars`
* 📜 **Unified playbook** (`site.yml`) orchestrates all nodes
* 🧰 **Vagrantfile** handles provisioning and delegates configuration to Ansible

---

## 🚀 Usage

1. ▶️ **Start the environment**

   ```bash
   vagrant up
   ```

2. ⚙️ **Customize configuration**
   Modify `config.yml` or `inventory/vagrant.ini` to scale or add new environments.

3. 🧾 **Check the setup**

   * SSH into VMs:

     ```bash
     vagrant ssh ntp-server
     vagrant ssh ntp-client
     ```
   * Validate time sync:

     ```bash
     timedatectl
     sudo chronyc sources
     sudo chronyc clients
     ```

4. 🧹 **Clean up**

   ```bash
   vagrant destroy -f
   ```

---

## 🌐 Architecture Diagram (Conceptual)

```
          🌍 Internet NTP Source
                    │
                    ▼
         🖥️ ntp-server (Chrony)
          IP: 192.168.100.5
          ├── Timezone: Asia/Tbilisi
          ├── Allows subnet: 192.168.100.0/24
          └── Shares time to clients
                    │
                    ▼
         🖥️ ntp-client (Timesyncd)
          IP: 192.168.100.6
          └── Syncs from ntp-server
```

---

## 🧭 Summary

✅ **Server:** Chrony configured, subnet allowed, timezone set
✅ **Client:** Timesyncd points to server, timezone set, clock synchronized
✅ **Provisioning:** Automated end-to-end with Ansible + Vagrant
