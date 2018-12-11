# TSL2561 - Light Sensor

A sensor which detect someone's presence in the room to turn ON/OFF atuomatic light system.

![whatsapp image 2018-11-27 at 1 37 44 pm](https://user-images.githubusercontent.com/43556409/49169073-fde81980-f306-11e8-8c90-9055aa69f01d.jpeg)

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

## Setup raspberry pi

Once you have got your raspberry pi start working on its functionality download required operating System and allow all the permissions required. if you're first time installing os on raspberry pi and don't know how to do it follow these setps:

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

# Hardware Setup

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

Now that you know how to connect your sensor to raspberry pi you can start working on PCB that is to bring circuit that you made on a board permanently. For that you have to carefully design your PCB using software called Fritzing which will help you to design your PCB it should look like this:

![f](https://user-images.githubusercontent.com/43556409/49121140-6c809500-f27d-11e8-824c-f51ebca9b143.png)

The wires that are yellow in colour are on the top side of the board and orange ones are at the bottom. It is important not to cross two wires on the same side of board or in other words are in same colour. Note both sensor and Rpi should be soldered on each side of the board. Also, make sure all the wires that are touching the pi pins are to be soldered on top side hence should be same in colour same(yellow) and for sensor pins are going to be at bottom.

Next step is to get your PCB board made once you have got your PCB ready carefully solder socket headers to the PCB you have to very carefull.
Safety is the first priority so it is important to know what are you working with. If you haven't done soldering before you should get  help from someone with experience or from youtube videos.
For above design I have this PCB should look like this.

![t](https://user-images.githubusercontent.com/43556409/49833899-f2fea180-fd68-11e8-8358-18ec1be0048a.jpeg)	![b](https://user-images.githubusercontent.com/43556409/49833897-f134de00-fd68-11e8-8739-f2a3ebf3fe29.jpeg)

After that you can just attached your sensor and raspberry pi to PCB. Make sure all the wires are connected and your sensor is at the correct address.

![whatsapp image 2018-11-27 at 1 37 44 pm](https://user-images.githubusercontent.com/43556409/49169073-fde81980-f306-11e8-8c90-9055aa69f01d.jpeg)

# Get Data/Sensor Readings

So at this point you should have your raspberry pi and sensor ready to use to read data. To get data from sensor and display it in human readable form we have ro run a script you can program that in java/c/python. Here i am ruuning this python code over here.
Python Script Download [here](https://github.com/Simarjeet-Brar/CENG317/tree/master/TSL2561%20Scripts/TSL2561%20Scripts/Python)

```
import smbus
import time

while True:
		# Get I2C bus
		bus = smbus.SMBus(1)

		# TSL2561 address, 0x49(57)
		# Select control register, 0x00(00) with command register, 0x80(128)
		#		0x03(03)	Power ON mode
		bus.write_byte_data(0x49, 0x00 | 0x80, 0x03)
		# TSL2561 address, 0x49(57)
		# Select timing register, 0x01(01) with command register, 0x80(128)
		#		0x02(02)	Nominal integration time = 402ms
		bus.write_byte_data(0x49, 0x01 | 0x80, 0x02)

		time.sleep(0.5)

		# Read data back from 0x0C(12) with command register, 0x80(128), 2 bytes
		# ch0 LSB, ch0 MSB
		data = bus.read_i2c_block_data(0x49, 0x0C | 0x80, 2)

		# Read data back from 0x0E(14) with command register, 0x80(128), 2 bytes
		# ch1 LSB, ch1 MSB
		data1 = bus.read_i2c_block_data(0x49, 0x0E | 0x80, 2)

		# Convert the data
		ch0 = data[1] * 256 + data[0]
		ch1 = data1[1] * 256 + data1[0]

		# Output data to screen
		print "---------------------------------"
		print "Full Spectrum(IR + Visible) :%d lux" %ch0
		print "Infrared Value :%d lux" %ch1
		print "Visible Value :%d lux" %(ch0 - ch1)
		time.sleep(5)
```

As you can see in code its geting redaings from address Ox49 and converting it into integer. I am also using a loop here which will get readings every 5 seconds.
so can you compile and run the above code to get readings.

# Data Display

If you run the above script you should be able to get readings on screen......

![r](https://user-images.githubusercontent.com/43556409/49171345-52da5e80-f30c-11e8-9374-0f1c3e677f76.PNG)

![r2](https://user-images.githubusercontent.com/43556409/49171347-540b8b80-f30c-11e8-8c70-6986534afb44.PNG)

You can test sensor by changeing the reading for example use your phone's flash light to raise and cover it by your hand to decrease the amount of light on your sensor.

# Enclosure

If you reach upto this point that means you did a great job lets see what we have achieved so far.
Lets complete a check list:

- [ ] Everything is going according to schedule
- [ ] Raspberry pi and Sensor working as expected
- [ ] Sensor is on right address and we are geting readings
- [ ] Readings are changing accroring to presence of light

If everything mention above is checked You're good!. 
Last but not least, you may want to build a case to protect your pi and prevent it from damage.

To build case for your pi you have to software called <font color="red">Corel Draw</font>

To build a case that is perfect for your pi first thing to do is to get all the measurements for example Height, Width, Length. 
If you don't know how to use corel draw when visit their website for [help](https://www.coreldraw.com/en/pages/tutorials/coreldraw/)
After you got your case pieces sperated using leaser cut, you can combine them to get perfect case:

![c](https://user-images.githubusercontent.com/43556409/49172748-de092380-f30f-11e8-9b7a-511d0ce77400.JPG)

# Production Testing 
