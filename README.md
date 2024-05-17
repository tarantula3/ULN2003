# All About IC ULN2003

[![vO6adrETQIA](https://i.imgur.com/AZoLrVb.png)](https://youtu.be/dtfGf7kf__g)

The UNL2003 IC contains 7 High Voltage, High Current NPN Darlington Transistor Arrays each rated at 50V, 500mA in a 16-pin DIP package. You can connect the IC directly to a digital logic (like Arduino or Raspberry Pi, TTL or 5V CMOS device) without an external dropping resistor. This IC features "common-cathode flyback diodes" for switching inductive loads. The ULN2003 is known for its high current and high voltage capacity.

The Darlington pairs can be "paralleled" for higher current Output.
The inputs are capable with TTL and 5v CMOS logic.

Now, let's deep-dive and check out the internals of the IC and how it can be used in our projects.


Pin Configuration and Functions
-------------------------------
![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjj2DLHcy1EbPExyBLRnSGOumW_qp9QkXWJu_0LNhsC2w8aE06ZAJSiOUVaAbDMBSvHOLJy9RRNi6b-OM6dy9nNJX1SJCSkXjz5_oWVQnFbtbO6uG6Pg4q8djHcW1ZU3X6osmSU9hhovGaeXlJdQbArY4ObmYv0Pn9fLWBZ8Vf37c1lfVaT87DLYCwJUUF4/w640-h360/1.png)

The notch on the top indicates the starting and stopping points of the numberings of the chip. Starting from left to right going counterclockwise this is the Pin number 1 of the IC. 
* On the left hand side Pin 1 to 7 are the Base Inputs.
* On the right hand side Pin 10 to 16 are the Collector Outputs.
* Pin 9 is the Common Cathode node for flyback diodes (required for inductive loads).
* And, Pin 8 is the Common Emitter shared by all channels of the IC. This pin is typically tied to ground.


Detailed Description
--------------------
![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh-G7nJfZRspOzS0FgmKxPG87djduyH0u_P-wperbKuhvOHzvI-ENVIXpQr5fcJw09NM_k8aGP_AFB6UUD_QftyV9ut30f0FgCwUGLAVbZlHfjKS_WoEMqCfkJzx6iWjAMyTY_8doy7ZDNeMclVT8j_nObkVhb43Eu_iYBd4GnjGdjZbCqX6pI5ikaOllIA/w640-h360/2.png)

Inside the IC is the arrays of the 7 NPN "Darlington Transistors".
Darlington Transistors were first invented in 1953 by Sidney Darlington. A Darlington pair is a circuit consisting of two Bipolar Transistors with the Emitter of one transistor connected to the Base of the other transistor. In this setup, the current amplified by the first transistor is further amplified by the second transistor. 
The collectors of both transistors are connected together. This configuration has a much higher current gain than each transistor taken separately. A small base current can make the pair switch to a much higher current. 

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg12gNqxlxxCehr9pS2RokIPySlyr16U1p3pOYp-By34DIwUiWQk-ouOdO53ggYGLDHx9cPdJKt5LZ5IAo6ljEyyjJIcotl0hL2ZoCPzKjR_CeQKo2x2eY5bMyD-YWyv1tJPbiU77JqcLQ0UG10sZtso1HK2Zr6FScBeHXbiTm5HvxwAsRxm18hVYCm6uLl/s1054/3.png)

It appears as if it is just a single transistor, with only one base, one collector, and one emitter. Creating a high current gain approximately to the product of the gains of the two transistors:
 ```β Darlington = (β 1 * β 2) + β 1 + β 2 ```

Since, β1 and β2 are high enough, we can write the above statement as:
 ```β Darlington ≈ β 1 * β 2 ```
This connection creates the effect of a single transistor with a very high-current gain.

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjGh5ZrI1CZ1Buc3JLoKmIDJCSZj9xRp95r-zjw56DkmCsWp7mcgcts1MwTCqbxfksvL0GsMalo9ZmK-q4B613YFK81RgSgb9wzG6wUa1s0XMu6tTSuZaH9cRLXd7-W4m_D6Tiov0KkY85EPmKIvLIvbjvUbKvED2xXs53Q40PHMEhu38GTdkdP8tc_mg4Z/w640-h360/4.png)

The 7 outputs are all "Open Collector".
By Open Collector, we mean a collector that is not attached to anything. It's just open.
In order for an open collector output device to work, the open collector has to receive sufficient power.
In order for an NPN transistor to work, the collector and the base both need to receive sufficient power. The base turns the transistor on, and then a much greater current flows from collector to emitter, but only if the collector has sufficient positive voltage. 

So if you want to connect a load to the Output of the chip with an open-collector-output, you must attach the load to a positive voltage source that is sufficient enough to drive the load. Hence, the +ve side of the load connects to the +ve voltage rail and the -ve side connects to the OUTPUT pin of the IC.
Hence, when the Base current goes HIGH, the current flows from the collector to emitter and the Output logic goes LOW turning ON the LED (load) connected to the OUT pin of the IC and vice-versa. 

The maximum Output Current of a single OUTPUT pin is 500mA and the total emitter-terminal current is 2.5A as per the datasheet.

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiHvvYFoZRuqN-9lU8s1SygdZXC6Hvwn-xpHlGj-uYtBJZJBixMf9dcs-_BG3fGO76HdAXgA2MAt_3LomSkW4Ro7_hwm0WPtooidsIUpFkk7wFQd52UTUso2p-_vRPIji6QG3fBJemWX1tdKmifemdbR71SYdjlPW1OY44ZCNqMmKPR1sSct0J0L-iMEZSd/w640-h360/5.png)

Now, let's have a closer look at a single Darlington pair (internal circuit diagram) of the ULN2003 IC. 
The GPIO input voltage is converted to base current through a series base 2.7kΩ resistor connected between the Input and Base of the Darlington NPN junction. This allows the IC to connect directly to a digital logic (like Arduino, Raspberry Pi, TTL or 5V CMOS device) without the need of external dropping resistors operating at supply voltages of 5V or 3.3V.

The 7.2kΩ and the 3kΩ resistors connected between the Base and the Emitter of each respective NPN transistor acts as pulldown resistors preventing floating states and suppressing the amount of leakage that may occur from the input.

To maximize the effectiveness, these units contain "Suppression Diodes" for inductive loads. The diode connected between the OUT pin and the COM pin (PIN 9) is used to suppress the "kick-back voltage" from an inductive load which is generated when the NPN drivers are turned off and the stored energy of the coils causes a reverse flow of current.

A reverse biased suppressing diode is also placed between the Base-Emitter and the Collector-Emitter pair to avoid the Parasitic nature of the NPN transistors.

Pin 8 is connected to the GND.


Device Functional Modes
-----------------------
![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjhdgdEBIwS_k10mJlaHKe-WeFLBRKujAux7u0dd39a4Bm-AtAn-L-fb2dFkVjNaHPVICeYoa5PMdEQ4VGgHP-L3UPpTcgKe0xm1P9j_4Wxk4Tq5Jz7WAqoVCXEjM8wb5GXo1rMb0m8dYZMHMEzRfSGSCarHToJH-Ka-0_rLkwMNi0Xl1VZfZtB9VjwEmow/w640-h360/6.png)

Inductive Load
In case of an inductive load, when the COM pin is tied to a coil, the IC is able to drive inductive loads and suppress the kick-back voltage through the internal free-wheeling diodes.

Resistive Load
When driving a resistive load, a pullup resistor is needed in order for the IC to sink current and maintain a logic HIGH level. In this case the COM pin can be left floating (not connected).

This device can operate over a wide temperature range between –40°C to 105°C.


Applications
------------
![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgFPkZU8CkM4eRjPa0P-pukLCJB-NQMVRjADGsIKcnm2fTrGf64gygC-6gfMJR3pyxo6Z03TQx5vG7-ZalheTnx09A8IhFBDQXSmV8YaiSiHEX4XkBydjPe7POk3jzC6F-H5KZVgjJTqCqtMHu0td8AB3_Y0hzaMPafChsFy849tOjxD1F3BIsTC4AnV6rL/w640-h360/7.png)

Now, lets hook this IC to a circuit.
As we know, the ULN2003 IC can easily drive a high-current or high-voltage (or both) device, which a Microcontroller or a Logic Device cannot tolerate. Hence, they are widely used in driving inductive loads like motors, solenoids and relays.

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh9edZxYtg3Q5gTNSp8asDvAnpO5IhCTpXP87XgqpomX07wAcDERZjeSMW_JkCmqurGtOrnRFfEctpB1Avytl0cWlEIafy9fwp4uYd7EUOkdG2ZZTglcInRh9BG3u5WSUWcTZkHc7_qBT28vyvK13AWE7JLK-iezFgH11QczcDyEBxdyW6MB1qThj2ozljU/w640-h360/7_.png)

1. In my first example, I am going to light up a few LEDs using this IC
I have connected 7 LEDs to the 7 OUT Pins of the IC via 220Ohm resistors. On my left, are the 7 digital inputs directly interfaced to either a Microcontroller or a TTL Digital Logic. When a logic HIGH is sent to the input pin the corresponding OUT pin goes LOW lighting up the LED.

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhOSQplKHwid7hsxc1luldpl928qosLsa8VhzRoh7fwlary9lDdxt-Y9NE6zFtf_Z9xgEDM3pfaIXH7arfZz50nEJafPK0iZXtNwImcE0az518Kyjw0dWVYArd1aVLZE3TJ3wdAzaxu_m3FQHwfDnz5ihoBuQV5CsWfG-4HuQi7iF5I8vfb4SZqtGXp9F36/w640-h360/8.png)

2. In my second example, I am driving a Unipolar Stepper Motor using this IC
In this setup, I am using Pin 1~4 for INPUT and Pin 13~16 for OUTPUT. Each OUT pin is rated at 500mA.
Pin 9 has the spike suppressor diode, and is connected to the +ve terminal.
By sending combinations of 0's and 1's to the 4 input pins we can rotate our stepper motor.
I have used this setup in my award winning Video Tutorial: "NodeMCU Based - 3D Printed Indoor Gauge Thermometer" the link is in the description below.

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgjHUT01v43JGJEZeiOm3dEv59555LphDynaHiRBY98XGYXL07rG2PzXeDMXmnpo3MZSo0ojgkfLucPcMKXVR555OrU22doQkfVlJYm6UhDraIePVEsGAzZdzW9cuV1BqtxVrEsEdXYyLryEzFGO4ltaa7v1eTrBDrd5Sa1kAiZVDIk-9CDp9uD4hM1jhfK/w640-h360/9.png)

3. In my third example, I am going to light-up a few AC Lightbulbs using this IC
For high voltage applications, we can use RELAYS to control motors, heaters, lamps or AC circuits which themselves can draw a lot more electrical voltage/current and therefore power. We can hook up a maximum of 7 Relays to this IC.
In my setup, I have connected 4 Relays to the 4 OUT pins of the IC. An AC Lightbulb is connected to the NO-pin of the relay. When we send a Digital HIGH to the INPUT pin the corresponding OUT pin goes LOW and current flows through the coil pulling the armature, completing the circuit and hence lighting up the 220V Light Bulb.
Same as the previous setup, Pin 9 with the suppressor diode is tied back to the +ve terminal.

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhAqkXFXZ0j9HbyQzh9YOGf4NsnCIfv4IMxrkPFK4nDSxOzZidjtgkGpuR0DMI_qLKNA05U_x5tGTgZrh54mkPoZY5F_w94gvYrHzU48yGI-CjJxBXwnFU2-9zgWnc6hLijDPD-te88F3vrccy4WHjw86hPh9QqUejBFDuJbcUEJtRmiKBUAdhqX8363IN9/w640-h360/10.png)

4. In my 4th example, I am going to show you guys how to obtain more than 500mA at the OUTPUT
As we know that each of the OUT Pins are rated at 500mA, then how can I drive a 1Amp device?
All we have to do is, tie 3 of the OUTPUT pins on the OUT side, and tie 3 of the corresponding INPUT Pins on the INPUT side. Now the 3 INPUT pins act like a single INPUT Pin. So basically, we can parallel the inputs to get a higher amplified value of paralleled output. 

You may ask, why did I combine 3 INPUTS and OUTPUTS and not just 2? 
As per the datasheet each pin is rated at 500mA but the total output is 2.5A (*** Page 4 of datasheet ****).
Hence, 2.5A / 7 Pins = 0.36 Approx.
So, 0.36 * 3 = 1.07Amp Approx. which is what we want.


Areas of Application
--------------------
![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg2GQ1RWHumuQVyFJWlstC8DTp8cuyq4z5uGbd5-_XOB_OIoG3GFDHrVi7Lk_1uKrxdRjmoGU9J9qq9BD6R2MwzTnBILxiRcPhm2M_IVUdx5de5m6gx2YxV-jq5tgs4jfIlA-IPtnGILqkBv1QQfkIFAueUibFVfImKjFhjYttkBghzTQxOq5H8droS7-Ug/w640-h360/11.png)

The ULN2003A produced by Texas Instruments can be used for:
1. Driving motors and solenoids
2. Can be used as a Relay Driver for high voltage application (7 relays at the max)
3. To drive high current loads using Digital Circuits
4. To drive high current LED's
5. To create a water level indicator circuit
6. As a LED and Gas Discharge Display Drivers
7. Can also be used as a logic buffer in digital circuits and more...

For more information about the packaging and the material used, please have a look at the datasheet. The link is in the description below.
Always consult a manufacturer's datasheet before assuming industrial conventions, no matter how intuitive or obvious they may be. "In the face of ambiguity, refuse the temptation to guess." - Zen of Python


Thanks
------

[![vO6adrETQIA](https://i.imgur.com/AZoLrVb.png)](https://youtu.be/dtfGf7kf__g)

Thanks again for checking my post. I hope it helps you.
If you want to support me subscribe to my YouTube Channel: https://www.youtube.com/user/tarantula3

Video:  https://youtu.be/dtfGf7kf__g

Full Blog Post:  https://diy-projects4u.blogspot.com/2024/05/All-About-IC-UNL2003.html


References
----------
DataSheet:  https://github.com/tarantula3/ULN2003

Darlington transistor:  https://en.wikipedia.org/wiki/Darlington_transistor

Open Collector Output:  https://www.learningaboutelectronics.com/Articles/Open-collector-output.php

Transistor–Transistor Logic:  https://en.wikipedia.org/wiki/Transistor%E2%80%93transistor_logic

CMOS:  https://en.wikipedia.org/wiki/CMOS

Parasitic Structure:  https://en.wikipedia.org/wiki/Parasitic_structure



Related Videos
--------------
NodeMCU Based - 3D Printed Indoor Gauge Thermometer:  https://www.youtube.com/watch?v=vO6adrETQIA


Acronyms
--------
TTL: Transistor–Transistor Logic

CMOS: Complementary Metal–Oxide–Semiconductor



**Support My Work:**

BTC:   1Hrr83W2zu2hmDcmYqZMhgPQ71oLj5b7v5

LTC:   LPh69qxUqaHKYuFPJVJsNQjpBHWK7hZ9TZ

DOGE:  DEU2Wz3TK95119HMNZv2kpU7PkWbGNs9K3

ETH:   0xD64fb51C74E0206cB6702aB922C765c68B97dCD4

BAT:   0x9D9E77cA360b53cD89cc01dC37A5314C0113FFc3

LBC:   bZ8ANEJFsd2MNFfpoxBhtFNPboh7PmD7M2

COS:   bnb136ns6lfw4zs5hg4n85vdthaad7hq5m4gtkgf23 Memo: 572187879

BNB:   0xD64fb51C74E0206cB6702aB922C765c68B97dCD4

MATIC: 0xD64fb51C74E0206cB6702aB922C765c68B97dCD4


Thanks, ca again in my next tutorial.



Odysee : https://odysee.com/@Arduino:7/All-About-IC-ULN2003:d

Rumble : https://rumble.com/v4umzvl-all-about-ic-uln2003.html

Cos : https://cos.tv/videos/play/52680878888358912


Blog1: https://diy-projects4u.blogspot.com/2024/05/All-About-IC-UNL2003.html

Blog2: https://diyfactory007.blogspot.com/2024/05/All-About-IC-UNL2003.html
