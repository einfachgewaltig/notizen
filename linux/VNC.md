VNC
========================






----------------------------------------------------------
################################################
###############################################




https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-20-04-de

sudo apt install tightvncserver
 
Führen Sie als Nächstes den Befehl vncserver aus, um ein VNC-Zugangspasswort festzulegen, die anfänglichen Konfigurationsdateien zu erstellen und eine VNC-Serverinstanz zu starten:

vncserver
 
Sie werden dazu aufgefordert, ein Passwort einzugeben und zu verifizieren, um ferngesteuert auf Ihren Rechner zuzugreifen:

Output
You will require a password to access your desktops.

Password:
Verify:
Das Passwort muss zwischen sechs und acht Zeichen lang sein. Passwörter mit mehr als 8 Zeichen werden automatisch verkürzt.

Sobald Sie das Passwort verifiziert haben, können Sie ein schreibgeschütztes Passwort einrichten. Bent erutzer, die sich mit dem schreibgeschützten Passwort anmelden, können die VNC-Instanz nicht mit der Maus oder Tastatur steuern. Das ist eine hilfreiche Option, wenn Sie mit Ihrem VNC-Server anderen etwas zeigen möchten, ist aber nichforderlich.

Der Prozess erstellt dann die notwendigen Standard-Konfigurationsdateien und Verbindungsinformationen für den Server. Zudem startet er eine Standard-Serverinstanz auf Port 5901. Dieser Port nennt sich Anzeige-Port und wird vom VNC als :1 bezeichnet. VNC kann mehrere Instanzen auf anderen Anzeige-Ports starten. :2 bezieht sich auf Port 5902, :3 auf 5903 und so weiter:

Output
Would you like to enter a view-only password (y/n)? n
xauth:  file /home/sammy/.Xauthority does not exist

New 'X' desktop is your_hostname:1

Creating default startup script /home/sammy/.vnc/xstartup
Starting applications specified in /home/sammy/.vnc/xstartup
Log file is /home/sammy/.vnc/your_hostname:1.log
Wenn Sie Ihr Passwort ändern oder ein schreibgeschütztes Passwort hinzufügen möchten, beachten Sie, dass Sie dies mit dem Befehl vncpasswd tun können:

vncpasswd
 
Das ist der Moment, ab dem der VNC-Server installiert ist und läuft. Nun konfigurieren wir ihn, um Xfce zu starten und um uns Zugriff auf den Server über eine grafische Oberfläche zu erteilen.

Schritt 2 — Konfiguration des VNC-Servers
Der VNC-Server muss wissen, welche Befehle er beim Start ausführen soll. VNC muss vor allem wissen, mit welcher grafischen Desktop-Umgebung er sich verbinden soll.

Die Befehle, die der VNC-Server beim Starten ausführt, befinden sich in einer Konfigurationsdatei namens xstartup im Ordner .vnc unter Ihrem Stammverzeichnis. Das Start-Skript wurde erstellt, als Sie den vncserver im vorherigen Schritt ausgeführt haben, aber Sie erstellen Ihr eigenes, um den Xfce-Desktop zu starten.

Da Sie die Konfiguration des VNC-Servers ändern werden, müssen Sie zunächst die VNC-Server-Instanz stoppen, die auf Port 5901 ausgeführt wird. Dazu verwenden Sie den folgenden Befehl:

vncserver -kill :1
 
Die Ausgabe sollte wie folgt aussehen, auch wenn Sie eine andere PID sehen werden:

Output
Killing Xtightvnc process ID 17648
Bevor Sie die Datei xstartup ändern, sollten Sie ein Backup der Originaldatei vornehmen:

mv ~/.vnc/xstartup ~/.vnc/xstartup.bak
 
Erstellen Sie eine neue xstartup-Datei und öffnen Sie sie in einem Texteditor wie nano:

nano ~/.vnc/xstartup
 
Fügen Sie der Datei anschließend folgende Zeilen hinzu:

~/.vnc/xstartup
#!/bin/bash
xrdb $HOME/.Xresources
startxfce4 &
 
Die erste Zeile ist ein shebang. In ausführbaren Klartext-Dateien auf *nix-Plattformen weist ein shebang das System an, an welchen Interpreter die Datei zur Ausführung weitergegeben wird. In diesem Fall übergeben Sie die Datei dem Bash-Interpreter. Dies erlaubt es, jede aufeinanderfolgende Zeile als Befehl der Reihe nach auszuführen.

Der erste Befehl in der Datei, xrdb $HOME/.Xresources weist das GUI Framework des VNC an, die .Xresources-Datei. . des Serverbenutzers zu lesen. Xresources ist der Ort, an dem ein Benutzer bestimmte Einstellungen des grafischen Desktops ändern kann, wie die Terminal-Farben, Cursor-Gestaltung und das Font-Rendering. Der zweite Befehl weist den Server an, Xfce zu starten. Immer, wenn Sie den VNC-Server starten oder neu starten, werden diese Befehle automatisch ausgeführt.

Speichern und schließen Sie die Datei nach dem Hinzufügen dieser Zeilen. Wenn Sie nano verwendet haben, drücken Sie STRG+X, Y, dann ENTER.

Um sicherzustellen, dass der VNC-Server diese neue Start-Datei ordnungsgemäß verwenden kann, müssen Sie sie ausführbar machen:

chmod +x ~/.vnc/xstartup
 
Starten Sie den VNC-Server anschließend neu:

vncserver -localhost