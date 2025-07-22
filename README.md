# 🌐 WireGuard VPN - Low Latency PUBG Global from India 🇮🇳 → 🇸🇬

A blazing-fast, lightweight, and secure VPN using **WireGuard**, optimized to connect **PUBG Global** from **India** with **low latency** by routing through an **AWS EC2 server in Singapore**.

## 🚀 Why This Project?

Many Indian users face high ping and server mismatch issues while playing PUBG Global. This open-source VPN setup:

- Connects you securely to a **Singapore region AWS server**
- Routes game traffic directly — reducing **latency** and **packet loss**
- Works flawlessly with the **WireGuard mobile app**
- Can be deployed on **AWS Free Tier (0 cost)**

---

## ☁️ Host It Yourself (AWS Free Tier)

This setup runs on a **t2.micro** instance (1 vCPU, 1GB RAM), eligible under AWS Free Tier for **6 months**.

### ✅ Requirements:
- AWS account: [https://aws.amazon.com/free](https://aws.amazon.com/free)
- Launch Ubuntu 20.04 or 22.04 EC2 instance in `ap-southeast-1` (Singapore)
- Allow **UDP 51820** in the EC2 Security Group
- SSH access to your instance

### 🌍 Suggested Region:
- **Singapore (`ap-southeast-1`)** — best for Indian PUBG Global players

---

## ⚙️ Server Setup Instructions

### SSH into your EC2 server

```bash
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

## 🛠️ Setup Instructions

### 1. Update and Install WireGuard

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install wireguard netfilter-persistent -y
```
### 2. Create Server Keys
```bash
wg genkey | tee /etc/wireguard/server_private.key | wg pubkey > /etc/wireguard/server_public.key
chmod 600 /etc/wireguard/server_private.key /etc/wireguard/server_public.key
```
### 3. Configure the VPN (wg0.conf)
### Create /etc/wireguard/wg0.conf:
```bash
[Interface]
Address = 10.0.0.1/24
ListenPort = 51820
PrivateKey = <SERVER_PRIVATE_KEY>
SaveConfig = true

[Peer]
PublicKey = <MOBILE_PUBLIC_KEY>
AllowedIPs = 10.0.0.2/32
```
Replace <SERVER_PRIVATE_KEY> and <MOBILE_PUBLIC_KEY> accordingly.
### 4. Enable IP Forwarding
```bash
echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
sysctl -p
```
### 5. Set up firewall/NAT
```bash
sudo iptables -t nat -A POSTROUTING -o enX0 -j MASQUERADE
sudo apt install netfilter-persistent -y
sudo netfilter-persistent save
```
Replace enX0 with your network interface if different (check with ip addr).
### 6. Start WireGuard
```bash
sudo systemctl enable wg-quick@wg0
sudo systemctl start wg-quick@wg0
```
---
## 📱 Mobile Client Setup (WireGuard App)
 ### 1. Download WireGuard app from Play Store or App Store
 ### 2. Create a new tunnel and fill in:
 ```bash
[Interface]
PrivateKey = <your-client-private-key>
Address = 10.0.0.2/32
DNS = 8.8.8.8

[Peer]
PublicKey = <your-server-public-key>
Endpoint = <your-ec2-public-ip>:51820
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 25
```
✅ Replace your-client-private-key, your-server-public-key, and your-ec2-public-ip with actual values.
### 3. Save and toggle the connection ON.

---
## 🧪 Test Your VPN
On server:
```bash
ping 10.0.0.2
```
On mobile, enable tunnel and check:
* In-app status turns green
* You can visit https://whatismyipaddress.com to confirm IP is from Singapore
## 🧾 License
This project is open-source under the MIT License. See LICENSE file for details.
## 🙌 Credits
Built with ❤️ using WireGuard and hosted on AWS EC2.
## 📣 Disclaimer
This tool is shared for educational purposes only. Use responsibly and comply with the terms of service of games and platforms you connect to.

---

Let me know if you'd like this uploaded as a `README.md` file automatically into your GitHub repo — or if you'd like me to generate the `.conf` example files as well!


