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


🔧 Installation & Setup (Clean & Reproducible)

This section documents the exact, minimal, and reliable steps to set up a WireGuard VPN server on a rooted Android device using Termux.

📋 Requirements
Hardware

Rooted Android phone (dedicated / always-on recommended)

Stable internet connection (Wi-Fi or mobile data)

Software

Android 10+ (tested on Android 11+)

Termux

Root access (su or tsu)

📦 Step 1: Prepare Termux Environment

Update packages and install required tools:

pkg update && pkg upgrade -y
pkg install wireguard-tools iproute2 nano -y


Verify WireGuard installation:

wg --version

🔑 Step 2: Gain Root Access & Fix PATH

WireGuard and iptables require root access on Android.

Enter root shell:

su


Ensure Termux binaries are accessible:

export PATH=/data/data/com.termux/files/usr/bin:/system/bin:$PATH


(Optional but recommended: add this to .bashrc)

🔐 Step 3: Generate WireGuard Keys

Create a secure directory for WireGuard:

mkdir -p /data/data/com.termux/files/usr/etc/wireguard
cd /data/data/com.termux/files/usr/etc/wireguard
chmod 700 .


Generate server and client keys:

wg genkey | tee server_private.key | wg pubkey > server_public.key
wg genkey | tee client_private.key | wg pubkey > client_public.key


✔️ No passwords are used — authentication is purely key-based.

⚙️ Step 4: Create Server Configuration (wg0.conf)

Create the WireGuard interface configuration:

nano wg0.conf


Example server config:

[Interface]
Address = 10.0.0.1/24
ListenPort = 51820
PrivateKey = <SERVER_PRIVATE_KEY>
SaveConfig = true

PostUp   = iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE
PostDown = iptables -t nat -D POSTROUTING -o wlan0 -j MASQUERADE


📌 Replace:

<SERVER_PRIVATE_KEY> with contents of server_private.key

wlan0 with the correct outbound interface (wlan0, rmnet_data0, etc.)

👤 Step 5: Add Client Peer

Append to wg0.conf:

[Peer]
PublicKey = <CLIENT_PUBLIC_KEY>
AllowedIPs = 10.0.0.2/32

🌐 Step 6: Enable IP Forwarding (MANDATORY)

Enable IPv4 forwarding at runtime:

sysctl -w net.ipv4.ip_forward=1


Verify:

cat /proc/sys/net/ipv4/ip_forward


Output should be:

1

▶️ Step 7: Start WireGuard VPN

Bring up the VPN interface:

wg-quick up wg0


Check status:

wg
ip a show wg0

🧪 Verification Checklist

✔ Interface created (wg0)
✔ Handshake visible in wg
✔ Client can ping 10.0.0.1
✔ Internet access works through VPN

🛡️ Security Notes

WireGuard uses modern cryptography by default

No passwords or usernames

Non-default port recommended

iptables NAT tightly scoped

Keys can be rotated anytime

🧠 Lessons Learned

Android is extremely stable for long-running services

Root access unlocks full Linux networking

Battery = built-in UPS

WireGuard performs exceptionally well on mobile hardware

Termux makes Android a legitimate Linux host

🔮 Future Improvements

Auto-start VPN on boot

Watchdog script to reapply iptables

DNS-based ad blocking

Monitoring & alerting

IPv6 support
