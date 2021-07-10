# CubeSatSim

Following steps from https://gpsd.gitlab.io/gpsd/installation.html

gpsd steps:

1. plug it in and type:

sudo stty -F /dev/ttyUSB0 ispeed 4800 && cat </dev/ttyUSB0

2. install gpsd software:

sudo apt-get -y install gpsd gpsd-clients python-gps

3. see if running:

ps aux | grep gpsd

4. Set to auto start:

sudo dpkg-reconfigure -plow gpsd

5. update firmware

sudo apt-get update
sudo apt-get dist-upgrade
sudo rpi-update
sudo reboot now

The CubeSat Simulator https://github.com/alanbjohnston/CubeSatSim/wiki is a low cost satellite emulator that runs on solar panels and batteries, transmits UHF radio telemetry, has a 3D printed frame, and can be extended by additional sensors and modules.  This project is sponsored by the not-for-profit [Radio Amateur Satellite Corporation, AMSAT®](https://amsat.org).

There are several hardware versions and software branches to go with them - see below for information.

See the Wiki Software Install page for more details: https://github.com/alanbjohnston/CubeSatSim/wiki/2.-Software-Install. The software runs on any Raspberry Pi including the Raspberry Pi 4B, 3B, 3B+, Pi Zero or Pi Zero W.

There are two ways to get the CubeSatSim software for your Pi.

One option is to download the disk image file and write it to a 16GB micro SD card or larger.  The image is based on Raspberry Pi OS (Rasbian) Lite, dated December 2020. All software is installed, you just need to login to change your password and set your amateur radio callsign if you have one.  You can run the ./update.sh script to update all packages and update and compile the latest CubeSatSim software.

The other option is to start with any Raspberry Pi OS (Rasbian) image and run the installation script ./install.sh which will install and compile all the related software.  This includes the following packages:
- wiringpi
- git
- libasound2-dev
- pi-power-button
- Direwolf
- rpitx
- python3-pip 
- python-smbus

## Disk Image Option Steps

See the Wiki Software Install page for details: https://github.com/alanbjohnston/CubeSatSim/wiki/2.-Software-Install.

## Installation Script Option Steps

CubeSatSim runs on any version of Raspberry Pi OS (Desktop or Lite), although a Pi Zero or Pi Zero W should only run Lite.  Your Pi will need to have internet access to update settings and install packages.

To get the software follow these steps:

`sudo apt-get install -y git`

`git clone http://github.com/alanbjohnston/CubeSatSim.git`

`cd CubeSatSim`

`git checkout master`

You are now ready to install the software using this script in the CubeSatSim directory:

`./install`

The installation script will run for quite a while.  You will get prompted for your amateur radio callsign in all capitals, if you have one.  If you don't you can put some other word which will be transmitted as a CW ID.  You will also be prompted for your latitude and longitude for APRS packets. The script will prompt you if you want to modify /boot/config.txt file.  Type a `y` and the script will complete.  You will need to reboot.

See the Wiki for more details about the CubeSatSim https://github.com/alanbjohnston/CubeSatSim/wiki

Older Versions

There are several versions of the hardware and software to go with them:

- The original design used a Digital Transceiver Board for the Raspberry Pi (DigitalTxRxRPi) and APRS AFSK 1200 bps telemetry only.  Use the aprs-digitaltxrx branch https://github.com/alanbjohnston/CubeSatSim/tree/aprs-digitaltxrx for this and the vB2 wiki page https://github.com/alanbjohnston/CubeSatSim/wiki/vB2-Home (e.g. run `git checkout aprs-digitaltxrx` before running the ./install.sh script)
- An updated design that used the Transmitter/Filter Board (TFB) instead of the the Transceiver Board.  For the same APRS AFSK telemetry, use the aprs-rpitx branch https://github.com/alanbjohnston/CubeSatSim/tree/aprs-rpitx and the vB3 wiki page https://github.com/alanbjohnston/CubeSatSim/wiki/vB3-Home. (e.g. run `git checkout aprs-rpitx` before running the ./install.sh script) Note that this hardware can still use the master code branch.
