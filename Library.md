On this page you find a list of all methods that are implemented by the DogLcd-library.



# Display setup #
The methods which must be called to initialize a display before use.

## Assign the Hardware IO-Pins to the display ##
This is done in the constructor of the class. The basic version the constructor expects 4 arguments
`DogLcd(int SI, int CLK, int RS, int CSB);`
  * `SI` The (arduino-)pin connected to the SI-pin on the display
  * `CLK` The (arduino-)pin connected to the CLK-pin on the display
  * `RS` The (arduino-)pin connected to the RS-pin on the display
  * `CSB` The (arduino-)pin connected to the CSB-pin on the display
This is all it takes for a display where the `Reset`-line permanently connected to +5V and no software backlight control is needed.

If your hardware supports one or both of these features, there is another version of the constructor that takes  two mor arguments

`DogLcd(int SI, int CLK, int RS, int CSB, int RESET=-1, int backLight=-1);`
  * `RESET` The (arduino-)pin connected to the RESET-pin on the display
  * `backLight` The (arduino-)pin connected to some external hardware for controling the backlight from software.
There is a default value of -1 for the extra arguments which tells the library code that the specific hardware feature is not available.

**Example** Create a display where RESET permannently wired to +5V, but software backlight switching is available on  pin 6
```
DogLcd myDisplay(2,3,4,5,-1,6)
```

## Initialize the display ##
The method `begin()` resets and initializes the display. The method takes 3 arguments

  * `model` the type of display that is connected. This is the only required argument for the method. It must be one of the constants
    * `DOG_LCD_M081` for a 1-line display
    * `DOG_LCD_M162` for a 2-line display
    * `DOG_LCD_M163` for a 3-line display
  * `contrast` the contrast setting for the display. Values of between 0..63 (0x00...0x3f hex) are allowed here. The default value 0x28 was a good choice for all combinations of display-type and backlight color I have been able to test so far. Values below 0x1A usually result in a contrast that is so small, you probably won't see anything.
  * `vcc` The library implements a switch to operate the display at 3.3 Volts (the default argument is to run the display at 5 Volts).
> `vcc` must be one of the constants :
    * `DOG_LCD_VCC_5V` for 5V operation
    * `DOG_LCD_VCC_3V3` for 3.3V operation

If any one of the arguments is invalid the method will return -1 and the display will not be initialized. On sucess 0 is returned.

**Example 1** initialize a 3-line display working at +5V using the standard setting for the contrast
```
if(myDisplay.begin(DOG_LCD_M163)) {
    Serial.println("Error setting up display");
}
```
Checking the return value might help you debugging possible errors

**Example 2** now we initialize a 1-line display working at +5V using a higher contrast setting
```
myDisplay.begin(DOG_LCD_M081,0x30);
```

**Example 3** When operating at 3.3V we have to supply a value for each of the arguments
```
myDisplay.begin(DOG_LCD_M162,0x30,DOG_LCD_VCC_3V3);
```

## Reset the display ##
You can reset the display from your sketch code with the `reset()` method. This will put the display into the state it had when you initialized it with `begin()`.

**Example**
```
myDisplay.reset();
```

## Software controlled contrast setting ##
With the method `setContrast()` you can implement a software controlled contrast setting feature for the user. The same restrictions already listed with the `begin()` method apply here. Values of between 0..63 (0x00...0x3f hex) are allowed, but values below 0x1A usually result in a contrast that is so small, you probably won't see anything.

**Example**
```
//This is the standard setting used in the class.
myDisplay.setContrast(0x28);
```

## Software controlled backlight ##
If your hardware supports this there is a specific method to set the backlight of the display. The DogLcd-library supports two different ways to control the backlight.
  * You can simply switch it on/off when the control circuit is wired to a _normal_ Arduino IO-Pin.
or
  * you can wire the background switching circuit to a PWM-Pin on the Arduino and control the brightness of the backlight in 256 discrete steps.

The method is defined as
```
setBacklight(int value, bool usePWM=false)
```

The default is to assume a _normal_ IO-Pin is used (`````usePWM=false`````). You must set `````usePWM=true````` for a PWM-pin. The library will not automatically check wether the backlight is connected to a PWN-pin. You have to call the `setBacklight()` method that matches the hardware you have build.

**Example 1** : Backlight is connected to a _normal_ IO-Pin
```
//switch backlight off
myDisplay.setBacklight(LOW);   
//switch backlight on
myDisplay.setBacklight(HIGH);   
```

**Example 2** The backlight is connected to a PWM-Pin
```
//switch backlight off
myDisplay.setBacklight(0,true);   
//switch backlight to medium brightness
myDisplay.setBacklight(0x128,true);   
```

# Printing #
The DogLcd-library uses the same method-names an argumnets for printing text and moving the cursor as the [LiquidCrystal-library](http://arduino.cc/en/Reference/LiquidCrystal) so there is no need to copy the whole documentation.

There is are currently only a single issue with the [createChar()](#Create_a_user-defined_character.md) method.

The rest of the information we link to is 100% compatible with the DogLcd-calls.


## Clearing the display ##
  * http://arduino.cc/en/Reference/LiquidCrystalClear

## Move cursor to home-position ##
  * http://arduino.cc/en/Reference/LiquidCrystalHome

## Move cursor ##
  * http://arduino.cc/en/Reference/LiquidCrystalSetCursor

## Write a character ##
  * http://arduino.cc/en/Reference/LiquidCrystalWrite

## Print formatted text ##
  * http://arduino.cc/en/Reference/LiquidCrystalPrint

## Switch the cursor on/off ##
  * http://arduino.cc/en/Reference/LiquidCrystalCursor
  * http://arduino.cc/en/Reference/LiquidCrystalNoCursor

## Switch the cursor-blinking on/off ##
  * http://arduino.cc/en/Reference/LiquidCrystalBlink
  * http://arduino.cc/en/Reference/LiquidCrystalNoBlink

## Switch the display on/off ##
  * http://arduino.cc/en/Reference/LiquidCrystalDisplay
  * http://arduino.cc/en/Reference/LiquidCrystalNoDisplay

## Scroll the display contents ##
  * http://arduino.cc/en/Reference/LiquidCrystalScrollDisplayLeft
  * http://arduino.cc/en/Reference/LiquidCrystalScrollDisplayRight

## Turn automatic display scrolling on/off ##
  * http://arduino.cc/en/Reference/LiquidCrystalAutoscroll
  * http://arduino.cc/en/Reference/LiquidCrystalNoAutoscroll

## Set the text output direction ##
  * http://arduino.cc/en/Reference/LiquidCrystalLeftToRight
  * http://arduino.cc/en/Reference/LiquidCrystalRightToLeft

## Create a user-defined character ##
While the basic documentation found in the reference for LiquidCrystal-lib
  * http://arduino.cc/en/Reference/LiquidCrystalCreateChar
is correct, there are two minor problems with this method on a DogLcd.
  1. In the DogLcd-lib You can not call the **`creatChar()`** method _before_ the **`begin()`** method. The library code has to do some hardware specific initializations before defining a custom character.
  1. After you defined all of your custom characters, you have to call **`home()`** or **`setCursor()`** once, to be able to print them on the display. (see [this issue](http://code.google.com/p/doglcd/issues/detail?id=3))