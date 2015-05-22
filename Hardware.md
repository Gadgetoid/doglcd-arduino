## Basic schematic ##
This is the basic schematic for the display with datatransfer over SPI.

![http://www.wayoda.org/share/pictures/DogLcd/DogText.jpg](http://www.wayoda.org/share/pictures/DogLcd/DogText.jpg)

Four input signals on the display have to be connected to four IO-Pins on the Arduino-board. There are no restrictions which pins on the arduino to use. You simply pass the number of the pins you have chosen to the library-code.

The current that is drawn by the display is nearly equivalent to the current drawn by the backlight. The backlight Leds are connected in parallel here.
Please refer to the datasheet when selecting a value for the current limiting resistor `R`.

## Hardware reset and backlight switching ##
The basic schematic is fine for a display that is powered by mains, but if your arduino runs on batteries (or your battery powered notebook) you certainly want a way to switch the backlight on and off from your code.
All you need is a transistor driven by another Arduino-pin. If you drive the transistor from a PWM-pin you can even dim the backlight (fading in and out is also very cool). The transistor I used in the schematic is a logic level MOSFet that can switch up to 2.5 amps at 60 volts. They are not really cheap (0.50 €) but I just love this little power packs for switching all kinds of loads.

The display also provides a pin for doing a hardware reset. I don't know who needs this, but since its there we want to support it too. All you have to do is wire the `Reset` signal to an Arduino-pin. The library will then do a hardware-reset every time you call the `begin()` method.


![http://www.wayoda.org/share/pictures/DogLcd/DogTextPwmBacklight.jpg](http://www.wayoda.org/share/pictures/DogLcd/DogTextPwmBacklight.jpg)


## Adding a second (third...) Display ##
A feature of the SPI-bus, is that all devices on the bus can share the datalines `SI,RS` and `CLK`. For each new display that you add you only have to wire a dedicated `CSB` signal. Here is a simplified schematic that shows how to connect a second  display to an arduino.

![http://www.wayoda.org/share/pictures/DogLcd/DogText_Chaining.jpg](http://www.wayoda.org/share/pictures/DogLcd/DogText_Chaining.jpg)

Both displays tap the datalines `SI,RS,CLK`. But each has its own `CSB` signal. For the sake of clarity the Reset-line is hardwired to +5V and the backlight switching circuit is not shown.

Your code talks to each display individually. The moment data is to be send the `CSB`-signal of the display you want to talk to is activated and only the selected display will be updated. There is a example on the [Code](Code.md)-page that shows you how to talk to each display with the DogLcd-library.




