
#Interfacing to Rally Fighter


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


Ignore the following for the ATT hackathon.

###Rally Fighter Private cloud UUID
```
c43462d1-1cea-11e4-861d-89322229e557
```

###Rally Fighter Johnny-five script UUID
```
3c701ab0-2a69-11e4-ba29-b7d9779a4387
```
