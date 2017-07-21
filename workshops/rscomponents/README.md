# The Titan Private Blockchain for participants

Feel free to use the Titan Private Blockchain because mining might be faster then the testnet or livenet ( all the details about how to connect ). This Blockchain can also be used with the raspberries.

**[gist.github.com/andysign/492ae66095bf9a20df2d0b403934437f](https://gist.github.com/andysign/492ae66095bf9a20df2d0b403934437f)**

# IoTblockchain Pi

The main idea behind **IoTblockchain Pi is** to provide give developers a simple *ETH* **Full Node** / **Test Node** so that they can use it to building their solutions within the **Blockchain** space with the main focus **Internet of Things**.

# Description

**Autonommous IoT Blockchain Smart Devices**

# Prerequisites for Hardware

* **[Raspberry Pi 3](http://uk.rs-online.com/web/p/processor-microcontroller-development-kits/8968660/ "pi3")** or if you don't wan't WiFi / you have a dongle already, **[Raspberry Pi 2 Model B](http://uk.rs-online.com/web/p/processor-microcontroller-development-kits/8326274/)**
* **[Sandisk 16 GB SD Card](http://uk.rs-online.com/web/p/secure-digital-cards/7504786/)** or bigger ( 64 GB or 128 if you want to store the entire blockchain or a hard drive )
* **[Raspberry Pi, 13W Plug In Power Supply 5.1V, 2.5A 1 Output, Micro USB](http://uk.rs-online.com/web/p/plug-in-power-supply/1235272/)** or similar with a **5.1V/2.5A** output or lower for **Raspberry Pi 2**
* **[RS Pro Raspberry Pi 3 Case](http://uk.rs-online.com/web/p/development-board-enclosures/1034296/)** (optional)
* **[PiTFT Plus 3.5 Raspberry Pi Touchscreen -- Resistive](http://uk.rs-online.com/web/p/products/1245487/)** (optional)
* **[Raspberry Pi Camera V2 Camera Module](http://uk.rs-online.com/web/p/video-modules/9132664/)** (or any other sensors)
* **[Raspberry Pi Camera case](http://uk.rs-online.com/web/p/development-board-enclosures/7846190/)** (optional)
* **[Toshiba Canvio Basics Black 500 GB Portable Hard Drive](http://uk.rs-online.com/web/p/portable-hard-drives/8336461/)** (optional for building full nodes)
* **[Raspberry Pi Sense Hat
](http://uk.rs-online.com/web/p/interface-development-kits/8949310/)** (optional sensor)


# Prerequisites for Software

For this project you will have to first download and prepare the Raspbian Linux system for the raspberry board itself, on your personal machine you don't need anything apart from a **SSH client**. 

**Linux OS**:

* **[Raspbian](http://downloads.raspberrypi.org/raspbian/images/raspbian-2016-09-28/2016-09-23-raspbian-jessie.zip)** - preferably `Raspbian Jessie 2016-09-23 kernel: 4.4`

**Others**: 

* For this project you will need to install on the pi various dependencies such as **NodeJS**, **NPM** and so on.

# Getting Started

**This is a step by *step do it yourself* process that enables you to build the same image from scratch**

## Preparing the OS

Prepare the **Micro SD** card and insert it in your machine directly or using a **Memory Card Adapter**.

Download the latest version of the **Raspbian Jessie** from the Raspberry Pi official website **[downloads page](https://www.raspberrypi.org/downloads/raspbian/)** or, if you want to use the version tested here, go to **[downloads.raspberrypi.org](http://downloads.raspberrypi.org/raspbian/images/)** and get the **2016-09-23-raspbian-jessie.zip** version.

### Burning the card on Windows

The recommended program for burning is  **[Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/)** . Download and install the image burner and follow the instructions.

### Burning the card on Mac

The perfect image burner for this case is **[Etcher](https://etcher.io/ "Etcher")**. Download and install the image burner and follow the instructions.

### Burning the card on Linux

For Linux you can just use data definition like `sudo dd bs=1M if=2016-09-23-raspbian-jessie.img of=/dev/mmcblk0`

## SSH

The **SSH** service should be enable by default.

Just ssh connect in the terminal if you have Linux or Mac (use **raspberry** as password)

```shell
ssh pi@raspberrypi.local
```

Or just use [Putty](http://www.putty.org/) if you have Windows.

If not, use a screen, boot and run `sudo raspi-config` and then go to `Interfacing Options` find the SSH optoin and then enable it by selecting `Yes` then reboot. If you don't have a screen connect the board to the network using a classic ethernet cable, make sure your **Pi** can be *seen* by your other computer that you want to connect from, try pinging different ip addresses or use a simple IP scanner like **[angryip.org](http://angryip.org/download/)** or **[nmap.org](https://nmap.org)** used with `nmap -sL --traceroute 192.168.0.1-255` where 192.168.0 is the beginign of your ip address determined using `ifconfig | grep inet addr`

## Wi-Fi

Feel free to connect to your office or home Wi-Fi network by booting in GUI mode with a screen and selecting the wifi from **Settings**. 

Alternatively if you are connected via a basic Ethernet cable trough a ssh remote edit the **wpa_supplicant.conf** with `sudo nano /etc/wpa_supplicant/wpa_supplicant.conf` as described below. 

After the third line ( *update_conf=1* ) add:

```
network={
ssid="example"
psk="password"
}
```

Optional, if it doesn’t work,add `key_mgmt=WPA-PSK`  before the last line (the line with the closing bracket). If you have other security settings or the key management is different and you are not sure what to put there, use `sudo iwlist wlan0 scan`

<!-- #Used Wi-Fi Settings (need to be removed) 

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=GB

network={
        ssid="Electro-WiFi"
        psk=f7ad33d069dea7059b25f5edc87e621da405d0ca9599708e1926edb9e67e16d6
}

network={
        ssid="SamsungAs"
        psk=2d798f953bdd1a0f4ce35bcebb7dd5d87a50163e43eed89e01c27089f74a26b5
}

network={
        ssid="Dulles International Airport"
        psk=f2bb0d967c3268fe9bf5842db6eb0ae74d70074c2da303d9bb10bbbd85a95c1d
}

-->

## Expand the partition

**!Expand the file system if needed as described in the [official config article](https://www.raspberrypi.org/documentation/configuration/raspi-config.md)** ( `sudo raspi-config` and select the first option to expand the filesystem )

## Boot mode

For better performance the main recommandation is to boot directly in **command line** not in **desktop**. That's easily configurable with `sudo raspi-config` in **Boot Options**.

## Extra Components

### PiTFT Resistive Touch Display ( optional )

#### TFT hardware options

There are various version of PiTFT displays. For a small budget the best display is the 2.8 inch resistive display. Alternatively you can use the 3.5 inch resistive display.

#### TFT software install and config

The optional **[PiTFT Plus 2.8in TFT Resistive Touchscreen Display](http://uk.rs-online.com/web/p/graphics-display-development-kits/1245479/)** or **[PiTFT Plus 3.5in TFT Resistive Touchscreen Display](http://uk.rs-online.com/web/p/graphics-display-development-kits/1245487/)** screen installation is slow because the kernel needs to be downloaded and installed and that might take some time according to [Adafruit 2.8](https://learn.adafruit.com/adafruit-pitft-28-inch-resistive-touchscreen-display-raspberry-pi/easy-install) or [Adafruit 3.5](https://learn.adafruit.com/adafruit-pitft-3-dot-5-touch-screen-for-raspberry-pi/easy-install) .

Add adafruit to the sources list and update package database with:

`curl -SLs https://apt.adafruit.com/add-pin | sudo bash`

Then download the kernel with:

`sudo apt-get install --yes --force-yes raspberrypi-bootloader adafruit-pitft-helper raspberrypi-kernel`

Enable and configure the tft with then reboot:

`sudo adafruit-pitft-helper -t 28r`

or, if you have the big screen

`sudo adafruit-pitft-helper -t 35r`

Reboot again and everything should be fine. You can rotate by editing the /boot/config.txt file and you can also calibrate by reading the **[adafruit calibration instructions 2.8](https://learn.adafruit.com/adafruit-pitft-28-inch-resistive-touchscreen-display-raspberry-pi/touchscreen-install-and-calibrate)** or **[adafruit calibration instructions 3.5](https://learn.adafruit.com/adafruit-pitft-3-dot-5-touch-screen-for-raspberry-pi/touchscreen-install-and-calibrate)**

All the above can be done in one line for the 2.8 inc TFT resistive screen with:

`curl -SLs https://apt.adafruit.com/add-pin | sudo bash && sudo apt-get install --yes --force-yes raspberrypi-bootloader adafruit-pitft-helper raspberrypi-kernel && sudo adafruit-pitft-helper -t 28r`

and also in one line for the 3.5 inch TFT resistive screen with:

`curl -SLs https://apt.adafruit.com/add-pin | sudo bash && sudo apt-get install --yes --force-yes raspberrypi-bootloader adafruit-pitft-helper raspberrypi-kernel && sudo adafruit-pitft-helper -t 35r`

#### TFT display or switch to HDMI

If you want the the display to go to HDMI, and shut off the TFT display, if it's plugged in, otherwise go to the TFT display then a new display layout needs to be configured. The `/etc/X11/xorg.conf.d/99-fbdev.conf` configuration file needs to be changed to:

```shell
 # FBTFT xorg config file
 #
 # startx -- -layout TFT
 # startx -- -layout HDMI
 #
 # When not specifying the layout, the first is used: TFT
 #

Section "ServerLayout"
    Identifier "TFT"
    Screen 0 "ScreenTFT"
EndSection

Section "ServerLayout"
    Identifier "HDMI"
    Screen 0 "ScreenHDMI"
EndSection

Section "Screen"
    Identifier "ScreenHDMI"
    Monitor "MonitorHDMI"
    Device "DeviceHDMI"
Endsection

Section "Screen"
    Identifier "ScreenTFT"
    Monitor "MonitorTFT"
    Device "DeviceTFT"
Endsection

Section "Monitor"
    Identifier "MonitorHDMI"
Endsection

Section "Monitor"
    Identifier "MonitorTFT"
Endsection

Section "Device"
    Identifier "DeviceHDMI"
    Driver "fbturbo"
    Option "fbdev" "/dev/fb0"
    Option "SwapbuffersWait" "true"
EndSection

Section "Device"
    Identifier "DeviceTFT"
    Option "fbdev" "/dev/fb1"
EndSection
```

Then just type `startx -- -layout TFT` to start using the TFT or `startx -- -layout HDMI` to use the HDMI. A better way is to run a script at start-up to check if the HDMI cable is connected and if not to fall back on TFT. For this a new service needs to be created and therefore a new file `/etc/init.d/fbdev` with the following script inside:

```shell
 #!/bin/sh
 # /etc/init.d/fbdev
 ### BEGIN INIT INFO
 # Provides: fbdev
 # Required-Start: $remote_fs $syslog
 # Required-Stop: $remote_fs $syslog
 # Default-Start: 2 3 4 5
 # Default-Stop: 0 1 6
 # Short-Description: Start X server on HDMI, if plugged, otherwise TFT, at boot time
 # Description: Start X Server at boot time.
 # ## END INIT INFO

 # Set the FBUSER variable to the name of the user to start Xserver under
FBUSER="pi"

 # Set the LAYOUT variable with which to start the Xserver under
LAYOUT="TFT"

PLUGGED=$(tvservice -s | grep -i RGB)$(tvservice -s | grep -i hdmi)

if [ -n "$PLUGGED" ]
then
   LAYOUT="HDMI"
   su $FBUSER -c "con2fbmap 1 0"
   su $FBUSER -c "gpio -g mode 18 pwm"
else
   su $FBUSER -c "con2fbmap 1 1"
fi

eval cd ~$FBUSER

case "$1" in
 start)
   su $FBUSER -c "startx -- -layout '$LAYOUT'"
   echo "Starting Xserver for $FBUSER "
   ;;
 stop)
   pkill xinit
   echo "Xserver stopped"
   ;;
 *)
   echo "Usage: /etc/init.d/fbdev {start|stop}"
   exit 1
   ;;
esac
exit 0
```

This will not work unless the **chmod** attribute for the file is changed:

```
sudo chmod 755 /etc/init.d/fbdev
```

And finally this needs to run permanently so insert the service with the following and restart:

```
sudo update-rc.d fbdev defaults
```

If everything goes well, the raspberry should boot without errors and show the command prompt cursor on the **TFT** screen when booting with no cable connected and show the cursor on the attached screen when connecting the **HDMI** cable.

Now, there might be some errors when starting the graphic interface with the HDMI cable connected because the `startx` script tries to render on the TFT screen, therefore, to start the GUI on HDMI manually, you need to run `startx -- -layout HDMI` or add a short-cut script with:   

`echo "startx -- -layout HDMI" | sudo tee /usr/bin/startxhdmi && sudo chmod +x /usr/bin/startxhdmi`

This will start the GUI correctly whenever you run `startxhdmi`

To simplify the process a bit, a good alternative is to run everything from above with one line.

```shell
echo -e '\nSection "ServerLayout"\n\tIdentifier "TFT"\n\tScreen 0 "ScreenTFT"\nEndSection\n\nSection "ServerLayout"\n\tIdentifier "HDMI"\n\tScreen 0 "ScreenHDMI"\nEndSection\n\nSection "Screen"\n\tIdentifier "ScreenHDMI"\n\tMonitor "MonitorHDMI"\n\tDevice "DeviceHDMI"\nEndsection\n\nSection "Screen"\n\tIdentifier "ScreenTFT"\n\tMonitor "MonitorTFT"\n\tDevice "DeviceTFT"\nEndsection\n\nSection "Monitor"\n\tIdentifier "MonitorHDMI"\nEndsection\n\nSection "Monitor"\n\tIdentifier "MonitorTFT"\nEndsection\n\nSection "Device"\n\tIdentifier "DeviceHDMI"\n\tDriver "fbturbo"\n\tOption "fbdev" "/dev/fb0"\n\tOption "SwapbuffersWait" "true"\nEndSection\n\nSection "Device"\n\tIdentifier "DeviceTFT"\n\tOption "fbdev" "/dev/fb1"\nEndSection\n\n' | sudo tee /etc/X11/xorg.conf.d/99-fbdev.conf &&
```

```shell
echo -e '#!/bin/sh\n# /etc/init.d/fbdev\n### BEGIN INIT INFO\n# Provides: fbdev\n# Required-Start: $remote_fs $syslog\n# Required-Stop: $remote_fs $syslog\n# Default-Start: 2 3 4 5\n# Default-Stop: 0 1 6\n# Short-Description: Start X server on HDMI, if plugged, otherwise TFT, at boot time\n# Description: Start X Server at boot time.\n### END INIT INFO\n# Set the FBUSER variable to the name of the user to start Xserver under\nFBUSER="pi"\n# Set the LAYOUT variable with which to start the Xserver under\nLAYOUT="TFT"\nPLUGGED=$(tvservice -s | grep -i RGB)$(tvservice -s | grep -i hdmi)\nif [ -n "$PLUGGED" ]\nthen\n   LAYOUT="HDMI"\n   su $FBUSER -c "con2fbmap 1 0"\n   su $FBUSER -c "gpio -g mode 18 pwm"\nelse\n   su $FBUSER -c "con2fbmap 1 1"\nfi\neval cd ~$FBUSER\ncase "$1" in\n start)\n   su $FBUSER -c "startx -- -layout '\''$LAYOUT'\''"\n   echo "Starting Xserver for $FBUSER "\n   ;;\n stop)\n   pkill xinit\n   echo "Xserver stopped"\n   ;;\n *)\n   echo "Usage: /etc/init.d/fbdev {start|stop}"\n   exit 1\n   ;;\nesac\nexit 0' | sudo tee /etc/init.d/fbdev &&
```

```shell
sudo chmod 755 /etc/init.d/fbdev && sudo update-rc.d fbdev defaults &&
```

```shell
echo "startx -- -layout HDMI" | sudo tee /usr/bin/startxhdmi && sudo chmod +x /usr/bin/startxhdmi
```

## Setting up the Ethereum client

### Ethereum Go ( GETH )

First of all, building the client from source might take a hours especially when taking into account the difficulty of setting up the compiler.

To make it easy, use the cross-compiled **[geth](https://github.com/ethereum/go-ethereum)**.

There are several versions for all the processor architectures like `ARM64`, `ARMv5`, `ARMv6` and `ARMv7` but your processor should be `ARMv7`.

You can check it with `name -a`

The easiest way is to download the client directly with wget.

In this case we are using `geth v1.6.7` but it could be a newer version.

`wget https://gethstore.blob.core.windows.net/builds/geth-linux-arm7-1.6.7-ab5646c5.tar.gz`

Unzip the file with

`tar xf geth-linux-arm7-1.6.7-ab5646c5.tar.gz`

And install the client by simply performing a copy to `$PATH`

`sudo cp geth-linux-arm7-1.6.7-ab5646c5/geth /usr/local/bin/`

Don't forget to clean up ater with `rm -R geth-linux-arm7-1.6.7-ab5646c5*` and to make thigns more clear you can create a symbolic link in **/home/pi/** with `ln -s /usr/local/bin/geth ~`

Everything can be executed with one line with:

```
GETHVER=geth-linux-arm7-1.6.7-ab5646c5 && wget https://gethstore.blob.core.windows.net/builds/$GETHVER.tar.gz && tar xf $GETHVER.tar.gz && sudo cp $GETHVER/geth /usr/local/bin/ && rm -R $GETHVER* && ln -s /usr/local/bin/geth ~
```

### GETH Auto Start

There are at least **[5 methods](https://www.dexterindustries.com/howto/run-a-program-on-your-raspberry-pi-at-startup/ "5 methods")** to run a program on your raspberry at start-up. For now, let's assume that we have an executable script (`chmod +x *.sh`) `startgeth.sh` in `~` with just `geth` or `geth --testnet` ( we will look at this later ). 

Now the question becomes, what is the best way to run this at startup user your raspberry depending on the various ways you want to your your raspberry so that you don't have to use a keyboard or a ssh connection every time you power the board. 

#### GETH Startup in detached screen

If the objective is to use the raspberry shell session from multiple locations and therefore it is important to keep the shell connection active even tough there are network disruptions, the best way is to use [linux screen](https://linux.die.net/man/1/screen "linux screen"). This allows you to use `Ctrl+A, C` to detach the screen and then attach a new one. 

First install it with:

`sudo apt-get install -y screen`

Then edit the root startup script file `/etc/rc.local` with:

`sudo nano /etc/rc.local`

Here add the following line before the last line ( before *exit 0* ):

```
 # Run a command as pi from home in a screen named pistartup
sudo su - pi -c "screen -d -m -U -S GETHSCREEN /home/pi/startgeth.sh"
```

Now after you log in you can run `screen -ls` to see the fact that the virtual screen is running and you will see something like this.

```
There is a screen on:
  730.GETHSCREEN  (17/07/17 15:59:06)     (Detached)
```

And you can now run `screen -DR` to re-attach the geth screen

All in one line (for example to run private geth) :

```
sudo apt-get install -y screen && echo "geth --networkid 20170125 " > /home/pi/startgeth.sh && chmod +x startgeth.sh && sudo sed -i '0,/exit 0/s//exit zero/' /etc/rc.local && sudo sed -i '/exit 0/i sudo su - pi -c "screen -d -m -U -S GETHSCREEN /home/pi/startgeth.sh"' /etc/rc.local
```


#### GETH Startup as daemon service

Another way to rung geth and this is the most used way right now is to make use of the systemd init system.

Simply create a file with `sudo nano /etc/systemd/system/geth.service` and add:

```
[Unit]
Description=Ethereum geth client daemon
After=network.target

[Service]
 # EnvironmentFile=/etc/geth/geth.conf
ExecStart=/usr/local/bin/geth
Restart=always
User=pi

[Install]
WantedBy=multi-user.target
```

Dont forget to change the file attribute to make it accessible with:

`sudo chmod 644 /etc/systemd/system/geth.service`

And for the final step we can tell the `sytemd` to start it during the boot sequence:

```
sudo systemctl daemon-reload
sudo systemctl enable geth.service
```

You can then manage the daemon with 

`sudo systemctl stop|start|restart|status geth`

#### GETH Startup Arguments

As mentioned before, a simple shell script file called `startgeth.sh` would be ideal especially when working various private chains or with the `testnet` chain and you want to change the way geth starts very often. 

In order to create this script just run:

`nano startgeth.sh`

Inside this file, in case this script is for the **main public *Ethereum *blockchain** add:

`geth`

Don't forget to make it executable with:

`chmod +x startgeth.sh`

For other networks this will look like:

* **ROPSTEN TestNet** <br>
`geth --testnet`

* **RINKEBY PoA TestNet** <br>
`geth --rinkeby`

* **Your Private TestNet** ( if the blockchain is initialized already with `geth init genesis.json` ) <br>
`geth --networkid 123456789`

You can then attach another instance of `geth` with:

`geth attach`

or when you want to use the testnet:

`geth attach ipc:.ethereum/testnet/geth.ipc`

#### GETH Startup Other Scripts

Display the ip address at startup so that you know what ip to use to SSH

Edit `.bashrc` with `sudo nano /home/pi/.bashrc` and add the following at the end:

```
 # Echo welcome message and ip
sleep 2 && _IP=$(hostname -I) && echo "Welcome! The IP address is " && echo $_IP
```

Or in one line:

```
sudo echo '# Echo welcome message and ip' >> .bashrc && sudo echo 'sleep 2 && _IP=$(hostname -I) && echo "Welcome! The IP address is " && echo $_IP' >> .bashrc
```

<!-- 
sudo echo '# Echo welcome message and ip' >> .bashrc && sudo echo 'sleep 2 && _IP=$(hostname -I) && echo "Welcome! Use screen -DR to attach. The IP address is " && echo $_IP' >> .bashrc 
-->

#### GETH Startup Advanced

In order to make it easy to start the `geth` client with all the parameters needed for development, especially in cases where typing long arguments for private blockchains after geth in the terminal it's always nice to have a script to start everything.

##### GETH Startup Advanced Genesis

As described in the [ethereum documantation](http://ethdocs.org/en/latest/network/test-networks.html#the-genesis-file), for private networks, the geth client needs to be initiated with `init`.

The simplest genesis file is the following:

```json
    {
    "config": { "chainId": 123 }, "nonce": "0x0000000000000042", "timestamp": "0x0",
    "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",    
    "extraData": "0x3535353535353535353535353535353535353535353535353535353535353535",
    "gasLimit": "0x8000000", "difficulty": "0x30000",
    "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "coinbase": "0x3333333333333333333333333333333333333333",
    "alloc": {     }
    }
```

One **example** can be found here on [git.io/vDzbY](https://gist.githubusercontent.com/andysign/3a02e5c9797d5cc93cdf86fc649f4a71/raw/d1615e139d24740a151c935704ba2ea07124dec6/genesis.json) (the network id is declared in the file on line 3, that is **20170125**) 

`wget https://git.io/vDzbY -O genesis.json`

`geth init genesis.json`

`geth --networkid 20170125 console`

##### GETH Startup Advanced Networkid

The Network identifier can be changed to any integer with 

`geth --networkid $NETWORKID`

##### GETH Startup Advanced Identity

In order to start with a custom node name use

`geth --identity $USER`

##### GETH Startup Advanced Maxpeers

Maximum number of network peers can be set with 

`geth --maxpeers $MAXPEERS`

##### GETH Startup Advanced NewAccount

You can create a new account with

`geth --password <(echo 123) account new`

##### GETH Startup Advanced Unlock

The main account can be unlocked with 

`geth --unlock 0 --password <(echo 123)`

##### GETH Startup Advanced Bootstrap Node

You can bootstrap a node with

`geth --bootnodes $NODE`

##### GETH Startup Advanced RPC

The HTTP Json-RPC server can be enabled either on the localhost, local ip address or public address or DNS with ( don't forget to filter the corsdomain to avoid someone else getting control of your node and therefore loosing funds ):

`geth --rpc --rpcaddr $IP --rpcport 8545 --rpccorsdomain "*"`

#### GETH Startup ALL

The following script can be added in `startgeth.sh` ( don't forget chmod +x startgeth.sh )

```shell
#!/bin/bash
NETWORKID=20170125
USER=$(hostname)
MAXPEERS=10
NODE=enode://01df9f9f514a969e525fd93da93e30d4407773dbd619b0b892780de2547921a75c3b86dba69190a2d2c01b8aa7cc1539652b842f9221b2d98fec591239a958ea@34.199.201.240:30303
IP=localhost
geth --networkid $NETWORKID --identity $USER --maxpeers $MAXPEERS --bootnodes $NODE --unlock 0 --password <(echo 123) --rpc --rpcaddr $IP --rpcport 8545 --rpccorsdomain "*"
```

With an additional script `1sttime.sh` ( don't forget chmod +x startgeth.sh )

```
[[ -f /home/pi/.ethereum/geth/chaindata/MANIFEST-000000 ]] && rm /home/pi/.ethereum/geth/chaindata/* && wget https://git.io/vDzbY -O genesis.json && geth init genesis.json
[[ ! -n "$(ls -A /home/pi/.ethereum/keystore)" ]] && geth --password <(echo 123) account new
```

An additional script can be added in `attach.sh` ( don't forget chmod +x attach.sh )

`geth attach ipc:.ethereum/geth.ipc`

### GETH Node Security

The Go Ethereum client is able to function in various ways depending on what protocol is enabled at start-up. 

By default **geth** runs with **[IPC - Inter-process communication](https://en.wikipedia.org/wiki/Inter-process_communication "IPC")** open enabling communication within the environment. 

```
    IPC:
    +--------------machine-------------+
    | [geth node] <==> [other program] |
    +----------------------------------+
```

In addition, to that, **geth** can run with RPC - JSON remote procedure call protocol enabling communication with external environments as well. 

```
    RPC:
              +----------------+----------------------------------+
              |                +---------------machine------------+
    [Internet | Intranet] <==> | [geth node] <==> [other program] |
              |                +---------------machine------------+
              +----------------+----------------------------------+
```

The best and most secure way is to disable `ipc` with --ipcdisable and to never enable `rpc`. 

`echo '{"jsonrpc":"2.0","method":"ipc_modules","params":[],"id":1}' | nc -U .ethereum/geth.ipc`

Another useful security tip is to only enable rpc for specific IPs with `--rpccorsdomain "172.0.*.*"` otherwise use `--rpccorsdomain "*"`. The main apis are enabled by default like **web3,db,net,eth,shh** but not **~~admin,debug,txpool,miner~~**

The address of the RPC can be forced with `--rpcaddr 172.0.0.2` or sometimes you can put the dns directly or the public IP like `--rpcaddr website.com` .  

The `rpc` can be deactivated from the console or from `ipc` with 

`admin.stopRPC() `

and activated with ( assuming this is on the intranet )

`admin.startRPC("127.0.0.2", 8545, "*")`

a simple way to test if the RPC protocol is working is:

`curl -X POST --data '{"jsonrpc":"2.0","method":"rpc_modules","id":1}' http://localhost:8545`

**! RPC can be deactivated and re-activated using with no filter with IPC.**

`echo '{"jsonrpc":"2.0","method":"admin_stopRPC","id":1}' | nc -U .ethereum/geth.ipc`

`IP=$(hostname -I | rev | cut -c 2- | rev ) && echo '{"jsonrpc":"2.0","method":"admin_startRPC","params":["'$IP'"],"id":1}' | nc -U .ethereum/geth.ipc`

All in one line

```
echo 'echo '\''{"jsonrpc":"2.0","method":"admin_stopRPC","id":1}'\'' | nc -U .ethereum/geth.ipc' >> ipcstop.sh && chmod +x ipcstop.sh

echo 'IP=$(hostname -I | rev | cut -c 2- | rev ) && echo '\''{"jsonrpc":"2.0","method":"admin_startRPC","params":["'\''$IP'\''"],"id":1}'\'' | nc -U .ethereum/geth.ipc' >> ipcstart.sh && chmod +x ipcstart.sh
```

In addition to this, you can have the main ethereum account always locked or unlock at start-up with a special description key stored on a removable media drive at start-up with `mount -t vfat -o rw /dev/sda1 /media/usbstick/` . Store the passphrase in a text file there and use it to unlock the wallet with `--password /media/usb/pwd --unlock 0` for example.

Finally you can use an external device and therefore an external script to sign transactions. 

For that , the best option is **[ethjs-signer for node.js](https://www.npmjs.com/package/ethjs-signer)** like the following example:

```javascript
const HttpProvider = require('ethjs-provider-http');
const Eth = require('ethjs-query');
const eth = new Eth(HttpProvider('http://localhost:8545'));
const sign = require('ethjs-signer').sign;
 
const address = '0x0F6af8F8D7AAD198a7607C96fb74Ffa02C5eD86B';
const privateKey = '0xecbcd9838f7f2afa6e809df8d7cdae69aa5dfc14d563ee98e97effd3f6a652f2';
 
eth.getTransactionCount(address).then((nonce) => {
  eth.sendRawTransaction(sign({
    to: '0xce31a19193d4b23f4e9d6163d7247243bAF801c3',
    value: 300000,
    gas: new BN('43092000'),
    nonce: nonce,
  }, privateKey)).then((txHash) => {
    console.log('Transaction Hash', txHash);
  });
});
```

## Install NodeJS

First the most common used packages like `git`

`sudo apt-get -y install curl git`

Optional install build essentials

`sudo apt-get -y install build-essential`

Then install Node 6.x by simply executing the script from their main site with:

`curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -`

Then

`sudo apt-get install -y nodejs`

Optional, install **ExpressJs** 

`sudo npm install -g express`

## Install Truffle

Install Truffle node packages with

`sudo npm install -g truffle`

## Install TestRPC

`sudo npm install -g ethereumjs-testrpc`

## Launch testrpc 

to see if everything works fine with **[testrpc](https://github.com/ethereumjs/testrpc)** run the following perhaps with blocktime 10 to make it seem like a real chain (it is always a good idea to close `geth` to avoid conflicts). 

`testrpc -b 10`

You can put a different hostname with

`testrpc -b 10 -h $(hostname -I)`

You can put a specific private key with

`--account="0xaa73b5c98e60d589e71ce7cff59c02f82e12c7ce676ee356da8e058a285ccd61,100000"`



## Test Truffle project

Init a truffle project (first create the folder as described in the **[truffle doc tutorial](http://truffleframework.com/tutorials/building-testing-frontend-app-truffle-3)**)

`mkdir myproject`

`cd myprojet/`

then

`truffle init webpack`

`truffle compile`

The **private blockchain** or **testnet blockchain** or **testrpc** should be launched

Deploy contracts on local chain 

`truffle migrate`

This should create a transaction or two

Finally build your front-end with

`npm run build`

Launch the testing server

`truffle serve`

if this shows errors, you can use in `build/`

`python -m SimpleHTTPServer 8080`

You can now use localhost or your intranet ip address to access the front-end

# Raspberry Pi Camera Script

You can use just for making the project simple, the **[Raspberry Pi Camera V2 Camera Module](http://uk.rs-online.com/web/p/video-modules/9132664/)** to collect data, either still snap-shots or hashes of stills or use a special script for Recognizing QR Codes like **[Qrcode Reader for NodeJS](https://www.npmjs.com/package/qrcode-reader)** or a sensor like the **[Raspberry Pi Sense Hat
](http://uk.rs-online.com/web/p/interface-development-kits/8949310/)**

Focusing on the Raspberry Pi Camera module, you need to first activate the camera with : 

`sudo raspi-config`

Then select **Enable Camera**

You have to plug in the camera correctly so make sure to follow the instructions from the **[How to install Raspberry Pi camera board](http://xmodulo.com/install-raspberry-pi-camera-board.html)** article. 

You can take still snap-shots with :

`raspistill -t 1 -o output.jpg`

Where `-t` is the delay time before activating the camera and `-o` is of course the output.

You can also reduce the resolution with 

`raspistill -w 640 -h 480`

We can use NodeJs to execute `raspistill`. For that we need to use `require('child_process')` .

For example 

```javascript
cprocess = require('child_process'); cprocess.exec('raspistill -o pia0.jpg', function (){});
```

will run the camera for a short period of time and generate a Jpeg file:

`pia0.jpg`

## camera.js

```javascript
//********************************//
// Take a still shot of and obj   //
// using the raspberry pi camera  //
// Usage: node camera [out.jpg]   //
//********************************//

var defaultfname = "pia0.jpg";
var fname   = process.argv[2] == undefined ? defaultfname : process.argv[2];
var command = 'raspistill -w 640 -h 480 -t 1 -o  ' + fname; // + ' && echo "password" > ' + fname; // 
cprocess = require('child_process');
cprocess.exec(command, function (error, stdout, stderr){
	console.log(stdout);
	if(!error) console.log(fname + ' done!');
});

```

# Hash

For this project it is enough to use a simple hash function like **[MD5](https://en.wikipedia.org/wiki/MD5)(the most common message digest algorithms)**. E.g.: `d41d8cd98f00b204e9800998ecf8427e`

We can use another **NodeJs** require like `require('crypto')` and to handle **files** use `require('fs')`

## hash.js

```javascript
//********************************//
// Calculate the md5 hash of a    //
// file based on input argument   //
// Usage: node hash [file]        //
//********************************//

var defaultfname = "pia0.jpg";
var fname   = process.argv[2] == undefined ? defaultfname : process.argv[2];
var f = require('fs').ReadStream(fname); 
var md5sum = require('crypto').createHash('md5');
 
f.on('data', function(d){ 
	md5sum.update(d); 
}).on('end', function() { 
	console.log(md5sum.digest('hex')); 
});

```

# Contract New ( Deploy a new solidity smart contract )

To keep thing simple for storing hashes or storing sensor information, a 6 lines of code smart contract is enough. 

```java
pragma solidity ^0.4.0
contract SimpleStorage {
  bytes32 public storedData = " ";
  function set(bytes32 x) {
    storedData = x;
  }
}
```

This can be directly compiled in the geth console with `eth.compile.solidity( source )` or using  **[Browser Solidity](http://ethereum.github.io/browser-solidity/#version=soljson-v0.4.8+commit.60cc1668.js)** aka **[remix](https://remix.ethereum.org/)**

## contractnew.js

```javascript
//*****************************************//
// Send transaction with a smart contract  //
// wait until it's mined and get address   //
// Usage: node contractnew | miner.start() //
//*****************************************//

var Web3 = require('web3');
var web3 = new Web3();

web3.setProvider( new web3.providers.HttpProvider('http://localhost:8545') );

var eth = web3.eth;

if (me = eth.coinbase) console.log("Connected to RPC localhost:8545 !");

// pragma solidity ^0.4.0
source = 'contract SimpleStorage { ' +
'  bytes32 public storedData = " ";' +
'  function set(bytes32 x) {' +
'    storedData = x;' +
'  }' +
'}';

// var code = eth.compile.solidity( source ).SimpleStorage.code; // pragma solidity ^0.4.0
var code =	/*'0x60606040527f200000000000000000000000000000000000000000000000000000000000000060'+
			'006000505560408060376000396000f3606060405260e060020a60003504632a1afcd98114602457'+
			'8063db80813f14602c575b005b603660005481565b6004356000556022565b6060908152602090f3';*/
			'0x60606040527f200000000000000000000000000000000000000000000000000000000000000060'+
			'006000505560488060376000396000f3606060405260e060020a60003504632a1afcd98114602657'+
			'8063db80813f146032575b6002565b34600257603e60005481565b34600257600435600055005b60'+
			'60908152602090f3';
// var abi  = eth.compile.solidity( source ).SimpleStorage.info.abiDefinition;
var abi = 
	/*	[ {	"constant":true,
		  	"inputs":[],
		  	"name":"storedData",
		  	"outputs":[{"name":"","type":"bytes32"}],
		  	"type":"function"},
		  { "constant":false,
		  	"inputs":[{"name":"x","type":"bytes32"}],
		  	"name":"set",
		  	"outputs":[],
		  	"type":"function"}	]; //old */

		[ {	"constant":true,
			"inputs":[],
			"name":"storedData",
			"outputs":[{"name":"","type":"bytes32"}],
			"payable":false,"type":"function"},
		{	"constant":false,
			"inputs":[{"name":"x","type":"bytes32"}],
			"name":"set",
			"outputs":[],
			"payable":false,
			"type":"function"}	];

// [ {	"constant":true,"inputs":[],"name":"storedData","outputs":[{"name":"","type":"bytes32"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"x","type":"bytes32"}],"name":"set","outputs":[],"payable":false,"type":"function"}	];

var filterlast = eth.filter('latest');

var estimatedgas=eth.estimateGas( { data : code } );

				// eth.contract(abi).at("0x0")

var myContract = eth.contract(abi).new( { from: me, data: code, gas : estimatedgas }, function(e,c){  //var MyContract = eth.contract(abi);
	if(!e) {
		// print out the contract hash
		chash = c.transactionHash;
		if (chash) console.log("Contract Hash: " + chash);
		// Print the status or empty the filter 
		filterlast.watch( function(e,blkhash){
			if (!e) {
				if (eth.getTransactionReceipt(chash)) {
					console.log("Done waiting for mining. Mined at block #%s. Contract %s "	, eth.getBlock(blkhash).number, eth.getTransactionReceipt(chash).contractAddress);
					filterlast.stopWatching(); web3.reset();
				} else {
					console.log("Waiting for mining.  Currently at block #" + eth.getBlock(blkhash).number);
				}
			}

			/*
			if (!e) { 
				if (eth.getBlock(blkhash).transactions.length) {
					console.log("Block number %s with %d transaction(s) mined.", eth.getBlock(blkhash).number, eth.getBlock(blkhash).transactions.length);
					if (eth.getTransactionReceipt(chash)) {
						console.log(eth.getTransactionReceipt(chash).contractAddress);
						filterlast.stopWatching(); // web3.reset();
					}
				} else {
					console.log("Regular empty block mined. Waiting for the contract to be mined...");
				}
			}*/
		} );

	}
} );


```

# Contract ( call the existing smart contract )

We don't necessary need to build the smart contract object in memory to call the smart contract. The only function needed is `personal.sendTransaction` or to make it more simple, `eth.sendTransaction(` **`object`** `)` . The full object for send transaction contains more than just **from** , **to** and **value**. There is also **gas**, **gasPrice**, nonce and **data** but let's focus on **data**.

```
object = {
	from: me, 
	to: ct, 
	data: data,
}
```

The data is basically the has data but the `set(bytes32)` function selector prepends the hash. 

Since the contract has one function in it and the name of this function is `set` and the argument is a `bytes32` argument, 

```java
contract SimpleStorage { 
  bytes32 public storedData = " ";
  function set(bytes32 x) {
    storedData = x;
  }
}
```

The Function Selector, function selection of `set(bytes32)`, is the **first four bytes** of the **Keccak (SHA-3)** hash of the signature of the function. 

This means , `web3.sha3( fselector )` will output : "0x**db80813f**eaa91d0c6e9c6f6e47edc15732470a1f66e0e49b3228eb40d85e0037" and therefore the first 4 bytes after 0x are **db80813f**

After the signature we have to append the hash, for example **md5('password')** = **"d41d8cd98f00b204e9800998ecf8427e"** = **"6434316438636439386630306232303465393830303939386563663834323765"** (converted from Ascii) meaning the final data :  **db80813f**6434316438636439386630306232303465393830303939386563663834323765

```
eth.sendTransaction( {
	from: me, 
	to: ct, 
	data: 'db80813f6434316438636439386630306232303465393830303939386563663834323765',
} )
```

## contract.js

```javascript
//******************************************//
// Send transaction w/ data smart contract  //
// wait until transaction is mined          //
// Usage: node contract hash 0x123 | miner.s //
//******************************************//

var Web3 = require('web3');
var web3 = new Web3();

    web3.setProvider( new web3.providers.HttpProvider('http://localhost:8545') ); 

var eth = web3.eth;

if (me = eth.coinbase) console.log('Connected to RPC localhost:8545 !');

var defaulthash = 'd41d8cd98f00b204e9800998ecf8427e';
var hash = process.argv[2] == undefined ? defaulthash : process.argv[2];
var x = hash; // set the value as in the argument for the function x

var defaultctaddress = '0x54497301d7663f0c3833b05c58d38e00a62ef1cc'; // '0xb02834a91f8d79a484a7b4c0c824797cd0df60ca';
var ctaddress = process.argv[3] == undefined ? defaultctaddress : process.argv[3]; console.log( ctaddress );


/*source = 
'contract SimpleStorage { ' +
'  bytes32 public storedData = " ";' +
'  function set(bytes32 x) {' +
'    storedData = x;' +
'  }' +
'}';*/

// var abi  = eth.compile.solidity( source ).SimpleStorage.info.abiDefinition;
var abi = 
	/*	[ {	"constant":true,
		  	"inputs":[],
		  	"name":"storedData",
		  	"outputs":[{"name":"","type":"bytes32"}],
		  	"type":"function"},
		  { "constant":false,
		  	"inputs":[{"name":"x","type":"bytes32"}],
		  	"name":"set",
		  	"outputs":[],
		  	"type":"function"}	]; //old  */
		[ {	"constant":true,
			"inputs":[],
			"name":"storedData",
			"outputs":[{"name":"","type":"bytes32"}],
			"payable":false,"type":"function"},
		{	"constant":false,
			"inputs":[{"name":"x","type":"bytes32"}],
			"name":"set",
			"outputs":[],
			"payable":false,
			"type":"function"}	];		  	
// abi = [{"constant":true,"inputs":[],"name":"storedData","outputs":[{"name":"","type":"bytes32"}],"type":"function"},{"constant":false,"inputs":[{"name":"x","type":"bytes32"}],"name":"set","outputs":[],"type":"function"}];
						 
/*String.prototype.rpad = function(padString) {
	var str = this;
    while (str.length-2 < 64)
        str = str + padString;
    return str;
}*/

var pad = '0000000000000000000000000000000000000000000000000000000000000000';
x = web3.fromAscii(x).slice(2); // 61
x = x + pad.substr( x.length ); // 6100000000000000000000000000000000000000000000000000000000000000

// 0xdb8081 (db80813f)
var fselector = abi[1].name + '(' + abi[1].inputs[0].type + ')'; // 'set(bytes32)' Function Selector. It is the first four bytes of the Keccak (SHA-3) hash of the signature of the function
fselector = web3.sha3( fselector ).slice(2,10);

var data = '0x' + fselector + x; // 0xdb80813f6100000000000000000000000000000000000000000000000000000000000000

var filterlast = eth.filter('latest');

eth.sendTransaction( { from: me, to: ctaddress, data: data }, function(e,c){  // eth.contract(abi).at(ctaddress).set
	if(!e) {
		// print out the contract hash
		if (c) console.log("Transaction to Contract Hash: " + c);
		// Print the status or empty the filter 
		filterlast.watch( function(e,blkhash){
			if (!e) {
				if (eth.getTransactionReceipt(c)) { 
					console.log("Done waiting for mining. Mined at block #%s. ", eth.getBlock(blkhash).number);
					filterlast.stopWatching(); web3.reset();
				} else {
					console.log("Waiting for mining.  Currently at block #" + eth.getBlock(blkhash).number);
				}
			}
		} );
	}
} );



```

# All Together

Finally we can put all together in one script. 

To run the camera take **still snap-shot function** and the **hash function** after that and and finally the **contract function** at a specific time we can use a **crontab** , `crontab -e` to be more exact and add `m h  dom mon dow   command` , or another require like `schedule = require( 'node-schedule' )` and then `schedule.scheduleJob( rule , function () { ... } )`. 

We can put all together in a javascript like the one below:

```javascript
//**********************************//
// Take a still shot of and obj     //
// using the raspberry pi camera    //
// Usage: camera(['out.jpg'], [cb]) //
//**********************************//
var camera = function(fname, callback){

// TODO: ADD THE CODE HERE

}

//********************************//
// Calculate the md5 hash of a    //
// file based on input argument   //
// Usage: hash([file], [cb])      //
//********************************//
hash = function(file, callback){

// TODO: ADD THE CODE HERE

}

//******************************************//
// Send transaction w/ data smart contract  //
// wait until transaction is mined          //
// Usage: contract( [hash], [0x123] ) | miner.s //
//******************************************//
contract = function(hash, ctaddress){

// TODO: ADD THE CODE HERE

}

var schedule = require( 'node-schedule' ); 
var rule = new schedule.RecurrenceRule();
rule.second = (new Date()).getSeconds() + 1; // Start in ~1 sec 
rule.minute = [ new schedule.Range(0,59) ]; // Repeat scheduled job every minute
var iteration = 0;

var cron = schedule.scheduleJob(rule, function(){  ;

	console.log('Creating frame number: #%s using Pi Cam A.', iteration);
	n = 'pia' + iteration + '.jpg';
	camera( n, function(e,r){ 
		if(!e) hash( n, function(e, h){ 
			if (!e) { // console.log('Done creating the hash. pia' + iteration + '-' + h );
				contract( h ); 
				iteration++;
			}
		} );
	} );
} ); if (iteration>180) cron.cancel();
```

# License

MIT

# Acknowledgements

To all my friends :)
