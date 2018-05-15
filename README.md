# Yorktel WiFi/USB Power Reset Board API

This document covers the API interface for the product developed by NCD for Yorktel.

### Version
0.0.2


### Configuration of settings Overview
Controller accepts setting configurations sent via JSON format over USB connection.  Partial JSON is accepted, send only what you want to change.  Controller mounts to computer OS as a virtual Serial/COM port with a baud rate of 115200.
### Configurable settings
All settings documented here are stored in device EEPROM and will pursist device power cycles.  Changes to WiFi network settings will cause WiFi to disconnect temporarily and then connect with new WiFi network settings.

> **WiFi SSID** 
>Key: ```ssid```
>Value type: ```String```
>Example: ```{"ssid":"my_wifi"}```

> **WiFi passphrase**
>Key: ```pass```
>Value type: ```String```
>Example: ```{"pass":"superSecurePassword"}```

> **Server Checkin Interval** 
>Key: ```interval```
>Value type: ```String```
>Example: ```{"interval":5}```
>Description: The interval in seconds at which the controller should check in over USB and with the HTTPS server.

> **Server Checkin Interval** 
>Key: ```server```
>Value type: ```String```
>Example: ```{"server":"google.com"}```
>Description: The server which the controller will check in with on interval.  Do not include https://

> **Server Endpoint Path** 
>Key: ```path```
>Value type: ```String```
>Example: ```{"path":"/api/circuit_reboot_check"}```
>Description: The server endpoint which check in requests will be made.

> **Server SSL Certificate Fingerprint** 
>Key: ```finger_print```
>Value type: ```String```
>Example: ```{"finger_print":"00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0F 10 11 12 13 14"}```
>Description: The SSL certificate fingerprint for the server which the controller will make requests to.

> **Server Connection Port** 
>Key: ```server_port```
>Value type: ```String```
>Example: ```{"server_port":443}```
>Description: The port the controller will connect to when making HTTPS requests.  Default value is 443, only configure if needed.

> **Pulse Duration** 
>Key: ```pulse_duration```
>Value type: ```String```
>Example: ```{"pulse_duration":200}```
>Description: The duration which the relay will be pulsed when a reboot command is received.  Note: Setting this shoudl not be required on most systems.  Default value is 200

### Reboot over USB
It is possible to send a reboot command over the USB connection to reboot the system.  To do this simply send the following JSON command
> **Reboot**
>Key: ```relay```
>Value type: ```String```
>Example: ```{relay:"reboot"}```

### Device Checkin over USB
The device checks in on interval over USB.  At time of checkin the controller will output all Configurable settings as documented above as well as the following information.

> **Event Type** 
>Key: ```event_type```
>Value type: ```String```
>Example: ```{"event_type":"INFO"}```
>Description: This indicates the type of event being reported by the device.  Possible values are ERROR, INFO, INTERVAL.

> **Event Reason** 
>Key: ```event_reason```
>Value type: ```String```
>Example: ```{"event_reason":"WiFi Connect Failed"}```
>Description: The controller can checkin over USB or HTTPS for a multitude of reasons.  This value indicates why the device has checked in.  Current possible reasons are WiFi Connect Failed, WiFi Connected, Input Change, Check In, Save Settings failed Could not parse JSON, Settings Update, Server does not recognize device, Parse Server response failed Could not parse JSON, Certificate does not match.

> **Firmware Version** 
>Key: ```firmware_version```
>Value type: ```String```
>Example: ```{"finger_print":"0.0.2"}```
>Description: This is the current version of firmware running on this particular controller.

> **Device ID** 
>Key: ```device_id```
>Value type: ```String```
>Example: ```{"device_id":"00:01:02:03:04:05:06"}```
>Description: This unique device ID is the Mac address of the device.

> **WiFi Network Connection Status** 
>Key: ```wifi_connected```
>Value type: ```String```
>Example: ```{"wifi_connected":"true"}```
>Description: Indication as to whether or not the device is currently connected a WiFi network.  true if connected, false if not.

> **Input** 
>Key: ```input```
>Value type: ```String```
>Example: ```{"input":"open"}```
>Description: The current status of the controllers on board input.  value:open if the input is open, value:closed if the input is closed.

> **Server Connection Status** 
>Key: ```server_connection```
>Value type: ```String```
>Example: ```{"server_connection":"good"}```
>Description: The current status of the controllers connection to the remote server.  Possible values are boot, good, or error.  If the previous server connection was successful value will be good.  If the previous server connection was unsuccessful the value will be error.  If the device has just booted and has not yet attempted a connection to the remote server the value will be boot.

### Device Checkin with Remote Server via HTTPS
The controller will, on interval, checkin with the remote server as configured.  Upon checkin the controller will report information to the remote server as documented here as well as accept a response from the server to reboot if needed.  If a reboot is desired simply respond with a device reboot request just as it is documented under the Reboot over USB section above. 

   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
