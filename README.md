# 4inch-dashboard

1. 
Get a Raspberry Pi WH and a Waveshare 4inch DPI LCD and assemble them

2.
Download an old version of Raspberry Pi OS Buster, I used this one: https://archive.org/details/2021-05-07-raspios-buster-armhf

3. 
Install IMG with Raspberry Pi Imager, and set up SSH and Wifi. 

4.
After finishing saving to the SD card, re-mount it to your computer and copy the files in `4DPIC-DTBO.zip` to the `/boot/overlays` folder (Downloaded from https://www.waveshare.com/wiki/4inch_DPI_LCD_(C)) and then open the file `config.txt` from the SD card's root folder and add the following to the end of the file

```
gpio=0-9=a2
gpio=12-17=a2
gpio=20-25=a2
dtoverlay=dpi24
enable_dpi_lcd=1
display_default_lcd=1
extra_transpose_buffer=2
dpi_group=2
dpi_mode=87
dpi_output_format=0x7f216
dpi_timings=720 0 46 2 42 720 0 16 2 18 0 0 0 60 0 60000000 6
dtoverlay=waveshare-4dpic-3b-4b
dtoverlay=waveshare-4dpic-3b
dtoverlay=waveshare-4dpic-4b
```

5. 
Start the raspberry pi, the screen should turn on, wait until it has connected to WIFI and then use SSH to connect to it

6. 
Update everything with `sudo apt-get update && sudo apt-get upgrade -y` and then `sudo apt-get install unclutter` to hide the mouse cursor

7. 
Edit the file `sudo nano /etc/xdg/lxsession/LXDE-pi/autostart` and add this to the end (update to your URL)

```
@unclutter -idle 0.1 -root

@xset s off
@xset -dpms
@xset s noblank
@chromium-browser --no-sandbox --disable-infobars --noerrdialogs --incognito --check-for-update-interval=1 --simulate-critical-update --kiosk https://yoururlhere.com
```

8. 
Reboot with `sudo reboot` and everything should work!


## Sources

* https://www.reddit.com/r/dakboard/comments/fgiqn3/setup_a_raspberry_pi_zero_w_to_run_a_web_browser/
* https://raspberrypi.stackexchange.com/questions/69204/open-chromium-full-screen-on-start-up
* https://www.waveshare.com/wiki/4inch_DPI_LCD_(C)
