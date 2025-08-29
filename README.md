## How to Install OTBR (Open-Thread Border Router) on a Raspberry Pi  
  
<img src="/Images/m2e-OTBR.jpg" height="200"> 
  
An **OTBR**, or **OpenThread Border Router**, is the open-source implementation of a Thread Border Router that acts as a gateway, connecting a Thread network (a low-power wireless mesh protocol for IoT) to external IP-based networks like the internet or Wi-Fi. It provides essential services such as IP connectivity, service discovery, and external commissioning, allowing Thread devices to communicate with services and devices beyond the Thread network, which is crucial for smart home ecosystems like Matter.  
  
An **OTBR** on a Raspberry Pi acts as a gateway between an IPv6-based Thread network and an external IP network like the internet. It uses the Raspberry Pi as its "host" platform and a Radio Co-Processor (RCP) or Network Co-Processor (NCP) device (often a Nordic nRF52840 dongle or Silicon Labs Explorer kit) to handle the Thread network's radio communication. This setup allows Thread devices to access IP networks and is crucial for building networks that support Matter over Thread.  
  
### Prerequisites 🧰
  
To set the OpenThread Border Router (OTBR) using a Raspberry Pi there are following Hardware-software Prerequisites - 
  
### Hardware
- Raspberry Pi: A Raspberry Pi 3 or 4 is recommended. A monitor, keyboard, and mouse can be helpful for the initial setup, though you can also use a headless setup with SSH.
- MicroSD card: At least 8 GB, to hold the Raspberry Pi OS.
- MicroSD card Reader.  
- Thread Radio Co-processor (RCP): This is a key component. The RCP acts as the radio for the Thread network. Common choices include a Nordic Semiconductor nRF52840 USB Dongle The RCP needs to be flashed with OpenThread RCP firmware.
- Power supply and cables: A power supply for the Raspberry Pi and a USB cable to connect the RCP.
- Network connection: Your Raspberry Pi needs an internet connection (either Wi-Fi or Ethernet) to download necessary software.  
  
### Software  
- Raspberry Pi OS: A recent version of Raspberry Pi OS (either the Lite or Desktop version) installed on the SD card.
- Raspberry Pi Imager - To flash the OS into SD Card.
- OTBR Software: The OpenThread Border Router software stack, which you will typically download and build from the official GitHub repository, openthread/ot-br-posix.
- RCP Firmware: The RCP device must be flashed with the correct OpenThread RCP firmware to function as a co-processor.  
- nRF Connect for Desktop.  
- PuTTY or any other Remote Terminal Access Software.
  

------------------------------------------------------------------------------------------------------

📕 **YouTube Video Links**  

- In this tutorial we will see How to install OTBR on Raspberry Pi  

▶️ [Tutorial]How to install OTBR on Raspberry Pi  - 🔗  https://youtu.be/   
  

-------------------------------------------------------------------------------------------------------
📒 **Important Links**  
 
🌐 What is OpenThread -  Docs - 🔗 https://github.com/openthread/openthread    
🌐 OpenThread Border Router - 🔗 https://openthread.io/guides/border-router   
📙 Set up your Raspberry Pi 🔗 https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up  
🌐 Raspberry Pi Imager - 🔗 https://www.raspberrypi.com/software/  
🌐 Raspberry Pi OS  - 🔗 https://www.raspberrypi.com/software/operating-systems/  
🌐 NoMachine RDS - 🔗 https://www.nomachine.com/  
🌐 SD Card Formatter - 🔗 https://www.sdcard.org/downloads/  


------------------------------------------------------------------------------------------------------

📜 Source Code, Circuit Diagrams and Documentation : 

🌐 GitHub Repository - 🔗 https://github.com/make2explore/Open-Thread-Border-Router-on-RaspberryPi/tree/main/Open-Thread-Border-Router   
  
🌐 Hackster Blog - 🔗 https://www.hackster.io/make2explore  
  
🌐 Instructable Blog - 🔗 https://www.instructables.com/make2explore  
  

------------------------------------------------------------------------------------------  

Shield: [![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]

This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg