## MQTT Broker installieren

### Vorbereitungen

1. **Was du brauchst**:
   - Raspberry Pi
   - eingerichtetes Betriebssystem auf der SD-Karte
   - eingerichtete Internetverbindung.

### Mosquitto  installieren

1. **Öffne das Terminal**: Sobald dein Raspberry Pi eingerichtet ist, öffne das Terminal. Du findest es in der Menüleiste oder kannst es durch Drücken von `Ctrl + Alt + T` öffnen.

2. **Aktualisiere die Paketlisten**: Gib den folgenden Befehl ein, um sicherzustellen, dass alle deine Paketlisten aktuell sind:
    ```
    sudo apt-get update
    ```
    Dieser Schritt ist wichtig, um sicherzustellen, dass du die neuesten Versionen aller Software installierst, die du hinzufügen möchtest.

3. **Installiere Mosquitto**: Führe den folgenden Befehl aus, um Mosquitto und den Mosquitto-Client zu installieren:
    ```
    sudo apt-get install -y mosquitto mosquitto-clients
    ```
    Dieser Befehl installiert den Mosquitto MQTT Broker und die Client-Tools, die du zur Interaktion mit dem Broker benötigst.

4. **Starte Mosquitto automatisch**: Damit Mosquitto automatisch startet, wenn dein Raspberry Pi hochfährt, führe den folgenden Befehl aus:
    ```
    sudo systemctl enable mosquitto.service
    ```
    Mit diesem Befehl wird dein Raspberry Pi so konfiguriert, dass Mosquitto automatisch startet.

### Konfiguration und Test

1. **Broker testen**: Teste den MQTT Broker, indem du eine einfache Nachricht von einem Client an den Broker sendest und dann mit einem anderen Client abonnierst, um die Nachricht zu empfangen. Öffne dafür zwei Terminalfenster oder -tabs.

    - In Terminal 1 (um Nachrichten zu abonnieren):
        ```
        mosquitto_sub -h localhost -t test/topic
        ```
        Dieser Befehl abonniert alle Nachrichten, die unter dem Thema `test/topic` gesendet werden.

    - In Terminal 2 (um eine Nachricht zu senden):
        ```
        mosquitto_pub -h localhost -t test/topic -m "Hallo MQTT"
        ```
        Dieser Befehl sendet die Nachricht "Hallo MQTT" an das Thema `test/topic`.

    Wenn alles richtig konfiguriert ist, solltest du die gesendete Nachricht "Hallo MQTT" im ersten Terminal sehen, das das Abonnement durchführt.

### Zusätzliche Hinweise

- **Sicherheit**: Denk über die Sicherheit deines MQTT Brokers nach. Du solltest Authentifizierung und Verschlüsselung einrichten, um deine Daten zu schützen.

- **Weiterführende Nutzung**: Überlege, wie du Mosquitto in deinen Projekten nutzen kannst. MQTT ist ideal für IoT-Projekte, in denen Geräte Daten senden oder empfangen müssen.
