# Aufgabe: SQL-Dump mit Python

## Ziel

Deine Aufgabe ist es, ein Python-Skript zu erstellen, das einen SQL-Dump von einer lokalen MySQL-Datenbank macht. Du sollst dabei über die Konsole die Verbindungsdaten zur Datenbank abfragen und anschliessend den Dump in einer `.sql`-Datei speichern.

## Anleitung

### 1. Vorbereitung

- **Python installieren**: Stelle sicher, dass Python auf deinem System installiert ist. Du kannst das überprüfen, indem du in der Konsole `python --version` eingibst.
- **MySQL-Python-Connector installieren**: Installiere das benötigte Python-Paket, um eine Verbindung zu MySQL herzustellen. Das kannst du mit dem folgenden Befehl machen:
  ```bash
  pip install mysql-connector-python
  ```

### 2. Skript erstellen

Erstelle ein Python-Skript, das folgendes macht:

1. **Eingabe der Verbindungsdaten**: Frage den Nutzer nach den folgenden Informationen:

   - Host (z. B. `localhost`)
   - Datenbankname
   - Benutzername
   - Passwort

2. **Verbindung zur Datenbank**: Nutze die eingegebenen Informationen, um eine Verbindung zur MySQL-Datenbank herzustellen. Verwende dafür den `mysql-connector-python`.

3. **SQL-Dump erstellen**: Verwende SQL-Befehle, um die Struktur und die Daten der Datenbank in eine `.sql`-Datei zu exportieren. Achte darauf, dass die Datei den Namen der Datenbank trägt.

Ressourcen:

- https://www.mybb.de/doku/haeufig-gestellte-fragen/was-ist-ein-sql-dump/ (deutsch)
- https://stackoverflow.com/questions/2512593/what-is-sql-dump-for (englisch)

4. **Fehlerbehandlung**: Implementiere eine einfache Fehlerbehandlung, falls z. B. die Verbindung fehlschlägt oder die Datenbank nicht existiert.

Ressourcen:

- https://www.almabetter.com/bytes/tutorials/python/exception-handling (englisch)
- https://www.youtube.com/watch?v=NMTEjQ8-AJM (englisch)

### 3. Testen

- **Lokale Datenbank**: Erstelle eine Testdatenbank in MySQL Workbench und fülle sie mit ein paar Tabellen und Daten.
- **Skript ausführen**: Führe dein Skript aus und überprüfe, ob die `.sql`-Datei korrekt erstellt wurde.

### 4. Ein Beispiel

So könnte die Konsole aussehen, wenn du das Skript ausführst:

```bash
Bitte gib deinen MySQL-Host ein:
Bitte gib den Namen der Datenbank ein:
Bitte gib deinen MySQL-Benutzernamen ein:
Bitte gib dein MySQL-Passwort ein:
```

Nach der Eingabe sollte das Skript eine Datei namens test_db.sql im gleichen Verzeichnis erstellen.

### 5. Abgabe

- Erstelle ein Repository auf GitHub.
- Lade dein Skript in das Repository hoch.
- Schreibe eine kurze Erklärung in die README.md, wie man dein Skript benutzt.

Viel Erfolg!

### Für Erweiterte

Stell dir vor, wir möchten, dass das Skript jeden Sonntag um 3:00 Uhr morgens automatisch ausgeführt wird und ein Backup erstellt. Um dies zu erreichen, müsstest du einen Cron-Job unter WSL erstellen.

Ressourcen:

Cronjob:

- https://www.hivelocity.net/kb/what-is-cron-job/ (englisch)
- https://de.ryte.com/wiki/CronJob/ (deutsch)

WSL:

- https://learn.microsoft.com/de-de/windows/wsl/about (deutsch)
- https://learn.microsoft.com/en-us/windows/wsl/about (englisch)

## 3. Skript im WSL ausführen

Da das Skript auf dem `C:`-Laufwerk liegt, musst du den Pfad entsprechend anpassen, wenn du es unter WSL ausführst:

- **Wechsle zum Skript-Verzeichnis**: Im WSL, kannst du auf das `C:`-Laufwerk zugreifen, indem du den Pfad `/mnt/c/` benutzt. Beispiel:

  ```bash
  cd /mnt/c/Pfad/zu/deinem/Skript
  ```

- **Skript ausführen**: Führe das Skript wie gewohnt aus:
  ```bash
  python dump_script.py
  ```

### 4. Automatisierung mit Cron

Um das Skript jeden Sonntag automatisch auszuführen, musst du einen Cron-Job erstellen:

1. **Cron öffnen**: Öffne die Crontab-Datei, um einen neuen Job hinzuzufügen:

   ```bash
   crontab -e
   ```

2. **Job hinzufügen**: Füge die folgende Zeile am Ende der Datei hinzu, um das Skript jeden Sonntag um 2:00 Uhr morgens auszuführen:

   ```bash
   0 2 * * 0 /usr/bin/python3 /mnt/c/Pfad/zu/deinem/Skript/dump_script.py
   ```

   Ersetze `/mnt/c/Pfad/zu/deinem/Skript` mit dem tatsächlichen Pfad zu deinem Python-Skript.

3. **Crontab speichern und schliessen**: Speichere die Änderungen und schliesse den Editor.

### 5. Testen

- **Testlauf**: Führe das Skript manuell über WSL aus, um sicherzustellen, dass es korrekt funktioniert.
- **Cron-Job überprüfen**: Vergewissere dich, dass der Cron-Job korrekt eingerichtet ist, indem du folgendes eingibst:
  ```bash
  crontab -l
  ```
