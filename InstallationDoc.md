
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
13. [Datenspeicher konfigurieren und mounten](#13-datenspeicher-konfigurieren-und-mounten)
14. [Owncloud installieren](#14-owncloud-installieren)
15. [Webserver für OwnCloud mit SSL absichern](#15-webserver-für-owncloud-mit-ssl-absichern)
16. [Webserver für OwnCloud konfigurieren](#16-Webserver-für-owncloud-konfigurieren)
17. [OwnCloud Einrichten](#17-owncloud-einrichten)
18. [Smartphone und Desktop Client Apps](#18-smartphone-und-desktop-client-apps)
19. [Tunneling SSH over PageKite](#19-tunneling-ssh-over-pagekite)


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
	
1. Im Terminal über  `$ raspi-config`  konfigurieren

![raspi-config2](https://cloud.githubusercontent.com/assets/21320216/19016649/0ac09662-8821-11e6-865e-62c679fbea56.png)

  1.1 Mit den Pfeiltasten Internationalisation Options markieren und mit Enter öffnen.
	- Change Keybord Layout: Generic 105
	- die Sprache wählen: German
2. Um über PC zugreifen zu können muss SSH aktiviert sein.
	- Im Hauptmenu Advanced Options markieren und mit Enter bestätigen. Jetzt SSH auswählen und mit Enter öffnen. Dort Enable bestätigen.
3. “Finish” wählen und 
 ` $sudo reboot `


## 6. Via Konsole mit SSH Verbinden

1. Mit dem Kommando “Ifconfig” auf der Konsole/Terminal die IP-Adresse auslesen

![raspi-ifconfig](https://cloud.githubusercontent.com/assets/21320216/19016671/c28c9980-8821-11e6-8774-ad2a0da8f6dc.jpg)



## 7. Raspberry Pi Remote konfigurieren

1. Nachdem die IP-Adresse oder den Hostnamen (raspberrypi) in der Terminal eingegeben wurde, sollte sich ein Terminal öffnen das nach einem Benutzer und Passwort fragt.
	- dort mit den bekannten Daten (pi & raspberry) einloggen 
2. Konfiguration führen

	`$ sudo raspi-config`
	
  - 1. Expand Filesystem markieren und Enter drücken, mit Ok bestätigen
  - 2. Change User Password markieren und Enter drücken. Die nächste Meldung mit Ok bestätigen und in der Konsole das neue Passwort eingeben.
  - 3. Enable Boot to Desktop/Scratch markieren und Enter drücken
  - 4. Internationalisation Options markieren und mit Enter öffnen.
     - Change Locale auswählen -> in der Liste de_DE.UTF-8 UTF 8 mit Leertaste markieren  -> Enter drücken und de_DE.UTF-8 auswählen  -> Enter drücken.
    - Wieder in Menüpunkt 4 und diesmal Change Timezone -> Enter auswählen -> die richtige Zeitzone einstellen 
  - 5. Overclock markieren -> Enter drücken -> die Warnung mit Enter bestätigen -> Medium markieren und Enter drücken 
  - 6. Advanced Options markieren und mit Enter bestätigen. 
     - Memory Split auswählen und mit Enter öffnen. Dort 16 eintragen und mit Enter bestätigen.
  - 7. Finish über zwei mal Tabulator drücken wählen und mit Enter bestätigen. Danach zum Abschluss im Terminal folgendes eintippen:
  
	`$ sudo reboot`


## 8. System aktualisieren-2

Nach dem Reboot wir noch eine Paketaktualisierung mit folgenden Befehlen gemacht:
       `$ sudo apt-get update
       
	$ sudo apt-get upgrade
	
	$ sudo reboot`
- Damit ist der Pi nun startklar für den ersten Projekt

- Befehl für die Ausschalten des Rasspberry Pi : 

	`$ sudo shutdown -h now`


## 9. Apache2 Webserver für OwnCloud installieren und testen

- Damit der Apache (Webserver) installiert werden kann, werden Nutzergruppen benötigt – ansonsten schlägt die Installation fehl.  Mit den folgenden Befehlen werden die Standardnutzergruppen für den Apachen anlegt:

`sudo groupadd www-data

sudo usermod -a -G www-data www-data`


1. Apache2 Webserver installieren 

	`$ sudo apt-get install apache2 -y`
	
2. Der WEB SERVER testen

 - http://localhost/
 
 - http://<IP-Adresse>/
 
 It works!
 
 - die Raspberry Pi Adresse herausfinden: 
 
 `$ hostname -I`
	
![apache-it-works](https://cloud.githubusercontent.com/assets/21320216/19016867/fa589f26-8826-11e6-9091-ab9024e5b60e.png)
- Das zeigt, das der Apache Webserver funktioniert

3. Ändern des Standard-WEBSEITE
- Diese Standard-Web-Seite ist nur eine HTML-Datei auf dem Dateisystem . Es befindet sich auf: `/var/www/html/index.html`
- Hinweis: Das Verzeichnis war `/ var / www` in Raspbian Wheezy ist aber jetzt `/ var / www / html` in Raspbian Jessie
- Navigieren zu diesem Verzeichnis im Terminal 

	`$ cd /var/www/html
	
	 $ ls -al`


## 10. PHP Modul installieren und testen
1. Installieren

	`$ sudo apt-get install php5`
	
2. Installation testen
- Das Verzeichnis wechseln (/var/www)

	`$ cd /var/www`
	
3. Die Datei phpinfo.php erstellen

	`$ sudo nano phpinfo.php`
	
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


	`$ sudo bash`
	
	
2. MySQL installieren

	`apt-get install mysql-server mysql-client php5-mysql`
	
3. Passwort festlegen
4. Neustart

	`$ sudo restart`


## 12. phpMyAdmin instalieren

1. Root Rechte holen

	`$ sudo bash`
	
2. phpMyAdmin installieren

	`$ apt-get install libapache2-mod-auth-mysql php5-mysql phpmyadmin`
	
3. phpMyAdmin auf Apache konfigurieren
 - "apache2" auswählen
4. Datenbanken automatisch erstellen
 - Das System benötigt ein paar Datenbanken für die korrekte Funktion. Mit YES bestätigen
5. Passwort für phpMyAdmin und Datenbaknenserver
6. Installation testen
 -  die Adresse http://ip-adresse-deines-pis/phpmyadmin/ aufrufen

![phomyphpadmin](https://cloud.githubusercontent.com/assets/21320216/19017123/c43e70b0-882f-11e6-9349-6103fa47d42b.png)

- Somit läuft phpMyAdmin auf deinem Raspberry Pi!


! Wichtige Tipps ! 
- ein sicheres Passwort zu wählen ist wichtig
- den Zugriff nur auf das lokale Netz möglich zu sein
- diese schritte sollte man unbedingt machen ansonsten ist die PhpMyAdmin Oberfläche aus dem internet erreichbar

1. Per ssh am pi  anmelden

2. `sudo nano /etc/apache2/conf.d/phpmyadmin.conf  ( symlink auf /etc/phpmyadmin/apache.conf)`

3. Datei folgendermaßen anpassen :

` <directory /usr/share/phpmyadmin>
        options followsymlinks
        directoryindex index.php
        order deny,allow
        deny from all
        allow from 192.168.2.0/24  <- hier natürlich euer netzwerk rein
        <ifmodule mod_php5.c> `

4. Datei speichern
5. Apache restarten 

`/etc/init.d/apache2 restart `

  - jetzt ist die phpmyadmin oberfläche nur noch aus dem lokalen netzwerk erreichbar.


*** Test nicht erfolgreich???
- falls der browser nichts anzeigt versuche das Problem mit folgendem Code zu beheben

`ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf.d/phpmyadmin.conf`

- nun noch die Änderungen neu laden und wie in Sßchritt 7 testen

`/etc/init.d/apache2 reload`

`sudo reboot`



## 13. [Datenspeicher konfigurieren und mounten](#Datenspeicher konfigurieren und mounten)
    1. Der Treiber installieren, damit NTFS Speichermedien eingebunden werden kann
   
	`$ sudo apt-get -y install ntfsprogs `
	
   2. Neue Ordner in Verzeichnis /media anlegen (hier wird später der Usb-Speichermedium eingebunden - ist als Mountpoint gennant)
   
	`$ sudo mkdir /media/usb-hdd `	
	
   3. Die Log Ausgabe aktivieren, um herauszufinden welchem Gerät die Festplatte zugeordnet wird
   
	`$ tail –f /var/log/messages `
	
     - es kann sein, dass die USB-Stick als `sda1` erkannt ist
   4. Der folgende Befehl angeben, um die UUID der Festplatte zu erhalten, und ersetzt SDA1 mit dem Gerät
   
	`$ sudo blkid /dev/sda1 `
	
	- der UUID notieren
   5. Zum automatisch mounten des richtigen USB-Sticks wird die “fstab” mit NANO editiert
   
	`$ sudo nano /etc/fstab `
	
   6. Am Ende der Datei die folgende Zeile einführen und mit UUID ersetzen
	- nach der nächsten Neustart wird der USB-Stick unter /media/usb-hdd/ automatisch eingehängt
	“ UUID=1C5638245637FCD8 /media/usb-hdd/ ntfs-3g permissions,defaults,auto ”
   7. Rebooten
   
	` 	`$ sudo reboot `
	
	- Tipp: Nach dem Reboot überprüfen, ob der USB-Stick über  /media/usb-hdd/ zugreifbar ist 


## 14. Owncloud installieren

   1. Das OwnCloud Repository einfügen

wget -nv https://download.owncloud.org/download/repositories/stable/Debian_8.0/Release.key -O Release.key
sudo apt-key add - < Release.key
sudo sh -c "echo 'deb http://download.owncloud.org/download/repositories/stable/Debian_8.0/ /' >> /etc/apt/sources.list.d/owncloud.list"
	- diese Befehl wird die Software installieren und später problemlos die Software auch aktualisieren
   2. Root Passwort für die MySQL Datenbank auswählen

   3. Datenbank einrichten
	- Auf dem MySQL Server neue Datenbank einrichten
	- die MySQL öffnen
	
	` sudo mysql -u root -p `
	
   4. Benutzer erstellen
   
	` CREATE DATABASE owncloud; `
	
   5. Noch einen Benutzer erstellen (Name: owncloud und eine sichere Passwort)
   
	` CREATE USER 'owncloud'@'localhost' IDENTIFIED BY 'SicheresPasswort'; 
	
	` GRANT ALL PRIVILEGES ON owncloud.* TO 'owncloud'@'localhost'; `
	
   6. Das Remote Login für den root dezaktivieren
   
	` DELETE FROM mysql.user WHERE User='root' AND Host NOT IN ('localhost', '127.0.0.1', '::1'); `
	
   7. Die MySQL Eingabe beenden
   
   
	` FLUSH PRIVILEGES;
	  exit; `

## 15. Webserver für OwnCloud mit SSL absichern

	` $ sudo openssl genrsa -out server.key 4096
	
	  $ sudo openssl req -new -key server.key -out server.csr `
	  
   1. Common Name - Hostname oder den kompletten DynDNS Namen des Raspbis : “raspberrypi”
   2. Digitales SSL Zertifikat erstellen
   
	` $ sudo openssl x509 -req -days 1825 -in server.csr -signkey server.key -out server.crt -sha256 `
	
	- die “server.crt” Datei ist nun unser SSL-Zertifikat
  3. Die Dateien daher in ein anderes Verzeichnis für die spätere Verwendung verschieben
  
	`$ sudo chmod 400 server.key

 	 $ sudo mv server.key /root/server.key
	 
	 $ sudo mv server.crt /root/server.crt `

## 16. Webserver für OwnCloud konfigurieren

Version 1:
  1.Das DocumentRoot anpassen ( um nicht immer “/owncloud” hinten an URL anhängen zu müssen )

` sudo nano /etc/apache2/sites-available/000-default.conf `

  2. Innerhalb der Datei das DocumentRoot von 

`/var/www/html` 

in folgenden Pfad ändern

`DocumentRoot /var/www/owncloud`

- Speichern mit CTRL+X und Y 

  4. “html” Verzeichnis löschen

	`sudo rm -rf /var/www/html/`

  5. Die SSL Verschlüsselung mit Nano editieren

`sudo nano /etc/apache2/sites-available/default-ssl.conf`

  6. Die Pfade zu der generierten Datei anpassen

`SSLCertificateFile /root/server.crt
SSLCertificateKeyFile /root/server.key
`
  7. Innerhalb der Datei das DocumentRoot ändern

`DocumentRoot: /var/www/owncloud`
→ Speichern

  8. SSL Verschlüsselung aktivieren && speichern && der Server neu starten

`sudo a2ensite default-ssl.conf

sudo a2enmod ssl

sudo service apache2 force-reload`

  9. Die Konfiguration Nano editieren

`sudo nano /etc/apache2/sites-available/default`


Version 2:
1. Am Ende der Datei die folgende Konfiguration für OwnCloud Webseite einfügen && speichern

`<VirtualHost *:443>
DocumentRoot /var/www/owncloud
ServerName raspberrytips.ddns.net
SSLEngine on
SSLCertificateFile /root/server.crt
SSLCertificateKeyFile /root/server.key
</VirtualHost>

2. SSL Verschlüsselung aktivieren und restarten

`sudo a2enmod ssl

 sudo apache2ctl restart`





##17. OwnCloud Einrichten

1. Ein Verzeichnis auf dem USB-Stick liegen und dessen Rechte anpassen 

	`sudo mkdir -p /media/usb-hdd/owncloud/data
	sudo chown -R www-data:www-data /media/usb-hdd/owncloud/data
	sudo chmod 0770 /media/usb-hdd/owncloud/data
 
	sudo reboot`

2.Die OwnCloud im Browser aufrüfen mit “ https://cloudspeicher.bfh.ch/owncloud“ (mit der angepassten Adresse)

  !- wenn das klappt, das heisst das OwnCloud erfolgreich installiert ist
  !- falls nicht klappt können aus verschiedenen Gründen sein:
    - entweder die IP-Adresse ist vom DynDNS Client nicht aktualisiert oder der Router reicht nicht richtig die Anfragen an den Raspberry Pi weiter
  ! - Im Problemfall ist es möglisch erstmal auch die interne Adresse des Pis aufzurufen und auf den Zugriff via Internet zu verzichten

- https://raspberrypi/owncloud/  oder

- https://<IP-Adresse des RasPi>/owncloud/

3. Konfigurtionkatalog des OwnClouds
  - ein Admin Benutzer angeben
  - eine feste Password
  - Speicher und Datenbank auswählen und die Pfad des USB-Stick angeben z.B  `/media/usb-hdd/owncloud/data`
  - Datenbank: MySQL


Wichtig!
Da das Datenverzeichnis geändert würde, müssen die Berechtigungen anpassen werden.
Mit den folgenden Befehle:

	`sudo find /var/www/owncloud/ -type f -print0 | sudo xargs -0 chmod 0640
	sudo find /var/www/owncloud/ -type d -print0 | sudo xargs -0 chmod 0750
 
	sudo chown -R root:www-data /var/www/owncloud/
	sudo chown -R www-data:www-data /var/www/owncloud/apps/
	sudo chown -R www-data:www-data /var/www/owncloud/config/
	sudo chown -R www-data:www-data /media/usb-hdd/owncloud/data/
	sudo chown -R www-data:www-data /var/www/owncloud/themes/
 
	sudo chown root:www-data /var/www/owncloud/.htaccess
	sudo chown root:www-data /media/usb-hdd/owncloud/data/.htaccess
 
	sudo chmod 0644 /var/www/owncloud/.htaccess
	sudo chmod 0644 /media/usb-hdd/owncloud/data/.htaccess
 
	sudo reboot `

- nachdem ist es möglsih auf eigenen OwnCouud zu landen

![owncloud](https://cloud.githubusercontent.com/assets/21320216/19146318/3fb8caa2-8bb3-11e6-9536-79ac0221ab30.png)




## 18.Smartphone und Desktop Client Apps

Um auf die eigene Cloud zuzugreifen, git es verschiedenen Möglichkeiten. Das Smartphone kann via iOS oder Android App zugreifen, der Desktop Rechner via Desktop Client oder über das Bekannte Webinterface mit einem beliebigen Browser.

![screen_shot_2016-10-06_at_10_24_07](https://cloud.githubusercontent.com/assets/21320216/19145904/7640824c-8bb1-11e6-84f8-8cc903d56226.jpg)




##19. Tunneling SSH over PageKite

SSH kann über PageKite getunnelt werden, so dass Sie Ihren SSH-Server von überall erreichbar sein kann, auch wenn es hinter NAT oder einer strengen Firewall ist.

![image002](https://cloud.githubusercontent.com/assets/21320216/19147267/a3c913ae-8bb7-11e6-994e-68fc8b98fe2c.png)



