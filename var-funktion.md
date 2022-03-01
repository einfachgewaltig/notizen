# var-funktion
function name ()
{
        Befehle
}


Beispiel 1: Im nachfolgenden Beispiel verändert die
Funktion Test eine globale Variable.
Die Funktion selbst hat keine Parameter.

#!/bin/bash
#
# functest1, Beispiel mit function
# Rückgabewerte der Funktion über globale Variable

# Globale Variable
ORT1=Berlin

# Funktion
function test ()
{
    ORT1="10777 "$ORT1
    echo "ORT1 innnerhalb der Funktion: $ORT1"
}

clear
# Variable ORT1?
echo "ORT1 vor dem Ausführen der Funktion: $ORT1"

# Funktion ausführen
test
echo "ORT1 nach dem Ausführen der Funktion: $ORT1"

Und so sieht das Ergebnis aus:

~/bin # functest1         ↵
ORT1 vor dem Ausführen der Funktion: Berlin
ORT1 innnerhalb der Funktion: 10777 Berlin
ORT1 nach dem Ausführen der Funktion: 10777 Berlin

Beispiel 2: Im 2. Beispiel eine kleine Variation, 
die Variable ORT1 ist leer, es wird ein Parameter an die Funktion übergeben.

#!/bin/bash
#
# functest2, Beispiel mit function
# Rückgabewerte der Funktion über globale Variable

# Globale Variable
ORT1=""

# Funktion
function test ()
{
    # Parameter $1 auswerten
    ORT1="10777 "$1
    echo "ORT1 innnerhalb der Funktion: $ORT1"
}

clear
# Variable ORT1?
echo "ORT1 vor dem Ausführen der Funktion: $ORT1"

# Funktion ausführen, einen Parameter übergeben.
test Berlin
echo "ORT1 nach dem Ausführen der Funktion: $ORT1"

Das Ergebnis:

~/bin # functest2         ↵
ORT1 vor dem Ausführen der Funktion:
ORT1 innnerhalb der Funktion: 10777 Berlin
ORT1 nach dem Ausführen der Funktion: 10777 Berlin

Beispiel 3: Im nächsten Beispiel wird der Rückgabewert mit Hilfe von echo
in die Standard-Ausgabe der Funktion geschrieben. Ausserdem wird beim Aufruf 
der Funktion die Kommandosubstitution (s. Lektion 3) verwendet.

Hinweis: Wenn man die Funktion mit Hilfe der Kommandosubstitution ausführt, 
erfolgt keine Ausgabe von echo am Bildschirm.
#!/bin/bash
#
# functest3, Beispiel mit function
# Rückgabewerte der Funktion werden mit echo
# in die Standardausgabe geschrieben.

# Globale Variable
ORT1=""

# Funktion
function test ()
{
# Parameterübergabe
ORT="10777 "$1
echo "$ORT"
}

clear
# Variable ORT1?
echo "ORT1 vor dem Ausführen der Funktion: $ORT1"

# Funktion ausführen, mit Kommandosubstitution
ORT1=$(test Berlin)
echo "ORT1 nach dem Ausführen der Funktion: $ORT1"

Das Ergebnis:

~/bin # functest3          ↵
ORT1 vor dem Ausführen der Funktion:
ORT1 nach dem Ausführen der Funktion: 10777 Berlin

Zum Seitenanfang

Der Befehl return
Der Befehl sieht so aus:

return [n]

Wenn der Befehl innerhalb einer Funktion ausgeführt wird, 
wird die Funktion verlassen und der Wert n als Integerzahl 
zurückgegeben. n kann als Parameter auch entfallen. Wenn n entfällt,
wird der Rückgabewert des zuletzt ausgeführten Befehls zurückgegeben.
Der positive Wert für n kann jedoch nicht grösser als 256 werden.
Negative Werte können grösser sein, ich weiss jedoch nicht wo die Grenze liegt.

Der Rückgabewert von return wird innerhalb des Skriptes, nach dem Aufruf der Funktion, mit $? ermittelt.
Wenn man auf diese Art eine Rückgabe von einer Funktion erhält,
dann macht dies meist nur Sinn, wenn es sich dabei um eine Statusinformation handelt. 
Also z.B. WAHR oder FALSCH. Man kann natürlich in dieser Integerzahl auch mehrere 
Informationen in binärer Form speichern und diese dann mit Hilfe des bitweisen UND (s. Lektion 9) ermitteln.
Auf diese Weise lassen sich in einem Byte 8 Statusinformationen speichern.

Beispiel 4: Rückgabe erfolgt mit return

#!/bin/bash
#
# functest4, Beispiel mit function
# Rückgabe mit return
# Beim Aufruf von functest4 muss ein Ortsname als
# Parameter übergeben werden

# Funktion
function test ()
{
# Parameterübergabe
ORT=$1
if [ "$ORT" == "Berlin" ] ; then
        # OK
        return 1
else
        # nicht OK
        return -1
fi
}

# Funktion ausführen
test $1
echo "Der Rückgabewert von return ist $?"

Das Ergebnis:

~/bin # functest4 Berlin         ↵
Der Rückgabewert von return ist 1

Beispiel 5: Range von return testen. Dazu functest5 mit einer Integerzahl als Parameter aufrufen.

#!/bin/bash
#
# functest5, Beispiel mit function und return
# Dient zum Testen des Range von return

# Funktion
function test ()
{
        return $1
}

# Funktion ausführen
test $1
echo "Der Rückgabewert von return ist $?"

Und hier das Ergebnis. Wenn man Werte eingibt die +256 überschreiten,
 wird der Wert 1 Zurückgegeben. Der negative Bereich ist dagegen viel grösser.

~/bin # functest5 10         ↵
Der Rückgabewert von return ist 10
~/bin # functest5 255         ↵
Der Rückgabewert von return ist 255
~/bin # functest5 256         ↵
Der Rückgabewert von return ist 256
~/bin # functest5 257         ↵
Der Rückgabewert von return ist 1
~/bin # functest5 500         ↵
Der Rückgabewert von return ist 1
~/bin # functest5 -65535         ↵
Der Rückgabewert von return ist -65535
~/bin # functest5 -2000000         ↵
Der Rückgabewert von return ist -2000000

Zum Seitenanfang

local - Lokale Variablen in Funktionen verwenden
Lokale Variablen sind nur in Funktionen zulässig. Mit

local Variable=Wert

weisst man der Variablen einen Wert zu. Alle Werte, die die Variable im Laufe ihres Lebens annimmt,
gelten nur in der Funktion, in der die Variable erzeugt wurde.

Da die Variable nur in einer Funktion ihre Gültigkeit hat, kann man der Variablen auch einen Namen geben, 
en es global, also im aufrufenden Skript, schon gibt.
Mit Hilfe dieser Funktionalität kann man die lokalen Variablen in der Funktion,
vor dem Rest des Skriptes verstecken, oder in der Funktion "einkapseln".

Beispiel 6: Das Verhalten von globalen und lokalen Variablen testen

#!/bin/bash
#
# functest6, Beispiel mit function
# Das Verhalten von globalen und lokalen Variablen testen

# Globale Variable
NAME1=Meyer
NAME2=Mayr

# Funktionfunction name ()
{
        Befehle
}


function test ()
{
# lokale Variablen definieren
local NAME1=Schmiedt
local NAME2=Schmitt

# lokale Variablen am Bildschirm ausgeben
echo "Lokale Variable NAME1 in test(): $NAME1"
echo "Lokale Variable NAME2 in test(): $NAME2"
}

clear
# Globale Variablen?
echo "NAME1 (global) vor dem Ausführen von test(): $NAME1"
echo "NAME2 (global) vor dem Ausführen von test(): $NAME2"

# Funktion ausführen
test

# Globale Variablen?
echo "NAME1 (global) nach dem Ausführen von test(): $NAME1"
echo "NAME2 (global) nach dem Ausführen von test(): $NAME2"

functest6 ausführen:

~/bin # functest6         ↵
NAME1 (global) vor dem Ausführen von test(): Meyer
NAME2 (global) vor dem Ausführen von test(): Mayr
Lokale Variable NAME1 in test(): Schmiedt
Lokale Variable NAME2 in test(): Schmitt
NAME1 (global) nach dem Ausführen von test(): Meyer
NAME2 (global) nach dem Ausführen von test(): Mayr
