## Netzwerktechnik mit Linux (Ubuntu 22 LTS)
### Befehlsübersicht Terminal
|Aufgabe | Befehl |
|---|---|
|IP Konfiguration anzeigen| ```:~$ ip address```
|Default Gateway anzeigen| ```:~$ ip route```
|DNS Server anzeigen| ```:~$ resolvectl```
|IP-/DNS-Konfiguration (alternativ)| ```:~$ nmcli```
|Erreichbarkeit eines Hosts prüfen| ```:~$ ping 127.0.0.1```
||```:~$ ping www.cisco.com```
|Routenverfolgung zu einem Host| ```:~$ traceroute 192.168.0.1```
|| ```:~$ traceroute dns.google```
|DNS Informationen zu einer Domain| ```:~$ nslookup www.cisco.com```
||```:~$ dig cisco.com```
|Informationen zum Besitzer einer Domain| ```:~$ whois cisco.com```
|Verbindung zu Cisco Router/Switch (**als root**)| ```:~$ sudo -s``` 
|| ```:~# minicom cisco```
|Texteditor (CLI) öffnen mit _datei.txt_| ```:~$ vim datei.txt```
|| ```:~$ nano datei.txt```
|Texteditor (GUI) öffnen mit _datei.txt_| ```:~$ gedit datei.txt```

### Anleitung: IP Konfiguration
#### Statische IPv4 Adresse einrichten (GNOME 3)
* Weg 1: Über die Einstellungen
  * Auf _Aktivitäten_ oben links klicken oder _Windows Taste_ drücken
  * Im Suchfeld _Einstellungen_ eingeben und App **Einstellungen** anklicken
* Weg 2: Über die Taskleiste
  * Auf Taskleiste oben rechts klicken
  * _Kabelgebunden verbunden_ wählen
  * _LAN Einstellungen_ wählen
* Im Fenster der Netzwerkeinstellungen unter **Kabelgebunden** auf das Zahnrad-Icon klicken
* Tab _IPv4_ wählen
* Bei **IPv4-Methode** Radiobutton _Manuell_ wählen
* Unter **Adressen** die IP Adresse, die Netzmaske und ggf. den Gateway eintragen
* Gegebenenfalls unter **DNS** die IP Adresse des DNS Servers eintragen.
  * bei mehreren DNS Servern Adressen mit Komma trennen.
  * die erste Adresse ist dann der primäre DNS Server
* Oben rechts auf den Button _Anwenden_ klicken
* Im Fenster der Netzwerkeinstellungen unter **Kabelgebunden** den Schieberegler aus- und danach wieder anschalten.
* **Die IPv4 Adresse ist nun eingerichtet** 

#### Statische IPv4 Adresse einrichten (GNOME Flashback)
* In der Taskleiste oben auf das Netzwerkicon (zwei Pfeile klicken)
* In der Liste _Verbindungen bearbeiten ..._ auswählen
* Im Fenster der Netzwerkeinstellungen unter **Kabelgebunden** auf das Zahnrad-Icon klicken
* Tab _IPv4_ wählen
* Bei **IPv4-Methode** im Dropdown-Menü _Manuell_ wählen
* Unter **Adressen** die IP Adresse, die Netzmaske (CIDR-Notation) und ggf. den Gateway eintragen
* Gegebenenfalls unter **DNS** die IP Adresse des DNS Servers eintragen.
  * bei mehreren DNS Servern Adressen mit Komma trennen.
  * die erste Adresse ist dann der primäre DNS Server
* Unten rechts auf den Button _Speichern_ klicken
* In der Taskleiste oben wieder auf das Netzwerkicon (zwei Pfeile klicken)
* In der Liste _Kabelgebundene Verbindung 1_ auswählen, um die neue Adresskonfiguration anzuziehen
* **Die IPv4 Adresse ist nun eingerichtet**


#### Statische IPv4 Adresse einrichten (Terminal [CLI])
In this example the configured network interface is named _enp0s3_. The default gateway and DNS server (relay) is 192.168.0.1 and the netmask is /24 which is equivalent to 255.255.255.0 in dot decimal notation.
* set ip address using built-in tool ip
```
sudo ip address add 192.168.0.10/24 dev enp0s3
```

* remove existing IP address from interface, if any
```
sudo ip address del a.b.c.d/m dev enp0s3 
```

* delete default gateway
```
sudo ip route delete default 
```

* add default gateway
```
sudo ip route add default via 192.168.0.1 dev enp0s3
```

* temporarily change DNS server in file /etc/resolv.conf. Append line
_nameserver 192.168.0.1_ or without using an editior: 
```
sudo echo nameserver 192.168.0.1 >> /etc/resolv.conf
```

* switch (back) to DHCP if required
```
sudo dhclient -v enp0s3
```


### Anleitung: Auslesen der DHCP Client Konfiguration
#### Lease Informationen anzeigen
Die Lease Informationen befinden sich in der Datei _/var/lib/dhcp/dhclient.leases_. Wenn die Datei nicht existiert, z.B. weil die Netzwerkkonfiguration von Network Manager durchgeführt wird, kann sie wie folgt angelegt werden. Ersetzen Sie den Interface-Namen durch denjenigen auf Ihrem System.
``` 
:~$ /usr/sbin/dhclient -v enp0s3
```
Wenn sich der Pfad _/usr/sbin_ bereits in der Pfadvariablen _$PATH_ befindet, kann der Präfix _/usr/sbin_ weggelassen werden.
<br/>

Anschließend können die Lease Informationen abgefragt werden:
```
:~$ cat /var/lib/dhcp/dhclient.leases
```


### Anleitung: Zugriff auf Cisco Router / Switch
#### Vorbereitung
Kopieren Sie die bereitgestellte Textdatei _minirc.cisco_ in den Ordner _/etc/minicom/_. Hierfür werden ggf. **root**-Rechte benötigt.

#### Verbindungsaufbau
* Den _Console_ Port mit RJ45 Anschluss am Router / Switch mit einem USB Port am Computer verbinden. Verwenden Sie hierzu ein hellblaues Rollover-Kabel.
* Terminal öffnen
* zum **root** Benutzer wechseln
* serielle Verbindung zum Cisco Gerät aufbauen. Hierfür wird die vorbereitete Konfigurationsdatei _minirc.cisco_ verwendet.
```
:~$ sudo -s 
:~# minicom cisco
```

#### Information: Konfigurationsdatei _minirc.cisco_
```
# Machinell erzeugte Datei - Verwenden Sie "minicom -s" zum Ändern
pu port             /dev/ttyUSB0
pu baudrate         9600
pu bits             8
pu parity           N
pu stopbits         1
```
Sollte eine Verbindung nicht möglich sein, kann der tatsächliche Port nach dem Anschließen des Rollover-Kabels wie folgt in Erfahrung gebracht werden:
```
:~$ dmesg | tail
```
Aus den Informationen im Log entnimmt man den Port. Anschließend kann die Konfigurationsdatei über _minicom -s_ (als **root**) angepasst werden.



### Copyright 
**Julius Angres** under **CC BY-NC-SA**
