# Air Quality Index Sensor

## How to make one
The Air Quality Sensor I made was built with a ready-to-use Raspberry Pi B+ (with NOOBS or Raspbian on) and a SDS011 sensor. That's it :)

## Building it
To build it, attach the sensor's serial to USB converter into your Pi. Then, plug in your Pi and the lights should come on if the image is ok. Then, you will need to open the terminal.

## Programming it
Programming the sensor is simple. Inside the terminal, type the following:

```sudo apt install git-core python-serial python-enum lighttpd```

This will install all the required packages on the Pi for us to use.

```dmesg```

This will tell us what USB port the sensor is connected to. You might get a response like this:

```[ 5.559802] usbcore: registered new interface driver usbserial

[ 5.559930] usbcore: registered new interface driver usbserial_generic 

[ 5.560049] usbserial: USB Serial support registered for generic 

[ 5.569938] usbcore: registered new interface driver ch341 

[ 5.570079] usbserial: USB Serial support registered for ch341-uart 

[ 5.570217] ch341 1–1.4:1.0: ch341-uart converter detected 

[ 5.575686] usb 1–1.4: ch341-uart converter now attached to ttyUSB0
```

In the last line you can see our interface: In our example, it's ```ttyUSB0```. Now type:

```wget -O /home/pi/aqi.py https://raw.githubusercontent.com/zefanja/aqi/master/python/aqi.py```

This will install the specific drivers needed for the sensor to work.

```sudo chown pi:pi /var/www/html/```

```echo [] > /var/www/html/aqi.json```

Now we can start the script. This will output the data from the sensor. First we need to give the sensor the correct permissions:

```chmod +x aqi.py```

And _now_ we can start.

```./aqi.py```

This runs a Python script we just downloaded along with the drivers.

### Creating a Crontab process
Now, we need to create a Crontab process to automatically run the sensor whenever we turn on the power to the Pi.
You create a new Crontab process with the ```crontab``` command:

```crontab -e @reboot cd /home/pi/ && ./aqi.py```

There we go! Now our script automatically starts with each reboot.

## Creating a HTML page
We can now put our data onto a HTML page. These are the files:

```wget -O /var/www/html/index.html https://raw.githubusercontent.com/zefanja/aqi/master/html/index.html```

```wget -O /var/www/html/aqi.js https://raw.githubusercontent.com/zefanja/aqi/master/html/aqi.js```

```wget -O /var/www/html/style.css https://raw.githubusercontent.com/zefanja/aqi/master/html/style.css```

Now, find your IP address with the ```ifconfig``` command. The website should show up when you enter it into a web browser!

# Thanks and have fun building it!
