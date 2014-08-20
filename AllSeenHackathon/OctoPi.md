
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

OctoPi should automatically boot up, run the Meshblu Server, a bindPhysical script, connect to the wireless network 
and then register to the Meshblu Parent cloud.

##Figuring out your IP Headless

If all went well your Private Meshblu cloud would have reported its IP address to the Parent Cloud. With a simple rest call
we can obtain this ip address in order to SSH in.

```
some code
```
