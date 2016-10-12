#Inhaltsverzeichnis
		
1. [Raspian installieren](#1-raspian-installieren)
2. [Grundeinrichtung System, Tastatur und Sprache](#2-grundeinrichtung-system-tastatur-und-sprache)
3. [Der erste Login Grafische User Interface](#3-der-erste-login-grafische-user-interface)
4. [Via Konsole mit SSH verbinden](#4-via-konsole-mit-ssh-verbinden)
5. [System aktualisieren](#5-system-aktualisieren)
6. [Apache2 Webserver für OwnCloud installieren und testen](#6--apache2-webserver-für-owncloud-installieren-und-testen)
7. [PHP Modul installieren und testen](#7--php-modul-installieren-und-testen)
8. [MySQL installieren](#8-mysql-installieren)
9. [phpMyAdmin instalieren](#9-phpmyadmin-instalieren)



#Installation von OwnCloud

1. [Datenspeicher konfigurieren und mounten USB-Stick](#1-datenspeicher-konfigurieren-und-mounten-usb-stick)
2. [Owncloud installieren](#2-owncloud-installieren)
3. [Datenbank einrichten](#3-datenbank-einrichten)
4. [Webserver für OwnCloud mit SSL absichern](#4-webserver-für-owncloud-mit-ssl-absichern)
5. [Webserver für OwnCloud konfigurieren](#5-webserver-für-owncloud-konfigurieren)
6. [OwnCloud einrichten](#6-owncloud-einrichten)
7. [Smartphone und Desktop Client Apps](#7-smartphone-und-desktop-client-apps)
8. [Tunneling SSH over PageKite](#8-tunneling-ssh-via-pagekite)




##1. Raspian installieren


1. Raspbian mithilfe der Installer  NOOBS Lite installieren.

2.  SD-Karte (mindesten 8 GB ) mit Disk Utiliy formatieren (FAT32). Die SD-Karte wird in SD Card Reader eingesteckt und mit dem PC verbunden

3.  NOOBS Like (www.raspberrypi.org/downloads) herunterladen und die ZIP Datei entpacken. Wir verwenden ein Network-Installer

4. Die Dateien, die sich in der heruntergeladenen ZIP-Datei befinden, auf die SD-Karte kopieren

5. Die SD-Karte in den Raspberry Pi einstecken und diesen mit einem LAN-Kabel verbinden

 6. Der Bildschirm via HDMI, USB Maus, USB Tastatur und der USB Netzteil werden auch verbunden

7. Der Raspberry Pi mit der Speicherkarte starten und " Raspbian " auswählen

8. Der Raspberry musst eine Interbetverbindung haben, damit  die Instalationsdateien heruntergeladen werden können

9. Noobs startet und Raspian wird installiert



##2. Grundeinrichtung System, Tastatur und Sprache

Nach der erfolgreichen Installation wird die Raspberry Pi Configuration (raspi-config) geladen. 
Hierbei sind verschiedene Einstellungen möglisch:

1.Expand Filesystem - Filesystem erweitern
2.Change User Password 
	a.Hier ist es möglisch die Password für der Benuter „pi“ zu wechseln
3.Internationalisation Options
	a.Change Locale (die Sprache anpassen) ➜ "de_DE.UTF-8 UTF-8" 
	b.Change Keyboard Layout ➜ Generic 105-key
	c.Change Timezone : Europe -> Schweiz
	d.Memory Split ➜ 16 MB einstellen
	e.Overclock : Medium

- Die Raspberry Pi Configuration mit einem Klick auf OK beenden und die Rückfrage nach einem Neustart mit Yes bestätigen


##3. Der erste Login Grafische User Interface

Standardmäßig ist nach der Installation von Raspbian bereits ein Benutzer eingerichtet. 

`Benutzername: pi
Passwort: raspberry`


##4. Via Konsole mit SSH verbinden

1.	Mit dem Kommando “  Ifconfig ” auf der Konsole die „inet addr“ auflesen 

2. SSH Verbindung aus dem PC machen 

	`$ ssh username@<IP-Adresse>  ( Beispiel: ssh pi@147.107.87.17 ) `


	` $ sudo reboot`


##5. System aktualisieren

- Nachdem der Raspberry Pi wieder gebootet ist wird den Raspberry Pi aktualisiert

- Dort mit den bekannten Daten (Standard : pi & raspberry) einloggen 

- Raspberry Pi aktualisieren 

	`$ sudo apt-get update`
	
	`$ sudo apt-get upgrade

	sudo reboot`
	


##6.  Apache2 Webserver für OwnCloud installieren und testen 

- Damit der Apache Webserver installiert werden kann, werden Nutzergruppen benötigt – ansonsten schlägt die Installation fehl.  Mit den folgenden Befehlen werden die Standardnutzergruppen für den Apachen anlegt:

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



##7.  PHP Modul installieren und testen 
1. Installieren

	`$ sudo apt-get install php5 libapache2-mod-php5 -y`  

2.	Das Verzeichnis wechseln (/var/www)

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

7. Testen  
- In dem Browser die IP Adresse + php.info eingeben

- Somit ist PHP erfolgreich auf dem Raspberry Pi installiert!



##8. MySQL installieren

1. Root Rechte holen

	`$ sudo bash`
	
	
2. MySQL installieren

`sudo bash`

	 `apt-get install mysql-server mysql-client php5-mysql`
	
3. Passwort festlegen

4. Neustart

	`$ sudo reboot`



##9. phpMyAdmin instalieren 

1. Root Rechte holen

	`$ sudo bash`
	
2. phpMyAdmin installieren

	`$ apt-get install libapache2-mod-auth-mysql php5-mysql phpmyadmin`

	
3. phpMyAdmin auf Apache konfigurieren

 	 "apache2" auswählen

4. Datenbanken automatisch erstellen

 - Das System benötigt ein paar Datenbanken für die korrekte Funktion. Mit YES bestätigen

5. Passwort für phpMyAdmin und Datenbaknenserver

- Das Password des Root MySQL 

6. Installation testen
 -  die Adresse http://ip-adresse-des-Raspberry PI`s/phpmyadmin/ aufrufen

! Wichtige Tipps ! 
- ein sicheres Passwort zu wählen ist wichtig
- den Zugriff nur auf das lokale Netz zu beschränken
- diese schritte sollte man unbedingt machen ansonsten ist die PhpMyAdmin Oberfläche aus dem internet erreichbar




#Installation von OwnCloud


##1. Datenspeicher konfigurieren und mounten USB-Stick

1. Der Treiber installieren, damit NTFS Speichermedien eingebunden werden kann
   
	`$ sudo apt-get -y install ntfsprogs `
	
2. Neue Ordner in Verzeichnis /media anlegen (hier wird später der USB-Speichermedium eingebunden - ist als Mountpoint gennant)
   
	`$ sudo mkdir /media/usb-hdd `	
	
3. Die Log Ausgabe aktivieren, um herauszufinden welchem Gerät die Festplatte zugeordnet wird
   
	`$ tail –f /var/log/messages `
	
     - es kann sein, dass die USB-Stick als `sda1` erkannt ist

4. Der folgende Befehl angeben, um die UUID der Festplatte zu erhalten, und ersetzt SDA1 mit dem Gerät
   
	`$ sudo blkid /dev/sda1 `
	
	- der UUID notieren

5. Zum automatisch mounten des richtigen USB-Sticks wird die fstab Datei mit NANO editiert:
   
	`$ sudo nano /etc/fstab `
	
6.  Am Ende der Datei die folgende Zeile einführen.
Die UUID richtig anpassen.

	“ UUID=1C5638245637FCD8 /media/usb-hdd/ ntfs-3g permissions,defaults,auto ”

- nach dem nächsten Neustart wird der USB-Stick unter /media/usb-hdd/ automatisch eingehängt


7. Rebooten
   
	` 	`$ sudo reboot `
	
	- Tipp: Nach dem Reboot überprüfen, ob der USB-Stick über  /media/usb-hdd/ zugreifbar ist 




##2. Owncloud installieren

1. Das OwnCloud Repository einfügen


	`wget -nv https://download.owncloud.org/download/repositories/stable/Debian_8.0/Release.key -O Release.key
	sudo apt-key add - < Release.key
	sudo sh -c "echo 'deb http://download.owncloud.org/download/repositories/stable/Debian_8.0/ /' >> /etc/apt/sources.list.d/owncloud.list `

	- diese Befehl wird die Software installieren und später auch die Software aktualisieren

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

2. Digitales SSL Zertifikat erstellen
   
	` $ sudo openssl x509 -req -days 1825 -in server.csr -signkey server.key -out server.crt -sha256 `
	
	- die “server.crt” Datei ist nun der SSL-Zertifikat

	- “server.key” ist der Schlüssel

3. Diese Dateien werden in ein anderes Verzeichnis verschieben für die spätere Verwendung
  
	`$ sudo chmod 400 server.key

 	 $ sudo mv server.key /root/server.key
	 
	 $ sudo mv server.crt /root/server.crt `



##5. Webserver für OwnCloud konfigurieren

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


Alternative:
1. Am Ende der Datei die folgende Konfiguration für OwnCloud Webseite einfügen && speichern

` <VirtualHost *:443>
DocumentRoot /var/www/owncloud
ServerName raspberrytips.ddns.net
SSLEngine on
SSLCertificateFile /root/server.crt
SSLCertificateKeyFile /root/server.key
</VirtualHost> `

2. SSL Verschlüsselung aktivieren und restarten

`sudo a2enmod ssl

 sudo apache2ctl restart`




##6. OwnCloud einrichten

1. Ein Verzeichnis auf dem USB-Stick anliegen und dessen Rechte anpassen 

	` sudo mkdir -p /media/usb-hdd/owncloud/data
	sudo chown -R www-data:www-data /media/usb-hdd/owncloud/data
	sudo chmod 0770 /media/usb-hdd/owncloud/data
 
	sudo reboot `

2.Die OwnCloud im Browser aufrüfen mit:

 “ https://cloudspeicher.bfh.ch/owncloud“ (mit der angepassten Adresse)

oder

- https://raspberrypi/owncloud/  

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

Um auf die eigene Cloud zuzugreifen, gibt es verschiedenen Möglichkeiten. Das Smartphone kann via iOS oder Android App zugreifen, der Desktop Rechner via Desktop Client oder über das Bekannte Webinterface mit einem beliebigen Browser.

[desktopapp](https://cloud.githubusercontent.com/assets/21320216/19246178/57e2d418-8f25-11e6-8c32-0311ec18e59e.jpg)



##8. Tunneling SSH via PageKite

SSH kann über PageKite getunnelt werden, so dass Sie Ihren SSH-Server von überall erreichbar sein kann, auch wenn es hinter NAT oder einer strengen Firewall ist.

![desktopapp](https://cloud.githubusercontent.com/assets/21320216/19305382/e4d4af30-9070-11e6-8021-7f109801ca9c.jpg)

###Installationsanleitung

#### Add our repository to `/etc/apt/sources.list`

	`echo deb http://pagekite.net/pk/deb/ pagekite main | sudo tee -a /etc/apt/sources.list`

#### Add the PageKite packaging key to your key-ring

	`sudo apt-key adv --recv-keys --keyserver keys.gnupg.net AED248B1C7B2CAC3`

#### Refresh your package sources by issuing

	`sudo apt-get update`

#### Install pagekite !

	`sudo apt-get install pagekite`

	

`$ pagekite 80 yourname.pagekite.me` ➠ Access http://yourname.pagekite.me/ from anywhere!

