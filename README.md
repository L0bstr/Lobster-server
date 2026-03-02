# 🦞 Lobster-Server

> Personal notes on home servers and the services running on them.
> Not an expert - just someone who enjoys learning. Hopefully useful to others too.

Starting a homelab means going from *consuming* the internet to becoming **part of it** - building something real, learning
from experience, and sharing it with the world.

---

## 📖 Contents

> [!IMPORTANT]
> **"server"** - the entire host setup: machine, OS, and management software.<br>
> **"services"** - the individual programs the server hosts.<br>
> This guide is Linux-focused 🐧

**The Server**
- [x] What is a server
- [x] How to setup a server
- [ ] How to manage services

**The Services**
- [ ] What is a service?
- [ ] How to run services
- [ ] How to write services
- [ ] How to connect services

---

## 🖥️ What is a Server?

A machine designed to be **always on**. It provides a secure environment for its services and handles routing, starting, and
stopping them.

---

## ⚙️ How to Setup a Server

### 🔩 Choosing Hardware

Even an old laptop or unused PC will do.

| Component | Minimum |
|-----------|---------|
| 🧠 CPU | x86_64, 2+ cores |
| 💾 RAM | 2 GB |
| 💿 Storage | 32 GB |
| 🌐 Network | Ethernet or WiFi |

> Minimum specs depend on the OS - some are heavier than others.

---

### 🐧 Choosing an OS

**General checklist:**
- Architecture & driver support for your hardware
- Package ecosystem - your tools are available
- Stability & LTS - infrequent breaking changes
- Security - fast patches, small attack surface
- Community & docs - findable answers when things break
- Headless support - no GUI, less bloat *(optional but recommended)*

**Recommendations:**

| Distro | Description | Resources | Ease |
|--------|-------------|-----------|------|
| Ubuntu Server | Most beginner-friendly, large community, extensive docs | ![Heaviest](https://img.shields.io/badge/Heaviest-red) | ![Easiest](https://img.shields.io/badge/Easiest-green) |
| Debian | Stable, minimal, well documented. Good middle ground | ![Medium](https://img.shields.io/badge/Medium-orange) | ![Medium](https://img.shields.io/badge/Medium-orange) |
| Arch | Build from scratch, full control, best for learning | ![Lightest](https://img.shields.io/badge/Lightest-green) | ![Hardest](https://img.shields.io/badge/Hardest-red) |

> I went with Arch - already familiar with it and I want the full learning experience, suffering included.

---

### 🛠️ Configure the system

#### OpenSSH 🌐

OpenSSH allows to securely access the server shell over a network.

<details>

<summary>Setup</summary>

- Install `openssh` on the server and your main machine.
- Start the `ssh` service on the server.
```bash
# Debian/Ubuntu based distros:
sudo systemctl enable ssh
sudo systemctl start ssh

# RHEL/Arch/etc. based distros:
sudo systemctl enable sshd
sudo systemctl start sshd
```
- Try to connect to your server.
> [!NOTE]
> The server and your main machine have to be on the same network.
```bash
# On your server
ip -c a # look for "inet 192.168.x.x"

# On your main machine
ssh server-username@192.168.x.x

# exit
exit
```
- Generate an `ssh-key` on your main machine.
```bash
ssh-keygen -t ed25519 -C "my-main-machine-key" # accept the defaults
```
- Share your public key with the server so it recognizes you.
```bash
ssh-copy-id server-username@192.168.x.x
```
- Connect to the server again and configure it to be secure.
```bash
ssh server-username@192.168.x.x

sudo nano /etc/ssh/sshd_config

# Uncomment these lines:
Port 2222                    # non-default port
PermitRootLogin no           # disable to login as root
PasswordAuthentication no    # disable password login
PubkeyAuthentication yes     # enable login with ssh-key
AllowUsers server-username   # whitelist users

# Restart the ssh service:

# Debian/Ubuntu based distros:
sudo systemctl restart ssh

# RHEL/Arch/etc. based distros:
sudo systemctl restart sshd

# exit
exit
```
- Try to reconnect with your key.
```bash
ssh server-username@192.168.x.x -p 2222
```

Nice.<br>
Now only with the keys that the server know about can access and manage it remotely.

</details>