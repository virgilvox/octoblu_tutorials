
![Alt text](http://www.octoblu.com/wp-content/uploads/2014/06/octoblu-300x76.png)

#Octo-Pi Setup

##Burn Image to SD Card

For this part you will need an 8gb SD card.

Downloads:
- image link

Follow [these instructions](http://lifehacker.com/how-to-clone-your-raspberry-pi-sd-card-for-super-easy-r-1261113524) to burn the image.


##Register Private Cloud UUID

Run this command to register a new private cloud. Keep a record of your UUID/TOKEN.

```
some code

```

##Configure WiFi

After having burned the OctoPi image to your SD card:

1. Open the root directory of the SD card in a file explorer.
2. Open the file wifi.conf with a text editor.
3. Enter in your wifi credentials. 
4. Save and close the file.

##Configure Private Cloud

1. In the root folder of the SD card open a file named meshstart.sh inside a text editor.
2. Change the UUID/TOKEN to match the one you saved earlier.
3. Save and close.

##First Run

1. Put the SD card in your rasperry pi.
2. Place a raspian compatible USB wifi adapter in one of the USB ports
3. Plug an Arduino compatible board with the StandardFirmata sketch loaded to the Pi.
4. Power on the Pi (plug in the 5V usb adapter).

OctoPi should automatically boot up, run the Meshblu Server, a [bindPhysical](https://github.com/octoblu/serial/tree/master/examples/firmata/bindPhysical) script, connect to the wireless network 
and then register to the Meshblu Parent cloud.

##Figuring out your IP Headless

If all went well your Private Meshblu cloud would have reported its IP address to the Parent Cloud. With a simple rest call
we can obtain this ip address in order to SSH in.

```
some code
```

##Alljoyn

![Alt text](http://smartzona.es/content/uploads/2013/12/alljoyn-logo.jpg)
![Alt text](http://media.marketwire.com/attachments/201402/220921_allseen-alliance-logo.jpg)

The OctoPi image comes pre-loaded with the Alljoyn node.js module. Its locally installed in your Pi's home directory.

/home/pi/alljoyn


For detailed documentation goto the [Alljoyn npm Github repo](https://github.com/octoblu/alljoyn).


##Using NodeBlu to control a remote Arduino connected to OctoPi


###Your Arduino Device Credentials
You can goto /serial/examples/firmata/bindPhysical and add a new UUID/TOKEN but by default they are:
```
UUID
05fc6570-27f7-11e4-b242-8ff2c8c79338

Token
00sovuic32gr2j4iydzspejkwxldte29
```

1. Install and Open [NodeBlu](https://chrome.google.com/webstore/detail/nodeblu/aanmmiaepnlibdlobmbhmfemjioahilm?hl=en-US)
2. Drag in a new Arduino node.
3. Double click the Arduino node and select Remote Device
4. Add a new skynet_firmware device and enter your private cloud UUID backslash your Arduino device UUID.
```
YOUR_PRIVATE_CLOUD_UUID/05fc6570-27f7-11e4-b242-8ff2c8c79338

```

After you hit deploy you will be able to send payloads to this node to control Digital/Analog pins and Servos!
