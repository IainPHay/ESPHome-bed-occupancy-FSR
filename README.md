# ESPHome-bed-occupancy-FSR in Homeassistant

Easy EDA files added.

Bed sensor based on Force Sensitive Resistor (FSR) for double bed works for each side, can just use one side if required. One FSR (60cm recommended) is fixed to a slat on each side underneath the middle of the sleeping position. Each sensor is soldered to bell wire and heat shrink is used to reinforce the join, extreme care is needed to do this as you do not want to melt the plastic tape, you can purchase connectors instead if not confident but it is very easy. I suggest pretinning the bell wire and taping the wire and FSR down to a flat surface with the tinned wire on top of the copper contact area of FSR, a tiny dab with solder iron and solder will make the join. 
The FSR tapes are stuck down to the slat but we recommend each strip is also held down with wrap of masking tape all around the slat just for extra protection.

One ESP32 (36pin) is used and connects to both FSRs. The project was inspired by the following link, some excellent information here, and code taken from here and modified for this particular project.

https://community.home-assistant.io/t/fsr-the-best-bed-occupancy-sensor/365795

FSR used obtained from Pihut in UK:

https://thepihut.com/products/extra-long-force-sensitive-resistor-fsr

One end of each FSR is connected to 3.3V and the other to an ADC pin, an additional resistor is needed to bring signal into a range where the resistance of the FSR when been is occupied and unoccupied can be detected. Following the original project, the  easiest way to measure this is to use a multimeter connected to the wire soldered to each resistor, use a crocodile clip or a wago connector clipped onto the probe and wire. Measure the resistance with bed occupied and unoccupied, it will drift so take an average value, a min max multimeter works very well for this but is not needed! With this PCB you can eliminate this stage if desired as it is not necessary but it does give a good starting point for adjustment I found that a little tweaking over the first few days of use gave the best performance long-term. Change of bedding etc, and sleeping position can affect it but using this PCB with trim pots allows adjustments without needing to replace resistors.

The resistance needed is Sqrt (in bed*out of bed)

Set the trim pot for each side to the value determined, you will need a multimeter connected to the PCB, do not at this stage have the FSR or ESP32 connected. The resistance for each side can be measured between the pin and the 3.3V pin. When you connect this to the FSRs I have found you want to set it so that the out of bed reading from the ESPHome sensor is about 2.9V. Clockwise turns on the trim pot reduce the voltage, you can just do this instead of measuring resistance.

The FSRs can then be connected, one wire from each FSR goes into the 3.3V terminal and then the other wires go into their respective terminals. The ESP32 (previously Flashed with ESPHome code) can be connected along with an i2c device if desired, the example code shows nothing and also an option with BMP280 for temperature and pressure. In addition, an example is given where the Bluetooth on board is also used for iwatch tracking (to add).

I have had some issues with power on the ESP32 I used (suggested ESP32 to be added to BOM) I resolved this by flashing and then connecting it to a decent power supply which seems to sort it.

Example code is attached. 

The occupancy sensor can be used for whatever you want, turning a lowlevel light on if up at night is one example. I also use node-red with an and gate to establish when both people are up in the morning to open all the blinds, turn on the kettle, etc.

PCB
A PCB has been designed to allow for a dual bed sensor with trim pots on the board to allow for resistance adjustment on the device, you can add an i2c device for example a BME280 for room humidity, pressure, and temperature but it's not needed. Schematics and gerbers are in the repo.

![image](https://user-images.githubusercontent.com/25230544/213453713-87fe6fbe-26c4-4dbe-aaa1-92949d8bd352.png)



For example, YAML for both is included, BOM to be added.
