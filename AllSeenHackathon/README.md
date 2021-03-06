
![Alt text](http://www.octoblu.com/wp-content/uploads/2014/06/octoblu-300x76.png)

#Octo-Pi Setup

##Burn Image to SD Card

For this part you will need an 8gb SD card.


Follow [these instructions](http://lifehacker.com/how-to-clone-your-raspberry-pi-sd-card-for-super-easy-r-1261113524) to burn the image.


##Register Private Cloud UUID

Run this command to register a new private cloud. Keep a record of your UUID/TOKEN.

```
curl -X POST -d "type=cloud" http://meshblu.octoblu.com/devices

```

##Configure WiFi

After having burned the OctoPi image to your SD card:

1. Open the root directory of the SD card in a file explorer.
2. Open the file wifi.conf with a text editor.
3. Enter in your wifi credentials. 
4. Save and close the file.

##Configure Private Cloud

1. In the root folder of the SD card open a file named meshconf.sh inside a text editor.
2. Change the UUID/TOKEN to match the one you saved earlier.
3. Save and close.

##First Run

1. Put the SD card in your rasperry pi.
2. Place a raspian compatible USB wifi adapter in one of the USB ports
3. Plug an Arduino compatible board with the StandardFirmata sketch loaded to the Pi.
4. Power on the Pi (plug in the 5V usb adapter).

OctoPi should automatically boot up, run the Meshblu Server, a [bindPhysical](https://github.com/octoblu/serial/tree/master/examples/firmata/bindPhysical) script or in the case of the rally fighter it will be a script in /nodescripts/RallyFighter called win.js, connect to the wireless network 
and then register to the Meshblu Parent cloud.

Here are the list of import files and directories:

/meshblu - this is your private cloud folder
/nodescripts - This has some nifty scripts and things built for the Rally Fighter Specifically
/serial/examples/firmata/bindPhysical - a way to interface to an Arduino
/home/pi/alljoyn - This is where alljoyn is located! There is a tutorial below. This is the alljoyn NPM module, lots of info there.

##Figuring out your IP Headless

If all went well your Private Meshblu cloud would have reported its IP address to the Parent Cloud. With a simple rest call
we can obtain this ip address in order to SSH in.

```
curl -X GET http://meshblu.octoblu.com/devices/{meshblu uuid} --header "skynet_auth_uuid: {meshblu uuid}" --header "skynet_auth_token: {meshblu token}"
```

##Alljoyn


![Alt text](http://media.marketwire.com/attachments/201402/220921_allseen-alliance-logo.jpg)

The OctoPi image comes pre-loaded with the Alljoyn node.js module. Its locally installed in your Pi's home directory.

/home/pi/alljoyn

There some sample scripts included.

For detailed documentation goto the [Alljoyn npm Github repo](https://github.com/octoblu/alljoyn).

IMPORTANT: Before doing the following you'll need to set up Gateblu on your laptop https://github.com/octoblu/gateblu 

1. Run npm install skynet-alljoyn on the gateway
2. Connect your web browser the car's meshblu instance:

{ip address}/jsconsole

3. Run this from the browser console to add the alljoyn subdevice:

```
conn.gatewayConfig({
    uuid:  '{gateway uuid}',
    token: '{gateway uuid}',
    method: 'createSubdevice',
    type: 'skynet-alljoyn',
    name: 'alljoyn', options:{
      advertisedName: 'test',
      interfaceName: 'org.alljoyn.bus.samples.chat',
      findAdvertisedName: 'org.alljoyn.bus.samples.chat',
      signalMemberName: 'Chat',
      messageServiceName: '/chatService',
      relayUuid: '*'
    }
  }, function(results){ console.log(results); });

```

4. Open Nodeblu and configure the following flow: Inject > Javascript > SkyNet gateway

![cursor_and_nodeblu](https://cloud.githubusercontent.com/assets/1184415/4019977/463abd7a-2a9b-11e4-9ed4-00ca95af2663.png)

5. Add this logic to the javascript function:

```
msg.subdevice="alljoyn";
msg.payload={"method":"notify", "message":"do your homework!"};
return msg;
```

6. Click Inject!

##Using NodeBlu to control a remote Arduino connected to OctoPi Meshblu Private cloud


###Your Arduino Device Credentials
You can goto /serial/examples/firmata/bindPhysical and add a new UUID/TOKEN but by default they are:
```
UUID
05fc6570-27f7-11e4-b242-8ff2c8c79338

Token
00sovuic32gr2j4iydzspejkwxldte29
```

1. Install and Open [NodeBlu](https://chrome.google.com/webstore/detail/nodeblu/aanmmiaepnlibdlobmbhmfemjioahilm?hl=en-US)
2. Goto Tools->Extensions and enable Developer Mode
3. Enter "chrome://flags" into your address bar.
4. Enable debugging for packed apps.
5. Goto your open Nodeblu app.
6. Right click anywhere and click "Inspect Background Page"
7. In the command line at the bottom of the window type replacing IP:

```
setupConn('http://YOUR-PRIVATE-CLOUD-IP', 80, function(data){ console.log('hi', data); } );

```

8. Drag in a new Arduino node.
9. Double click the Arduino node and select Remote Device
10. Select at new device from the skynet_device drop down menu.
11. Enter in your arduino UUID.
12. Change Pin to 13 and hit save.
13. Drag in an Inject node.
14. Double click the inject node and set payload type to string.
15. Enter in either a 1 or 0. 
16. Now hit save.
17. Make a wire connection (drag the dot from the right end of the inject node) to the Arduino node.
18. Hit Deploy!


After you hit deploy you will be able to send payloads to this node to control Digital/Analog pins and Servos!


#Interfacing to Rally Fighter

###Rally Fighter Private cloud UUID
```
c43462d1-1cea-11e4-861d-89322229e557
```

###Rally Fighter Johnny-five script UUID
```
3c701ab0-2a69-11e4-ba29-b7d9779a4387
```

###To control the rally fighter from the main Meshblu cloud (from anywhere in the world) using NodeBlu
```
c43462d1-1cea-11e4-861d-89322229e557/3c701ab0-2a69-11e4-ba29-b7d9779a4387

```
Here are the respective payloads for each control:

Wipers on = { m : "wipe" } 
Wipers off { m : "stopwipe" } 
Hazards On = { m : "hazardon" } 
Hazards Off = { m : "hazardoff"} 
Lock = { m : "lock"} 
Unlock = { m : "unlock"}
Left Headlight On = {m : "headlighton"}
Left Headlight Off = {m : "headlightoff"}

In a function node you could put
```
if(msg.payload){

msg.payload = { m: 'wipe'};

return msg;
}
```

During the hackathon you can send just the payload to UUID 6a1c4491-0e1f-11e4-ba98-ed547cf24cbd and it will function similarly. 

If any payload is passed to afunction node like the one above it will pass a payload of { m : "wipe"} to its outlet.
Wire it up a skynet out node to the UUID c43462d1-1cea-11e4-861d-89322229e557/3c701ab0-2a69-11e4-ba29-b7d9779a4387 and it will pass it to the rally fighter. 

