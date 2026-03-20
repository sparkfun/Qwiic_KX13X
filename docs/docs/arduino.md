# Arduino Library

The SparkFun KX13x Arudino library makes it easy to get started measuring acceleration data from the sensor. Install the library through the Arduino Library Manager by searching for **"SparkFun KX13x Arduino Library"**. If you prefer manually downloading the library, you can grab it from the [GitHub repository](https://github.com/sparkfun/SparkFun_KX13X_Arduino_Library).

## Examples

The SparkFun Qwiic KX13x Arduino Library includes four examples to get started with both KX13x boards.

### Example 1 - Basic Readings

Example 1 is a basic example to demonstrate how to read data from the accelerometer. Open the example by navigating to **"File > Examples > SparkFun Qwiic KX13x Library > Example1BasicReadings"**. Next, open the **Tools** menu and select your board (in this case, Arduino Uno) and correct Port your board enumerated on. Upload the code, open the [serial monitor](https://learn.sparkfun.com/tutorials/terminal-basics) and set the baud rate to **115200**.

The example defaults to use the KX132 so if you are using the KX134, make sure to comment/uncomment the appropriate line:

```c
SparkFun_KX132 kxAccel;
//SparkFun_KX134 kxAccel; // For the KX134, uncomment this and comment line above
```

The setup initializes the sensor and performs a software reset, configures it to operate at the 16g range and enable the accelerometer. Just as above, make sure to select the appropriate option for either the KX132/134 as the code defaults to the KX132.

```c
    if( !kxAccel.begin() )
    {
        Serial.println("Could not communicate with the the KX13X. Freezing.");
        while(1);
    }

    Serial.println("Ready.");

    if( kxAccel.softwareReset() )
        Serial.println("Reset.");

    //Give some time for the accelerometer to reset.
    //It needs two, but give it five for good measure.
    delay(5);

    // Many settings for KX13X can only be
    // applied when the accelerometer is powered down.
    // However there are many that can be changed "on-the-fly"
    // check datasheet for more info, or the comments in the
    // "...regs.h" file which specify which can be changed when.
    kxAccel.enableAccel(false);

    kxAccel.setRange(SFE_KX132_RANGE16G);         // 16g Range
    //kxAccel.setRange(SFE_KX134_RANGE16G);         // 16g for the KX134

    kxAccel.enableDataEngine();     // Enables the bit that indicates data is ready.
    // kxAccel.setOutputDataRate(); // Default is 50Hz
    kxAccel.enableAccel();
}
```

After initializing the IC, the code prints out data for all three axes every 20ms. The delay here is important as it should be 1/ODR (Output Data Rate) and the default setting is 50Hz.

```c
void loop() {

  myData = kxAccel.getAccelData();
  Serial.print("X: ");
  Serial.print(myData.xData, 4);
  Serial.print("g ");
  Serial.print(" Y: ");
  Serial.print(myData.zData, 4);
  Serial.print("g ");
  Serial.print(" Z: ");
  Serial.print(myData.zData, 4);
  Serial.println("g ");

  delay(20); // Delay should be 1/ODR (Output Data Rate), default is 50Hz

}
```

### Example 2 - Interrupts

Example 2 shows how to use the hardware interrupt pin(s) on the accelerometer. In order to use this example, connect the INT1 pin on the KX13x breakout to an interrupt-capable pin. This example assumes a SparkFun RedBoard Qwiic is used so adjust the code as necessary. To follow along with this example (as well as the Buffer Example), assemble your circuit with INT1 connected to `2` on your development board.

If you aren't sure which pins on your development board are capable of external interrupts, [this reference page](https://www.arduino.cc/reference/pt/language/functions/external-interrupts/attachinterrupt/) has a list of available pins on common Arduino development boards.

Along with creating the KX13x and data objects, the code sets the physical interrupt pin as `2`.

```c
byte dataReadyPin = 2;
```

The code initializes the accelerometer and disables the accelerometer briefly to configure the interrupt settings for data ready on INT1:

```c
kxAccel.enableDataEngine();             //  Enables the bit that indicates data is ready.
kxAccel.enablePhysInterrupt();          //  Enables interrupt pin 1
kxAccel.routeHardwareInterrupt(0x10);   //  Routes the data ready bit to pin 1
```

After initializing the sensor, the main loop monitors the `dataReadyPin` (`D1`) and if it is HIGH, prints out data for all three axes:

```c
void loop() {

  if( digitalRead(dataReadyPin) == HIGH ){ // Wait for new data to be ready.

    myData = kxAccel.getAccelData();
    Serial.print("X: ");
    Serial.print(myData.xData, 4);
    Serial.print("g ");
    Serial.print(" Y: ");
    Serial.print(myData.zData, 4);
    Serial.print("g ");
    Serial.print(" Z: ");
    Serial.print(myData.zData, 4);
    Serial.println("g ");

     //kxAccel.clearInterrupt();// Because the data is being read in "burst"
     //mode, meaning that all the acceleration data is being read at once, we don't
     //need to clear the interrupt.
  }
  delay(20); // Delay should be 1/ODR (Output Data Rate), default is 50Hz
}
```

### Example 3 - Buffer

The third example shows how to configure and use the KX13x buffer settings to trigger hardware interrupts when the buffer is full. Just like Example 2, the code sets the physical interrupt/data ready pin as `2` which is driven HIGH when the buffer is full. Just like with Example 2, in order to use this example, connect the INT1 pin on the KX13x breakout to an interrupt-capable pin. This example assumes a SparkFun RedBoard Qwiic/Arduino Uno is used so adjust the code as necessary.

```c
byte dataReadyPin = 2;
```

The setup configures the KX13x to enable the buffer interrupt as a hardware interrupt in FIFO mode:

```c
kxAccel.enableBufferInt();              //  Enables the Buffer interrupt
kxAccel.enablePhysInterrupt();          //  Enables interrupt pin 1
kxAccel.routeHardwareInterrupt(0x40);   //  Routes the data ready bit to pin 1

kxAccel.enableSampleBuffer();           // Enable buffer.
kxAccel.setBufferOperationMode(0x00);   // Enable the buffer to be FIFO.
```

After setting everything up, the main loop waits for the buffer to fill and drive the data ready pin HIGH. Once the pin goes HIGH, the code prints out acceleration data for all three axes just like the other examples.
