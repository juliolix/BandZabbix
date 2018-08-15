# BandZabbix External Script 


This is a external colector script created to improve Zabbix, if you you dont wast your time with a lot of bored configurations.
<div align="center"><b>Make its easly dude ...</b></div>

![Screenshot](zabbix1.png)


<b> 1º step | Downloading BandZabbix </b>

<pre><code># cd /usr/lib/zabbix/externalscripts
# curl -O https://raw.githubusercontent.com/juliolix/BandZabbix/master/BandZabbix
# chown zabbix.zabbix BandZabbix
# chmod 755 BandZabbix
</code></pre>

<b> 2º step | Install snmpwalk </b>

<pre><code># cd /usr/lib/zabbix/externalscripts
# apt-get install snmp 
# vim /etc/snmp/snmp.conf 
change 
          # mibs : 
to 
            mibs :
</code></pre>

<b> 3º step | lets testing the BandZabbix  </b>

<pre><code># ./BandZabbix 10.0.0.7 pjf 
</code></pre>







