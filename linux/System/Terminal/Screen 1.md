
# Screen




Die drei wichtigsten Befehle bzw. Tastenkombinationen, die man kennen sollte, sind:

- 

Strg + 
A , gefolgt von 
C zum Erstellen eines neuen Fensters (siehe auch [Unterschied zwischen Sitzung und Fenster](https://wiki.ubuntuusers.de/Screen/#Unterschied-zwischen-Sitzung-und-Fenster))

- 

Strg + 
A , gefolgt von 
zum Wechseln zwischen den einzelnen Fenstern einer Sitzung

- 

Strg + 
A , gefolgt von 
D zum Trennen (detach) der Verbindung zur aktuellen Sitzung, die Sitzung läuft dann im Hintergrund weiter



Eine Übersicht über alle Tastenkürzel erhält man mit 
Strg + 
A , gefolgt von 
? .

Eine Sitzung beendet man, indem man die dort laufende Shell beendet, also entweder mit dem Befehl 
```
exit
```
oder durch Drücken von 
Strg + 
D .


### Weitere Befehle[¶](https://wiki.ubuntuusers.de/Screen/#Weitere-Befehle)

Starten einer neuen Sitzung mit dem Namen "sitzung1" (siehe auch [Unterschied zwischen Sitzung und Fenster](https://wiki.ubuntuusers.de/Screen/#Unterschied-zwischen-Sitzung-und-Fenster)):


```
screen -S sitzung1 
```


Trennt (engl.: "detach") die Verbindung zur aktuellen Sitzung: 
Strg + 
A + 
D 

Nimmt die Sitzung wieder auf, falls nur eine einzige Sitzung im Hintergrund läuft:


```
y


Visuelle Benachrichtigung umschalten (Flackern oder Ton; wenn der Bildschirm manchmal flackert, sollte man diesen Befehl ausführen, bis links unten "switched to audible bell" steht.): 
Strg + 
A + 
G 


### Unterschied zwischen Sitzung und Fenster[¶](https://wiki.ubuntuusers.de/Screen/#Unterschied-zwischen-Sitzung-und-Fenster)

Den Unterschied zwischen einer Screen-Sitzung und einem Screen-Fenster kann man sich etwa so wie bei einem Browser mit Tabs vorstellen, wobei Screen-Sitzungen einem Browserfenster und Screen-Fenster einem Browser-Tab entsprechen. Es können mehrere Screen-Sitzungen gleichzeitig laufen und in jeder Screen-Sitzung können mehrere Screen-Fenster geöffnet sein, so wie man mehrere Browserfenster öffnen kann und in jedem Browserfenster mehrere Tabs geöffnet sein können.


### Ausgabe scrollen[¶](https://wiki.ubuntuusers.de/Screen/#Ausgabe-scrollen)

Um in der Ausgabe eines Screen-Fenster mit den bekannten Tastenkombinationen 
⇧ + 
Bild ↑ und 
⇧ + 
Bild ↓ zu scrollen, trägt man die Zeile

```
termcapinfo xterm|xterms|xs|rxvt ti@:te@
```

in die Datei **.screenrc** (welche eventuell noch angelegt werden muss) im Heimatverzeichnis ein.

Falls das nicht funktioniert, bleibt noch die Möglichkeit, mit 
Strg + 
A + 
Esc in den copy-Modus zu wechseln und dort mit den Pfeiltasten oder 
Strg + 
U (halbes Fenster hoch), 
Strg + 
D (halbes Fenster runter), 
Strg + 
B (ganzes Fenster zurück), 
Strg + 
F (ganzes Fenster vorwärts) zu scrollen. Danach verlässt man den copy-Modus mit 
Esc oder 
Q .


### Statuszeile einblenden[¶](https://wiki.ubuntuusers.de/Screen/#Statuszeile-einblenden)

Wer viele virtuelle Terminals öffnet, verliert schnell den Überblick. Für eine bessere Übersicht lässt sich eine Statusleiste einblenden:


```
screen -X caption always "%{rw} * | %H * $LOGNAME | %{bw}%c %D |
%{-}%-Lw%{rw}%50>%{rW}%n%f* %t %{-}%+Lw%<" 
```


Dabei stehen die verschiedenen Variablennamen für:


```
$LOGNAME
```
der Benutzername 
```
%H
```
der Hostname 
```
%c
```
die Uhrzeit im 24-Stunden-Format 
```
%D
```
der aktuelle Wochentag 
```
%n
```
Nummer des virtuellen Terminals 
```
%f
```
Flag; so zeigt das Sternchen das aktive virtuelle Terminal an, ein Minuszeichen die zuletzt besuchte Sitzung 
```
%t
```
der mit 
Strg + 
A , 
⇧ + 
A gesetzte Titel der Sitzung 
```
%id
```
` Backtick-Referenz, wobei id = 1,2,3 ...

Die Angaben in den geschweiften Klammern beschreiben u.a. die Farben. Die Angabe 
```
%50>
```
sorgt dafür, dass screen bei einer zu langen Fensterleiste die Ausgabe abschneidet, so dass die Angabe mittig erscheint. In der "man page" finden sich weitere anwendbare Escape-Sequenzen (string escapes). Über entsprechende Akzent-Zeichen (backticks) lassen sich Rückgabewerte von Shellscripten, z. B. das Auslesen der IP-Adresse, in die Statuszeile einblenden.

Damit die Statusleiste dauerhaft erscheint, ohne alles mühsam von Hand einzugeben, kann ein Eintrag in der Konfigurationsdatei systemweit unter **/etc/screenrc** oder für den Benutzer unter **~/.screenrc** vorgenommen werden. In der Datei sollte dann folgender Eintrag hinzugefügt werden:

```
caption always "%{rw} * | %H * $LOGNAME | %{bw}%c %D | %{-}%-Lw%{rw}%50>%{rW}%n%f* %t %{-}%+Lw%<"
```

Unter Umständen muss man für die Benutzereinstellung eine Kopie von **/etc/screenrc** nach **~/.screenrc** kopieren.

Ein "backtick" wird in der Form 
```
backtick id lifespan autorefresh cmd arg
```
in die **.screenrc** eingetragen und über 
```
%id\` 
```
in die caption-Zeile referenziert. Um die IP-Adresse in die caption-Zeile einzublenden, müsste man folgendes Shellscript **myip.sh** zum Auslesen der IP-Adresse erstellen:


```
1
2
3
```

```
#!/bin/sh
# unter einem ausführbaren Pfad als "myip" abspeichern und ausführbar machen (chmod +x myip).
ifconfig | grep 'inet Adresse:'| grep -v '127.0.0.1' | cut -d: -f2 | awk '{ print $1}'

```



Dies muss nach **/usr/local/bin** kopiert und die **.screenrc** wie folgt angepasst werden:

```
backtick 1 2 2 /usr/local/bin/myip
caption always "Meine IP-Adr.: %1`"
```

### Automatischer Aufruf[¶](https://wiki.ubuntuusers.de/Screen/#Automatischer-Aufruf)

Um den Aufruf von "screen" beim Anmelden zu automatisieren (was bei einem Desktop-System evtl. nicht sinnvoll ist), kann die Datei **.bash_profile** im Homeverzeichnis wie folgt erweitert werden [[3]](https://wiki.ubuntuusers.de/Screen/#source-3):

```
if [ -z $STY ] && [ $TERM != "screen" ]; then
/usr/bin/screen -xRR;
else
/usr/bin/screen -X hardstatus alwayslastline '[%H] %Lw%=%u %d.%m.%y %c '
fi
```

### ssh-Screen[¶](https://wiki.ubuntuusers.de/Screen/#ssh-Screen)

Mit den folgenden Erweiterung am Ende der Datei **.bash_profile** wird automatisch mit einer screen-Sitzung verbunden, wenn die Verbindung per ssh erfolgt. Bestehende Verbindungen zu der Session werden ggf. getrennt:

```
if [ "$TERM" != "screen" ] && [ "$SSH_CONNECTION" != "" ]; then
/usr/bin/screen -S sshscreen -d -R && exit
fi
```

Wird screen beendet oder getrennt, wird auch die SSH-Verbindung getrennt – so ist also nur eine SSH-Verbindung möglich. Das kann umgangen werden, indem man 
```
&& exit
```
weglässt.


### Serielle Konsole[¶](https://wiki.ubuntuusers.de/Screen/#Serielle-Konsole)

Screen kann auch verwendet werden, um sich über [Nullmodem-Kabel](https://de.wikipedia.org/wiki/Nullmodem-Kabel) mit einer seriellen Konsole zu verbinden. Für eine Verbindung mit 38400 Baud lautet der Befehl:


```
screen /dev/ttyS0 38400 
```

## Problembehebung[¶](https://wiki.ubuntuusers.de/Screen/#Problembehebung)

Beim Starten von screen bekommt man eine Fehlermeldung:



"Cannot open your terminal '/dev/pts/0' - please check."



Lösung: screen sollte der erste Befehl im Terminal sein. Den Benutzer wechseln mit 
```
su
```
sollte also erst nach dem Start von screen erfolgen.

Alternativ kann auch ein neues Pseudo-Terminal geöffnet werden:


```
script /dev/null 
```


Anschliessend kann 
```
screen
```
selbst nach einem 
```
su
```
ausgeführt werden.

Beim Verlassen muss dann aber ein Terminal zusätzlich - das script-Terminal - beendet werden.


## Links[¶](https://wiki.ubuntuusers.de/Screen/#Links)

- 

[GNU Screen - Mehrere Terminals in einem](https://www.youtube.com/watch?v=Cy6W71Bb1yE) 🇩🇪 - 50min Vortrag mit Axel Beckert, CLT 2015

- 

[Projektseite](https://www.gnu.org/software/screen/screen.html) 🇬🇧

- 

[tmux](https://wiki.ubuntuusers.de/tmux/) - Alternative zu screen

- 

[byobu](https://wiki.ubuntuusers.de/byobu/) - Erweiterung für screen








[Diese Revision](https://wiki.ubuntuusers.de/Screen/a/revision/999652/) wurde am 26. November 2021 19:37 von [noisefloor](https://ubuntuusers.de/user/noisefloor/) erstellt.


Die folgenden Schlagworte wurden dem Artikel zugewiesen:
[Shell](https://wiki.ubuntuusers.de/wiki/tags/Shell/), [Fenstermanager](https://wiki.ubuntuusers.de/wiki/tags/Fenstermanager/), [Fernwartung](https://wiki.ubuntuusers.de/wiki/tags/Fernwartung/)








- [Wiki](https://wiki.ubuntuusers.de/)


- [Screen](https://wiki.ubuntuusers.de/Screen/)








- 
Powered by [Inyoka](https://ubuntuusers.de/inyoka/)




Inyoka v0.26.1




- 
🄯 2004 – 2022 ubuntuusers.de • Einige Rechte vorbehalten

[Lizenz](https://ubuntuusers.de/lizenz/) •
[Kontakt](https://ubuntuusers.de/kontakt/) •
[Datenschutz](https://ubuntuusers.de/datenschutz/) •
[Impressum](https://ubuntuusers.de/impressum/) •
[Serverstatus](https://ubuntuusers.statuspage.io)


- 
Serverhousing gespendet von

[](http://noris.jobs/linux)
[](http://www.anexia.at/managed-hosting/) Wiki › ubuntuusers.de
==============================



<https://wiki.ubuntuusers.de/Screen/>


Artikel Bearbeiten Verlauf Diskussion Abonnieren
Screen
Dieser Artikel wurde für die folgenden Ubuntu-Versionen getestet:
Dieser Artikel ist größtenteils für alle Ubuntu-Versionen gültig.

Zum Verständnis dieses Artikels sind folgende Seiten hilfreich:
Installation von Programmen

Ein Terminal öffnen

Einen Editor öffnen

Inhaltsverzeichnis
Installation
Bedienung
Allgemein
Wichtige Befehle
Weitere Befehle
Unterschied zwischen Sitzung und Fenster...
Ausgabe scrollen
Statuszeile einblenden
Automatischer Aufruf
ssh-Screen
Serielle Konsole
Problembehebung
Links
Screen 🇬🇧 ist ein Fenstermanager zur Verwendung mit textbasierten Eingabefenstern (Textkonsole). Hierbei ist es möglich, innerhalb eines einzigen Zugangs (zum Beispiel über ein Terminal oder einer Terminalemulation) mehrere virtuelle Konsolensitzungen zu erzeugen und zu verwalten. Darüber hinaus können Sitzungen getrennt und später fortgeführt werden.

Ein Anwendungsbeispiel: Man meldet sich an seinem Server mittels SSH an und startet ein Programm. Beendet man nun die SSH-Sitzung, wird auch das Programm beendet. Mit screen kann man dies verhindern: Man meldet sich per SSH an, startet screen und danach das gewünschte Programm. Dann ruft man das detach-Kommando auf und kann sich abmelden. Im Hintergrund arbeitet jedoch das Programm weiter, und man kann beim nächsten Anmelden die Sitzung mit dem Programm wiederaufnehmen.

Installation
Zuerst muss das folgende Paket installiert werden [1]:

screen

Befehl zum Installieren der Pakete:

sudo apt-get install screen 
Oder mit apturl installieren, Link: apt://screen

Bedienung
Mit dem Befehl

screen 
in einem Terminal [2] lässt sich der Fenstermanager starten.

Allgemein
Nach dem Aufruf von screen scheint es so, als ob nichts geschehen wäre. Das stimmt aber nicht, denn im Hintergrund läuft nun screen zum Verwalten der Sitzungen. Man kann nun ganz normal weiterarbeiten und verschiedene Programme starten, wie man es gewohnt ist.

Wichtige Befehle
Die drei wichtigsten Befehle bzw. Tastenkombinationen, die man kennen sollte, sind:

Strg + A , gefolgt von C zum Erstellen eines neuen Fensters (siehe auch Unterschied zwischen Sitzung und Fenster)

Strg + A , gefolgt von          zum Wechseln zwischen den einzelnen Fenstern einer Sitzung

Strg + A , gefolgt von D zum Trennen (detach) der Verbindung zur aktuellen Sitzung, die Sitzung läuft dann im Hintergrund weiter

Eine Übersicht über alle Tastenkürzel erhält man mit Strg + A , gefolgt von ? .

Eine Sitzung beendet man, indem man die dort laufende Shell beendet, also entweder mit dem Befehl exit oder durch Drücken von Strg + D .

Weitere Befehle
Starten einer neuen Sitzung mit dem Namen "sitzung1" (siehe auch Unterschied zwischen Sitzung und Fenster):

screen -S sitzung1 
Trennt (engl.: "detach") die Verbindung zur aktuellen Sitzung: Strg + A + D

Nimmt die Sitzung wieder auf, falls nur eine einzige Sitzung im Hintergrund läuft:

screen -r 
Nimmt die Sitzung mit dem Namen "sitzung1" wieder auf:

screen -r sitzung1 
Auflisten der Namen aller laufenden Screen-Sitzungen:

screen -ls 
Trennt die Verbindung zu einer laufenden Sitzung mit dem Namen "sitzung1" (sehr hilfreich, wenn man z.B. die Verbindung per ssh verloren hat und deswegen die Sitzung nicht trennen konnte):

screen -d sitzung1 
Die Sitzung mit dem Namen "sitzung1" kann an mehreren Computern gleichzeitig angezeigt werden:

screen -rx sitzung1 
An die Sitzung mit dem Namen "sitzung1" einen Befehl senden und ausführen (\n für [ENTER]):

screen -S sitzung1 -X stuff $'ls -l\n' 
Visuelle Benachrichtigung umschalten (Flackern oder Ton; wenn der Bildschirm manchmal flackert, sollte man diesen Befehl ausführen, bis links unten "switched to audible bell" steht.): Strg + A + G

Unterschied zwischen Sitzung und Fenster
Den Unterschied zwischen einer Screen-Sitzung und einem Screen-Fenster kann man sich etwa so wie bei einem Browser mit Tabs vorstellen, wobei Screen-Sitzungen einem Browserfenster und Screen-Fenster einem Browser-Tab entsprechen. Es können mehrere Screen-Sitzungen gleichzeitig laufen und in jeder Screen-Sitzung können mehrere Screen-Fenster geöffnet sein, so wie man mehrere Browserfenster öffnen kann und in jedem Browserfenster mehrere Tabs geöffnet sein können.

Ausgabe scrollen
Um in der Ausgabe eines Screen-Fenster mit den bekannten Tastenkombinationen ⇧ + Bild ↑ und ⇧ + Bild ↓ zu scrollen, trägt man die Zeile

termcapinfo xterm|xterms|xs|rxvt ti@:te@
in die Datei .screenrc (welche eventuell noch angelegt werden muss) im Heimatverzeichnis ein.

Falls das nicht funktioniert, bleibt noch die Möglichkeit, mit Strg + A + Esc in den copy-Modus zu wechseln und dort mit den Pfeiltasten oder Strg + U (halbes Fenster hoch), Strg + D (halbes Fenster runter), Strg + B (ganzes Fenster zurück), Strg + F (ganzes Fenster vorwärts) zu scrollen. Danach verlässt man den copy-Modus mit Esc oder Q .

Statuszeile einblenden
Wer viele virtuelle Terminals öffnet, verliert schnell den Überblick. Für eine bessere Übersicht lässt sich eine Statusleiste einblenden:

screen -X caption always "%{rw} * | %H * $LOGNAME | %{bw}%c %D |
%{-}%-Lw%{rw}%50>%{rW}%n%f* %t %{-}%+Lw%<" 
Dabei stehen die verschiedenen Variablennamen für:

$LOGNAME	der Benutzername
%H	der Hostname
%c	die Uhrzeit im 24-Stunden-Format
%D	der aktuelle Wochentag
%n	Nummer des virtuellen Terminals
%f	Flag; so zeigt das Sternchen das aktive virtuelle Terminal an, ein Minuszeichen die zuletzt besuchte Sitzung
%t	der mit Strg + A , ⇧ + A gesetzte Titel der Sitzung
%id`	Backtick-Referenz, wobei id = 1,2,3 ...
Die Angaben in den geschweiften Klammern beschreiben u.a. die Farben. Die Angabe %50> sorgt dafür, dass screen bei einer zu langen Fensterleiste die Ausgabe abschneidet, so dass die Angabe mittig erscheint. In der "man page" finden sich weitere anwendbare Escape-Sequenzen (string escapes). Über entsprechende Akzent-Zeichen (backticks) lassen sich Rückgabewerte von Shellscripten, z. B. das Auslesen der IP-Adresse, in die Statuszeile einblenden.

Damit die Statusleiste dauerhaft erscheint, ohne alles mühsam von Hand einzugeben, kann ein Eintrag in der Konfigurationsdatei systemweit unter /etc/screenrc oder für den Benutzer unter ~/.screenrc vorgenommen werden. In der Datei sollte dann folgender Eintrag hinzugefügt werden:

caption always "%{rw} * | %H * $LOGNAME | %{bw}%c %D | %{-}%-Lw%{rw}%50>%{rW}%n%f* %t %{-}%+Lw%<"
Unter Umständen muss man für die Benutzereinstellung eine Kopie von /etc/screenrc nach ~/.screenrc kopieren.

Ein "backtick" wird in der Form backtick id lifespan autorefresh cmd arg in die .screenrc eingetragen und über %id\` in die caption-Zeile referenziert. Um die IP-Adresse in die caption-Zeile einzublenden, müsste man folgendes Shellscript myip.sh zum Auslesen der IP-Adresse erstellen:

1
2
3
#!/bin/sh
# unter einem ausführbaren Pfad als "myip" abspeichern und ausführbar machen (chmod +x myip).
ifconfig  | grep 'inet Adresse:'| grep -v '127.0.0.1' | cut -d: -f2 | awk '{ print $1}'
Dies muss nach /usr/local/bin kopiert und die .screenrc wie folgt angepasst werden:

backtick 1 2 2 /usr/local/bin/myip
caption always "Meine IP-Adr.: %1`"
Automatischer Aufruf
Um den Aufruf von "screen" beim Anmelden zu automatisieren (was bei einem Desktop-System evtl. nicht sinnvoll ist), kann die Datei .bash_profile im Homeverzeichnis wie folgt erweitert werden [3]:

 if  [ -z $STY ] && [ $TERM != "screen" ]; then
   /usr/bin/screen -xRR;
 else
   /usr/bin/screen -X hardstatus alwayslastline '[%H] %Lw%=%u %d.%m.%y %c '
 fi
ssh-Screen
Mit den folgenden Erweiterung am Ende der Datei .bash_profile wird automatisch mit einer screen-Sitzung verbunden, wenn die Verbindung per ssh erfolgt. Bestehende Verbindungen zu der Session werden ggf. getrennt:

if [ "$TERM" != "screen" ] && [ "$SSH_CONNECTION" != "" ]; then
   /usr/bin/screen -S sshscreen -d -R && exit
fi
Wird screen beendet oder getrennt, wird auch die SSH-Verbindung getrennt – so ist also nur eine SSH-Verbindung möglich. Das kann umgangen werden, indem man && exit weglässt.

Serielle Konsole
Screen kann auch verwendet werden, um sich über Nullmodem-Kabel mit einer seriellen Konsole zu verbinden. Für eine Verbindung mit 38400 Baud lautet der Befehl:

screen /dev/ttyS0 38400 
Problembehebung¶
Beim Starten von screen bekommt man eine Fehlermeldung:

"Cannot open your terminal '/dev/pts/0' - please check."

Lösung: screen sollte der erste Befehl im Terminal sein. Den Benutzer wechseln mit su sollte also erst nach dem Start von screen erfolgen.

Alternativ kann auch ein neues Pseudo-Terminal geöffnet werden:

script /dev/null 
Anschliessend kann screen selbst nach einem su ausgeführt werden.

Beim Verlassen muss dann aber ein Terminal zusätzlich - das script-Terminal - beendet werden.