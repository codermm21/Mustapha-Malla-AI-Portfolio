# SunFounder Picar-X AI Video Robot Car Kit - Setup Guide

This guide provides detailed instructions to set up your SunFounder Picar-X AI Video Robot Car Kit, including Raspberry Pi OS configuration, hardware assembly, and software dependencies installation.

## 1. Prepare your Raspberry Pi

The Picar-X is compatible with Raspberry Pi Zero 2w, 3B+, 4, and 5. Ensure your Raspberry Pi has a fresh installation of Raspberry Pi OS (formerly Raspbian).

### 1.1 Install Raspberry Pi OS

1.  **Download Raspberry Pi Imager**: Download the appropriate version for your operating system from the [official Raspberry Pi website](https://www.raspberrypi.com/software/).
2.  **Flash OS to SD Card**: 
    *   Open Raspberry Pi Imager.
    *   Choose your desired Raspberry Pi OS (e.g., Raspberry Pi OS Lite for headless setup or Raspberry Pi OS with desktop for a GUI).
    *   Select your SD card.
    *   Click 'Write' to flash the OS to the SD card.
3.  **Enable SSH (Optional but Recommended for Headless Setup)**: Before removing the SD card from your computer, create an empty file named `ssh` (no extension) in the `boot` partition of the SD card. This enables SSH access upon first boot.
4.  **Configure Wi-Fi (Optional for Headless Setup)**: Create a file named `wpa_supplicant.conf` in the `boot` partition with the following content (replace with your network details):
    ```
    country=US  # Your two-letter country code
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1

    network={
        ssid="YOUR_NETWORK_NAME"
        psk="YOUR_NETWORK_PASSWORD"
    }
    ```

## 2. Assemble the Picar-X Hardware

Refer to the official SunFounder Picar-X assembly manual for detailed step-by-step instructions. Ensure all components are securely connected, especially the motor drivers, camera module, and ultrasonic sensor.

*   **Official Assembly Guide**: [SunFounder Picar-X Documentation](https://picar-x.readthedocs.io/en/latest/index.html)

## 3. Install Software Dependencies

Once your Raspberry Pi is assembled and powered on, connect to it via SSH or a direct display and keyboard.

### 3.1 Update and Upgrade System Packages

```bash
sudo apt update
sudo apt upgrade -y
```

### 3.2 Install Git and Python Development Tools

```bash
sudo apt install -y git python3-dev python3-pip
```

### 3.3 Install Python Libraries (from `requirements.txt`)

Navigate to your project directory (where `requirements.txt` is located) and install the Python dependencies:

```bash
pip3 install -r requirements.txt
```

**Note**: `opencv-python` may require additional system dependencies for full functionality. If you encounter errors, refer to the official documentation for those libraries.

### 3.4 Install PiCar-X Raspberry Pi HAT Firmware

The PiCar-X HAT requires its own firmware for proper functionality and motor control.

```bash
wget -O ~/install_picar_x.sh https://github.com/sunfounder/picar_x/raw/master/install_picar_x.sh
sudo bash ~/install_picar_x.sh
```

### 3.5 Install Vilib (for Picar-X Camera and AI Features)

The Vilib library from SunFounder is crucial for Picar-X's visual recognition and AI functionalities.

```bash
git clone https://github.com/sunfounder/vilib.git
cd vilib
sudo python3 setup.py install
cd ..
```

### 3.6 Install Picar-X Python Library

The core Picar-X Python library is essential for controlling the robot's hardware components.

```bash
git clone https://github.com/sunfounder/picar-x.git
cd picar-x
sudo python3 setup.py install
cd ..
```

### 3.7 Run I2C Sample Script (`i2samp.py`)

After installing the HAT firmware and libraries, you can run the `i2samp.py` script to test the I2C communication with the HAT. This script is typically found in the `picar-x/example` directory after cloning the `picar-x` repository.

```bash
cd picar-x/example
sudo python3 i2samp.py
cd ../..
```

### 3.8 Camera Configuration

Ensure your Raspberry Pi camera is enabled. You can do this via `sudo raspi-config` -> `Interface Options` -> `Camera` -> `Yes`.

## 4. Initial Testing

After setting up, run basic tests to ensure all components are working correctly. Refer to the official Picar-X examples for testing motors, servos, and sensors.

This `setup_guide.md` should help you get started with your Picar-X project. For more in-depth information, always refer to the official SunFounder documentation.
