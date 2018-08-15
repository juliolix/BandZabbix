# BandZabbix


This is a external colector script created to improve Zabbix, if you you dont wast your time with a lot of bored configurations.
<div align="center"><b>Make its easly dude ...</b></div>

![Screenshot](zabbix1.png)


<b> 1º step | Downloading BandZabbix </b>

<pre><code># cd /usr/lib/zabbix/externalscripts
# curl -O https://raw.githubusercontent.com/juliolix/BandZabbix/master/BandZabbix
</code></pre>

<b> 2º step | Install snmpwalk Downloading BandZabbix </b>

<pre><code># cd /usr/lib/zabbix/externalscripts
# apt-get install snmp 
# vim /etc/snmp/snmp.conf 
change 
          # mibs : 
to 
            mibs :
</code></pre>





