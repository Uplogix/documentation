To connect the Uplogix appliance to a BigIP, you will need to modify a standard DB-9 adapter.

The typical pinout for a standard DB-9 to RJ-45 is:

|RJ-45 Pin|Color|DB-9 Pin|
|---:|:--:|:---|
|  1|	  blue|	  7|
|  2|	  orange|  4|
|  3|	  black|	  3|
|  4|	  green|	  5|
|  5|	  red|	  5|
|  6|	  yellow|	  2|
|  7|	  brown|	  6|
|  8|	  white|	  8|
 

The BigIP machine is looking for carrier detect on pin 1 of the DB-9. Since this pin is empty in the normal configuration, it needs to be wired into an electrical signal so that the BigIP will see carrier detect and provide the login prompt.

You can modify this DB-9 adapter by removing the wire from pin 6 and placing in pin 1.

![RJ-45 to DB-9 Adapter](http://uplogix.com/support/docs/img/lm-user-guide/DB-9-Pin-1-Adapter-01.jpg)

![RJ-45 to DB-9 Adapter](http://uplogix.com/support/docs/img/lm-user-guide/DB-9-Pin-1-Adapter-02.jpg)

![RJ-45 to DB-9 Adapter](http://uplogix.com/support/docs/img/lm-user-guide/DB-9-Pin-1-Adapter-03.jpg)

![RJ-45 to DB-9 Adapter](http://uplogix.com/support/docs/img/lm-user-guide/Uplogix-Pinout-RJ-45-to-DB9-01.png)

The typical serial settings for an F5 connection are 9600, 8 N 1, no flow control.  Also, configuration on the BigIP may affect communications through the serial port.