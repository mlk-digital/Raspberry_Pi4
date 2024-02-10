### Raspberry Pi Initial Setup
- **SSH aktivieren**: `sudo raspi-config` > Interfacing Options > SSH > Enable.
- **VNC aktivieren** (für Fernzugriff mit grafischer Oberfläche): `sudo raspi-config` > Interfacing Options > VNC > Enable.
- **WLAN konfigurieren**: Bearbeiten Sie die Datei `/etc/wpa_supplicant/wpa_supplicant.conf` und fügen Sie Folgendes hinzu:
  ```
  network={
      ssid="Name_des_WLAN"
      psk="WLAN_Passwort"
  }
  ```
- **Systemaktualisierungen ausführen**: `sudo apt-get update && sudo apt-get upgrade`.

### Dateiverwaltung und Navigation
- **Verzeichnis wechseln**: `cd /pfad/zum/verzeichnis`.
- **Dateiinhalt anzeigen**: `cat dateiname`.
- **Dateien und Verzeichnisse auflisten**: `ls -l`.
- **Datei oder Verzeichnis kopieren**: `cp quelle ziel`.
- **Datei oder Verzeichnis verschieben/umbenennen**: `mv quelle ziel`.
- **Datei oder Verzeichnis löschen**: `rm datei` oder `rm -r verzeichnis`.

### Netzwerkkonfiguration
- **IP-Adresse anzeigen**: `hostname -I`.
- **Netzwerkkonfiguration anzeigen**: `ifconfig`.
- **Netzwerkverbindungen testen**: `ping domain.com`.

### Softwareverwaltung
- **Software installieren**: `sudo apt-get install paketname`.
- **Installierte Pakete auflisten**: `dpkg --get-selections`.
- **Software entfernen**: `sudo apt-get remove paketname`.

### Sicherheit
- **Benutzerpasswort ändern**: `passwd`.
- **Neuen Benutzer anlegen**: `sudo adduser neuerbenutzer`.
- **Firewall konfigurieren**: `sudo ufw enable` zum Aktivieren und `sudo ufw status` zur Anzeige des Status.
- **SSH-Schlüsselpaar erstellen**: `ssh-keygen`.

### Systemüberwachung und -wartung
- **Systemneustart**: `sudo reboot`.
- **System herunterfahren**: `sudo shutdown now`.
- **Speicherplatz anzeigen**: `df -h`.
- **Arbeitsspeicher Nutzung anzeigen**: `free -m`.

### Hilfe und Dokumentation
- **Befehlshilfe anzeigen**: `man befehl` oder `befehl --help`.

