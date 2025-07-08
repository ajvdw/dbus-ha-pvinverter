# dbus-ha-pvinverter
Integrate your PVInverter from HomeAssistant into [Victron Energy Venus OS](https://github.com/victronenergy/venus)

## Purpose
With the scripts in this repo it should be possible to add the PVInverter to VenusOS. 

## Origin
This repo is based on similar projects for shelly and home wizard integration

## Install & Configuration
### Get the code
Just grap a copy of the main branche and copy them to `/data/dbus-ha-pvinverter`.
After that call the install.sh script.

The following script should do everything for you:
```
wget https://github.com/ajvdw/dbus-ha-pvinverter/archive/refs/heads/main.zip
unzip main.zip "dbus-ha-pvinverter-main/*" -d /data
mv /data/dbus-ha-pvinverter-main /data/dbus-ha-pvinverter
chmod a+x /data/dbus-ha-pvinverter/install.sh
/data/dbus-ha-pvinverter/install.sh
rm main.zip
```
⚠️ Check configuration after that - because service is already installed an running and with wrong connection data (host, username, pwd) you will spam the log-file

### Change config.ini
Within the project there is a file `/data/dbus-ha-pvinverter/config.ini` - just change the values - most important is the host

| Section  | Config vlaue | Explanation |
| ------------- | ------------- | ------------- |
| DEFAULT  | SignOfLifeLog  | Time in minutes how often a status is added to the log-file `current.log` with log-level INFO |
| DEFAULT  | CustomName  | Name of your device - usefull if you want to run multiple versions of the script |
| DEFAULT  | DeviceInstance  | DeviceInstanceNumber e.g. 40 |
| DEFAULT  | LogLevel  | Define the level of logging - lookup: https://docs.python.org/3/library/logging.html#levels |
| DEFAULT  | Host | IP or hostname of the homeassistant api |
| DEFAULT  | Token | Long lived token from homeassistant/profile/security |

python /data/dbus-ha-pvinverter/dbus-ha-pvinverter.py


### Debugging
You can check the status of the service with svstat:

svstat /service/dbus-ha-pvinverter

### Also useful:

tail -f /var/log/dbus-ha-pvinverter/current | tai64nlocal

### Stop the script
svc -d /service/dbus-ha-pvinverter

### Start the script
svc -u /service/dbus-ha-pvinverter

### Restart the script
If you want to restart the script, for example after changing it, just run the following command:

sh /data/dbus-ha-pvinverter/restart.sh

## Used documentation
- https://github.com/victronenergy/venus/wiki/dbus#grid   DBus paths for Victron namespace GRID
- https://github.com/victronenergy/venus/wiki/dbus#pv-inverters   DBus paths for Victron namespace PVINVERTER
- https://github.com/victronenergy/venus/wiki/dbus-api   DBus API from Victron
- https://www.victronenergy.com/live/ccgx:root_access   How to get root access on GX device/Venus OS
