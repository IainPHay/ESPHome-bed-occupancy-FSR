# ESPHome-bed-occupancy-FSR in Homeasistant

Bed sensor based on FSR for double bed works for each side. One resistor (60cm) is fixed to a slat on each side underneath middle of sleeping position. Each sensor is soldered to bell wire and heat shrink used to reinforce the join. Tapes are stuck down but each strip is also held down with wap of masking tape all around the slat to protect it as mattress is on ottoman and slides. this seems to work well.

One ESP32 is used and connects to both. Project built following 

https://community.home-assistant.io/t/fsr-the-best-bed-occupancy-sensor/365795

FSR obtained from Pihut in UK:

https://thepihut.com/products/extra-long-force-sensitive-resistor-fsr

As per the details in the above thread it is important to get the resistor between the 3.3V line and the resistor right. The easiest way to measure this is a multimeter connected to the wire soldered to each resistor, use a crocodile clip or a wago connector clipped onto the probe and wire. Measure the resistance with bed occupied and unoccupied, I found that a little tweaking of the resistance given gave the best range.

Resistance needed is Sqrt (In bed*out of bed)

Connect the 2 resistors between the 3.3V pin and the ADC pin used for each FSR, connect one wire from the FSR to the respective ADC pin and the other to a ground pin, you can use different ground pins if you want.

Example code is attached. You also need to set up two input numbers in Home assistant, min 0, max 3.5 and step 0.05. The input number trigger level needs to be set to a voltage between the bed unoccupied and occupied on that side. 

The occupancy sensor can be used for whatever you want, turning a lowlevel light on if up in night is one example. I also use node red with an and gate to estabish when bout people up in the morning to open all the blinds, turn on the kettle etc.

Further details to add
