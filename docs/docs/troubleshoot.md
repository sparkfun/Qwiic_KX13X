# Troubleshooting

## Switching to SPI

As we've covered before in this tutorial, using either KX13x Breakout in SPI mode requires a slight modification to the board. The ADR Jumper must be **completely opened** so the ADR/SDO pin is floating prior to being connected to the SPI controller's SDI/COPI pin. Also, make sure the controller the KX13x Breakout connects to runs at **3.3V** logic to avoid damaging the IC. Using either accelerometer breakout with a **5V** controller requires [level shifting](https://www.sparkfun.com/categories/361) the signal.
