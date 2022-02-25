# vim
## Datei erstellen
":w dateiname"
## Verlassen 
":q" gespeichert verlassen
":q!" ungescheichert verlassen 
## Mehrere Dateien öffnen
"vi *datei *datei" 
":n" ":next"
":N" ":prex"
## Kopieren
"v" Anfang des Bereichs "hy" kopiert "hp" paste fügt ein
## Löschen von Text
"dWort,Satz,Zeile*
*x* löschen Taste
*TABx* entf taste
*dd* ganze Zeile
*dw* Wort
*db* Wort HINTER dem Cursor
*3dd* 3 Zeilen
*5dw* 5 Wörter
*d^* oder *d0* Bis zum Anfang der Aktuellen Zeile
*d$* Bis zum Ende 
## Bewegung 
"30" "NACH-LINKS Taste" bezwegt Cursor 30 Zeichen nach Links 
"b" ein wort zurpck
"w" ein wort vor            "4w" 4 Sätze zurücl
"e" und E Wortende 
"(" satz zurück             "5(" 5 sätze zurück
")" satz vor
## Suchen 
*/suchbegriff/*ein Wort nur suchen 
*/suchbegriff/i*ignoriert Groß Kleinschreibung
## Suchen und ersetzen
*:1,$s/wort1/wort2/gc* ### 
*01$* vom Anfang bis zum ende 
*s* ersetzen 
*g* global - wird g weggelassen wird jede Zeile nur das erste vorkommen ersetzt
*c* nachfragen
----
*:'a,'bs/foo/bar/g* Makiert mit ma mb zwei Zeilenm
## Einfügen
:r datei
*:r !date* Datum 

Wer noch nie mit vi gearbeitet hat, wird nicht daran gewöhnt sein, dass die Backspace- und die Entf-Tasten
Zeilenumbrüche nicht wie normale Zeichen behandelt (sie also nicht löschen können). Dieses Verhalten kann
man durch Eintragen von *set bs=2* in die /etc/vim/vimrc
 ändern.
automatische Einrückung bevorzugen, versuchen Sie mal *set ai*.

13.2 Starten
Komando Beschreibung
vi Aufruf von vi mit leerem Text-Puffer.
vi Dateiname Datei wird geladen und der Cursor bei der ersten Zeile platziert.
vi + Dateiname Datei wird geladen und der Cursor bei der letzten Zeile platziert.
vi +n Dateiname Dateiname Datei wird geladen und der Cursor bei der n-ten Zeile
platziert.
vi +/Zeichenkette Dateiname Datei wird geladen, der Cursor bei der Zeile mit Zeichenkette
plaziert.
13.3 Beenden
Komando Beschreibung
:wq Speichern und vi verlassen.
ZZ Ebenfalls speichern und vi verlassen.
:q vi verlassen, falls Datei unverändert.
:q! vi verlassen, egal ob Datei verändert oder nicht.
:w Datei speichern.
13.4 Dateien laden
Komando Beschreibung
e Datei Datei wird geladen, wenn sie existiert, ansonsten erzeugt.
:next Die nächste Datei wird geladen, falls vi mit mehreren Dateien
aufgerufen wurde.
:prev Die vorherige Datei wird geladen, falls vi mit mehreren Dateien
aufgerufen wurde.
13.5 Cursorbewegungen
Komando Beschreibung
[Count]j Den Cursor um eine (bzw. Count) Zeile runter u.s.w.
[Count]k Den Cursor um eine (bzw. Count) Zeile rauf u.s.w.
[Count]l Den Cursor um ein (bzw. Count) Zeichen rechts u.s.w.
[Count]h Den Cursor um ein (bzw. Count) Zeichen links.
Praxisorientiertes vim-Tutorial Seite 9
SelfLinux-0.12.3
[Count]w Den Cursor um ein (bzw. Count) Wort rechts.
[Count]b Den Cursor um ein (bzw. Count) Wort links.
[Count]G Springe zum Ende der Datei oder, falls Count gegeben, zu Zeile
Count.
Ctrl-f Page-Down.
Ctrl-b Page-Up.
^ Springe zum Anfang der aktuellen Zeile.
$ Springe zum Ende der aktuellen Zeile.
13.6 Text eingeben
Komando Beschreibung
i (insert), Eingabe vor dem aktuellen Zeichen.
a (append), Eingabe nach dem aktuellen Zeichen.
I (Insert), Eingabe am Anfang der aktuellen Zeile.
A (Append), Eingabe am Ende der aktuellen Zeile.
o neue Zeile und Eingabe nach der aktuellen Zeile.
O neue Zeile und Eingabe vor der aktuellen Zeile.
Ctrl-v Eingabe eines Steuerzeichens.
13.7 Text ändern
Komando Beschreibung
[Count]rZeichen (replace), Änderung des aktuellen Buchstaben in Zeichen.
R (Replace), Überschreibmodus vom aktuellen Buchstaben aus.
cwWort ersetzt den Text ab der Cursorposition bis zum Wortende durch
Wort.
ccZeichenkette ersetzt die aktuelle Zeile durch Zeichenkette.
J hängt die der aktuellen folgende Zeile an die aktuelle an.
13.8 Text löschen
Komando Beschreibung
[Count]x 1 (bzw. Count) Zeichen unter dem Cursor (rechts) wird gelöscht.
[Count]X 1 (bzw. Count) Zeichen links vom dem Cursor wird gelöscht.
D löscht von der Cursorposition bis zum Zeilenende.
[Count]dd 1 (bzw. Count) Zeilen werden gelöscht.
[Count]d[Richtung] 1 (bzw. Count) mal wird in Richtung [Richtung] gelöscht.
13.9 Die Zwischenablagen
Komando Beschreibung
"1..0, a..z Die Ablage 1..0 bzw. a..z für die nächste Aktion auswählen.
[Count]y[Richtung] 1 (bzw. Count) Bewegungen in [Richtung].
[Count]yy 1 (bzw. Count) Zeilen werden in die aktuelle Zwischenablage
kopiert.
Praxisorientiertes vim-Tutorial Seite 10
SelfLinux-0.12.3
Beliebige Löschaktion Gelöschter Text wird in die aktuelle Zwischenablage kopiert.
p Inhalt der Zwischenablage wird hinter dem Cursor eingefügt.
P Inhalt der Zwischenablage wird vor dem Cursor eingefügt.
13.10 Suchen und Ersetzen
Komando Beschreibung
/Regex Suche vorwärts nach dem regulären Ausdruck Regex.
?Regex Suche rückwärts nach dem regulären Ausdruck Regex.
n Wiederholt das letzte Suchkommando.
N Wiederholt das letzte Suchkommando in die jeweils andere
Richtung.
fZeichen Sucht nach Zeichen in der aktuellen Zeile vorwärts.
FZeichen Sucht nach Zeichen in der aktuellen Zeile rückwärts.
:%s/Quelle/Ziel/ Ersetzt Quelle textweit beim 1. Vorkommen in der Zeile durch Ziel.
:%s/Quelle/Ziel/g Ersetzt Quelle im Text überall durch Ziel.
:%s/Quelle/Ziel/gc Ersetzt Quelle im Text überall durch Ziel, fragt aber vorher nach.
13.11 Bookmarks
Komando Beschreibung
mKey Setzt eine Marke an der aktuellen Stelle unter dem Namen der Taste
Key.
'Key Springt zu der Zeile mit der Marke Key.
`Key Springt zu der Stelle mit der Marke Key.
13.12 Sonstige Goodies
Komando Beschreibung
. Wiederholt die letzte Editieraktion,
% (über einer Klammer) Springt auf die korrespondierende Klammer.
:u oder u (undo) Rückgängig.
:redo (redo) Wiederherstellen.
