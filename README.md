# NagiosIoT
This project combine two libraries from Adafruit and lcd_i2c: 
   - git clone https://github.com/adafruit/Adafruit_Python_DHT.git
   - setup.py needs to be set up to run extension from code in C as well as  run the Adafruit library globally
   - import Adafruit lirary and lcd_i2c library in TempHud.py.

For Nagios, the Nagios and Nagios plugins are downloaded and installed.
wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.5.tar.gz
wget http://nagios-plugins.org/download/nagios-plugins-2.3.2.tar.gz
There are three main parts in Nagios: Host, Command and Service.
 We define command in commands.cfg.
 define command { 
    command_name   show-temp-humid
    command_line   /home/pi/Documents/tempHud.py 22 4
 }

and define host and service in pizero.

define host {
    use                     linux-server            ; Host group to use
    host_name               Pi Zero                 ; Name of this host
    alias                   pizero                  ; Alias
    address                 xxx.xxx.xxx.xxx            ; IP Address
}

define service {
    use                     local-service           ; Name of service template to use
    host_name               Pi Zero
    service_description     Show Temperature and Humidity 
    check_command           show-temp-humid
}
