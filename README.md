# SAMS
A Desktop GUI for Smart Attendance Management System Using Realtime Face Recognition System

[![Python 3.6](https://img.shields.io/badge/python-3.6-blue.svg)](https://www.python.org/downloads/release/python-360/)
![Py2app](https://img.shields.io/pypi/pyversions/py2app)
[![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)](https://www.python.org/)
[![made-with-bash](https://img.shields.io/badge/Made%20with-Bash-1f425f.svg)](https://www.gnu.org/software/bash/)
[![GitHub license](https://img.shields.io/github/license/saket13/iBatteryStats)](https://github.com/saket13/iBatteryStats/blob/master/LICENSE)

I use macOS X(10.14.5) Mojave and Apple removed the option to show the battery time remaining in the statusbar since the macOS X(10.12.2) release. So I made this my own little thing- its far from being perfect but hey, it works! ..

## Screenshots

**Charging & Discharging:**

| [![Charging](Charging.png)]  |  [![Discharging](Discharging.png)] |
|:---:|:---:|
| CHARGING | DISCHARGING |

**Low Battery Notification:**

![Notification](Notification.png)

## Design

This Apple Menu bar application has two parts - a bash script that runs as a cron job and dumps battery stats to log file, and a Python script that processes the log file to generate cumulative statistics like Charge Left, Status, Time Left, Cycles and Temperature etc and the Python script has been converted to a Status bar app using Rumps.

I've also modified the Python script that is being run to alert you (via Rumps Desktop Notification Feature) of 'Charge Your Mac' in the last 15 and 10 mins remaining.

## Installation

Clone the repo and install Rumps

```bash
git clone https://github.com/saket13/iBatteryStats 
sudo chmod +x path_to_iBatteryStats/iBatteryStats/battery.sh
sudo -H pip3 install rumps

```

Add this line to your cron tab (`crontab -e`):

     SHELL= /bin/bash   
     */1 * * * * /bin/bash/ path_to_iBatteryStats/iBatteryStats/battery.sh > path_to_iBatteryStats/iBatteryStats/back.log 2>&1
     # Here in crontab entry 1st argument says script is called every minute and second argument specifies where the script is and third where the log file is 

Modify your python script to fetch values:

```python
#Enter the absolute address of the file here and leave everything as it is
log_file_path = 'path_to_iBatteryStats/iBatteryStats/back.log'

```

## Usage

You can simply do:

```python
nohup python3 path_to_iBatteryStats/iBatteryStats/battery.py &

```
or to open the Application with no opening of terminal and on a single click

```bash
#Modify the content of app_shell to ::

#!/bin/sh
nohup python3 path_to_iBatteryStats/iBatteryStats/battery.py &

# And give it full permission ::

sudo chmod +x path_to_iBatteryStats/iBatteryStats/app_shell

```
## Future Ideas and TODOs

* Use `bokeh` to chart out the data?

* Handle every second stats and update it .
    * For now it is working every minute.

* Make this, the data dumping cron job and a battery status menu bar app indicator all a part of a single big application?

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

* MIT
