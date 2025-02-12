Raspberry Pi source files, see [Raspberry Pi 16-channel WS2812 NeoPixel LED driver](https://iosoft.blog/2020/09/29/raspberry-pi-multi-channel-ws2812/) for details

The application is compiled and run using:
```console
gcc -Wall -o rpi_pixleds rpi_pixleds.c rpi_dma_utils.c
 ```

```console
sudo ./rpi_pixleds [options] [RGB_values]

```

The options can be in upper or lower case:

* `-n num    # Set number of LEDs per channel`
* `-t        # Set test mode`
Test mode generates a chaser-light pattern for the given number of LEDs, on 8 or 16 channels as specified at compile-time, e.g. for 5 LEDs per channel:
```console
sudo ./rpi_pixleds -n 5 -t
```


It is also possible to set the RGB value of an individual LED using 6-character hexadecimals, so full red is FF0000, full green 00FF00, and full blue 0000FF. The RGB values for each LED in a channel are delimited by commas, and the channels are delimited by whitespace, e.g

```console
# All 8 or 16 channels, 5 LEDs per channel, all off
sudo ./rpi_pixleds -n 5
 
# All 8 or 16 channels, 3 LEDs per channel, all off apart from Ch2 LED0 red
sudo ./rpi_pixleds -n 3 0 0 ff0000
 
# 3 active channels, 1 LED per channel, set to half-intensity red, green, blue
sudo ./rpi_pixleds 7f0000 007f00 00007F
 
# 3 active channels, 2 LEDs per channel, set to full & light red, green, blue
sudo ./rpi_pixleds  ff0000,ff2020 00ff00,20ff20 0000ff,2020ff
```

You will note that it isn’t necessary to specify the number of LEDs per channel when RGB data is given; the code counts the number of RGB values for each channel, and uses the highest number for all the channels.


