## Netzwerktechnik mit Linux (Ubuntu 22 LTS)
### Befehlsübersicht
|Aufgabe | Befehl |
|---|---|
|IP Konfiguration anzeigen| ```:~$ ip address```
|DNS Server anzeigen| ```:~$ resolvectl status```
|Erreichbarkeit eines Hosts prüfen| ```:~$ ping 127.0.0.1```
||```:~$ ping www.cisco.com```
|Routenverfolgung zu einem Host| ```:~$ traceroute 192.168.0.1```
|| ```:~$ traceroute dns.google```
|Verbindung zu Cisco Router/Switch (**als root**)| ```:~$ sudo -s``` 
|| ```:~# minicom cisco```
|Texteditor (CLI) öffnen| ```:~$ vim```
|| ```:~$ nano```
|Texteditor (GUI) öffnen| ```:~$ gedit```

### Anleitung: IP Konfiguration
#### Statische IPv4 Adresse einrichten
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
  * die erste Adresse ist dann der primäre DNS Server.
* Oben rechts auf den Button _Anwenden_ klicken
* Im Fenster der Netzwerkeinstellungen unter **Kabelgebunden** den Schieberegler aus- und danach wieder anschalten.
* **Die IPv4 Adresse ist nun eingerichtet** 

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