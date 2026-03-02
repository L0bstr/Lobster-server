# 🦞Lobster-server

## Thoughts
Starting my own homelab is exciting, because instead of just consuming content from the internet I can become a 
*part of it*<br>
It’s a chance to learn from experience, build something meaningful, and share my creations with the world—something I’ve 
always struggled to do.

> [!IMPORTANT]
> "server": refers to the entire host setup — the machine, OS, and management software combined.<br>
> "services": are the individual programs the server hosts.
> This guide is Linux-focused.

## What is this repo about?
The Server
- [What is a server?](#what-is-a-server)
- [How to setup a server](#how-to-setup-a-server)
- how to manage services

The services
- what is a service
- how to run services
- how to write services
- how to connect services

## What is a server?
A server is a machine designed to be always on. It provides a secure environment for its services and handles routing, starting,
and stopping them.

## How to setup a server?

### Choosing hardware
Even an old laptop, pc that you don't use anymore will do.

> **Hardware minimum**
> - CPU: anything x86_64 (depends on the OS as well)
>   - Cores: 2
> - RAM: 2GB (depends on the OS as well)
> - Storage: 32GB (depends on the OS as well)
> - Network: ethernet or wifi

### Choosing OS
> With very minimum hardware, first check:
> - architecture support - available for your CPU
> - driver support - network card, storage controller
> - RAM requirements - some distros are heavier than others

**General checklist:**
- package ecosystem - tools you need are available
- stability & LTS - long-term support, infrequent breaking changes
- security - fast patches, small attack surface
- community/docs - findable answers when things break
- headless support - no GUI, less bloat (optional but recommended)

**Recommendations**
| Distro | Description | Resource Usage | Ease of Use |
|--------|-------------|----------------|-------------|
| Ubuntu Server | Based on Debian, most beginner friendly, large community, extensive docs. Best choice if you're new to Linux. | Heavy | Easy |
| Debian | Stable, minimal, well documented. Good middle ground between ease and control. | Medium | Moderate |
| Arch | Build everything from scratch manually. Full control, steep learning curve, best for learning. | Light | Hard |
<br>
I will go with Arch, because I'm already familiar with it and I want full learning experience even through suffering.

### Base tools
- OpenSSH - allows secure remote access and management of the server from another machine.
- Ufw - Firewall that blocks or allows network traffic based on rules.
- Fail2ban - bans IPs that show malicious behavior.
- Docker - manages services in isolated containers, keeping them separate from the host and each other.
