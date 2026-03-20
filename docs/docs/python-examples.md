# Python Examples

The Qwiic KX13X Python Package examples  to get users started with either Qwiic KX13x board using Python. The examples are detailed on [this page on GitHub](https://github.com/sparkfun/qwiic_kx13x_py/blob/main/examples/README.md).

In this section we'll go over the basic use of the sensor with Python. For more detailed documentation on using the Qwiic KX13x Python package, visit the [Qwiic KX13x Python Package Documentation](http://docs.sparkfun.com/qwiic_kx13x_py/) site.

Note, the examples default to using the Qwiic KX132 so if a Qwiic KX134 is used, adjust the code by un-commenting this line:

```python
myKX = qwiic_kx13x.QwiicKX134()
```

And replace any instance of `kx132` with `kx134`. The acceleration range can also be adjusted by uncommenting this line and adjusting the value set for the range:

```python
myKx.set_range(myKx.KX132_RANGE8G)
```

## Simple Example

This example is a basic example demonstrating how to initialize a Qwiic KX13x board on the I²C bus using its default settings. The full example code can be found below if you would prefer to copy it into your preferred Python interpreter:

```python
import qwiic_kx13x
import time
import sys

def runExample():

    print("\nSparkFun KX13X Accelerometer Example 1\n")
    # myKx = qwiic_kx13x.QwiicKX134() # If using the KX134 un-comment this line and replace other instances of "kx132" with "kx134"
    myKx = qwiic_kx13x.QwiicKX132()

    if myKx.connected == False:
            print("The Qwiic KX13X Accelerometer device isn't connected to the system. Please check your connection", \
                    file=sys.stderr)
            return

    if myKx.begin():
        print("Ready.")
    else:
        print("Make sure you're using the KX132 and not the KX134")

    if (myKx.software_reset()):
        print("Reset")

    # Many settings for KX13X can only be
    # applied when the accelerometer is powered down.
    # However there are many that can be changed "on-the-fly"
    # check datasheet for more info
    myKx.enable_accel(False)
    # myKx.set_range(myKx.KX134_RANGE16G)  # If using the KX134 un-comment this line and comment out below line
    myKx.set_range(myKx.KX132_RANGE16G)
    myKx.enable_data_engine()
    myKx.enable_accel()

    while True:
        if myKx.data_ready():    
            myKx.get_accel_data()
            # If using the KX134 un-comment the print below and comment out the print below that
            # print("X: {0}g Y: {1}g Z: {2}g".format(myKx.kx134_accel.x,
            #                         myKx.kx134_accel.y,
            #                         myKx.kx134_accel.z))
            print("X: {0} Y: {1} Z: {2}".format(myKx.kx132_accel.x,
                                                myKx.kx132_accel.y,
                                                myKx.kx132_accel.z))
            time.sleep(.02) #Set delay to 1/Output Data Rate which is by default 50Hz 1/50 = .02

if __name__ == '__main__':
 try:
  runExample()
 except (KeyboardInterrupt, SystemExit) as exErr:
  print("\nEnding Example 1")
  sys.exit(0)
```
