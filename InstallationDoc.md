
### Inhaltsverzeichnis
		
1. [Raspian installieren](#1raspian-installieren)
2. [Grundeinrichtung System, Tastatur und Sprache](#2-grundeinrichtung-system-tastatur-und-sprache)
3. [Netzwerk einrichten](#3-netzwerk-einrichten)
4. [System aktualisieren](#4-system-aktualisieren)
5. [Raspberry Pi Grundeinrichtung via Konsole](#5-raspberry-pi-grundeinrichtung-via-konsole)
6. [Via Konsole mit SSH Verbinde](#6-via-konsole-mit-ssh-verbinden)
7. [Raspberry Pi Remote konfigurieren](#7-raspberry-pi-remote-konfigurieren)
8. [System aktualisieren-2](#8-system-aktualisieren-2)
9. [Apache2 Webserver für OwnCloud installieren und testen](#9-apache2-webserver-f%C3%BCr-owncloud-installieren-und-testen
)
10. [PHP Modul installieren und testen](#10php-modul-installieren-und-testen)
11. [MySQL installieren](#11-mysql-installieren)
12. [phpMyAdmin instalieren](#12-phpmyadmin-instalieren)



## 1.Raspian installieren

1. Raspbian mithilfe der Installer  NOOBS Lite installieren (www.raspberrypi.org/downloads). Wir verwenden ein Network Installer
2. SD-Karte mit Disk Utiliy formatieren (FAT32),anhand  der Einleitung README zipfile im NOOBS Installer Packet
3. Die Dateien die sich in der heruntergeladenen ZIP-Datei befinden, auf die SD-Karte eincopiieren und entpacken
4. Die SD-Karte in den Raspberry Pi stecken und diesen mit einem LAN-Kabel verbinden (+ Bildschirm via HDMI, USB Maus, USB Tastatur und der Netzstecker)
5. Der Raspberry Pi mit der Speicherkarte starten und "Raspbian" auswählen
6. Der Raspbery musst eine Interbetverbindung haben, damit  die Instalationsdaten heruntergeladen werden können
7. Noobs startet und Raspian wird installiert


## 2. Grundeinrichtung System, Tastatur und Sprache

- Nachdem die SD-Karte im Pi eingesteckt ist, die Geräte wie Tastatur, Maus, Bildschirm verbunden sind, ersten Start von Raspbian wird grundsätzlich auf dem Desktop stattfinden.
1. Öffnet das Menu oben links

![rasuberry erste start](https://cloud.githubusercontent.com/assets/21320216/19016589/bc396d54-881e-11e6-8264-8e405f0e542f.png)


2. Öffnet das Unter-Menu Preferences
3. Im Programm klickt ihr nun auf Expand Filesystem


![raspberry-pi-expand-file-system](https://cloud.githubusercontent.com/assets/21320216/19016595/e14f22b4-881e-11e6-9c98-0986a3e31714.png)

4. Wechselt dann auf den Reiter Localisation um die Sprache und Tastatur auf deutsch umzustellen
5. Öffnet hierzu Set Locale und nehmt folgende Einstellungen vor (es empfiehlt sich die Sprache auf English zu lassen um Übersetzungsfehler zu vermeiden)
  5.1 Language: de (German)
  5.2 Country: DE (Germany)
  5.3 Character Set: UTF-8
6. Im Menu Set Timezone wird die richtige Zeitzone eingestellt
7. Das Tastaturlayout stellen wir dann noch über Set Keyboard ein
  8.1 Country: Switzerland
  8.2 Variant: German
8. Beendet die Raspberry Pi Configuration mit einem Klick auf OK und bestätigt die Rückfrage nach einem Neustart mit Yes



## 3. Netzwerk einrichten

1. Auf dem Desktop der linken Maustaste auf das Netzwerk Symbol rechts oben klicken
2. Die richtige Netzwerk aus der Liste auswählen
3. Die Password eingeben und eine  Internet-Verbindugng machen


## 4. System aktualisieren

- mit aktuellster Software und Firmware versorgen
1. SSH Verbindung via Console
2. Die folgend Befehle werden angegeben um den Raspberry Pi zu aktualisieren 

	`$ sudo apt-get update`
	`$ sudo apt-get upgrade`
	`$ sudo reboot` / `sudo shutdown -h now`


## 5. Raspberry Pi Grundeinrichtung via Konsole 

- Nach dem ersten Start fragt der Raspberry Pi nach Logindaten, für das Raspbian sind das im Standard immer folgende Daten:
	`
	User: pi
	Passwort: raspberry
	`
	
1. Im Terminal über  `raspi-config`  konfigurieren

![raspi-config2](https://cloud.githubusercontent.com/assets/21320216/19016649/0ac09662-8821-11e6-865e-62c679fbea56.png)

  1.1 Mit den Pfeiltasten Internationalisation Options markieren und mit Enter öffnen.
	- Change Keybord Layout: Generic 105
	- die Sprache wählen: German
2. Um über PC zugreifen zu können muss SSH aktiviert sein.
	- Im Hauptmenu Advanced Options markieren und mit Enter bestätigen. Jetzt SSH auswählen und mit Enter öffnen. Dort Enable bestätigen.
3. “Finish” wählen und 
 ` sudo reboot `


## 6. Via Konsole mit SSH Verbinden

1. Mit dem Kommando “Ifconfig” auf der Konsole/Terminal die IP-Adresse auslesen

![raspi-ifconfig](https://cloud.githubusercontent.com/assets/21320216/19016671/c28c9980-8821-11e6-8774-ad2a0da8f6dc.jpg)



## 7. Raspberry Pi Remote konfigurieren

1. Nachdem die IP-Adresse oder den Hostnamen (raspberrypi) in der Terminal eingegeben wurde, sollte sich ein Terminal öffnen das nach einem Benutzer und Passwort fragt.
	- dort mit den bekannten Daten (pi & raspberry) einloggen 
2. Konfiguration führen
	`sudo raspi-config`
	
  - Schritt 1: Expand Filesystem markieren und Enter drücken, mit Ok bestätigen
  - Schritt 2: Change User Password markieren und Enter drücken. Die nächste Meldung mit Ok bestätigen und in der Konsole das neue Passwort eingeben.
  - Schritt 3: Enable Boot to Desktop/Scratch markieren und Enter drücken
  - Schritt 4: Internationalisation Options markieren und mit Enter öffnen.
     - Change Locale auswählen -> in der Liste de_DE.UTF-8 UTF 8 mit Leertaste markieren  -> Enter drücken und de_DE.UTF-8 auswählen  -> Enter drücken.
    - Wieder in Menüpunkt 4 und diesmal Change Timezone -> Enter auswählen -> die richtige Zeitzone einstellen 
  - Schritt 5: Overclock markieren -> Enter drücken -> die Warnung mit Enter bestätigen -> Medium markieren und Enter drücken 
  - Step 6: Advanced Options markieren und mit Enter bestätigen. 
     - Memory Split auswählen und mit Enter öffnen. Dort 16 eintragen und mit Enter bestätigen.
- Schritt 7: Finish über zwei mal Tabulator drücken wählen und mit Enter bestätigen. Danach zum Abschluss im Terminal folgendes eintippen:
	`sudo reboot`


## 8. System aktualisieren-2

Nach dem Reboot wir noch eine Paketaktualisierung mit folgenden Befehlen gemacht:
       `sudo apt-get update
	sudo apt-get upgrade
	sudo reboot`
- Damit ist der Pi nun startklar für den ersten Projekt

- Befehl für die Ausschalten des Rasspberry Pi : 
	`sudo shutdown -h now`



## 9. Apache2 Webserver für OwnCloud installieren und testen

1. Apache2 Webserver installieren 
	`sudo apt-get install apache2 -y`
2. Der WEB SERVER testen
 - http://localhost/
 - http://Raspberrys Pi`s Adress
 - die Raspberry Pi Adresse herausfinden: `hostname -I`
	
![apache-it-works](https://cloud.githubusercontent.com/assets/21320216/19016867/fa589f26-8826-11e6-9091-ab9024e5b60e.png)
- Das zeigt, das der Apache Webserver funktioniert

3. Ändern des Standard-WEBSEITE
- Diese Standard-Web-Seite ist nur eine HTML-Datei auf dem Dateisystem . Es befindet sich auf: `/var/www/html/index.html`
- Hinweis: Das Verzeichnis war `/ var / www` in Raspbian Wheezy ist aber jetzt `/ var / www / html` in Raspbian Jessie
- Navigieren zu diesem Verzeichnis im Terminal 
	`cd /var/www/html
	 ls -al`



## 10.PHP Modul installieren und testen
1. Installieren
	`sudo apt-get install php5`
2. Installation testen
- Das Verzeichnis wechseln (/var/www)
	`cd /var/www`
3. Die Datei phpinfo.php erstellen
	`sudo nano phpinfo.php`
4. Mit dem Nano Editor den folgenden Text in die Datei schreiben:
       `<?php
	phpinfo();
	?>`
5. CTRL + X; CTRL + O verwenden
6. In dem Browser die IP Adresse + php.info eingeben
![8_phpinfo](https://cloud.githubusercontent.com/assets/21320216/19017087/c5006572-882e-11e6-8fdd-cf9b8a27701e.png)

- Somit ist PHP erfolgreich auf dem Raspberry Pi installiert!


## 11. MySQL installieren

1. Root Rechte holen
	`sudo bash`
2. MySQL installieren
	`apt-get install mysql-server mysql-client php5-mysql`
3. Passwort festlegen
4. Neustart
	`sudo restart`


## 12. phpMyAdmin instalieren

1. Root Rechte holen
	`sudo bash`
2. phpMyAdmin installieren
	`apt-get install libapache2-mod-auth-mysql php5-mysql phpmyadmin`
3. phpMyAdmin auf Apache konfigurieren
 - "apache2" auswählen
4. Datenbanken automatisch erstellen
 - Das System benötigt ein paar Datenbanken für die korrekte Funktion. Mit YES bestätigen
5. Passwort für phpMyAdmin und Datenbaknenserver
6. Installation testen
 -  die Adresse http://ip-adresse-deines-pis/phpmyadmin/ aufrufen

![phomyphpadmin](https://cloud.githubusercontent.com/assets/21320216/19017123/c43e70b0-882f-11e6-9349-6103fa47d42b.png)

- Somit läuft phpMyAdmin auf deinem Raspberry Pi!
