ESP WIRELESS LAYOUT COMMAND CONTROL

Welcome to my git related to the development of a wireless command control system for model railroads utilizing the ESP 32 microprocessor. My goal with this project is to develop a low-cost, wireless, command control system for model railroads.

The current LCC system that has been “standardized” by the NMRA is primarily driven by one manufacturer. It utilizes a CAN Bus for the exchange of data packets. The CAN Bus is a very resilient system, primarily utilized in automobiles. It is tolerant to multiple vibrations, over the short distances within a vehicle. That tolerance is not necessitated by our stationary model railroads.

The CAN Bus does have limitations with respect to length and number of nodes. Packet size limitations are also relevant with the utilization of a CAN Bus. CAN Bus interfaces also add a level of expense to the projects. That said, ESP 32’s could be utilized with a CAN Bus, and there is a manufacturer of an ESP32’s which contains a CAN interface on the board.

50 years ago, I was always impressed by the miles of wire that would exist under large model railroad layouts with block control. The organization of that wiring with numerous terminal strips truly was a thing of beauty. As I have gotten older, I find that my personal wiring, at my workstations, looks more like a bowl of spaghetti than a thing of beauty. Therefore, my desire to create a wireless LCC system. Another goal of this development is to create a low-cost option for LCC implementation.

Factors that required consideration for this project include:
• The relatively small size of data packets required for model railroading (why a CAN Bus works).
• The relatively small volume of packets transmitted, even on a large layout.
• The transmission protocol utilized. This theoretically could be based on an 802.11 transmission protocols or Bluetooth. I have elected to utilize a Wi-Fi-based system for the following reasons:
o The range of Wi-Fi transmission is greater than Bluetooth.
o The ESP32 nodes can be connected to a 5 V bus underneath the layout, and therefore power consumption is not a major concern.
o Web apps can be developed for interfacing with ESP32 modules versus specific apps for Android and iOS systems.
• The use of ESP 32’s as the basis for nodes in the system. The great value with these microcontrollers is that:
o They can be purchased for less than $5 apiece.
o They contain built-in Wi-Fi, Bluetooth, and LE Bluetooth modules. The newer modules from Espressif have increased the processing power, but have dropped Bluetooth.
o They have 16 pulse width modulation (PWM) output pins. That translates into the ability to control 16 servomotors or 16 LED’s for signals.
o At less than $5 per unit, SG90 servos controlling turnouts with PWM signals can offer another significant savings to model railroaders.

My prior endeavors with wireless LCC development utilized XBEE transmitters for layout control. These too utilize 802.11 protocol to deliver small data packets. The system itself worked well, and a dispatcher could control the layout on a different level of the building than the layout itself. The limitations of the use of the XBEE modules were the availability of a single PWM pin. Secondary to this constraint, my initial system utilized relays to control Tortoise Switch Machines (A great product). This required a second 12 V bus for the tortoise switch machines, the purchase of relays, and the cost of the XBEE units and the Tortoise units. The currently proposed system can be run from a 5V bus which powers the ESP32 units and the SG90 servos.

Currently, I am exploring three different protocols for the development of the wireless LCC system. Those are ESP_NOW, ESP Painlessmesh, and the ESP_MESH protocol from Espressif. An advantage of the mesh protocols is that they do have a broadcast clock function incorporated into the protocol. This conceivably could be translated into a fast clock for operations and timestamps for events. The disadvantage of the time protocol is that it recycles every 71 minutes. This should be easily modified by the addition of a single byte to the timestamp.

All three protocols have a limitation in the number of nodes that may be present on a particular bus. This is a function of the module memory. As the Espressif protocol could have multiple layers, it would not be difficult to incorporate over 350 modules, each module driving 16 PWM circuits (the actual number in this case would be almost 5700 turnouts or led controls).
Another consideration has been the programming language to utilize for this endeavor. ESP32;s can be programmed with the Arduino IDE. This is a C++ platform. While many younger programmers utilize Python as a preferred programming language and Python available for the ESP 32, Python could be an option for the system language. Taking the preceding into consideration, this platform will be developed in C++. The reason for this decision is:
• C++ is theoretically faster.
• Python is written in C++.
• I believe that the Arduino IDE is friendlier to novice programmers than writing code in Micro Python.

My final comments in this introduction to the wireless LCC platform concerns data packets. Exchanging data in JSON has become a common practice at this time. JSON objects can also be directly saved into some of the Non-SQL databases such as MongoDB & Neo4j. Fortunately, JSON objects look a whole lot like C++ struct’s (There really isn’t much new under the Sun). Therefore, my initial endeavors will consist in the construction of a generic struct for data packet transmission.
