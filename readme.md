# Installation Cups

Print-Server with CUPS and AirPrint - German site
https://www.elektronik-kompendium.de/sites/raspberry-pi/2007081.htm


Cups Webserver will be started on RPi with port 631
``https://<rpi>>:631``

# Installing PPD
Copying model ppd file to /usr/share/cups/model/zjiang
This is the offical ppd from Zjiang (http://www.zjiang.com/en/init.php/service/driver) > see "Linux Printer Driver" 

# Installing Filter
Using supplied ```rastertozjto``` and copy it to ```/usr/lib/cups/filter```
 
## Add printer to Cups
- Use user and pwd under which Cups is running on Rpi.
- Select local printer (USB): ``Unknown``
- Enter Name, description and place as you like it and check "Freigabe"
- Select from "Vendor"-dropdown: `Zijang`` 
- Select from "Modell"-dropdown: ``Zijang POS-80250``
- Click on "add printer"
- That's it.

It will looks like:
```
Driver: POS-80250
Connection: usb://Unknown/Printer
Defaultconfiguration: job-sheets=none, none media=om_x-80mm-y-210mm_80.08x209.9mm sides=one-sided
```

# Helpful commands
## How to Enable Debug in CUPS
CUPS creates a few log files in the default logs directory (normally ```/var/log/cups/```) 

Enabling and disabling CUPS debug logging is done via cupsctl
   
Enable CUPS debug logging. ```cupsctl --debug-logging```

Disable CUPS debug logging. ```cupsctl --no-debug-logging```

Then restart CUPS using one of the locations:

```sudo /etc/init.d/cupsys restart``` or
```sudo /etc/init.d/cups restart```


## Testing directly
Make sure permissions are correct:
``sudo chmod 0666 /dev/usb/lp0``

Then try
```echo -e 'It Works' > /dev/usb/lp0```

Papercut
```echo -e '\x1dVA' > /dev/usb/lp0``` 
    


    
# Further Resources
https://github.com/klirichek/zj-58

## How to compile at your own
```
sudo apt install build-essential cmake libcups2-dev libcupsimage2-dev system-config-printer
git clone https://github.com/klirichek/zj-58.git
cd zj-58
mkdir build && cd build && cmake ..
cmake --build .
make
sudo make install
```

# Issues
1. Paper cutting seems not to work properly.
2. and so on... :)