##Alljoyn


![Alt text](http://media.marketwire.com/attachments/201402/220921_allseen-alliance-logo.jpg)

The OctoPi image comes pre-loaded with the Alljoyn node.js module. Its locally installed in your Pi's home directory.

/home/pi/hardware_examples/node_modules/alljoyn

There some sample scripts included.

For detailed documentation goto the [Alljoyn npm Github repo](https://github.com/octoblu/alljoyn).


1. Goto the [meshblu jsconsole](http://meshblu.octoblu.com/jsconsole)

2. Run this from the browser console to add the alljoyn subdevice:

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

3. Open Nodeblu and configure the following flow: Inject > Javascript > SkyNet Out (in this node add the UUID/TOKEN of your gateway)

![cursor_and_nodeblu](https://cloud.githubusercontent.com/assets/1184415/4019977/463abd7a-2a9b-11e4-9ed4-00ca95af2663.png)

4. Add this logic to the javascript function node:

```
msg.subdevice="alljoyn";
msg.payload={"method":"notify", "message":"do your homework!"};
return msg;
```

6. Click Inject!
