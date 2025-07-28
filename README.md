# OpenThread Border Router (OTBR) Setup on Raspberry Pi with nRF52840 Dongle

This guide will walk you through setting up an OpenThread Border Router (OTBR) on a Raspberry Pi using an nRF52840 Dongle as the Radio Co-Processor (RCP).

---

## 🧰 System Information: Check Raspberry Pi Hardware and OS

Run these commands on your Raspberry Pi to verify hardware and OS details:

```bash
cat /proc/device-tree/model
cat /proc/cpuinfo | grep Model
cat /etc/os-release
uname -a
uname -m
free -m
```

---

## 🛠️ Step 1: Flash RCP Firmware to nRF52840 Dongle  
  
### 🔨 Build your own RCP Firmware from scratch (Optional) - [GUIDE](https://github.com/make2explore/Open-Thread-Border-Router-on-RaspberryPi/tree/main/Build-Your-Own-RCP-Firmware)  
  
### 🔽 Download Precompiled Firmware (Recommended)

Download the RCP firmware binary from the official repository:  
[Download Link](https://github.com/make2explore/Open-Thread-Border-Router-on-RaspberryPi/archive/refs/heads/main.zip)

### 💡 Flash using nRF Connect for Desktop

Use the **Programmer App** from **nRF Connect for Desktop** to flash the downloaded firmware onto the nRF52840 Dongle.

### 🚨 Enter DFU Mode on nRF52840 Dongle

1. **Press and hold** the reset button.
2. **Plug** the dongle into a USB 2.0 port on the Raspberry Pi while holding the button.
3. **Release** the button after inserting.  
If successful, the red LED will show a **breathing effect**, indicating DFU mode is active.

---

## 🧪 Step 2: Setup OpenThread Border Router (OTBR)

### 🔄 Update Raspberry Pi

```bash
sudo apt update && sudo apt upgrade -y
```

### 🧰 Install Git

```bash
sudo apt install git -y
```

### 📥 Clone the OTBR Repository

```bash
git clone https://github.com/openthread/ot-br-posix
cd ot-br-posix/
```

### ⚙️ Bootstrap and Setup

```bash
WEB_GUI=1 NAT64=1 NAT64_SERVICE=openthread ./script/bootstrap
INFRA_IF_NAME=wlan0 WEB_GUI=1 ./script/setup
```

---

## 🌐 Configure and Access Web GUI

### 🔧 If WebGUI is not running

Check current web service configuration:

```bash
sudo cat /etc/systemd/system/otbr-web.service
```

### 📝 Fix: Create/Edit ENV Config File

```bash
sudo nano /etc/default/otbr-web
```

Add the following line:

```bash
OTBR_WEB_OPTS="-p 8080 -a 0.0.0.0"
```

### 🔄 Restart Web Service

```bash
sudo systemctl restart otbr-web
sudo reboot now
```

---

## 📊 Monitor and Troubleshoot Services

### ✅ Check Service Status

```bash
sudo systemctl status otbr-agent
sudo systemctl status otbr-web
```

### 🪵 View Logs

```bash
journalctl -u otbr-agent.service
journalctl -u otbr-web.service
```

---

## ✅ Final Check

Make sure the OTBR services are running correctly:

```bash
sudo systemctl status
```

---

## 📎 Notes

- Replace `wlan0` with your actual Wi-Fi interface name if different.
- Ensure your Raspberry Pi is connected to the internet during the setup.

---