🚀 WireGuard VPN Server on Rooted Android (24/7, Low Power)
📌 Overview

This project demonstrates how I successfully built and deployed a personal WireGuard VPN server running 24/7 on a rooted Android device.

Initially, the VPN server was hosted on an Ubuntu server, but continuous uptime, power backup, and reliability became a concern. To solve this, the VPN server was migrated to a rooted Android phone, turning it into a low-power, always-on VPN appliance using Termux, WireGuard, and iptables.

The result is a stable, secure, and energy-efficient VPN server that works flawlessly for remote access to my home network and secure internet usage.

❓ Why Android as a VPN Server?

Using a rooted Android phone as a VPN server offers several practical advantages over a traditional server or PC:

✅ Always On & Reliable

Designed to run continuously

No sudden shutdowns like laptops or desktops

🔋 Built-in Battery Backup

Automatically acts as a UPS during power cuts

No external inverter or UPS required

⚡ Low Power Consumption

Consumes significantly less power than a PC or server

Ideal for 24/7 operation

📶 Flexible Connectivity

Works on Wi-Fi or mobile data

Easy to move between networks if needed

🔐 Full Control (Root Access)

Direct control over:
WireGuard interfaces
iptables NAT and firewall rules
Kernel IP forwarding
This makes Android a surprisingly powerful and cost-effective VPN host.

🧠 Architecture Overview
4
[ Client Devices ]
  (Laptop / Phone)
         |
         |  Encrypted WireGuard Tunnel
         |
[ Rooted Android Phone ]
   - Termux Linux Environment
   - WireGuard (wg0)
   - iptables NAT & Firewall
         |
      Internet

🧰 Technologies Used

WireGuard – Lightweight, secure VPN protocol
Termux – Linux environment on Android
iptables – NAT and packet forwarding
Android (Rooted)
Linux networking stack

🎯 Use Cases

Secure remote access to home network
Safe browsing on public Wi-Fi
Lightweight self-hosted VPN
Learning low-level Linux networking on Android
Always-on VPN without expensive hardware

📌 What’s Next?

In the next sections, this repository will document:

🔧 Complete installation & setup

🔑 Key generation and configuration

🔥 iptables NAT & forwarding rules

▶️ Starting & managing the VPN

🛡️ Security considerations

🧪 Troubleshooting

📈 Future improvements

⭐ If you find this project useful

Give it a star ⭐ on GitHub and feel free to fork or contribute.
