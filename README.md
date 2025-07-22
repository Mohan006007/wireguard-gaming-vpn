# 🔰 WireGuard VPN for PUBG Global (Low-Latency from India)

This project provides a ready-to-use, secure, and lightweight WireGuard VPN server setup designed for connecting to **PUBG Global** servers from India with improved latency. It includes setup scripts, configuration examples, and step-by-step deployment instructions on an Ubuntu-based cloud server (e.g., AWS EC2 in **Singapore region** 🇸🇬).

> ✅ Zero-bloat  
> ✅ Fast setup  
> ✅ Low-latency routing via Singapore  
> ✅ Mobile-optimized

---

## 🌐 Use Case

If you're in India and want to connect to **PUBG Global servers** with lower ping and minimal packet loss, this VPN provides a secure tunnel to an overseas relay hosted in **Singapore**, offering stable and responsive gameplay.

---

## ⚙️ Server Requirements

- Ubuntu 20.04 or 22.04 (tested)
- Root or sudo access
- Public IP (AWS EC2 🇸🇬 recommended)
- Open UDP port (default: `51820`)
- Knowledge of basic Linux commands

---

## 🛠️ Setup Instructions

### 1. Update and Install WireGuard

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install wireguard netfilter-persistent -y
