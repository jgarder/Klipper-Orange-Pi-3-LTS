# Orange Pi 3 LTS Setup
 homebuilt HyperQbert Ie Hypercube (predecessors to voron/hevOrt gang.)  with Klipper. 
 
 This will hold Orange Pi 3 LTS Setup with some overlap of the next tutorial on Klipper Setup.

1. Get Orange Pi 3 LTS
2. [Goto Armbian website and get latest bullseye (debian) CLI image](https://redirect.armbian.com/region/NA/orangepi3-lts/Bullseye_current)
3. flash image to A1 8+ gb MicroSD card. there is many options to flash OS image i use the [raspberry Pi OS image Utiliy](https://www.raspberrypi.com/software/)
4. install microsd into orange pi. 
5. Plug in HDMI and usb keyboard. follow onscreen instructions to choose bash for your shell, your user and password ,and to connect to wifi network
6. Enter'apt-get update' then 'apt-get upgrade'. you could now copy the OS to the onboard eMMC with 'nand-sata-install'. (this is for Orange Pi 3 LTS and armbian bullseye)
7. your new Orange Pi 3 LTS is now a fully operational SBC server. next steps will Install and turn it into a klipper server

# Klipper Setup

1. SSH into your Opi OR sit at the terminal and enter the commands that follow.
2. Enter "sudo apt-get install git -y" this will install Git which has different open source projects (we will be using a few!)
3. Enter "cd ~" to ensure your on the root user directory
4. Enter "git clone https://github.com/th33xitus/kiauh.git" to download a clone of the latest KIAUH (klipper install and update helper utility)
5. Enter "bash ./kiauh/kiauh.sh" to boot up into the utlilty.
6. Install Klipper, install python 3.x (it works for me ), install moonraker, install mainsail OR fluidd (i choose mainsail)
7. many prefer  "sudo reboot" and replug in the Opi.

# Klipper+Opi to MCU Board (Your printer) Setup
we will now setup our MCU, this will go over the full process, but your mcu will be different in some places.

1. get your mcu USB address by entering into your terminal after reboot: "ls /dev/serial/by-id/*"
2. enter :"ip address" or like i did "ip address | grep 192.*" which will bring up local ip address if your a normal human.
3. goto your web browser and enter your ip "http://192.168.*.***" to get to the mainsail web frontend.
4. on the web frontend mainsail, press machine on the left sidebar, and open your printer.cfg 
5. change your serial: /dev/serial/by-id/<your-mcu-id> to what it should be, click save & restart. Mine was "/dev/serial/by-id/usb-Klipper_lpc1769_11000019871C4AAF7D687C5DC72000F5-if00"


# Accelerometer ADXl Setup (incomplete)
    here we will setup the accelerometer 
Should be able to: http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/details/orange-pi-4-LTS.html

http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/details/orange-pi-3-LTS.html

https://www.klipper3d.org/Measuring_Resonances.html

You're going to need to connect your standard 5v and ground up to energize.

Then you SPI connectors per the device :

ADXL:CS - RPI Pin: GPIO08 (CS) | OPi4 Pin: GPIO-01-B2 (CS)

ADXL:SDO - RPi Pin: GPIO09 (MISO) | OPi4 Pin: GPIO-01-B0 (TXD)

ADXL:SDA - RPi Pin: GPIO10 (MOSI) | OPi4 Pin: GPIO-01-A7 (RXD)

ADXL:CLK/SCL - RPi Pin: GPIO11 (CLK) | OPi4 Pin: GPIO-01-B1 (CLK)

Opi3:

    Ph3 - CS

    Ph5 - SDO/MOSI/TX

    Ph6 - SDA/MISO/RX

    Ph4 - CLk

    [adxl345]

cs_pin: rpi:None

[resonance_tester]

accel_chip: adxl345

probe_points:

100, 100, 20 # an example

