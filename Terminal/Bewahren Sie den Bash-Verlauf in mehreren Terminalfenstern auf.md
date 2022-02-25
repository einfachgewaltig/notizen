Bewahren Sie den Bash-Verlauf in mehreren Terminalfenstern auf
========================================



[https://qastack.com.de/unix/1288/preserve-bash-history-in-multiple-terminal-windows](https://qastack.com.de/unix/1288/preserve-bash-history-in-multiple-terminal-windows)**





[*](https://qastack.com.de/)







- 
[Unix & Linux](https://qastack.com.de/unix/)


- 
[Tags](https://qastack.com.de/unix/tags/)






- 

[
Account
](https://qastack.com.de/unix/1288/#)

[Anmeldung](https://qastack.com.de/accounts/login/?next=/)
[Registrieren](https://qastack.com.de/accounts/signup/?next=/unix/1288/preserve-bash-history-in-multiple-terminal-windows)















# Bewahren Sie den Bash-Verlauf in mehreren Terminalfenstern auf







526 










Ich habe durchweg mehr als ein Terminal geöffnet. Irgendwo zwischen zwei und zehn, um verschiedene Dinge zu erledigen. Nehmen wir nun an, ich starte neu und öffne einen weiteren Terminalsatz. Manche erinnern sich an bestimmte Dinge, manche vergessen.

Ich möchte eine Geschichte, die:


- Erinnert sich an alles von jedem Terminal

- Ist sofort von jedem Terminal aus erreichbar (zB wenn ich 
```
ls
```
in einem bin , auf ein anderes bereits laufendes Terminal umsteige und dann auf drücke, erscheint 
```
ls
```
)

- Vergisst den Befehl nicht, wenn vor dem Befehl Leerzeichen stehen.



Was kann ich tun, um die Bash-Funktion zu verbessern?







[bash](https://qastack.com.de/unix/tagged/bash/) 

[command-history](https://qastack.com.de/unix/tagged/command-history/) 







—
[
Oli
](https://unix.stackexchange.com/users/880/oli)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows)












57








Ich kann den Vorteil davon sehen, aber persönlich würde ich das in meiner Schale HASSEN. Normalerweise lasse ich 3 oder 4 Tabs in meinem Terminal für ganz bestimmte Zwecke offen: einen zum Ausführen von 'make', einen mit vi, einen zum Ausführen von Dingen usw. Wenn ich also kompiliere, gehe ich zu Tab 1, drücke und 'make' kommt auf und so weiter. Das ist für mich äußerst produktiv. Also, wenn ich plötzlich zu meinem 'make'-Tab gehe und einen zufälligen grep-Befehl erhalte, würde ich wirklich sauer werden! Nur eine persönliche Nachricht



—
[axel_c ](https://unix.stackexchange.com/users/659/axel-c)










4








@axel_c das stimmt schon. Ich kann mir keine intelligente Methode vorstellen, bei der vorhandene Terminals nur ihre eigene Geschichte anzeigen, während neue Terminals eine chronologisch genaue Liste von Befehlen anzeigen.



—
[Oli ](https://unix.stackexchange.com/users/880/oli)










8








@Oli schrieb: "Ich kann mir keine intelligente Methode vorstellen, bei der vorhandene Terminals nur ihre eigene Geschichte anzeigen, während neue Terminals eine chronologisch genaue Liste von Befehlen anzeigen." Wie wäre es (unerprobten): 
```
export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
```
. Vorhandene Shells fügen jeden Befehl zur Verlaufsdatei hinzu, damit neue Shells angezeigt werden, zeigen jedoch nur ihre eigenen Verläufe an.



—
[Chris Seite ](https://unix.stackexchange.com/users/7814/chris-page)










2








Möchten Sie, dass der Verlauf entweder einzeln gespeichert oder in einer einzigen Verlaufsdatei zusammengeführt wird?



—
[kbyrd ](https://unix.stackexchange.com/users/26/kbyrd)










3








Die kurze Antwort lautet: Sie ist nicht für Bash-Entwickler gedacht. Lösungen, die auf Spülen und erneutem Lesen des Verlaufs basieren, funktionieren wahrscheinlich, aber Vorsicht vor [Shlemiel The Painter](http://c2.com/cgi/wiki?ShlemielThePainter) . In einfachen Worten: Der Umfang der Verarbeitungsarbeit zwischen den einzelnen Befehlen ist proportional zur Größe des Verlaufs.



—
[Stéphane Gourichon ](https://unix.stackexchange.com/users/19643/st%c3%a9phane-gourichon)












Antworten:







329 










Fügen Sie ~ / .bashrc Folgendes hinzu

```

```
# Avoid duplicates
export HISTCONTROL=ignoredups:erasedups 
# When the shell exits, append to the history file instead of overwriting it
shopt -s histappend

# After each command, append to the history file and reread it
export PROMPT_COMMAND="${PROMPT_COMMAND:+$PROMPT_COMMAND$'\n'}history -a; history -c; history -r"

```

```









—
[Pablo R.](https://unix.stackexchange.com/users/348/pablo-r)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/1292#1292)









20








Das Problem bei dieser PROMPT_COMMAND-Lösung besteht darin, dass sich die Nummern für jedes Verlaufselement nach jedem Befehl ändern :(. Wenn Sie beispielsweise history und 1) ls 2) rm eingeben, müssen Sie! 1 wiederholen, um 1 zu wiederholen, und die Verlaufsnummer kann sich ändern könnte den Befehl rm ausführen ...



—
[Chris Kimpton ](https://unix.stackexchange.com/users/26946/chris-kimpton)










2








Wenn ich dies tue, haben andere bereits geöffnete Terminals nicht den zuletzt eingegebenen Befehl, wenn ich auf "Auf" drücke, bis ich einen Befehl in diesem* Terminal erteile - wird dies erwartet? Wenn ja, gibt es eine Möglichkeit, den Verlauf anderer Terminals sofort zu ändern?



—
[Suan ](https://unix.stackexchange.com/users/28970/suan)










7








@Suan, das scheint mir aufgrund der Befehle richtig zu sein. Ich habe festgestellt, dass wir einen Null-Befehl ausgeben können (drücken Sie einfach die Eingabetaste), um den Verlauf zu aktualisieren.



—
[Salbei ](https://unix.stackexchange.com/users/17300/sage)










3








Tatsächlich *
```
history -a
```
löst (...) das Löschen von Duplikaten* gemäß [dieser](http://unix.stackexchange.com/a/18443/5355) Antwort auf die Frage " [Bash-Verlauf" nicht aus: Die Einstellungen "Ignoriert" und "Gelöscht" stehen in Konflikt mit dem gemeinsamen Verlauf zwischen Sitzungen](http://unix.stackexchange.com/q/18212/5355) . Diese Antwort gibt auch die Befehlssequenz an 
```
history -<option>
```
, die mit 
```
HISTCONTROL=ignoredups:erasedups
```
setting funktioniert .



—
[Piotr Dobrogost ](https://unix.stackexchange.com/users/5355/piotr-dobrogost)










23








Es gibt keinen Grund für 
```
export
```
die Variablen 
```
HISTCONTROL
```
und 
```
PROMPT_COMMAND
```
: Sie definieren sie in, 
```
.bashrc
```
sodass sie in jeder Shell definiert werden (auch in nicht interaktiven, was ebenfalls verschwenderisch ist).



—
[Dolmen ](https://unix.stackexchange.com/users/70275/dolmen)














248 










Das ist also alles, was mit meiner Geschichte zu 
```
.bashrc
```
tun hat:

```

```
export HISTCONTROL=ignoredups:erasedups # no duplicate entries
export HISTSIZE=100000 # big big history
export HISTFILESIZE=100000 # big big history
shopt -s histappend # append to history, don't overwrite it

# Save and reload the history after each command finishes
export PROMPT_COMMAND="history -a; history -c; history -r; $PROMPT_COMMAND"
```

```

Getestet mit bash 3.2.17 unter Mac OS X 10.5, bash 4.1.7 unter 10.6.









—
[kch](https://unix.stackexchange.com/users/3689/kch)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/48113#48113)









3








Hmm .. Dadurch wird die Verwendung von $! 34 zunichte gemacht, da sich die Befehlsnummern bei jeder Eingabeaufforderung ändern. Gibt es eine Problemumgehung @Davide @Schof @kch?









5








Verwenden Sie dies, um eine unendliche Geschichte zu erhalten: [Bash ewige Geschichte](http://www.debian-administration.org/articles/543) . Dies ist jedoch kostenlos für den obigen Code, da er nicht automatisch neu geladen wird.









7








Zu Ihrer Information: Keine der hier genannten Lösungen kann das folgende Problem lösen. Ich habe zwei Shell-Fenster A und B. In Shell-Fenster A renne ich 
```
sleep 9999
```
und (ohne auf das Ende des Ruhezustands zu warten) in Shell-Fenster B möchte ich 
```
sleep 9999
```
in der Bash-Historie sehen können.



—
[Pkt. ](https://unix.stackexchange.com/users/3054/pts)










1








@pts Auch ich habe auf Live-Verhalten abgezielt, aber dann wurde mir klar, dass es bequemer ist, terminalspezifische Historien zu haben, die das Arbeiten an verschiedenen Dingen in verschiedenen Terminals erleichtern. Ich fand das sehr nützlich: [stackoverflow.com/questions/338285/#answer-7449399](http://stackoverflow.com/questions/338285/#answer-7449399) Auf dieser Grundlage habe ich mir einen Alias ​​erstellt 
```
href
```
, der den Verlauf meines aktuellen Terminals sofort aktualisiert und dabei die Verlaufsdatei bereinigt. Jedes Mal, wenn ich ein neues Terminal öffne, wird diese Bereinigung / Synchronisierung in meiner bashrc-Datei ausgeführt, sodass das neue Terminal den neuesten Verlauf aufweist. Ich benutze das zusammen mit
```
history -a
```




—
[trusktr ](https://unix.stackexchange.com/users/5536/trusktr)










6








Es gibt keinen Grund für 
```
export
```
die Variablen: Sie definieren sie in, 
```
.bashrc
```
so dass sie in jeder Shell definiert werden (auch in nicht interaktiven, was ebenfalls verschwenderisch ist)



—
[Dolmen ](https://unix.stackexchange.com/users/70275/dolmen)














118 










Hier ist mein Versuch, den Verlauf der Bash-Sitzung zu teilen. Dies ermöglicht die gemeinsame Nutzung des Verlaufs zwischen Bash-Sitzungen, sodass der Verlaufszähler nicht verwechselt wird und die Verlaufserweiterung wie 
```
!number
```
gewünscht funktioniert (mit einigen Einschränkungen).

Verwendung von Bash Version 4.1.5 unter Ubuntu 10.04 LTS (Lucid Lynx).

```

```
HISTSIZE=9000
HISTFILESIZE=$HISTSIZE
HISTCONTROL=ignorespace:ignoredups

_bash_history_sync() {
builtin history -a #1
HISTFILESIZE=$HISTSIZE #2
builtin history -c #3
builtin history -r #4
}

history() { #5
_bash_history_sync
builtin history "$@"
}

PROMPT_COMMAND=_bash_history_sync
```

```

## Erläuterung:


- 

Hängen Sie die gerade eingegebene Zeile an 
```
$HISTFILE
```
(Standard ist 
```
.bash_history
```
). Dadurch wird 
```
$HISTFILE
```
eine Zeile größer.

- 

Wenn Sie die Spezialvariable 
```
$HISTFILESIZE
```
auf einen bestimmten Wert setzen, wird Bash 
```
$HISTFILE
```
nicht länger als 
```
$HISTFILESIZE
```
Zeilen gekürzt, indem die ältesten Einträge entfernt werden.

- 

Löschen Sie den Verlauf der laufenden Sitzung. Dadurch wird der Verlaufszähler um den Betrag von reduziert 
```
$HISTSIZE
```
.

- 

Lesen Sie den Inhalt von 
```
$HISTFILE
```
und fügen Sie ihn in den aktuellen Sitzungsverlauf ein. Dadurch wird der Verlaufszähler um die Anzahl der Zeilen in erhöht 
```
$HISTFILE
```
. Beachten Sie, dass die Zeilenzahl von 
```
$HISTFILE
```
nicht unbedingt ist 
```
$HISTFILESIZE
```
.

- 

Die 
```
history()
```
Funktion überschreibt den integrierten Verlauf, um sicherzustellen, dass der Verlauf synchronisiert ist, bevor er angezeigt wird. Dies ist für die Historienerweiterung nach Zahlen erforderlich (dazu später mehr).



## Weitere Erklärung:


- 

Schritt 1 stellt sicher, dass der Befehl aus der aktuell ausgeführten Sitzung in die globale Verlaufsdatei geschrieben wird.

- 

Schritt 4 stellt sicher, dass die Befehle aus den anderen Sitzungen in den aktuellen Sitzungsverlauf eingelesen werden.

- 

Da Schritt 4 den Verlaufszähler erhöht, müssen wir den Zähler auf irgendeine Weise reduzieren. Dies erfolgt in Schritt 3.

- 

In Schritt 3 wird der Historienzähler um reduziert 
```
$HISTSIZE
```
. In Schritt 4 wird der Verlaufszähler um die Anzahl der Zeilen in erhöht 
```
$HISTFILE
```
. In Schritt 2 stellen wir sicher, dass die Zeilenzahl 
```
$HISTFILE
```
genau ist 
```
$HISTSIZE
```
(dies bedeutet, 
```
$HISTFILESIZE
```
dass die gleiche sein muss wie 
```
$HISTSIZE
```
).



## Über die Einschränkungen der Historienerweiterung:

Wenn durch die Anzahl der Geschichte Expansion verwenden, sollten Sie **immer** die Nummer nachschlagen **unmittelbar** vor dem Einsatz. Das bedeutet, dass zwischen dem Nachschlagen und der Verwendung der Nummer keine Eingabeaufforderung angezeigt wird. Das bedeutet normalerweise kein Enter und kein Strg + C.

Im Allgemeinen gibt es nach mehr als einer Bash-Sitzung keine Garantie dafür, dass eine Verlaufserweiterung nach Nummer ihren Wert zwischen zwei Bash-Eingabeaufforderungsanzeigen beibehält. Denn wenn 
```
PROMPT_COMMAND
```
ausgeführt wird, wird der Verlauf aller anderen Bash-Sessions in den Verlauf der aktuellen Session integriert. Wenn eine andere Bash-Sitzung einen neuen Befehl hat, unterscheiden sich die Verlaufsnummern der aktuellen Sitzung.

Ich finde diese Einschränkung vernünftig. Ich muss die Nummer ohnehin jedes Mal nachschlagen, weil ich mich nicht an willkürliche Verlaufsnummern erinnern kann.

Normalerweise verwende ich die Verlaufserweiterung nach dieser Nummer

```

```
$ history | grep something #note number
$ !number
```

```

Ich empfehle die Verwendung der folgenden Bash-Optionen.

```

```
## reedit a history substitution line if it failed
shopt -s histreedit
## edit a recalled history line before executing
shopt -s histverify
```

```

## Seltsame Bugs:

Wenn Sie den Befehl history ausführen, der an eine beliebige Stelle weitergeleitet wird, wird dieser Befehl zweimal im Verlauf aufgeführt. Zum Beispiel:

```

```
$ history | head
$ history | tail
$ history | grep foo
$ history | true
$ history | false
```

```

Alle werden zweimal in der Historie aufgeführt. Ich habe keine Idee warum.

## Verbesserungsvorschläge:


- 

Ändern Sie die Funktion 
```
_bash_history_sync()
```
so, dass sie nicht jedes Mal ausgeführt wird. Beispielsweise sollte es nicht nach einer 
```
CTRL+C
```
Aufforderung ausgeführt werden. Ich 
```
CTRL+C
```
verwerfe oft eine lange Befehlszeile, wenn ich beschließe, diese Zeile nicht auszuführen. Manchmal muss ich verwenden 
```
CTRL+C
```
, um ein Bash-Abschlussskript zu stoppen.

- 

Befehle aus der aktuellen Sitzung sollten immer die aktuellsten im Verlauf der aktuellen Sitzung sein. Dies hat auch den Nebeneffekt, dass eine bestimmte Verlaufsnummer ihren Wert für Verlaufseinträge aus dieser Sitzung beibehält.










—
[lesmana](https://unix.stackexchange.com/users/1170/lesmana)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/48116#48116)









1








Warum nicht "history -n" (Zeilen neu laden, die noch nicht geladen sind) anstelle von "history -c; history -r"?



—
[Graham ](https://unix.stackexchange.com/users/12260/graham)
















@ Abraham: Ich wollte nicht verwenden, 
```
history -n
```
weil es den Verlaufszähler durcheinander bringt . Ich fand 
```
history -n
```
es auch zu unzuverlässig.



—
[Lesmana ](https://unix.stackexchange.com/users/1170/lesmana)










1








Ein Nachteil: Befehle mit mehrzeiligen Zeichenfolgen bleiben normalerweise in der aktuellen Sitzung erhalten. Mit diesem Trick werden sie sofort in einzelne Zeilen aufgeteilt. Die Verwendung von -n für -c -r hilft nicht, ebenso wenig wie cmdhist oder lithist. Ich glaube nicht, dass es derzeit eine Problemumgehung gibt.



—
[Jo Liss ](https://unix.stackexchange.com/users/9281/jo-liss)










24








Nachdem ich dies ein wenig ausprobiert hatte, stellte ich fest, dass das Ausführen von nur 
```
history -a
```
, ohne 
```
-c
```
und 
```
-r
```
in Bezug auf die Benutzerfreundlichkeit besser ist (obwohl dies nicht die Frage ist, die gestellt wurde). Dies bedeutet, dass Befehle, die Sie ausführen, sofort in neuen Shells verfügbar sind, noch bevor Sie die aktuelle Shell verlassen, jedoch nicht in gleichzeitig ausgeführten Shells. Auf diese Weise wählt Arrow-Up immer die zuletzt ausgeführten Befehle *der aktuellen Sitzung aus* , was für mich weniger verwirrend ist.



—
[Jo Liss ](https://unix.stackexchange.com/users/9281/jo-liss)
















Hervorragend gute Antwort, dies funktioniert zuverlässig im Gegensatz zu der allgemeineren "Geschichte -a; Geschichte -n"



—
[RichVel ](https://unix.stackexchange.com/users/17681/richvel)














42 










Mir ist keine Verwendung bekannt 
```
bash
```
. Aber es ist eines der beliebtesten Features von [
```
zsh
```
](http://www.zsh.org/). 

Ich persönlich bevorzuge 
```
zsh
```
es, 
```
bash
```
also empfehle ich es zu versuchen.

Hier ist der Teil von mir 
```
.zshrc
```
, der sich mit der Geschichte befasst:

```

```
SAVEHIST=10000 # Number of entries
HISTSIZE=10000
HISTFILE=~/.zsh/history # File
setopt APPEND_HISTORY # Don't erase history
setopt EXTENDED_HISTORY # Add additional data to history like timestamp
setopt INC_APPEND_HISTORY # Add immediately
setopt HIST_FIND_NO_DUPS # Don't show duplicates in search
setopt HIST_IGNORE_SPACE # Don't preserve spaces. You may want to turn it off
setopt NO_HIST_BEEP # Don't beep
setopt SHARE_HISTORY # Share history between session/terminals
```

```









—
[Maciej Piechotka](https://unix.stackexchange.com/users/305/maciej-piechotka)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/1289#1289)









1








Bei JFTR- [*Namen wird die Groß- und Kleinschreibung nicht beachtet, und Unterstriche werden ignoriert*](https://linux.die.net/man/1/zshoptions) .



—
[Pablo A ](https://unix.stackexchange.com/users/209677/pablo-a)














16 










Dazu müssen Sie Ihrem Text zwei Zeilen hinzufügen 
```
~/.bashrc
```
:

```

```
shopt -s histappend
PROMPT_COMMAND="history -a;history -c;history -r;$PROMPT_COMMAND"
```

```

Von 
```
man bash
```
:




Wenn die Shell-Option histappend aktiviert ist (siehe Beschreibung von shopt unter SHELL BUILTIN COMMANDS unten), werden die Zeilen an die Verlaufsdatei angehängt, andernfalls wird die Verlaufsdatei überschrieben.










—
[Chris Down](https://unix.stackexchange.com/users/10762/chris-down)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/25335#25335)













10 










Sie können Ihre BASH-Eingabeaufforderung so bearbeiten, dass die von Mürr vorgeschlagenen Befehle "history -a" und "history -r" ausgeführt werden:

```

```
savePS1=$PS1
```

```

(falls Sie etwas vermasseln, was fast garantiert ist)

```

```
PS1=$savePS1`history -a;history -r`
```

```

(Beachten Sie, dass dies ein Back-Tick ist. Sie führen bei jeder Eingabeaufforderung den Verlauf -a und den Verlauf -r aus. Da sie keinen Text ausgeben, bleibt Ihre Eingabeaufforderung unverändert.

Sobald Sie Ihre PS1-Variable wie gewünscht eingerichtet haben, legen Sie sie dauerhaft in Ihrer ~ / .bashrc-Datei fest.

Wenn Sie beim Testen zu Ihrer ursprünglichen Eingabeaufforderung zurückkehren möchten, gehen Sie wie folgt vor:

```

```
PS1=$savePS1
```

```

Ich habe grundlegende Tests durchgeführt, um sicherzustellen, dass es funktioniert, kann aber nicht 
```
history -a;history -r
```
bei jeder Eingabeaufforderung auf Nebenwirkungen hinweisen.









—
[Schof](https://unix.stackexchange.com/users/122296/schof)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/48114#48114)









2








Die Lösung von kch funktioniert besser als meine. Ich verwende jetzt seine Lösung in meinem .bashrc.













9 










Wenn Sie eine Lösung für die Bash- oder Zsh-Verlaufssynchronisierung benötigen, die auch das unten stehende Problem löst, lesen Sie diese unter [http://ptspts.blogspot.com/2011/03/how-to-automatically-synchronize-shell.html](http://ptspts.blogspot.com/2011/03/how-to-automatically-synchronize-shell.html)

Das Problem ist das Folgende: Ich habe zwei Shell-Fenster A und B. In Shell-Fenster A starte ich 
```
sleep 9999
```
und (ohne darauf zu warten, dass der Ruhezustand beendet ist) in Shell-Fenster B möchte ich in der Lage sein, 
```
sleep 9999
```
den Bash-Verlauf zu sehen.

Der Grund, warum die meisten anderen Lösungen dieses Problem nicht lösen können, ist, dass sie ihre Verlaufsänderungen in die Verlaufsdatei schreiben, indem sie 
```
PROMPT_COMMAND
```
oder 
```
PS1
```
, die beide zu spät ausgeführt werden, erst nach 
```
sleep 9999
```
Beendigung des Befehls verwenden.









—
[pts](https://unix.stackexchange.com/users/3054/pts)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/48117#48117)









1








Dies ist eine schöne Lösung, aber ich habe ein paar Fragen. 1. Kann ich die ursprüngliche .bash_history-Datei verwenden, ich möchte nicht, dass eine andere Bash-History-Datei in meinem $ HOME existiert? 2. Möglicherweise sollten Sie in Betracht ziehen, ein Github-Repo dafür zu erstellen.



—
[Weynhamz ](https://unix.stackexchange.com/users/13276/weynhamz)
















Es scheint, dass der Debug-Hook mit bashdb in Konflikt steht, die Ausgabe folgt jedes Mal, wenn ich eine bash-Sitzung starte. `` `bash debugger, bashdb, release 4.2-0.8 Copyright 2002, 2003, 2004, 2006, 2007, 2008, 2009, 2010, 2011 Rocky Bernstein Dies ist freie Software, die unter der GNU General Public License steht es ändern und / oder Kopien davon unter bestimmten Bedingungen verteilen. ** Interner Debug-Fehler _Dbg_is_file (): Dateiargument null bash: _Dbg_filenames [$ fullname]: ungültiger Array-Index ``



—
[weynhamz ](https://unix.stackexchange.com/users/13276/weynhamz)
















@Techlive Zheng: 1. Die ursprüngliche .bash_history wird absichtlich nicht unterstützt, da .merged_bash_history ein anderes Dateiformat verwendet. Falls .merged_bash_history nicht ordnungsgemäß geladen werden kann, wird die akkumulierte Historie durch Bash nicht versehentlich gelöscht. Robustheit durch Design bleibt erhalten. 2. Ein Github-Repo ist im Allgemeinen eine gute Idee, aber ich habe keine Zeit, das für dieses Projekt beizubehalten, also mache ich es nicht. - Ja, es ist ein Konflikt mit bashdb, und es gibt keine einfache Lösung (sie verwenden dieselben Hooks). Ich habe nicht vor, an einem Fix zu arbeiten, aber ich akzeptiere Patches.



—
[Pkt. ](https://unix.stackexchange.com/users/3054/pts)
















Okay, danke. Ich habe mir eine einfache und bessere Lösung ausgedacht.



—
[Weynhamz ](https://unix.stackexchange.com/users/13276/weynhamz)
















@TechliveZheng: Würden Sie uns Ihre einfache und bessere Lösung mitteilen, damit wir alle daraus lernen können? (Wenn ja, geben Sie bitte eine Antwort auf die Frage an.)



—
[pts ](https://unix.stackexchange.com/users/3054/pts)














8 










Mit können Sie 
```
history -a
```
den Verlauf der aktuellen Sitzung an die Histdatei anhängen und dann 
```
history -r
```
auf den anderen Terminals die Histdatei lesen. 









—
[jtimberman](https://unix.stackexchange.com/users/30875/jtimberman)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/48112#48112)













8 










Richtig, also hat mich das schließlich geärgert, eine anständige Lösung zu finden:

```

```
# Write history after each command
_bash_history_append() {
builtin history -a
}
PROMPT_COMMAND="_bash_history_append; $PROMPT_COMMAND"
```

```

Was dies bedeutet, ist eine Art Verschmelzung dessen, was in diesem Thread gesagt wurde, mit der Ausnahme, dass ich nicht verstehe, warum Sie die globale Historie nach jedem Befehl neu laden sollten. Ich kümmere mich sehr selten darum, was in anderen Terminals passiert, aber ich führe immer eine Reihe von Befehlen aus, beispielsweise in einem Terminal:

```

```
make
ls -lh target/*.foo
scp target/artifact.foo vm:~/
```

```

(Vereinfachtes Beispiel)

Und in einem anderen:

```

```
pv ~/test.data | nc vm:5000 >> output
less output
mv output output.backup1
```

```

Auf keinen Fall möchte ich, dass der Befehl geteilt wird









—
[Yarek T](https://unix.stackexchange.com/users/124644/yarek-t)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/217828#217828)









1








Der Grund, warum Sie den Verlauf nach jedem Befehl neu laden, ist, dass dies das von der Frage geforderte Verhalten ist (und die Frage daher nicht so beantwortet wird, wie sie gestellt wurde).



—
[Michael Homer ](https://unix.stackexchange.com/users/73093/michael-homer)










2








@MichaelHomer Messepunkt. Fühlen Sie sich frei, eine Ablehnung vorzunehmen, damit die Antwort unten bleibt. Ich würde dies jedoch dem OP melden, ohne zu bemerken, wie schlecht das angeforderte Verhalten sein würde und dass dies eine sehr heikle Frage ist.



—
[Yarek T ](https://unix.stackexchange.com/users/124644/yarek-t)










3








Op hier, ja, das ist ein fairer Kompromiss. Meine Hauptbeschwerde ist, dass ich die Geschichte verloren habe. Dies sollte aufhören, auch wenn es keine sofortigen Aktualisierungen über mehrere gleichzeitige Sitzungen hinweg bedeutet.



—
[Oli ](https://unix.stackexchange.com/users/880/oli)














7 










Hier ist eine Alternative, die ich benutze. Es ist umständlich, behebt jedoch das von @axel_c erwähnte Problem, bei dem manchmal eine separate Verlaufsinstanz in jedem Terminal gewünscht wird (eine für make, eine für monitoring, eine für vim usw.). 

Ich behalte eine separate angehängte Verlaufsdatei, die ich ständig aktualisiere. Ich habe die folgenden Hotkeys zugeordnet:

```

```
history | grep -v history >> ~/master_history.txt
```

```

Damit wird der gesamte Verlauf des aktuellen Terminals an eine Datei mit dem Namen master_history.txt in Ihrem Ausgangsverzeichnis angehängt. 

Ich habe auch einen separaten Hotkey zum Durchsuchen der Master-History-Datei:

```

```
cat /home/toby/master_history.txt | grep -i
```

```

Ich benutze Katze | grep, weil es den Cursor am Ende verlässt, um meinen regulären Ausdruck einzugeben. Ein weniger hässlicher Weg, dies zu tun, wäre, ein paar Skripte zu Ihrem Pfad hinzuzufügen, um diese Aufgaben zu erledigen, aber Hotkeys funktionieren für meine Zwecke. Ich werde auch in regelmäßigen Abständen den Verlauf von anderen Hosts abrufen, an denen ich gearbeitet habe, und diesen Verlauf an meine master_history.txt-Datei anhängen. 

Es ist immer schön, in der Lage zu sein, schnell nach diesem kniffligen Regex oder diesem seltsamen Perl-Einzeiler zu suchen, den Sie vor 7 Monaten erfunden haben. 









—
[Toby](https://unix.stackexchange.com/users/92245/toby)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/169053#169053)













6 










Ich kann eine Lösung für die letzte anbieten: Stellen Sie sicher, dass die env-Variable HISTCONTROL nicht "ignorespace" (oder "ignoreboth") angibt.

Aber ich spüre Ihren Schmerz bei mehreren gleichzeitigen Sitzungen. Es ist einfach nicht gut in bash gehandhabt.









—
[jmanning2k](https://unix.stackexchange.com/users/396/jmanning2k)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/1290#1290)













6 










Hier ist meine Erweiterung zu @ lesmanas [Antwort](https://unix.stackexchange.com/a/48116/45761) . Der Hauptunterschied besteht darin, dass gleichzeitige Fenster den Verlauf nicht gemeinsam nutzen. Dies bedeutet, dass Sie in Ihren Fenstern weiterarbeiten können, ohne dass Kontext von anderen Fenstern in Ihre aktuellen Fenster geladen wird.

Wenn Sie explizit 'history' eingeben ODER wenn Sie ein neues Fenster öffnen, erhalten Sie den Verlauf von allen vorherigen Fenstern.

Außerdem verwende ich [diese Strategie,](https://debian-administration.org/article/543/Bash_eternal_history) um jeden Befehl zu archivieren, der jemals auf meinem Computer eingegeben wurde.

```

```
# Consistent and forever bash history
HISTSIZE=100000
HISTFILESIZE=$HISTSIZE
HISTCONTROL=ignorespace:ignoredups

_bash_history_sync() {
builtin history -a #1
HISTFILESIZE=$HISTSIZE #2
}

_bash_history_sync_and_reload() {
builtin history -a #1
HISTFILESIZE=$HISTSIZE #2
builtin history -c #3
builtin history -r #4
}

history() { #5
_bash_history_sync_and_reload
builtin history "$@"
}

export HISTTIMEFORMAT="%y/%m/%d %H:%M:%S "
PROMPT_COMMAND='history 1 >> ${HOME}/.bash_eternal_history'
PROMPT_COMMAND=_bash_history_sync;$PROMPT_COMMAND
```

```









—
[Rubel](https://unix.stackexchange.com/users/45761/rouble)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/359217#359217)













5 










Ich habe mich dafür entschieden, den Verlauf in eine Datei pro Tag zu schreiben, da mehrere Personen auf demselben Server arbeiten können. Durch das Trennen der Befehle jeder Sitzung wird die Prüfung vereinfacht.

```

```
# Convert /dev/nnn/X or /dev/nnnX to "nnnX"
HISTSUFFIX=`tty | sed 's/\///g;s/^dev//g'`
# History file is now .bash_history_pts0
HISTFILE=".bash_history_$HISTSUFFIX"
HISTTIMEFORMAT="%y-%m-%d %H:%M:%S "
HISTCONTROL=ignoredups:ignorespace
shopt -s histappend
HISTSIZE=1000
HISTFILESIZE=5000
```

```

Die Geschichte sieht jetzt so aus:

```

```
user@host:~# test 123
user@host:~# test 5451
user@host:~# history
1 15-08-11 10:09:58 test 123
2 15-08-11 10:10:00 test 5451
3 15-08-11 10:10:02 history
```

```

Die Dateien sehen folgendermaßen aus:

```

```
user@host:~# ls -la .bash*
-rw------- 1 root root 4275 Aug 11 09:42 .bash_history_pts0
-rw------- 1 root root 75 Aug 11 09:49 .bash_history_pts1
-rw-r--r-- 1 root root 3120 Aug 11 10:09 .bashrc
```

```









—
[Litch](https://unix.stackexchange.com/users/94018/litch)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/222407#222407)













3 










An dieser Stelle möchte ich auf ein Problem hinweisen

```

```
export PROMPT_COMMAND="${PROMPT_COMMAND:+$PROMPT_COMMAND$'\n'}history -a; history -c; history -r"
```

```

und 

```

```
PROMPT_COMMAND="$PROMPT_COMMAND;history -a; history -n"
```

```

Wenn Sie source ~ / .bashrc ausführen, lautet das $ PROMPT_COMMAND wie folgt 

```

```
"history -a; history -c; history -r history -a; history -c; history -r"
```

```

und 

```

```
"history -a; history -n history -a; history -n"
```

```

Diese Wiederholung erfolgt jedes Mal, wenn Sie 'source ~ / .bashrc' ausführen. Sie können PROMPT_COMMAND nach jedem Ausführen von 'source ~ / .bashrc' überprüfen, indem Sie 'echo $ PROMPT_COMMAND' ausführen.

Sie konnten sehen, dass einige Befehle anscheinend nicht funktionierten: "history -n history -a". Aber die gute Nachricht ist, dass es immer noch funktioniert, da andere Teile immer noch eine gültige Befehlssequenz bilden (nur mit einigen zusätzlichen Kosten, da einige Befehle wiederholt ausgeführt werden. Und nicht so sauber.)

Persönlich benutze ich folgende einfache Version:

```

```
shopt -s histappend
PROMPT_COMMAND="history -a; history -c; history -r"
```

```

das hat die meisten der Funktionalitäten, während kein solches Problem wie oben erwähnt.

Ein weiterer Punkt ist: **Es gibt wirklich nichts Magisches** . PROMPT_COMMAND ist nur eine einfache Bash-Umgebungsvariable. Die darin enthaltenen Befehle werden ausgeführt, bevor Sie die Bash-Eingabeaufforderung (das $ -Zeichen) erhalten. Beispielsweise lautet Ihr PROMPT_COMMAND "echo 123" und Sie führen "ls" in Ihrem Terminal aus. Der Effekt ist wie das Ausführen von "ls; echo 123".

```

```
$ PROMPT_COMMAND="echo 123"
```

```

Ausgabe (So wie 'PROMPT_COMMAND = "echo 123"; $ PROMPT_COMMAND' ausgeführt wird): 

```

```
123
```

```

Führen Sie Folgendes aus:

```

```
$ echo 3
```

```

Ausgabe: 

```

```
3
123
```

```

"history -a" wird verwendet, um die history-Befehle in den Speicher von ~ / .bash_history zu schreiben

Mit "history -c" werden die Verlaufsbefehle im Speicher gelöscht

"history -r" wird verwendet, um Verlaufsbefehle von ~ / .bash_history in den Speicher zu lesen

Eine Erklärung zu den history-Befehlen finden Sie hier: [http://ss64.com/bash/history.html](http://ss64.com/bash/history.html)

PS: Wie andere Benutzer bereits betont haben, ist der **Export nicht** erforderlich. Siehe: [Verwenden des Exports in .bashrc](https://unix.stackexchange.com/questions/107851/using-export-in-bashrc)









—
[fstang](https://unix.stackexchange.com/users/140465/fstang)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/309087#309087)













2 










Ich habe ein Skript zum Festlegen einer Verlaufsdatei pro Sitzung oder Aufgabe auf der Grundlage der folgenden Informationen geschrieben.

```

```
# write existing history to the old file
history -a

# set new historyfile
export HISTFILE="$1"
export HISET=$1

# touch the new file to make sure it exists
touch $HISTFILE
# load new history file
history -r $HISTFILE
```

```

Es ist nicht notwendig, jeden Verlaufsbefehl zu speichern, aber es speichert die, die mir wichtig sind, und es ist einfacher, sie abzurufen, als jeden Befehl zu durchlaufen. Meine Version listet auch alle Verlaufsdateien auf und bietet die Möglichkeit, sie alle zu durchsuchen.

Vollständige Quelle: [https://github.com/simotek/scripts-config/blob/master/hiset.sh](https://github.com/simotek/scripts-config/blob/master/hiset.sh) 









—
[simotek](https://unix.stackexchange.com/users/67477/simotek)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/133912#133912)













2 










Hier ist eine Lösung, *die nicht* die Historien einzelner Sitzungen verwechselt!

Grundsätzlich muss der Verlauf jeder Sitzung separat gespeichert und bei jeder Aufforderung neu erstellt werden. Ja, es werden mehr Ressourcen verwendet, aber es ist nicht so langsam, wie es sich anhört. Die Verzögerung macht sich erst bemerkbar, wenn Sie mehr als 100000 Verlaufseinträge haben.

Hier ist die Kernlogik:

```

```
# on every prompt, save new history to dedicated file and recreate full history
# by reading all files, always keeping history from current session on top.
update_history () {
history -a ${HISTFILE}.$$
history -c
history -r
for f in `ls ${HISTFILE}.[0-9]* | grep -v "${HISTFILE}.$$\$"`; do
history -r $f
done
history -r "${HISTFILE}.$$"
}
export PROMPT_COMMAND='update_history'

# merge session history into main history file on bash exit
merge_session_history () {
cat ${HISTFILE}.$$ >> $HISTFILE
rm ${HISTFILE}.$$
}
trap merge_session_history EXIT
```

```

In [dieser Übersicht finden Sie](https://gist.github.com/jan-warchol/89f5a748f7e8a2c9e91c9bc1b358d3ec) eine vollständige Lösung, einschließlich einiger Sicherheitsmaßnahmen und Leistungsoptimierungen.









—
[Jan Warchoł](https://unix.stackexchange.com/users/32950/jan-warcho%c5%82)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/430128#430128)













1 










Dies funktioniert bei ZSH

```

```
##############################################################################
# History Configuration for ZSH
##############################################################################
HISTSIZE=10000 #How many lines of history to keep in memory
HISTFILE=~/.zsh_history #Where to save history to disk
SAVEHIST=10000 #Number of history entries to save to disk
#HISTDUP=erase #Erase duplicates in the history file
setopt appendhistory #Append history to the history file (no overwriting)
setopt sharehistory #Share history across terminals
setopt incappendhistory #Immediately append to the history file, not just when a term is killed
```

```









—
[Mulki](https://unix.stackexchange.com/users/243254/mulki)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/381535#381535)















Leider ist die Frage nur für Bash :-)



—
[Jaleks ](https://unix.stackexchange.com/users/104277/jaleks)










1








Es ist das erste Ergebnis auf Google, wenn ich auch nach zsh suche ... Dachte, es könnte helfen



—
[Mulki ](https://unix.stackexchange.com/users/243254/mulki)










3








Sie sollten die neue Frage ~ "zsh-Verlauf in mehreren Terminalfenstern beibehalten" stellen, sofern noch keine vorhanden ist. Es ist völlig in Ordnung - auch wenn Sie dazu ermutigt werden -, Ihre eigene Frage zu beantworten, wenn es sich um eine gute Frage handelt.



—
[Oli ](https://unix.stackexchange.com/users/880/oli)














1 










Ich wollte dies seit langem, vor allem die Möglichkeit, einen Befehl abzurufen, indem er ausgeführt wurde, um ihn in einem neuen Projekt erneut auszuführen (oder ein Verzeichnis mit einem Befehl zu finden). Deshalb habe ich [dieses Tool](https://github.com/gawells/ariadne) zusammengestellt, das frühere Lösungen zum Speichern eines globalen CLI-Verlaufs mit einem interaktiven Grepping-Tool namens Percol (C ^ R zugeordnet) kombiniert. Es ist auf dem ersten Computer, auf dem ich mit der Verwendung begonnen habe, immer noch ein Kinderspiel.

Mit dem lokalen CLI-Verlauf ist es in Bezug auf die Pfeiltasten nicht verwirrend, aber Sie können ganz einfach auf den globalen Verlauf zugreifen (den Sie auch einem anderen Element als C ^ R zuordnen können).









—
[Gordon Wells](https://unix.stackexchange.com/users/247036/gordon-wells)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/386808#386808)















das ist für zsh?



—
[17. ](https://unix.stackexchange.com/users/21880/sjas)










1








ja, ich habe es zunächst für zsh gemacht. Habe es aber auch für Bash und Fisch gemacht. Lassen Sie mich wissen, ob es funktioniert oder nicht. Ich habe es eine Weile nicht mehr geändert und bin mir nicht sicher, wie deutlich ich in meinen Installationsanweisungen war



—
[Gordon Wells, ](https://unix.stackexchange.com/users/247036/gordon-wells)














1 










Weil ich unendliche Geschichte bevorzuge, die in einer benutzerdefinierten Datei gespeichert ist. Ich erstelle diese Konfiguration basierend auf [https://stackoverflow.com/a/19533853/4632019](https://stackoverflow.com/a/19533853/4632019) :

```

```
export HISTFILESIZE=
export HISTSIZE=
export HISTTIMEFORMAT="[%F %T] "

export HISTFILE=~/.bash_myhistory
PROMPT_COMMAND="history -a; history -r; $PROMPT_COMMAND"
```

```









—
[Eugen Konkov](https://unix.stackexchange.com/users/129967/eugen-konkov)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/446010#446010)













-1 










Hier ist der Ausschnitt aus meinem .bashrc und kurze Erklärungen, wo immer nötig:

```

```
# The following line ensures that history logs screen commands as well
shopt -s histappend

# This line makes the history file to be rewritten and reread at each bash prompt
PROMPT_COMMAND="$PROMPT_COMMAND;history -a; history -n"
# Have lots of history
HISTSIZE=100000 # remember the last 100000 commands
HISTFILESIZE=100000 # start truncating commands after 100000 lines
HISTCONTROL=ignoreboth # ignoreboth is shorthand for ignorespace and ignoredups
```

```

HISTFILESIZE und HISTSIZE sind persönliche Einstellungen und können nach Belieben geändert werden.









—
[Hopfender Hase](https://unix.stackexchange.com/users/79890/hopping-bunny)


[
quelle
](https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/203084#203084)















##### Ähnliche Fragen:




- 
[Wie entferne ich eine einzelne Zeile aus dem Verlauf?](https://qastack.com.de/unix/49214/how-to-remove-a-single-line-from-history)
 202



- 
[Bash_history für eine bestimmte Shell vorübergehend aussetzen?](https://qastack.com.de/unix/10922/temporarily-suspend-bash-history-on-a-given-shell)
 115



- 
[Wie wiederhole ich den letzten Befehl ohne die Pfeiltasten zu verwenden?](https://qastack.com.de/unix/147563/how-do-i-repeat-the-last-command-without-using-the-arrow-keys)
 115



- 
[Grundlegendes zum Ausrufezeichen (!) In bash](https://qastack.com.de/unix/3747/understanding-the-exclamation-mark-in-bash)
 108



- 
[Gibt es eine Möglichkeit, Befehle aus dem Verlauf auszuführen?](https://qastack.com.de/unix/275053/is-there-any-way-to-execute-commands-from-history)
 99

















##### We use cookies







We use cookies and other tracking technologies to improve your browsing experience on our website,
to show you personalized content and targeted ads, to analyze our website traffic,
and to understand where our visitors are coming from.







By continuing, you consent to our use of cookies and other tracking technologies and
affirm you're at least 16 years old or have consent from a parent or guardian.







You can read details in our
[Cookie policy](https://qastack.com.de/legal/cookies-policy.html) and
[Privacy policy](https://qastack.com.de/legal/privacy-policy.html).




OK, enter website!













Durch die Nutzung unserer Website bestätigen Sie, dass Sie unsere [Cookie-Richtlinie](https://qastack.com.de/legal/cookies-policy.html) und [Datenschutzrichtlinie](https://qastack.com.de/legal/privacy-policy.html) gelesen und verstanden haben.





Licensed under [cc by-sa 3.0](https://creativecommons.org/licenses/by-sa/3.0/)
with attribution required.









**