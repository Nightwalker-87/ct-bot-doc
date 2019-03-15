# CPU-Erweiterung für den c't-Bot

>> **Trac-2-Markdown Konvertierung:** *unchecked*

> **Trac-2-Markdown Konvertierung:** *deprecated*

## Installation von Ubuntu 12.04 LTS für ARM auf einem BeagleBoard

### Vorbereitungen

1. Herunterladen des Disk-Images *Texas Instruments OMAP3 (Hard-Float) preinstalled server image* von [http://cdimage.ubuntu.com/releases/12.04/release](http://cdimage.ubuntu.com/releases/12.04/release/ubuntu-12.04-preinstalled-server-armhf+omap.img.gz)
1. Entpacken und kopieren des Images auf eine Mikro-SD Karte: siehe [Installing pre-installed OMAP4 Precise (12.04) Server Images](https://wiki.ubuntu.com/ARM/Server/Install#Copy_the_image_to_SD_card)
1. Serielle Schnittstelle des BeagleBoards mit dem PC verbinden
1. Ethernet-Port des BeagleBoards an ein LAN mit Internetzugang anschließen
1. Ein Terminalprogramm starten und die serielle Schnittstelle, an der das BeagleBoard angeschlossen ist, öffnen
1. Mikro-SD-Karte ins BeagleBoard stecken und das Board mit Strom versorgen - vorzugsweise ein Netzteil benutzen (**5V**) - so dass das Board von der SD-Karte bootet
1. Im Terminalprogramm sollte es dann während des Bootens ungefähr so aussehen:
  ![Image: '01.png'](01.png)

### Installation von Ubuntu

* Nach dem Booten startet automatisch der Installationsassistent. Dort wählt man zunächst die gewünschte Sprache aus:
  ![Image: '02.png'](02.png)

* anschließend die Region:
  ![Image: '03.png'](03.png)
  ![Image: '04.png'](04.png)
  ![Image: '05.png'](05.png)

* und die Zeichenkodierung:
  ![Image: '06.png'](06.png)

* sowie die Zeitzone:
  ![Image: '07.png'](07.png)
  ![Image: '08.png'](08.png)

* Nun legt man einen User an, mit dem man sich später am System anmelden kann:
  ![Image: '09.png'](09.png)
  ![Image: '10.png'](10.png)
  ![Image: '11.png'](11.png)
  ![Image: '12.png'](12.png)
  ![Image: '13.png'](13.png)

* und vergibt einen Hostnamen:
  ![Image: '14.png'](14.png)

* Außerdem installiert man direkt einen SSH-Server mit:
  ![Image: '15.png'](15.png)

* Nach einiger Zeit ist die Installation abgeschlossen und man kann sich am System anmelden:
  ![Image: '16.png'](16.png)
  ![Image: '17.png'](17.png)
  ![Image: '18.png'](18.png)
  ![Image: '19.png'](19.png)

* Dann überprüft man am besten zunächst die Netzwerkkonfiguration mit `ifconfig`:
  ![Image: '20.png'](20.png)

### System aktualisieren

* Im nächsten Schritt sollte man das System auf einen aktuellen Stand bringen mit `sudo aptitude update`:
  ![Image: '21.png'](21.png)

* Nach Eingabe des zuvor gewählten Passworts für den Benutzer:
  ![Image: '22.png'](22.png)

* werden die Paketquellen aktualisiert und der Status angezeigt. Mit `sudo aptitude full-upgrade` startet man nun die Aktualisierung:
  ![Image: '23.png'](23.png)

* Die Sicherheitsabfrage beantwortet man mit `y`:
  ![Image: '24.png'](24.png)

* Die Ausgabe sollte ähnlich der Folgenden aussehen und es sollten keine Fehler angezeigt werden:
  ![Image: '25.png'](25.png)

* Jetzt startet man das System mit `sudo reboot` neu:
  ![Image: '26.png'](26.png)

* Anschließend erhält man erneut die Bootausgabe und kann sich wieder mit dem angelegten Benutzer anmelden:
  ![Image: '28.png'](28.png)
  ![Image: '29.png'](29.png)

* Von jetzt an kann man sich per SSH über die Ethernet Verbindung einloggen, was deutlich komfortabler ist als über die serielle Verbindung. Dazu startet man von einer Shell aus ssh unter Angabe von Benutzernamen des BeagleBoard-Systems und zugehöriger IP-Adresse, also z.B. `ssh bb@192.168.1.32`:
  ![Image: '30.png'](30.png)

* Da das System bisher unbekannt ist, stimmt man der Sicherheitsabfrage zu, gibt anschließend das Passwort des Benutzers ein und erhält eine Login-Shell auf dem BeagleBoard:
  ![Image: '31.png'](31.png)
  ![Image: '32.png'](32.png)

### Angepassten Kernel installieren

Damit das BeagleBoard mit der Hardware des c't-Bots kommunizieren kann, benötigt man einen speziell angepassten Kernel, der die Peripherie des Boards entsprechend konfiguriert und im Userspace zugänglich macht (siehe BeagleBoard). Die Versionsnummern im Folgenden bitte jeweils der verwendeten Kernelversion anpassen! Diese Kernelversion lässt sich wie folgt installieren:

* Z.B. über einen sftp-Client mit dem BeagleBoard verbinden:
  ![Image: '33.png'](33.png)

* Die heruntergeladenen Pakete für den Kernel auf das BeagleBoard kopieren (alternativ kann man sie auch auf die FAT-Partition der SD-Karte kopieren):
  ![Image: '34.png'](34.png)

* In das Verzeichnis mit den kopierten Paketen wechseln, im Beispiel mit `cd kernel-3.2.17-x11_0.1`:
  ![Image: '35.png'](35.png)

* Zuerst das Firmware-Image installieren mit `sudo dpkg --force-all -i ./linux-firmware-image_1.0cross_armhf.deb`:
  ![Image: '36.png'](36.png)
  ![Image: '37.png'](37.png)

* Im zweiten Schritt die Kernel-Header installieren mit `sudo dpkg -i ./linux-headers-3.2.17-x11_1.0cross_armhf.deb` (*Version entsprechend anpassen*):
  ![Image: '38.png'](38.png)

* Danach die libc-Header installieren mit `sudo dpkg -i ./linux-libc-dev_1.0cross_armhf.deb`:
  ![Image: '39.png'](39.png)

* Und abschließend das Kernel-Image installieren mit `sudo dpkg --force-all -i ./linux-image-3.2.17-x11_1.0cross_armhf.deb` (*Version entsprechend anpassen*):
  ![Image: '40.png'](40.png)

* Da die bereitgestellten Pakete derzeit eine abweichende Architekturbezeichnung tragen, muss man nun noch ein paar Dateien umbenennen, dazu mit `cd /boot` das Verzeichnis wechseln:
  ![Image: '41.png'](41.png)

* Und anschließend die Befehle `sudo mv vmlinux-3.2.17-x11 vmlinux-3.2.17-x11-omap`, `sudo mv initrd.img-3.2.17-x11 initrd.img-3.2.17-x11-omap`, `sudo mv config-3.2.17-x11 config-3.2.17-x11-omap` und `sudo mv System.map-3.2.17-x11 System.map-3.2.17-x11-omap` ausführen (*Versionen entsprechend anpassen*):
  ![Image: '42.png'](42.png)
  ![Image: '43.png'](43.png)
  ![Image: '44.png'](44.png)
  ![Image: '45.png'](45.png)

* Mit `sudo flash-kernel 3.2.17-x11-omap` (*Version entsprechend anpassen*) wird dann der neue Kernel auf der Boot-Partition installiert:
  ![Image: '46.png'](46.png)

* und mit `sudo reboot` gestartet:
  ![Image: '47.png'](47.png)

* Nach dem Reboot und einem erneuten Login (s.o.) teilt man dem Paketmanager mit, dass die installierte Kernel-Version nicht durch Distributionsupdates überschrieben werden soll. Dazu dient die folgenden, mehrzeilige Eingabe (*Versionen entsprechend anpassen*):

  ```shell
  sudo dpkg --set-selections << EOF
  linux-firmware-image hold
  linux-headers-3.2.17-x11 hold
  linux-image-3.2.17.x11 hold
  linux-libc-dev hold
  EOF
  ```

  ![Image: '49.png'](49.png)

* Anschließend kann man die alten Kernel-Versionen vollständig entfernen mit `sudo aptitude purge linux-image-3.2.0-23-omap`, `sudo aptitude purge linux-image-omap` und `sudo dpkg -P linux-image-3.2.0-24-omap`. Wichtig ist hierbei, dass die letzte Kernel-Version mit dpkg entfernt wird, damit der Paketmanager nicht auch die zugehörigen Hilfspakete entfernt:
  ![Image: '50.png'](50.png)
  ![Image: '51.png'](51.png)
  ![Image: '52.png'](52.png)

### WLAN konfigurieren

* Bevor man einen USB-WLAN-Adapter anschließt, sollte man sich zuerst einen Überblick über die derzeit angeschlossenen USB-Geräte verschaffen mit `lsusb`:
  ![Image: '54.png'](54.png)

* Die Ausgabe sollte dem obigen Beispiel entsprechen. Jetzt schließt man den WLAN-Adapter an und führt erneut `lsusb` aus. Der WLAN-Adapter sollte nun mit aufgelistet werden:
  ![Image: '55.png'](55.png)

* Nun kann man die Pakete *wpasupplicant* und *wireless-tools* mit `sudo aptitude install wpasupplicant` und `sudo aptitude wireless-tools` installieren:
  ![Image: '57.png'](57.png)
  ![Image: '58.png'](58.png)
  ![Image: '59.png'](59.png)

* Ein Aufruf von `iwconfig` sollte nun das Interface *wlan0* anzeigen:
  ![Image: '60.png'](60.png)
  ![Image: '61.png'](61.png)

* Im nächsten Schritt erzeugt man mit `wpa_passphrase <SSID>` den Pre-shared Key für die WPA2-Verschlüsselung, indem man anschließend das WPA2-Passwort eingibt:
  ![Image: '62.png'](62.png)

* Die Ausgabe des Programms kopiert man in die Zwischenablage, ruft `sudo nano /etc/wpa_supplicant.conf` auf:
  ![Image: '63.png'](63.png)

* und fügt die kopierte Ausgabe dort ein:
  ![Image: '64.png'](64.png)

* mit *CTRL + o* und *Enter* speichert man die Datei ab und schließt den Editor mit *CTRL + x*:
  ![Image: '65.png'](65.png)

* Jetzt kann man die WLAN-Verbindung testen, indem man `sudo wpa_supplicant -iwlan0 -c/etc/wpa_supplicant.conf -Dwext` ausführt:
  ![Image: '66.png'](66.png)

* Im Erfolgsfall bekommt man mit *CTRL-EVENT-CONNECTED* die Bestätigung für einen korrekten Verbindungsaufbau. Mit *CTRL + c* kann man den Test dann beenden:
  ![Image: '68.png'](68.png)

* Nun trägt man das Interface *wlan0* in */etc/network/interfaces* ein, indem man mit `sudo nano /etc/network/interfaces` einen Editor öffnet:
  ![Image: '69.png'](69.png)
und ergänzt:

  ```shell
  # The wifi interface
  auto wlan0
  iface wlan0 inet dhcp
  wpa-driver wext
  wpa-conf /etc/wpa_supplicant.conf
  ```
sodass die Datei wie folgt aussieht:
  ![Image: '70.png'](70.png)

* *CTRL + o* speichert die Datei und *CTRL + x* schließt den Editor wieder:
  ![Image: '71.png'](71.png)

* Das neu eingerichtete Interface aktiviert und testen man nun mit `sudo ifup -v wlan0`:
  ![Image: '72.png'](72.png)

* Die Ausgabe sollte ähnlich der Folgenden aussehen:
  ![Image: '73.png'](73.png)

* Außerdem überprüft man mit `ifconfig` die Konfiguration des Interfaces:
  ![Image: '74.png'](74.png)

* Nach einem Neustart mit `sudo reboot` kann man das Ethernet-Kabel entfernen und mit ssh auf die IP-Adresse der WLAN-Schnittstelle wie gewohnt eine Verbindung zum Board aufbauen:
  ![Image: '76.png'](76.png)
  ![Image: '77.png'](77.png)
  ![Image: '78.png'](78.png)

* Abschließend empfiehlt es sich, noch die Pakete *alsa-base* und *libasound2-dev* zu installieren mit `sudo aptitude install alsa-base libasound2-dev`:
  ![Image: '80.png'](80.png)

### Backup

* Nach der Installation und Konfiguration sollte man ein Backup des gesamten Systems durchführen, um später im Bedarfsfall leicht zu diesem Stand zurückkehren zu können. Da das komplette System auf der (Mikro-)SD-Karte installiert ist, fertigt man als Backup einfach ein Image der gesamten SD-Karte an. Unter Linux bzw. Mac OS X lässt sich das mit `dd if=/dev/sdb bs=8M | pbzip2 -c > beagle-sd-backup.iso.bz2` bzw. `dd if=/dev/rdisk4 bs=8m | pbzip2 -c > beagle-sd-backup.iso.bz2` erledigen:
  ![Image: '85.png'](85.png)
 `/dev/sdb` bzw. `/dev/rdisk4` ist entsprechend dem Gerät der SD-Karte anzupassen.

### Weitere Schritte

Siehe [BeagleBoard](../BeagleBoard/BeagleBoard.md).

[![License: CC BY-SA 4.0](../../License.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
