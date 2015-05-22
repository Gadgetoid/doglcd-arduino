## DogLcd ##
![http://www.wayoda.org/share/pictures/doglcd/DogTextTeaser.jpg](http://www.wayoda.org/share/pictures/doglcd/DogTextTeaser.jpg)

This is an Arduino library for the Dog Text-LCD modules manufactured by
[Electronic Assembly](http://www.lcd-module.com/products/dog.html).

The features that make them an interesting option for development are
  * the displays are available with 1, 2 and 3 lines of characters
  * they can be combined with Led backlights in 5 different colors
  * they are not too expensive
  * you only need 4 Arduino IO-pins to control the display (SPI-mode)
  * you can connect more than one display to your arduino (each new display will require one more IO-Pin)

## The Hardware ##
Here is the bare minimum of wiring needed to connect the display to an Arduino.

![http://www.wayoda.org/share/pictures/DogLcd/DogTextSmall.jpg](http://www.wayoda.org/share/pictures/DogLcd/DogTextSmall.jpg)

(Click [here](http://www.wayoda.org/share/pictures/DogLcd/DogText.jpg) for print resolution)

On the [Hardware](Hardware.md)-page I show you how to connect the display to your Arduino and how you can add a hardware reset and backlight switching with just a few more components.

There is also a section about driving more than one display from the Arduino.

## The Code ##
The DogLcd-library is a close relative of the **_new_** LiquidCrystal-library, that was first shipped with Arduino-0017. There are only a few minor changes necessary to port existing LiquidCrystal-code to the DogLcd-library.

The two libraries are so similar, I didn't have to bother writing my own examples, it was enough to recycle a few from the LiquidCrystal-library.

The **basic documentation** and a few examples for the DogLcd-lib are on on the [Code](Code.md)-page.

**All methods** that are available from the DogLcd-lib are documented on the [Library](Library.md)-page.

### Known Bugs ###
  * You have to call **`home()`** or **`setCursor()`** after creating a custom character otherwise it wont be printed on the display. http://code.google.com/p/doglcd/issues/detail?id=3

If you find another one please report it on the [Issues page](http://code.google.com/p/doglcd/issues), thank you!




