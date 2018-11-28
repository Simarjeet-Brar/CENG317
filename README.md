# TSL2561 - Light Sensor

A sensor which detect someone's presence in the room to turn ON/OFF atuomatic light system.

# Purpose:

Most of the energy gets wasted due to inproper handling i.e. leaving lights open when no ones is there. Also most of the outdoor and street lights are manually operated using light sensors we can put them on auto switch using light sensors which can save power.

# Component Requirements:

In order to build this project these are the essential components that you need:

- [x] Raspberry pi
- [x] TSL2561 Lux/Light Sensor
- [x] Jumper wires and breadboard to test out temporary circuit 
- [x] PCB board with final circuit printed on it with correct <b>address</b>
- [x] Socket Header to attach sensor and pi together on PCB
- [x] Case to hold ciruit together and prevent it from damage  

## Overall Budget will be approxmately as below:

![capture](https://user-images.githubusercontent.com/43556409/49119932-94b9c500-f278-11e8-9148-525e369e3618.PNG)

For me most of the components were provided by Humber College it costed me around $155

## Time Commitment 

Before we start it is important to make a schedule to keep us on track that will help us to check if everything is going as planed. 
Keep on checking if there were any delays and try to work accordingly.

![a](https://user-images.githubusercontent.com/43556409/49120029-ff6b0080-f278-11e8-9c4d-25a53ed098f7.PNG)

# Mechanical Assembly

- Setup raspberry pi

Once you have got your raspberry pi start working on its functionality download required operating System and allow all the permissions required. if you're first time installing os on raspberry pi and don't know how to do it follow: these setps:

---
### Setting up Raspberry Pi
After receiving the order, the first step is installing Raspian on Raspberry Pi.These are the steps for installation as given below:-

#### Step 1: Download Raspbian
It can easily take more than half an hour to download the software.Download Noobs from https://www.raspberrypi.org/downloads/ 

#### Step 2: Unzip the file
The Raspbian disc image is compressed, so you’ll need to unzip it. The file uses the ZIP64 format, so depending on how current your built-in utilities are, you need to use certain programs to unzip it.

#### Step 3: Write the disc image to your microSD card
Select the drive of your SD card in the ‘Device’ dropdown.

#### Step 4: Put the microSD card in your Pi and boot up
Select ‘Write’ and wait for the process to finish which may take around 20 minutes to complete.

---

# Hardare Setup

Once you have installed required OS and softwares in your reaspberry pi time to get your hardware ready.
starting with connections you have to make sure your sensor is at the right address.
In this case required address is <b>Ox49</b>
here is the connection for the address:

![c](https://user-images.githubusercontent.com/43556409/49120745-e9ab0a80-f27b-11e8-8392-84376b9dc8cc.jpeg)

Don't worry if you don't know whats going on follow these instructions:
---
- Connect VIN from sensor to 3.3V first pin of raspberry pi.
- Connect GND (ground) to ground pin 5 on raspberry pi.
- Connect ADDR from sensor to 3.3V as well
- Connect SDA to SDA on pi pin#2
- Connect SCL to SCL on pi pin#3
---

once you get the address open terminal on pi type the following command:

<b>i2cdetect -y 1</b>

you will get the following output:

![address](https://user-images.githubusercontent.com/43556409/49120993-e49a8b00-f27c-11e8-89f5-d8e9b2702336.PNG)

If you didn't get the same output, there is something worng with your circuit.

# PCB and Soldring

Now that you know how to connect your sensor to raspberry pi you can start working on PCB that is to bring circuit that you made on a board permanently. For that you have to carefully design your PCB using software called: Fritzing which will help you to design your PCB it should look like this:

![f](https://user-images.githubusercontent.com/43556409/49121140-6c809500-f27d-11e8-824c-f51ebca9b143.png)

The wires that are yellow in colour are on the top side of the board and orange ones are at the bottom. It is important not to cross two wires on the same side of board or in other words are in same colour. Also, check make sure all the wires that touching pi or sensor are to be soldered on same side hence should be same in colour.

Next step is to get your PCB board made once you have got your PCB ready carefully solder socket headers to the PCB you have to very carefull.
Safty is the first priority so it is important to know what are you working with. If you haven't done soldering before you should get nline help.
For above design I have this PCB ready: 
Top Side:
![t](https://user-images.githubusercontent.com/43556409/49121551-e49b8a80-f27e-11e8-9c9d-2d7057be33c5.jpeg)
Bottom:
![b](https://user-images.githubusercontent.com/43556409/49121553-e5ccb780-f27e-11e8-834c-2c057a4f223c.jpeg)

