# codingCHEAT
#!/bin/bash

# Variablen
#######VARIABLEN AUS DATEI AUSLESEN ##########
CONFIG="/home/mmk/qq/config"
. $CONFIG
###### read input $var ##########################
echo Dein Name? $var0 
read var0
echo Willkommen zurück $var0
################ else if #############################
$ echo "Sie haben `ls | wc -l` Dateien in `pwd`" 
Sie haben 43 Dateien in /home/wikifanm=10


# Funktionen
#Ein Beispiel zeigt, wie man zwei Zeichenketten miteinander vergleicht und dem Ergebnis entsprechend eine Meldung dazu ausgibt. Wichtig zu beachten sind hier die Leerzeichen 
#vor und hinter dem Vergleichsoperator sowie um die eckigen Klammern.
echo "Wie ist Ihr Name?"
read ANTWORT
if [ "$ANTWORT" == "root" ]
    then
        echo "Hallo, Administrator."
    else
        echo "Hallo, Anwender."
fi
################ Ein Beispiel zeigt, wie man auf die Existenz einer Datei hin prüft und entsprechend dem Ergebnisse eine Meldung dazu ausgibt.####
if [ -f /$DATEIPFAD/config ]
  then
    echo "Die config in qq ist da."
  else
    echo "Die configinq q FEHLT!."
fi

### Funktion
function function_B {
  echo "$CODEPFAD"
}
