
#Interfacing to Rally Fighter

Examples:
- www.fracture.cc/rally
- www.fracture.cc/rally/rally.zip

###To control the rally fighter from the main Meshblu cloud (from anywhere in the world) using NodeBlu
```
c43462d1-1cea-11e4-861d-89322229e557/3c701ab0-2a69-11e4-ba29-b7d9779a4387

```

Use [NodeBlu](https://chrome.google.com/webstore/detail/nodeblu/aanmmiaepnlibdlobmbhmfemjioahilm?hl=en-US)

To communicate with the rally fighter you will send a message to it's UUID as a payload.

That payload should contain the following JSON objects for control.

Here are the respective payloads for each control:

```
Wipers on = { m : "wipe" } 
Wipers off { m : "stopwipe" } 
Hazards not working currently::
Hazards On = { m : "hazardon" } 
Hazards Off = { m : "hazardoff"} 
Lock = { m : "lock"} 
Unlock = { m : "unlock"}
Left Headlight On = {m : "headlighton"}
Left Headlight Off = {m : "headlightoff"}
```

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

Paste the following into the Nodeblu designer window to get a sample flow to control the rally fighter:
```
[{"id":"d66d899c.299278","type":"skynet-device","uuid":"c43462d1-1cea-11e4-861d-89322229e557/3c701ab0-2a69-11e4-ba29-b7d9779a4387","token":"","name":"private_0","dne":""},{"id":"c21c9baf.3de368","type":"voice","name":"","topic":"","payload":"","payloadType":"string","repeat":"","crontab":"","active":true,"once":false,"x":286,"y":246,"z":"59a6132e.a659ec","wires":[["6f3a9470.90c56c","767d214c.8982e"]]},{"id":"6f3a9470.90c56c","type":"switch","name":"","property":"payload","rules":[{"t":"cont","v":"rain"},{"t":"cont","v":"raining"},{"t":"cont","v":"wipe"},{"t":"cont","v":"sunshine"},{"t":"cont","v":"stopwipe"},{"t":"cont","v":"danger"},{"t":"cont","v":"safe"},{"t":"cont","v":"unlock"},{"t":"cont","v":"lock"},{"t":"cont","v":"crap"},{"t":"cont","v":"hazardon"},{"t":"cont","v":"hazardoff"},{"t":"cont","v":"headlighton"},{"t":"cont","v":"headlightoff"}],"checkall":"true","outputs":14,"x":407,"y":246,"z":"59a6132e.a659ec","wires":[["711939c2.8ee6c8"],["711939c2.8ee6c8"],["711939c2.8ee6c8"],["e87c244e.1783d8"],["e87c244e.1783d8"],["68d684c5.97297c"],["9a84e493.657b18"],["f7c27063.083d9"],["958976de.6a7688"],["68d684c5.97297c"],["68d684c5.97297c"],["9a84e493.657b18"],["d2e088b4.2d1f78"],["ff3b6536.00c498"]]},{"id":"711939c2.8ee6c8","type":"function","name":"trigger wiper","func":"if(msg.payload){\n\nmsg.payload = { m: 'wipe'};\n}else{\n\nmsg.payload = 0;\n\n}\nreturn msg;","outputs":1,"x":641,"y":142,"z":"59a6132e.a659ec","wires":[["e5a6db4b.1a5928"]]},{"id":"e87c244e.1783d8","type":"function","name":"kill wiper","func":"if(msg.payload){\n\nmsg.payload = {m : \"stopwipe\"};\n}\nreturn msg;","outputs":1,"x":634,"y":173,"z":"59a6132e.a659ec","wires":[["e5a6db4b.1a5928"]]},{"id":"9a84e493.657b18","type":"function","name":"Hazards Off","func":"if(msg.payload){\n\nmsg.payload = {m : \"hazardoff\"};\n}\nreturn msg;","outputs":1,"x":635,"y":333,"z":"59a6132e.a659ec","wires":[["e5a6db4b.1a5928"]]},{"id":"68d684c5.97297c","type":"function","name":"Hazards On","func":"if(msg.payload){\n\nmsg.payload = {m : \"hazardon\"};\n}\nreturn msg;","outputs":1,"x":634,"y":298,"z":"59a6132e.a659ec","wires":[["e5a6db4b.1a5928"]]},{"id":"f7c27063.083d9","type":"function","name":"unlock","func":"if(msg.payload){\n\nmsg.payload = { m : \"unlock\" };\nreturn msg;\n}\n","outputs":1,"x":623,"y":395,"z":"59a6132e.a659ec","wires":[["e5a6db4b.1a5928"]]},{"id":"958976de.6a7688","type":"function","name":"lock","func":"if(msg.payload){\n\nmsg.payload = {m : \"lock\"};\nreturn msg;\n}\n","outputs":1,"x":624,"y":432,"z":"59a6132e.a659ec","wires":[["e5a6db4b.1a5928"]]},{"id":"767d214c.8982e","type":"tts","name":"","active":true,"complete":false,"voiceName":"","x":283,"y":408,"z":"59a6132e.a659ec","wires":[]},{"id":"7304bb5c.8cfb44","type":"skynet in","name":"","directToMe":true,"device":null,"x":138,"y":187,"z":"59a6132e.a659ec","wires":[["6f3a9470.90c56c"]]},{"id":"e5a6db4b.1a5928","type":"skynet out","name":"","broadcast":false,"device":"d66d899c.299278","outputs":0,"x":911,"y":336,"z":"59a6132e.a659ec","wires":[]},{"id":"2df78b73.d20874","type":"inject","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"sidebarInput":false,"x":440,"y":357,"z":"59a6132e.a659ec","wires":[["9a84e493.657b18"]]},{"id":"2b9f5ddf.d460a2","type":"inject","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"sidebarInput":false,"x":442,"y":398,"z":"59a6132e.a659ec","wires":[["68d684c5.97297c"]]},{"id":"ad103f21.52efc","type":"inject","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"sidebarInput":false,"x":388,"y":153,"z":"59a6132e.a659ec","wires":[["e87c244e.1783d8"]]},{"id":"f39a97d.f0c6568","type":"inject","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"sidebarInput":false,"x":398,"y":119,"z":"59a6132e.a659ec","wires":[["711939c2.8ee6c8"]]},{"id":"c3daf7e1.3c2508","type":"inject","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"sidebarInput":false,"x":443,"y":442,"z":"59a6132e.a659ec","wires":[["f7c27063.083d9"]]},{"id":"afd89ae4.502768","type":"inject","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"sidebarInput":false,"x":446,"y":477,"z":"59a6132e.a659ec","wires":[["958976de.6a7688"]]},{"id":"d2e088b4.2d1f78","type":"function","name":"Headlight ON","func":"if(msg.payload){\n\nmsg.payload = {m : \"headlighton\"};\n}\nreturn msg;","outputs":1,"x":625,"y":510,"z":"59a6132e.a659ec","wires":[["e5a6db4b.1a5928"]]},{"id":"2dcf5431.d230ac","type":"inject","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"sidebarInput":false,"x":422,"y":533,"z":"59a6132e.a659ec","wires":[["d2e088b4.2d1f78"]]},{"id":"ff3b6536.00c498","type":"function","name":"Headlight OFF","func":"if(msg.payload){\n\nmsg.payload = {m : \"headlightoff\"};\n}\nreturn msg;","outputs":1,"x":634,"y":542,"z":"59a6132e.a659ec","wires":[["e5a6db4b.1a5928"]]},{"id":"1f2012a4.e0dfed","type":"inject","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"sidebarInput":false,"x":431,"y":576,"z":"59a6132e.a659ec","wires":[["ff3b6536.00c498"]]}]
```


Ignore the following for the ATT hackathon.

###Rally Fighter Private cloud UUID
```
c43462d1-1cea-11e4-861d-89322229e557
```

###Rally Fighter Johnny-five script UUID
```
3c701ab0-2a69-11e4-ba29-b7d9779a4387
```
