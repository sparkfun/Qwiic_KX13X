# Python Setup

> **Note:** This package and the included examples assume you are using the latest version of Python 3. If this is your first time using Python or I²C hardware on a Raspberry Pi, these tutorials can help you get started:
>
> - [Python Programming with the Raspberry Pi](https://learn.sparkfun.com/tutorials/python-programming-tutorial-getting-started-with-the-raspberry-pi)
> - [Raspberry Pi SPI and I2C Tutorial](https://learn.sparkfun.com/tutorials/raspberry-pi-spi-and-i2c-tutorial)

We've written a Python package to control the KX13x Breakouts for users who prefer a Raspberry Pi or other Python-specific development environment. You can install the `sparkfun-qwiic-kx13x` Python package hosted by PyPi through a command interface. If you prefer to manually download and build the libraries from the [GitHub repository](https://github.com/sparkfun/Qwiic_KX13X_Py).

*\*Please be aware of any package dependencies. You can also check out the repository documentation page, hosted on [Read the Docs](https://qwiic-kx13x-py.readthedocs.io/en/latest/?).*

## Installation

The first step to using this package is installing it on your system. The install method depends on the python platform. The following sections outline installation on Python, MicroPython and CircuitPython.

### Python

#### PyPi Installation

The package is primarily installed using the `pip3` command, downloading the package from the Python Index - "PyPi".

Note - the below instructions outline installation on a Linux-based (Raspberry Pi) system.

First, setup a virtual environment from a specific directory using venv:

```sh
python3 -m venv path/to/venv
```

You can pass any path as path/to/venv, just make sure you use the same one for all future steps. Visit this link for more [information on venv](https://docs.python.org/3/library/venv.html).

Next, install the qwiic package with:

```sh
path/to/venv/bin/pip3 install sparkfun-qwiic-kx13x
```

Now you should be able to run any example or custom python scripts that have `import qwiic_kx13x` by running e.g.:

```sh
path/to/venv/bin/python3 example_script.py
```

### MicroPython Installation

If not already installed, follow the [instructions here](https://docs.micropython.org/en/latest/reference/mpremote.html) to install mpremote on your computer.

Connect a device with MicroPython installed to your computer and then install the package directly to your device with mpremote mip.

```sh
mpremote mip install github:sparkfun/qwiic_kx13x_py
```

If you would also like to install the examples for this repository, issue the following mip command as well:

```sh
mpremote mip install --target "" github:sparkfun/qwiic_kx13x_py@examples
```

### CircuitPython Installation

If not already installed, follow the [instructions here](https://docs.circuitpython.org/projects/circup/en/latest/#installation) to install CircUp on your computer.

Ensure that you have the latest version of the SparkFun Qwiic CircuitPython bundle.

```sh
circup bundle-add sparkfun/Qwiic_Py
```

Finally, connect a device with CircuitPython installed to your computer and then install the package directly to your device with circup.

```sh
circup install --py qwiic_kx13x
```

If you would like to install any of the examples from this repository, issue the corresponding circup command from below. (NOTE: The below syntax assumes you are using CircUp on Windows. Linux and Mac will have different path seperators. See the [CircUp "example" command documentation](https://learn.adafruit.com/keep-your-circuitpython-libraries-on-devices-up-to-date-with-circup/example-command) for more information)

```sh
circup example qwiic_kx13x\qwiic_kx13x_ex1
circup example qwiic_kx13x\qwiic_kx13x_ex3
circup example qwiic_kx13x\qwiic_kx13x_ex4
```
