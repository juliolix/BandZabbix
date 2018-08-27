## BandZabbix - Graphics Easily using Python   

This is an external colector Phyton created to improve Zabbix, if you dont wanna wast your time with a lot of bored configurations.

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
#criado por: Julio Martins Prefeitura de JF 
#juliolix@gmail.com
#Lembre de Instalar o snmpwalk no servidor Zabbix
#apt-get install net-snmp snmp-utils
#descomentar em /etc/snmp/snmp.conf
#mibs :


import sys, commands, string, time


class BzaB:

    def __init__(self, ip, community, oid):
        self.ip = sys.argv[1]          # Pega o primeiro parametro
        self.community = sys.argv[2]   # Pega o segundo parametro      
        self.oid = sys.argv[3]         # Pega o terceiro parametro
        self.time_data = 5             # Timer para 5 segundos
            
   
    def DadoBruto(self):  # Pega o dado bruto do roteador pegando apenas o ultimo campo 
        self.data = commands.getoutput("snmpwalk -c" + self.community + " -v 1 " + self.ip + " " + self.oid) 
        return int((self.data)[(string.find(self.data, ": ")) + 2:-1])
       
    def Cronometro(self):  # Timer de controle 
        time.sleep(self.time_data) 
        return 0
    
    def DadoLapidado(self): # Captura o dado bruto e depois de 5 segundos captura novamente obtendo a diferenca
        return ((self.DadoBruto() + self.Cronometro()) - self.DadoBruto()) * -1
        
    def CalculaVelocidade(self): # Calcula a velocidade convertendo para bytes por segundo
        self.bytes_data = (self.DadoLapidado() / self.time_data)
        return  (self.bytes_data * 8) * 10

   
if __name__ == '__main__':

     zab = BzaB(1, 2, 3)

     print zab.CalculaVelocidade()

</pre></code>



# Help us to improve it!
# Thanks!
