## Authentifizierung und Verschlüsselung 

### Schritt 1: Benutzerauthentifizierung einrichten

1. **Erstelle eine Passwortdatei**: Der erste Schritt, um deinen MQTT Broker sicherer zu machen, besteht darin, eine Benutzerauthentifizierung hinzuzufügen. Mosquitto bietet eine einfache Möglichkeit, dies mit einer Passwortdatei zu tun. Öffne das Terminal auf deinem Raspberry Pi und führe folgenden Befehl aus, um einen neuen Benutzer (ersetze `deinBenutzername` durch den gewünschten Benutzernamen) zu erstellen und zur Passwortdatei hinzuzufügen:

    ```
    sudo mosquitto_passwd -c /etc/mosquitto/passwd deinBenutzername
    ```

    Du wirst aufgefordert, ein Passwort einzugeben. Wähle ein starkes Passwort, um die Sicherheit zu erhöhen.

2. **Konfiguriere Mosquitto, um die Passwortdatei zu verwenden**: Nun musst du Mosquitto anweisen, diese Passwortdatei für die Benutzerauthentifizierung zu verwenden. Erstelle dazu eine Konfigurationsdatei namens `custom.conf` im Verzeichnis `/etc/mosquitto/conf.d/`:

    ```
    sudo nano /etc/mosquitto/conf.d/custom.conf
    ```

    Füge folgende Zeilen in die Datei ein:

    ```
    allow_anonymous false
    password_file /etc/mosquitto/passwd
    ```

    Speichere die Datei und schließe den Editor. Mit `allow_anonymous false` wird anonymen Verbindungen nicht mehr erlaubt, und mit `password_file` wird der Pfad zur Passwortdatei angegeben.

3. **Mosquitto neu starten**: Um die Änderungen zu übernehmen, starte Mosquitto neu:

    ```
    sudo systemctl restart mosquitto
    ```

### Schritt 2: Verschlüsselung mit TLS/SSL einrichten

Die Einrichtung einer Verschlüsselung für die Verbindung ist ein wichtiger Schritt, um die Kommunikation zwischen den Clients und deinem MQTT Broker zu sichern. Hierfür benötigst du ein TLS-Zertifikat. Du kannst ein selbstsigniertes Zertifikat erstellen oder ein Zertifikat von einer Zertifizierungsstelle (CA) beziehen.

1. **Erstelle ein selbstsigniertes Zertifikat (optional)**: Für Testzwecke oder den internen Gebrauch kannst du ein selbstsigniertes Zertifikat erstellen. Führe folgende Befehle aus:

    ```
    sudo openssl req -new -x509 -days 365 -extensions v3_ca -keyout /etc/mosquitto/certs/ca.key -out /etc/mosquitto/certs/ca.crt
    sudo openssl req -out /etc/mosquitto/certs/server.csr -key /etc/mosquitto/certs/server.key -new
    sudo openssl x509 -req -in /etc/mosquitto/certs/server.csr -CA /etc/mosquitto/certs/ca.crt -CAkey /etc/mosquitto/certs/ca.key -CAcreateserial -out /etc/mosquitto/certs/server.crt -days 365
    ```

    Diese Befehle erstellen ein neues selbstsigniertes CA-Zertifikat und ein Serverzertifikat, das für die Verschlüsselung verwendet wird.

2. **Konfiguriere Mosquitto für die Verwendung von TLS/SSL**: Bearbeite erneut die `custom.conf` Datei:

    ```
    sudo nano /etc/mosquitto/conf.d/custom.conf
    ```

    Füge folgende Zeilen hinzu, um TLS/SSL zu aktivieren:

    ```
    listener 8883
    cafile /etc/mosquitto/certs/ca.crt
    certfile /etc/mosquitto/certs/server.crt
    keyfile /etc/mosquitto/certs/server.key
    ```

    Speichere die Datei und schließe den Editor. Diese Konfiguration weist Mosquitto an, auf Port 8883 zu lauschen und die angegebenen Zertifikatdateien für TLS/SSL zu verwenden.

3. **

Mosquitto neu starten**: Starte Mosquitto erneut, um die Konfigurationsänderungen zu übernehmen:

    ```
    sudo systemctl restart mosquitto
    ```

Nun ist dein Mosquitto MQTT Broker auf dem Raspberry Pi mit Benutzerauthentifizierung und TLS/SSL-Verschlüsselung konfiguriert, was einen viel sichereren Betrieb ermöglicht.
