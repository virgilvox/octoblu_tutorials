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
2. Drag in a new Arduino node.
3. Double click the Arduino node and select Remote Device
4. Select at new device from the skynet_device drop down menu.
5. Enter in your arduino UUID.
6. Change Pin to 13 and hit save.
7. Drag in an Inject node.
8. Double click the inject node and set payload type to string.
9. Enter in either a 1 or 0. 
10. Now hit save.
11. Make a wire connection (drag the dot from the right end of the inject node) to the Arduino node.
12. Hit Deploy!


After you hit deploy you will be able to send payloads to this node to control Digital/Analog pins and Servos!
