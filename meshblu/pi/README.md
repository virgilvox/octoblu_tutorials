#Getting Started


##Burn Image to SD Card
http://lifehacker.com/how-to-clone-your-raspberry-pi-sd-card-for-super-easy-r-1261113524


##Upgrade/Update
```
sudo apt-get update
sudo apt-get upgrade
```

##Git Clone Meshblu
```
sudo apt-get install git-core

cd /
sudo git clone https://github.com/octoblu/meshblu.git
```

##Setup Node.js and NPM

```
sudo wget http://node-arm.herokuapp.com/node_latest_armhf.deb
sudo dpkg -i node_latest_armhf.deb
node -v
```

##Install Meshblu dependancies

```
cd /meshblu
sudo npm install
sudo npm install forever
```

##Create UUID/TOKEN for Private cloud

In OctoBlu, add a new Meshblu Private cloud channel. This will give you a UUID and TOKEN. Have that ready.

##Configure



##Set Up Start up Script


##Set Up Static IP - optional

##bindPhysical

##Alljoyn
