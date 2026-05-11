---
title: "Personal Homelab"
layout: single
classes: wide
excerpt: "A high-availability home server environment built for media streaming, network storage, and game hosting, managed via Proxmox VE."
header:
    teaser: /assets/images/homelab-teaser.webp
author_profile: true
---

This homelab serves as my primary sandbox for network administration, system security, and backend infrastructure testing. By moving away from commercial cloud solutions, I have built a private environment that prioritizes performance and ownership.

### Infrastructure Architecture
The environment is powered by **Proxmox VE**, a Type-1 Hypervisor based on Debian. This allows me to run multiple isolated instances on a single physical node while maintaining low overhead and high portability for my services.

*   **Virtualization Strategy:** I utilize a mix of **LXC (Linux Containers)** for lightweight services like my file servers, and **Full Virtual Machines (VMs)** for environment-heavy applications like my gaming server.
*   **Networking via Tailscale:** To solve the challenge of remote access without port forwarding, I implemented a **Tailscale Mesh VPN**. This creates an encrypted overlay network (tailnet), allowing me to manage my Proxmox dashboard and access files securely from my phone or laptop even when away from my home network.

---

### Core Services & Deployments

#### 1. Media Ecosystem (Jellyfin)
Instead of relying on proprietary streaming services, I deployed **Jellyfin** for media management. This service provides a centralized library for local and remote devices, allowing for a fully self-hosted entertainment hub.

#### 2. Network Attached Storage & Web Management (Samba + File Browser)
I configured a **Samba (SMB)** server to facilitating cross-platform file sharing across my devices. 
*   **Web Interface Implementation:** To enhance accessibility, I integrated **File Browser**, a web-based file management interface. This allows for effortless uploading, downloading, and managing of files directly through a browser, eliminating the need for a dedicated SMB client on every device.

#### 3. Dedicated Game Hosting (Minecraft)
Rather than using pre-packaged installers, the **Minecraft** server was built and configured entirely from scratch within a dedicated Linux environment.
*   **Problem-Driven Implementation:** I initiated this project to solve the practical frustrations of using "free" hosting services, which often involve long login queues, limited uptime, and restricted hardware resources. By self-hosting, I eliminated these bottlenecks, ensuring 24/7 availability and immediate access for me and my friends.
*   **Manual Configuration:** I handled the end-to-end setup, from installing the Java Runtime Environment (JRE) to configuring the server properties and mods. 

---

### Hardware & Software Stack
*   **Hypervisor:** Proxmox VE 8.4.0
*   **File Management:** Samba (SMB) & File Browser UI
*   **Remote Access:** Tailscale (WireGuard-based)
*   **Operating Systems:** Ubuntu Server, Debian 12 (Bookworm)
