# BandZabbix - Graphics Easily using this External Script.  

This is a external colector script created to improve Zabbix, if you dont wanna wast your time with a lot of bored configurations.

<div align="center"><b>Be happy easly dude ...</b></div>

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

<pre><code># ./BandZabbix 10.0.0.7(ip) pjf(community) .1.3.6.1.2.1.2.2.1.10.1(OIDs)

</code></pre>

If you note that's OID above. its is a interface "ether0" Mikrortik, however OIDS change ever. You will need be patience to <b>find out</b> correct OID to his interface. I gonna show you how to.

<pre><code>#  snmpwalk -v 2c -c hakyluffy -On 10.0.0.7 
</pre></code>

![Screenshot](terminal1.png)



