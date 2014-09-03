
![Alt text](http://www.octoblu.com/wp-content/uploads/2014/06/octoblu-300x76.png)

#Octo-Pi Setup

##Burn Image to SD Card

For this part you will need an 8gb SD card.


Follow [these instructions](http://www.raspberrypi.org/documentation/installation/installing-images/) to burn the image to an SD card.


##Register Gateway ( Gateblu ) device.

Run this command to register a new gateway. Keep a record of your UUID/TOKEN.

```
curl -X POST -d "type=gateway" http://meshblu.octoblu.com/devices

```

##Configure WiFi

After having burned the OctoPi image to your SD card:

1. Open the root directory of the SD card in a file explorer.
2. Open the file wifi.conf with a text editor.
3. Enter in your wifi configuration details. (This acts like a standard wpa_supplicant.conf file)
4. Save and close the file.

##Configure Gateblu (Gateway)

1. In the root folder of the SD card open a file named meshconf.sh inside a text editor.
2. Change the UUID/TOKEN to match the one you saved earlier.
3. Save and close.

##First Run

1. Put the SD card in your rasperry pi.
2. Place a raspian compatible USB wifi adapter in one of the USB ports
3. Power on the Pi (plug in the 5V usb adapter).

OctoPi should automatically boot up, run the Gateblu server.

Here are the list of import files and directories:

/home/pi/gateblu : This is where your Gateblu server lives.
/home/pi/hardware_examples : This directory has example scripts for interfacing your Pi's GPIO to Meshblu and Alljoyn.


##Figuring out your IP Headless

If all went well your Gateblu device would have reported its IP address to the Parent Cloud. With a simple rest call
we can obtain this ip address in order to SSH in.

```
curl -X GET http://meshblu.octoblu.com/devices/{gateblu uuid} --header "skynet_auth_uuid: {gateblu uuid}" --header "skynet_auth_token: {gateblu token}"
```

##Other Tutorials
[Using Alljoyn](https://github.com/virgilvox/octoblu_tutorials/blob/master/meshblu/pi/alljoyn.md)
[Controlling the Rally Fighter](https://github.com/virgilvox/octoblu_tutorials/blob/master/meshblu/pi/rally_fighter.md)
[Remote Arduino](https://github.com/virgilvox/octoblu_tutorials/blob/master/meshblu/pi/remote_arduino.md)

