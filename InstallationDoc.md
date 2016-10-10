Inhaltsverzeichnis
		
1. [Raspian installieren](#1raspian-installieren)
2. [Der erste Login & der Zugriff auf die GUI / das Grafische User Interface](2#der-erste-login-&-der-zugriff-auf-die-gui-/-das-grafische-user-interface)
3. [Via Konsole mit SSH Verbinden](#3via-konsole-mit-ssh-verbinden)
4. [System aktualisieren](#4-system-aktualisieren)
5. [Apache2 Webserver für OwnCloud installieren und testen](#5-apache2-webserver-f%C3%BCr-owncloud-installieren-und-testen)
6. [PHP Modul installieren und testen](#6php-modul-installieren-und-testen)
7. [MySQL installieren](#7-mysql-installieren)
8. [phpMyAdmin instalieren](#8-phpmyadmin-instalieren)

#Installation von OwnCloud
1. [Datenspeicher konfigurieren und mounten (USB-Stick)](#1datenspeicher-konfigurieren-und-mounten-(usb-stick))
2. [Owncloud installieren](#2owncloud-installieren)
3. [Datenbank einrichten](#3datenbank-einrichten)
4. [Webserver für OwnCloud mit SSL absichern](#4webserver-für-owncloud-mit-ssl-absichern)
5. [Webserver für OwnCloud konfigurieren](#5webserver-für-owncloud-konfigurieren)
6. [OwnCloud einrichten](#6owncloud-einrichten)
7. [Smartphone und Desktop Client Apps](#7smartphone-und-desktop-client-apps)
8. [Tunneling SSH over PageKite](#6tunneling-ssh- via-pagekite)


## 1.Raspian installieren



1. Raspbian mithilfe der Installer  NOOBS Lite installieren.

2.  SD-Karte (mindesten 8 GB gross) mit Disk Utiliy formatieren (FAT32). Die SD-Karte wird in SD Card Reader eingesteckt und mit dem PC verbunden

3.  NOOBS Like (www.raspberrypi.org/downloads) herunterladen und die ZIP Datei entpacken. Wir verwenden ein Network-Installer

4. Die Dateien, die sich in der heruntergeladenen ZIP-Datei befinden, auf die SD-Karte kopieren

5. Die SD-Karte in den Raspberry Pi stecken und diesen mit einem LAN-Kabel verbinden (+ Bildschirm via HDMI, USB Maus, USB Tastatur und der USB Netzteil )

6. Der Raspberry Pi mit der Speicherkarte starten und " Raspbian " auswählen

6. Der Raspberry musst eine Interbetverbindung haben, damit  die Instalationsdateien heruntergeladen werden können

7. Noobs startet und Raspian wird installiert

8. Nach der erfolgreichen Installation wird die Raspberry Pi Configuration (raspi-config) geladen. 
Hierbei sind verschiedene Einstellungen möglisch:

- Internationalisation Options ➜ Change Locale ➜ "de_DE.UTF-8 UTF-8" ➜ mit OK bestätigen
- Internationalisation Option ➜ Change Keyboard Layout ➜ Generic 105-key
- Internationalisation Option ➜ Change Timezone ➜ Europa, Schweiz
- Benutzer Password kann geändert werden
- Memory Split ➜ 16 MB einstellen
- Overclock : Medium
- Die Raspberry Pi Configuration mit einem Klick auf OK beenden und die Rückfrage nach einem Neustart mit Yes bestätigen


##2. Der erste Login & der Zugriff auf die GUI / das Grafische User Interface

Standardmäßig ist nach der Installation von Raspbian bereits ein Benutzer eingerichtet. 

`Benutzername: pi
Passwort: raspberry`


##3. Via Konsole mit SSH Verbinden

1. Mit dem Kommando “  Ifconfig ” auf der Konsole die IP-Adresse auslesen 

2. SSH Verbindung aus dem Pc machen 

	`$ ssh username@<IP-Adresse>  ( Beispiel: ssh pi@147.107.87.17 )

![raspi-ifconfig](https://cloud.githubusercontent.com/assets/21320216/19016671/c28c9980-8821-11e6-8774-ad2a0da8f6dc.jpg)

	` $ sudo reboot`


## 4. System aktualisieren


	Nachdem die IP-Adresse oder den Hostnamen (RaspberryPi) in der Terminal eingegeben wurde, sollte sich ein Terminal öffnen das nach einem Benutzer und Passwort fragt

	- dort mit den bekannten Daten (Standard : pi & raspberry) einloggen 

Mit aktuellster Software und Firmware versorgen

	- Die folgend Befehle werden angegeben um den Raspberry Pi zu aktualisieren 

	`$ sudo apt-get update`
	
	`$ sudo apt-get upgrade

	sudo reboot`
	

##5.  Apache2 Webserver für OwnCloud installieren und testen

- Damit der Apache (Webserver) installiert werden kann, werden Nutzergruppen benötigt – ansonsten schlägt die Installation fehl.  Mit den folgenden Befehlen werden die Standardnutzergruppen für den Apachen anlegt:

	 `sudo groupadd www-data
	 
	 sudo usermod -a -G www-data www-data

	sudo apt-get update
	
	sudo reboot`


1. Apache installieren 

	` $ sudo apt-get install apache2 `
	
2. Der WEB SERVER testen

 - http://localhost/
 
 - http://<IP-Adresse>/
 
 - die Raspberry Pi Adresse herausfinden: 
 
`if config`

![apache-it-works](https://cloud.githubusercontent.com/assets/21320216/19016867/fa589f26-8826-11e6-9091-ab9024e5b60e.png)
- Das zeigt, das der Apache Webserver funktioniert


3. Ändern des Standard-WEBSEITE 

- Diese Standard-Web-Seite ist nur eine HTML-Datei auf dem Dateisystem . Es befindet sich auf: `/var/www/html/index.html`

- Hinweis: Das Verzeichnis war `/ var / www` in Raspbian Wheezy ist aber jetzt `/ var / www / html` in Raspbian Jessie

- Navigieren zu diesem Verzeichnis im Terminal 

	`$ cd /var/www/html
	
	 $ ls -al`



##6.  PHP Modul installieren und testen 

1. Installieren

	`$ sudo apt-get install php5 libapache2-mod-php5 -y`  https://www.raspberrypi.org/documentation/remote-access/web-server/apache.md

2. Installation testen
- Das Verzeichnis wechseln (/var/www)

	`$ cd /var/www`

3. `index.html` löschen

	`sudo rm index.html`
	
4. Die Datei phpinfo.php erstellen

	`$ sudo nano phpinfo.php`
	
5. Mit dem Nano Editor den folgenden Text in die Datei schreiben:

       `<?php
	phpinfo();
	?>`
	
6. CTRL + O; CTRL + X verwenden

7. In dem Browser die IP Adresse + php.info eingeben

Test Bild Apache2 Installation

- Somit ist PHP erfolgreich auf dem Raspberry Pi installiert!



##7. MySQL installieren 

1. Root Rechte holen

	`$ sudo bash`
	
	
2. MySQL installieren

	`apt-get install mysql-server mysql-client php5-mysql`
	
3. Passwort festlegen

Bild währen der Installation 
4. Neustart

	`$ sudo reboot`



##8. phpMyAdmin instalieren 

1. Root Rechte holen

	`$ sudo bash`
	
2. phpMyAdmin installieren

	`$ apt-get install libapache2-mod-auth-mysql php5-mysql phpmyadmin`

3. phpMyAdmin auf Apache konfigurieren

Bild während der Installation

 	 "apache2" auswählen

4. Datenbanken automatisch erstellen

 - Das System benötigt ein paar Datenbanken für die korrekte Funktion. Mit YES bestätigen

5. Passwort für phpMyAdmin und Datenbaknenserver
- Das Password des Root MySQL 

6. Installation testen
 -  die Adresse http://ip-adresse-des-Raspberry PI`s/phpmyadmin/ aufrufen

- Somit läuft phpMyAdmin auf deinem Raspberry Pi!

! Wichtige Tipps ! 
- ein sicheres Passwort zu wählen ist wichtig
- den Zugriff nur auf das lokale Netz zu beschränken
- diese schritte sollte man unbedingt machen ansonsten ist die PhpMyAdmin Oberfläche aus dem internet erreichbar




#Installation von OwnCloud


##1. Datenspeicher konfigurieren und mounten (USB-Stick)

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

5. Zum automatisch mounten des richtigen USB-Sticks wird die fstab Datei mit NANO editiert:
   
	`$ sudo nano /etc/fstab `
	
6.  Am Ende der Datei die folgende Zeile einführen und mit UUID ersetzen

	- nach der nächsten Neustart wird der USB-Stick unter /media/usb-hdd/ automatisch eingehängt

	“ UUID=1C5638245637FCD8 /media/usb-hdd/ ntfs-3g permissions,defaults,auto ”

7. Rebooten
   
	` 	`$ sudo reboot `
	
	- Tipp: Nach dem Reboot überprüfen, ob der USB-Stick über  /media/usb-hdd/ zugreifbar ist 



## 2. Owncloud installieren


	1. Das OwnCloud Repository einfügen
	
	`wget -nv https://download.owncloud.org/download/repositories/stable/Debian_8.0/Release.key -O Release.key
	sudo apt-key add - < Release.key
	sudo sh -c "echo 'deb http://download.owncloud.org/download/repositories/stable/Debian_8.0/ /' >> /etc/apt/sources.list.d/owncloud.list `

	- diese Befehl wird die Software installieren und später problemlos auch die Software aktualisieren

        `sudo apt-get update
	  sudo apt-get install owncloud `

	2. Der Installier wird nach einem Root Password für die MySQL Datenbank fragen (es ist empfohlen, dieses sicher zu merken)


##3. Datenbank einrichten

1. Das MySQL Datenbank öffnen
	
	` sudo mysql -u root -p `
	
2. Datenbank “owncloud” erstellen
   
	` CREATE DATABASE owncloud; `
	
3. Einen Benutzer erstellen (Name: owncloud und eine sichere Passwort)
   
	` CREATE USER 'owncloud'@'localhost' IDENTIFIED BY 'SicheresPasswort'; 

4. Diese Benutzer wird Reche bekommen nur auf die gerade erstellte Datenbank
	
	 GRANT ALL PRIVILEGES ON owncloud.* TO 'owncloud'@'localhost'; `

5. Das Remote Login für den root dezaktivieren
   
	` DELETE FROM mysql.user WHERE User='root' AND Host NOT IN ('localhost', '127.0.0.1’,); `
	
6. Die MySQL Eingabe beenden
   
	` FLUSH PRIVILEGES;
	  exit; `



##4. Webserver für OwnCloud mit SSL absichern

Mit dem SSL Zertifikat werden die Daten, die über Netz übertragen verden verschlüsselt.

	` $ sudo openssl genrsa -out server.key 4096
	  $ sudo openssl req -new -key server.key -out server.csr `

Nachdem die oben stehenden Befehle eingeben würden werden ein paar Fragen gestellt:
	  
   1. Common Name - Hostname oder den kompletten DynDNS Namen des Raspbis : “raspberrypi”
Bild währen der Installation machen + eventuell mit Sketch bearbeiten

   2. Digitales SSL Zertifikat erstellen
   
	` $ sudo openssl x509 -req -days 1825 -in server.csr -signkey server.key -out server.crt -sha256 `
	
	- die “server.crt” Datei ist nun der SSL-Zertifikat

	- “server.key” ist der Schlüssel

  3. Diese Dateien werden in ein anderes Verzeichnis verschieben  für die spätere Verwendung
  
	`$ sudo chmod 400 server.key

 	 $ sudo mv server.key /root/server.key
	 
	 $ sudo mv server.crt /root/server.crt `



## 5. Webserver für OwnCloud konfigurieren

1.Das DocumentRoot anpassen ( um nicht immer “/owncloud” hinten an URL anhängen zu müssen )

	` sudo nano /etc/apache2/sites-available/000-default.conf `

2. Innerhalb der Datei das DocumentRoot von 

`/var/www/html`  in folgenden Pfad verschieben   `DocumentRoot /var/www/owncloud`

- Speichern mit CTRL+X und Y 

3. “html” Verzeichnis löschen

	`sudo rm -rf /var/www/html/`

4. Die SSL Verschlüsselung mit Nano editieren

`sudo nano /etc/apache2/sites-available/default-ssl.conf`

- Die Pfade zu der generierten Datei anpassen

	`SSLCertificateFile /root/server.crt

	SSLCertificateKeyFile /root/server.key`

 - Innerhalb der Datei das DocumentRoot ändern

`DocumentRoot: /var/www/owncloud`

→ Speichern

5. SSL Verschlüsselung aktivieren && speichern && der Server neu starten

	`sudo a2ensite default-ssl.conf

	sudo a2enmod ssl

	sudo service apache2 force-reload `

6. Die Konfiguration Nano editieren

	`sudo nano /etc/apache2/sites-available/default`


2 Alternative:
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


##6. OwnCloud einrichten

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
  - Datenbank: MySQL (mit den vorher angegebenen Zugangsdaten)

Wichtig!!
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


##7. Smartphone und Desktop Client Apps

Um auf die eigene Cloud zuzugreifen, git es verschiedenen Möglichkeiten. Das Smartphone kann via iOS oder Android App zugreifen, der Desktop Rechner via Desktop Client oder über das Bekannte Webinterface mit einem beliebigen Browser.

[desktopapp](https://cloud.githubusercontent.com/assets/21320216/19246178/57e2d418-8f25-11e6-8c32-0311ec18e59e.jpg)


##8. Tunneling SSH via PageKite

SSH kann über PageKite getunnelt werden, so dass Sie Ihren SSH-Server von überall erreichbar sein kann, auch wenn es hinter NAT oder einer strengen Firewall ist.

![image002](https://cloud.githubusercontent.com/assets/21320216/19147267/a3c913ae-8bb7-11e6-994e-68fc8b98fe2c.png)

