# Build and Install OpenThread Border Router (OTBR) on Raspberry Pi with nRF52840 Dongle

This guide explains how to build your own RCP firmware for the nRF52840 Dongle and set up the OpenThread Border Router (OTBR) on a Raspberry Pi.

---

## 🧰 System Information: Check Raspberry Pi Hardware and OS

Run these commands to inspect your system:

```bash
cat /proc/device-tree/model
cat /proc/cpuinfo | grep Model
cat /etc/os-release
uname -a
uname -m
free -m
```

---

## 🔨 Build Your Own RCP Firmware (nRF52840 Dongle)

### 🔄 Update and Install Required Packages

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git -y
sudo apt install gcc-arm-none-eabi -y
```

### 📥 Clone and Build OpenThread RCP Firmware

```bash
git clone --recursive https://github.com/openthread/ot-nrf528xx
cd ot-nrf528xx
./script/bootstrap
./script/build nrf52840 USB_trans -DOT_BOOTLOADER=USB
```

### 📂 Access and Convert Firmware

```bash
cd build/bin
cd ../..
arm-none-eabi-objcopy -O ihex build/bin/ot-rcp ot-rcp.hex
ls
```

> Use FileZilla or another SFTP software to transfer the `ot-rcp.hex` file from Raspberry Pi.

---

## 🧲 Flash Firmware to nRF52840 Dongle

### Enter DFU Mode

1. **Hold** the reset button on the dongle.
2. **Plug in** to a USB 2.0 port on the Raspberry Pi while holding the button.
3. **Release** the button. The **Red LED breathing effect** indicates successful DFU mode.

### Flash Firmware

Use **nRF Connect for Desktop → Programmer App** to flash the `ot-rcp.hex` file onto the dongle.

After successful flashing, **replug** the device.

---

## 🛠️ Setup OTBR on Raspberry Pi

### 🧰 Install and Build OTBR

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git -y
git clone https://github.com/openthread/ot-br-posix
cd ot-br-posix/
WEB_GUI=1 NAT64=1 NAT64_SERVICE=openthread ./script/bootstrap
INFRA_IF_NAME=wlan0 WEB_GUI=1 ./script/setup
```

---

## 🌐 Enable Web GUI (Optional)

### If Web GUI is not running:

Check service file:

```bash
sudo cat /etc/systemd/system/otbr-web.service
```

Edit environment file:

```bash
sudo nano /etc/default/otbr-web
```

Add the following line:

```bash
OTBR_WEB_OPTS="-p 8080 -a 0.0.0.0"
```

Restart the web service:

```bash
sudo systemctl restart otbr-web
sudo reboot now
```

---

## 📊 Monitor OTBR Services

Check status:

```bash
sudo systemctl status otbr-agent
sudo systemctl status otbr-web
```

View logs:

```bash
journalctl -u otbr-agent.service
journalctl -u otbr-web.service
```

Final service check:

```bash
sudo systemctl status
```

---

## 📎 Notes

- Replace `wlan0` with your actual network interface if needed.
- Ensure your Pi is connected to the internet during the entire process.