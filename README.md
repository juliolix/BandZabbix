## BandZabbix - Graphics Easily using Python   

This is a external colector script created to improve Zabbix, if you dont wanna wast your time with a lot of bored configurations.

<div align="center"><b>Be happy easly dude ...</b></div>

![Screenshot](zabbix1.png)


<b> 1º step - Downloading BandZabbix</b>

<pre><code># cd /usr/lib/zabbix/externalscripts
# curl -O https://raw.githubusercontent.com/juliolix/BandZabbix/master/BandZabbix
# chown zabbix.zabbix BandZabbix
# chmod 755 BandZabbix
</code></pre>

<b> 2º step - Install snmpwalk </b>

<pre><code># cd /usr/lib/zabbix/externalscripts
# apt-get install snmp 
# vim /etc/zabbix/zabbix_server.conf 
change 
          # Timeout=30
to 
            Timeout=30
</code></pre>

<b> 3º step - lets test the BandZabbix  </b>


<pre><code># ./BandZabbix 10.0.0.7(ip) huehuebr(community) .1.3.6.1.2.1.31.1.1.1.10.1(OID)
</code></pre>

If you note the OID above it is the "ether0" interface's "Mikrotik", however, OIDS aways change. You will need to be patience to <b>find out</b> the correct interface's OID. I'm gonna show you how.

<pre><code>#  snmpwalk -v 2c -c huehuebr -On 10.0.0.7 
</pre></code>
![Screenshot](terminal1.png)<br>
.1.3.6.1.2.1.31.1.1.1.10.1 = eth0 interface download 


<b> Final Step - Configuring Zabbix </b>

- Create host 
- Create Item 

![Screenshot](item1.png)
<br>
<br>
<br>

<b> Result: Status = Enabled</b><br>
![Screenshot](result.png)
You can also configure UPLOAD just setting correct OID Interface, create new item to do it.
<br>
<br>
<br>


<b><i> source code: </i></b>

<pre><code>
#!/usr/bin/env python

import sys, commands, string, time


class BzaB:

    def __init__(self, ip, community, oid):
        self.ip = ip
        self.community = community
        self.oid = oid

      
  
    def GetSpeed(self):
        self.data_arg = sys.argv
        self.ip = self.data_arg[1]
        self.community = self.data_arg[2]
        self.oid = self.data_arg[3]
        self.time_data = 5
               
               
        self.data = commands.getoutput("snmpwalk -c" + self.community + " -v 1 " + self.ip + " " + self.oid) 
        self.before_data = (self.data)[(string.find(self.data, ": ")) + 2:-1]

        time.sleep(self.time_data)
      
        self.data = commands.getoutput("snmpwalk -c" + self.community + " -v 1 " + self.ip + " " + self.oid)
        self.after_data = (self.data)[(string.find(self.data, ": ")) + 2:-1]

     
        self.total_data = (int(self.after_data) - int(self.before_data))
        self.bytes_data = (self.total_data / self.time_data)
        self.speed_data = ((self.bytes_data * 8) * 100) 

        print(self.speed_data)

   
x = BzaB(1,2,3)
BzaB.GetSpeed(x)





# Help us to improve it!
# Thanks!
