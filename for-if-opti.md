# for-if-opti
Sinnlose Kommandosubstitution¶
Ein Skript, in dem $( ... ) vorkommt, oder die veralteten Backticks, kann man sehr häufig optimieren.

1
2
3
for i in $(cat dateiname) ; do
  ...
done
Lässt sich optimieren nach

1
2
3
while read i ; do
  ...
done < dateiname
Wenn statt cat dateiname ein komplexerer Befehl benutzt wird, ist es besser statt

1
2
3
for i in $(komplexerer Befehl) ; do
  ...
done
1
2
3
while read i ; do
  ...
done< <(komplexer Befehl)
zu schreiben.

Sinnloses test
Es ist überflüssig

1
2
3
4
5
kommando
if [ $? -ne 0 ] ; then
  echo "fehler"
  exit 255
fi
zu schreiben, wenn doch auch

1
2
3
4
if ! kommando ; then
  echo "fehler"
  exit 255
fi

