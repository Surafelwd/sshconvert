# Raspberry Pi SSH Setup Guide

This guide will walk you through the steps to establish an SSH connection with your Raspberry Pi in a headless setup (without using a monitor or keyboard) and connect it to your Wi-Fi network.

## Required Software
You will need the following software installed on your computer:

### 1. PuTTY (for Windows users)
PuTTY is an SSH client that allows you to connect to your Raspberry Pi over the network.  
**Download PuTTY**: [https://www.putty.org/](https://www.putty.org/)

### 2. Advanced IP Scanner
Advanced IP Scanner helps you find the IP address of your Raspberry Pi on the local network.  
**Download Advanced IP Scanner**: [https://www.advanced-ip-scanner.com/](https://www.advanced-ip-scanner.com/)

For **Linux** or **macOS** users, SSH is available in the terminal by default. You can use network tools like `nmap` to find your Raspberry Pi's IP address.

---

## Step 1: Ensure Both Devices Are on the Same Network
Make sure that both your computer and the Raspberry Pi are connected to the same local network (e.g., the same Wi-Fi or Ethernet router). This is essential for them to communicate via SSH.

---

## Connecting the Raspberry Pi Without a Monitor (Headless Connection)

To connect your Raspberry Pi to Wi-Fi without a monitor, follow these steps:

1. Insert the SD card into your computer.
2. In the **boot** partition, create a new file named `wpa_supplicant.conf` and add the following configuration:

    ```bash
    country=ET   # Replace "ET" with your country code (e.g., ET for ethiopia)
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1

    network={
        ssid="Your_SSID"
        psk="Your_WiFi_Password"
        key_mgmt=WPA-PSK
    }
    ```

   Replace:
   - `Your_SSID` with the name of your Wi-Fi network.
   - `Your_WiFi_Password` with the password of your Wi-Fi network.

3. Save the file to the **boot** partition of the SD card.

---

## Step 2: Enable SSH

To enable SSH on your Raspberry Pi before booting for the first time, follow these steps:

1. In the **boot** partition of the SD card, create an empty file named `ssh` (no file extension).
   
   This file enables SSH on the Raspberry Pi when it boots.

---

## Step 3: Boot and Connect

1. Insert the SD card into your Raspberry Pi and power it on.
2. Use **Advanced IP Scanner** (or another network tool) to find the IP address of your Raspberry Pi on the local network. Look for a device named `raspberrypi` or similar.
3. Once you have the IP address, open **PuTTY** (or use the terminal on Linux/macOS) and enter the following command:

    ```bash
    ssh pi@<IP_ADDRESS>
    ```

    Replace `<IP_ADDRESS>` with the actual IP address of your Raspberry Pi.

4. Enter the password when prompted. If using the default `pi` user, the default password is `raspberry` (you can change this later).

---

## Troubleshooting

- **Cannot find the Raspberry Pi on the network**: Ensure both devices are connected to the same Wi-Fi network.
- **Permission denied**: Make sure you’ve entered the correct IP address and that SSH is enabled.

