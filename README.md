# Raspberry Pi and I2C addresss conflict

Use multiple I2C devices with same I2C address. No extra hardware required.

Add the following lines to your `config.txt` file

`dtoverlay=i2c-gpio,bus=4,i2c_gpio_delay_us=2,i2c_gpio_sda=17,i2c_gpio_scl=27`

`dtoverlay=i2c-gpio,bus=3,i2c_gpio_delay_us=2,i2c_gpio_sda=23,i2c_gpio_scl=24`

and then reboot `sudo reboot` to make the changes active.

The description of the above to lines is found in: [/boot/overlays/README](https://raw.githubusercontent.com/raspberrypi/firmware/master/boot/overlays/README)

I2C bus 3 : is GPIO 17, 27

I2C bus 4 : is GPIO 23, 24

**Name:**   i2c-gpio

**Info:**   Adds support for software i2c controller on gpio pins

**Load:**   `dtoverlay=i2c-gpio,<param>=<val>`

Params:

        i2c_gpio_sda            GPIO used for I2C data (default "23")

        i2c_gpio_scl            GPIO used for I2C clock (default "24")

        i2c_gpio_delay_us       Clock delay in microseconds (default "2" = ~100kHz)

        bus                     Set to a unique, non-zero value if wanting multiple i2c-gpio busses. If set,
                                will be used as the preferred bus number (/dev/i2c-<n>). If not set, the
                                default value is 0, but the bus number will be dynamically assigned - probably 3.

If you run: `sudo i2cdetect -l`

(Underscore L), you will see that i2c bus 3 and 4 is added

```
i2c-3	i2c       	3.i2c                           	I2C adapter
i2c-1	i2c       	bcm2835 I2C adapter             	I2C adapter
i2c-4	i2c       	4.i2c                           	I2C adapter
```

Now you need to change your applications to use those busses.

Ref.: https://www.instructables.com/id/Raspberry-PI-Multiple-I2c-Devices/
