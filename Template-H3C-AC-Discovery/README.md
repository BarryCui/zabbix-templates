# Description
I've created this template for the H3C Access Controller Model WX3510H.
For now, I've tested only on the AC model WX3510H with the software version ComwareV7 and the AP model WA4320i-ACN.

# Prerequisites
Before you can use this template, you must complete the steps below:
1. Download the MIB files from the H3C website: http://download.h3c.com.cn/download.do?id=5087748 or get it from my github template subfolders.
2. Unzip the .zip file and copy all the files under the subfolder "Comware MIB-20200713\H3C New Style Private MIB\" into the snmp mib folder(normally /usr/share/snmp/mibs/) on your zabbix server(Note: If you're running a dockerized zabbix, you need to copy the mib files into the container run by the zabbix/zabbix-server-mysql:alpine image).
3. Restart zabbix to take effect.

# Features
- Automatically discovers and adds items of the number of the currently associated stations for each AP.
- Links to the template "Template Module ICMP Ping" in order to do ping tests for AC.

# Usage
1. Import the template file.
2. Add a H3C WX3510H AC.
3. Link the AC host with this template.
4. Wait for discovery.

# Advanced Usage
You can make a real-time AP location map showing the current stations for each AP by the following steps:
1. Create a topology map.
2. Import your own location map picture as background.
3. Add an element as each of your AP:
   - type: host
   - tag:{the IP address of AC:hh3cDot11ApStationCurAssocSum[the name of ap, you can get it from the names of items].last(0)}  
   - host: choose your AC from list
       
# Note 
To be clear, here's an example of the content of my tag: 

AP39  //Here AP39 is one of my AP names. 

Current stations: {10.0.200.253:hh3cDot11ApStationCurAssocSum[ap39].last(0)} //And the second line shows dynamic statistics of the current stations of ap39, in which                                                                                          10.0.200.253 is the IP address of my AC,last(0) means to get the latest data. You can just replace                                                                                the IP of AC and the name 'ap39' in [] with your own values.

# Changelog

