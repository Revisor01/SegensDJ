# SegensDJ
Repo für die SegensDJ Installation für die Ausstellung Interreligiöse Segensräume.

## Benötigte Hardware
- RaspberryPi 4 - 8GB Ram
- Pioneer DDJ SB3
- Boxen bzw. Verstärker anschließbar via 3,5mm Klinke oder direkt über die Soundkarte des Pioneer DDJ SB3
<p float="left">
<img src="https://github.com/Revisor01/SegensDJ/blob/947d321dafee4506dcda4c5156c43726a6c6d8f8/docs/pi4.png" width="32%" height="32%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src="https://github.com/Revisor01/SegensDJ/blob/dc55fd12e33bb112308dbf6f5dd0f340d9205aa0/docs/sb3.svg" width="40%" height="40%">
</p>

## Installation

Sollten Sie bereits mit dem Flashen von SD-Karten vertaut sein, nutzen Sie bitte die Methode die Sie gewohnt sind.

1. Installieren Sie [Balena Etcher](https://www.balena.io/etcher/)
1. Laden Sie die Datei segensdj-pi.zip
1. Verbinden Sie ihre SD Karte mit dem Computer
1. Öffnen Sie Balena Etcher
1. Wählen Sie 'Flash from File' und im Anschluss die heruntergeladene Datei aus
1. Wählen Sie die SD Karte und bestätigen Sie, dass Sie nichts Relevantes überschreiben
1. Klicken Sie auf Flash und warten Sie bis der Prozess abgeschlossen ist

## Netwerkeinrichtung
Nach Abschluss des Vorgangs sollte die Partition boot gemounted sein.<br />
Wenn die Partition nicht erscheint einfach die SD-Karte aus- und wieder einstecken.<br />
Erstellen Sie die Datei ```wpa_supplicant.conf``` in der Partition.<br />
Der Inhalt der Datei:

```
country=DE
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
       ssid="DEINE WLAN SSID"
       psk="DEIN PASSWORT"
       key_mgmt=WPA-PSK
}
```
Im Anschluss die SD Karte in den Pi stecken und den Pi starten. Der Pi sollte nun im Netzwerk verfügbar sein.


## SSH Zugriff
Für SSH Zugriff wird die IP benötigt.<br />

Nutzername: ```pi```<br />
Passwort: ```mixxx```<br />
Terminal: ```ssh pi@XXX.XXX.XXX.XXX```

## VNC Zugriff
Für VNC Zugriff wird die IP benötigt.<br />
VNC stellt einen virtuellen Desktop zur Verfügung um auf die Oberfläche zugegeriffen zu können.<br /><br />
Der VNC Server muss via SSH gestartet werden wenn benötigt. Mit SSH ```ssh XXX.XXX.XXX.XXX@IP``` auf den Pi verbinden: ```sudo systemctl start vncserver@1.service```<br />
Wenn der Service ohne Fehler gestartet wird, kann im Anschluss mit dem VNC Clienten eine Verbindung hergestellt werden.<br />
Mögliche Clienten:<br />
- [VNC Viewer](https://www.realvnc.com/de/connect/download/viewer/) (Win, Mac, ios, Android, Linux)
- [TightVNC](https://www.tightvnc.com/download.php) (Win, Linux)
- [UltraVNC](https://uvnc.com/) (Windows)

Im VNC Clienten ```XXX.XXX.XXX.XXX:5901``` mit dem Passwort: ```mixxxpi```.

## Hinweis
- Im Script /home/pi/.mixxx/controllers/Pioneer-DDJ-SB3-scripts.js wurde Zeile 981 auskommentiert um Fehler beim Start zu umgehen. Sollte das Deck nicht korrekt funktionieren, ist das der erste Punkt an dem geschaut werden sollte.

- Den VNC Server im Autostart laufen zu lassen führt dazu, dass das Deck nicht erkannt wird. Eventuell muss die Bootreihenfolge des VNC Server angepasst werden.

# Copyright Hinweis
- Basiert auf dem Image von: [fayaaz/mixxx-pi-gen](https://github.com/fayaaz/mixxx-pi-gen)

## Änderungen
- Updates mit Stand: 08.11.2022 eingespielt
- Mixxx auf 2.3.3 geändert (Kompatibilität mit dem Deck)
- VNC Server hinzugefügt
- SMB Zugriff hinzugefügt
- Time Server hinzugefügt
