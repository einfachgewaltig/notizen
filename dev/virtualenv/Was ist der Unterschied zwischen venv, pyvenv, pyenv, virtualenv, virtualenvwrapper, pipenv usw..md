Was ist der Unterschied zwischen venv, pyvenv, pyenv, virtualenv, virtualenvwrapper, pipenv usw.
========================================



[https://qastack.com.de/programming/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe](https://qastack.com.de/programming/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe)**





[*](https://qastack.com.de/)







- 
[Programmierung](https://qastack.com.de/programming/)


- 
[Tags](https://qastack.com.de/programming/tags/)






- 

[
Account
](https://qastack.com.de/programming/41573587/#)

[Anmeldung](https://qastack.com.de/accounts/login/?next=/)
[Registrieren](https://qastack.com.de/accounts/signup/?next=/programming/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe)















# Was ist der Unterschied zwischen venv, pyvenv, pyenv, virtualenv, virtualenvwrapper, pipenv usw.?







1022 










Python 3.3 enthält das neue Paket in seiner Standardbibliothek 
```
venv
```
. Was macht es und wie unterscheidet es sich von allen anderen Paketen, die dem regulären Ausdruck zu entsprechen scheinen 
```
(py)?(v|virtual|pip)?env
```
?







[python](https://qastack.com.de/programming/tagged/python/) 

[virtualenv](https://qastack.com.de/programming/tagged/virtualenv/) 

[virtualenvwrapper](https://qastack.com.de/programming/tagged/virtualenvwrapper/) 

[pyenv](https://qastack.com.de/programming/tagged/pyenv/) 

[python-venv](https://qastack.com.de/programming/tagged/python-venv/) 







—
[
Flimm
](https://stackoverflow.comhttps://stackoverflow.com/users/247696/flimm)


[
quelle
](https://stackoverflow.com/programming/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe)












20








Um die engen Abstimmungen zu verhindern, hielt ich dies für eine allgemeinere Frage als [stackoverflow.com/questions/29950300/…](http://stackoverflow.com/questions/29950300/what-is-the-relationship-between-virtualenv-and-pyenv) , und daher fühlte ich mich nicht wohl, diese Frage zu bearbeiten oder eine übermäßig allgemeine Antwort auf diesen Beitrag zu veröffentlichen.



—
[Flimm ](https://stackoverflow.comhttps://stackoverflow.com/users/247696/flimm)










12








Diese Anleitung ist sowohl nützlich als auch ständig aktualisiert, da Python immer mehr "eine und nur eine offensichtliche Möglichkeit" hinzufügt, Dinge zu tun: [docs.python-guide.org/en/latest/dev/virtualenvs](http://docs.python-guide.org/en/latest/dev/virtualenvs/)



—
[michael ](https://stackoverflow.comhttps://stackoverflow.com/users/127971/michael)










2








Ab 3.6 fand ich es einfacher, virtualenv im Vergleich zu pyenv unter macOS zum Laufen zu bringen (ich bin ein pyNoob)



—
[HashRocketSyntax ](https://stackoverflow.comhttps://stackoverflow.com/users/5739514/hashrocketsyntax)
















@HashRocketSyntax 
```
virtualenv
```
und 
```
pyenv
```
führen nicht die gleiche Funktion aus und sind keine Alternativen zueinander. Siehe meine Antwort.



—
[Flimm ](https://stackoverflow.comhttps://stackoverflow.com/users/247696/flimm)










6








Ich habe einen ganzen Tag verbrannt und Zeit mit Pipenv verschwendet. Unterm Strich ist es übermarktet. Venv und virtualenv, wenn Sie py2 benötigen, sind die richtigen Werkzeuge. Conda (Miniconda, wenn Sie nicht den vollen Stapel benötigen) ist auch sehr gut. Sehr gute Zusammenfassung: [chriswarrick.com/blog/2018/07/17/…](https://chriswarrick.com/blog/2018/07/17/pipenv-promises-a-lot-delivers-very-little/)



—
[SwimBikeRun ](https://stackoverflow.comhttps://stackoverflow.com/users/1018733/swimbikerun)












Antworten:







1382 









# PyPI-Pakete nicht in der Standardbibliothek:


- 

**[
```
virtualenv
```
](https://pypi.python.org/pypi/virtualenv)**ist ein sehr beliebtes Tool, das isolierte Python-Umgebungen für Python-Bibliotheken erstellt. Wenn Sie mit diesem Tool nicht vertraut sind, empfehle ich dringend, es zu lernen, da es ein sehr nützliches Tool ist, und ich werde für den Rest dieser Antwort Vergleiche damit anstellen.

Es funktioniert, indem eine Reihe von Dateien in einem Verzeichnis installiert werden (z. B. 
```
env/
```
:) und anschließend die 
```
PATH
```
Umgebungsvariable so geändert wird, dass ihr ein benutzerdefiniertes 
```
bin
```
Verzeichnis vorangestellt wird (z 
```
env/bin/
```
. B. :) . Eine genaue Kopie der 
```
python
```
oder 
```
python3
```
binär wird in diesem Verzeichnis abgelegt, aber Python ist so programmiert, dass es zuerst im Umgebungsverzeichnis nach Bibliotheken relativ zu seinem Pfad sucht. Es ist nicht Teil der Standardbibliothek von Python, wird jedoch offiziell von der PyPA (Python Packaging Authority) gesegnet. Nach der Aktivierung können Sie Pakete in der virtuellen Umgebung mit installieren 
```
pip
```
.

- 

**[
```
pyenv
```
](https://github.com/yyuu/pyenv)**wird verwendet, um Python-Versionen zu isolieren. Beispielsweise möchten Sie Ihren Code möglicherweise gegen Python 2.7, 3.6, 3.7 und 3.8 testen, sodass Sie eine Möglichkeit benötigen, zwischen diesen zu wechseln. Nach der Aktivierung wird der 
```
PATH
```
Umgebungsvariablen ein Präfix vorangestellt 
```
~/.pyenv/shims
```
, in dem spezielle Dateien vorhanden sind, die den Python-Befehlen ( 
```
python
```
, 
```
pip
```
) entsprechen. Dies sind keine Kopien der von Python gelieferten Befehle. Hierbei handelt es sich um spezielle Skripts, die im Handumdrehen anhand der 
```
PYENV_VERSION
```
Umgebungsvariablen, der 
```
.python-version
```
Datei oder der 
```
~/.pyenv/version
```
Datei entscheiden, welche Version von Python ausgeführt werden soll. 
```
pyenv
```
Außerdem wird das Herunterladen und Installieren mehrerer Python-Versionen mithilfe des Befehls vereinfacht 
```
pyenv install
```
.

- 

**[
```
pyenv-virtualenv
```
](https://github.com/yyuu/pyenv-virtualenv)**ist ein Plugin für 
```
pyenv
```
vom selben Autor wie 
```
pyenv
```
zu ermöglichen , die Sie zu verwenden 
```
pyenv
```
und 
```
virtualenv
```
bequem gleichzeitig an. Wenn Sie jedoch Python 3.3 oder höher verwenden, 
```
pyenv-virtualenv
```
wird versucht, es auszuführen, 
```
python -m venv
```
wenn es verfügbar ist, anstatt 
```
virtualenv
```
. Sie können 
```
virtualenv
```
und 
```
pyenv
```
zusammen ohne verwenden 
```
pyenv-virtualenv
```
, wenn Sie die Komfortfunktionen nicht möchten.

- 

**[
```
virtualenvwrapper
```
](https://pypi.python.org/pypi/virtualenvwrapper)**ist eine Reihe von Erweiterungen für 
```
virtualenv
```
(siehe [Dokumente](http://virtualenvwrapper.readthedocs.io/en/latest/) ). Es gibt Ihnen Befehle wie 
```
mkvirtualenv
```
, 
```
lssitepackages
```
und insbesondere 
```
workon
```
zum Wechseln zwischen verschiedenen 
```
virtualenv
```
Verzeichnissen. Dieses Tool ist besonders nützlich, wenn Sie mehrere 
```
virtualenv
```
Verzeichnisse möchten .

- 

**[
```
pyenv-virtualenvwrapper
```
](https://github.com/yyuu/pyenv-virtualenvwrapper)**ist ein Plugin für 
```
pyenv
```
vom selben Autor wie 
```
pyenv
```
, um bequem zu integrieren 
```
virtualenvwrapper
```
in 
```
pyenv
```
.

- 

**[
```
pipenv
```
](https://pypi.python.org/pypi/pipenv)**zielt darauf ab 
```
Pipfile
```
, 
```
pip
```
und 
```
virtualenv
```
in einem Befehl in der Befehlszeile zu kombinieren . Das 
```
virtualenv
```
Verzeichnis wird normalerweise abgelegt 
```
~/.local/share/virtualenvs/XXX
```
, wobei 
```
XXX
```
es sich um einen Hash des Pfads des Projektverzeichnisses handelt. Dies unterscheidet sich von 
```
virtualenv
```
dem Verzeichnis, in dem sich das Verzeichnis normalerweise im aktuellen Arbeitsverzeichnis befindet. 
```
pipenv
```
ist für die Entwicklung von Python-Anwendungen vorgesehen (im Gegensatz zu Bibliotheken). Es gibt Alternativen zu 
```
pipenv
```
solchen 
```
poetry
```
, die ich hier nicht auflisten werde, da es sich bei dieser Frage nur um Pakete handelt, die ähnlich benannt sind.



# Standardbibliothek:


- 

**
```
pyvenv
```
**ist ein Skript, das mit Python 3 ausgeliefert wird, [in Python 3.6](https://docs.python.org/dev/whatsnew/3.6.html#id8) jedoch [veraltet ist,](https://docs.python.org/dev/whatsnew/3.6.html#id8) da es Probleme hatte (ganz zu schweigen vom verwirrenden Namen). In Python 3.6+ ist das genaue Äquivalent 
```
python3 -m venv
```
.

- 

**[
```
venv
```
](https://docs.python.org/3/library/venv.html)**ist ein mit Python 3 
```
python3 -m venv
```
geliefertes Paket, das Sie verwenden können (obwohl einige Distributionen es aus irgendeinem Grund in ein separates Distributionspaket aufteilen, z. B. 
```
python3-venv
```
unter Ubuntu / Debian). Es dient demselben Zweck wie 
```
virtualenv
```
, verfügt jedoch nur über eine Teilmenge seiner Funktionen ( [siehe Vergleich hier](https://virtualenv.pypa.io/en/latest/) ). 
```
virtualenv
```
ist weiterhin beliebter als 
```
venv
```
, zumal erstere sowohl Python 2 als auch Python 3 unterstützen.



# Empfehlung für Anfänger:

Dies ist meine persönliche Empfehlung für Anfänger: Start von Lernen [
```
virtualenv
```
](https://pypi.org/project/virtualenv/)und [
```
pip
```
](https://pypi.org/project/pip/)Werkzeugen sowohl mit Python der Arbeit 2 und 3 und in einer Vielzahl von Situationen und andere Werkzeuge abholen , sobald Sie sie starten zu müssen.









—
[Flimm](https://stackoverflow.com/users/247696/flimm)


[
quelle
](https://stackoverflow.com/programming/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe/41573588#41573588)









115








Das ist sehr hilfreich! Warum gibt es also 8 verwickelte Dinge anstelle von 1? ("Es sollte einen - und vorzugsweise nur einen - offensichtlichen Weg geben, dies zu tun." - Das Zen von Python)



—
[Jerry101 ](https://stackoverflow.comhttps://stackoverflow.com/users/1682419/jerry101)










59








@ Jerry101, die Einführung von venv ist teilweise eine Antwort auf dieses Durcheinander. Wenn Sie zur Verbesserung der Situation beitragen möchten, empfehle ich Ihnen, venv zu verwenden und andere zu ermutigen, dasselbe zu tun.



—
[Magnus Lind Oxlund ](https://stackoverflow.comhttps://stackoverflow.com/users/1662230/magnus-lind-oxlund)










31








"Die Einführung von venv ist zum Teil eine Reaktion auf dieses Durcheinander." Wie kommt es, dass die Leute, wenn es zu viele Dinge gibt, die "so etwas wie X" tun, immer denken, dass sie dieses Durcheinander verbessern können, indem sie eine andere Sache machen, die "so etwas wie X" tut? . Eigentlich ist es irgendwie lustig. Wir sind jetzt 4 Jahre später ... also ist es vielleicht angebracht zu fragen, 
```
venv
```
ob das Problem tatsächlich gelöst wurde.



—
[Kris ](https://stackoverflow.comhttps://stackoverflow.com/users/2141091/kris)










34








Die einzigen zwei Tools auf der Liste, die wirklich das wohl gleiche Gebiet abdecken, sind virtualenv und venv. Daher ist die Charakterisierung, dass es sich um ein Durcheinander handelt, das durch mehrere konkurrierende Tools verursacht wird, nicht sehr genau. Die Liste besteht jedoch aus mehreren Tools für die virtuelle Umgebung, die alle ähnlich klingende Namen haben. Das kann verwirrend sein, insbesondere für Benutzer, die gerade etwas über sie lernen. Hat venv die Situation verbessert? Es bot eine leichtere Alternative zu anderen Tools für virtuelle Umgebungen und profitierte von nativen Änderungen und einem Platz in der Standardbibliothek. …



—
[Magnus Lind Oxlund ](https://stackoverflow.comhttps://stackoverflow.com/users/1662230/magnus-lind-oxlund)










11








@cowbert Nachdem Sie gerade ein Upgrade von Python 3.5 auf Python 3.6 durchgeführt haben und alle meine virtuellen Anwendungen unterbrochen wurden, können Sie anscheinend 
```
venv
```
einfacher auf eine neue Python-Version aktualisieren.



—
[Daniel H ](https://stackoverflow.comhttps://stackoverflow.com/users/27302/daniel-h)














276 










Ich würde nur die Verwendung von 
```
virtualenv
```
nach Python3.3 + vermeiden und stattdessen die standardmäßige ausgelieferte Bibliothek verwenden 
```
venv
```
. Um eine neue virtuelle Umgebung zu erstellen, geben Sie Folgendes ein:

```

```
$ python3 -m venv <MYVENV> 
```

```

```
virtualenv
```
versucht, die Python-Binärdatei in das bin-Verzeichnis der virtuellen Umgebung zu kopieren. In diese Binärdatei eingebettete Bibliotheksdateiverknüpfungen werden jedoch nicht aktualisiert. Wenn Sie also Python aus dem Quellcode in ein Nicht-Systemverzeichnis mit relativen Pfadnamen erstellen, wird die Python-Binärdatei unterbrochen. Da Sie auf diese Weise eine kopierbare, verteilbare Python erstellen, ist dies ein großer Fehler. Übrigens, um eingebettete Bibliotheksdateilinks unter OS X zu überprüfen 
```
otool
```
. Geben Sie beispielsweise in Ihrer virtuellen Umgebung Folgendes ein:

```

```
$ otool -L bin/python
python:
@executable_path/../Python (compatibility version 3.4.0, current version 3.4.0)
/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1238.0.0)

```

```

Folglich würde ich 
```
virtualenvwrapper
```
und vermeiden 
```
pipenv
```
. 
```
pyvenv
```
ist veraltet. 
```
pyenv
```
scheint oft dort 
```
virtualenv
```
verwendet zu werden, wo es verwendet wird, aber ich würde mich auch davon fernhalten, da ich denke, dass es 
```
venv
```
auch das tut, wofür 
```
pyenv
```
es gebaut wurde. 

```
venv
```
Erstellt virtuelle Umgebungen in der Shell, die *frisch* und mit *Sandboxen versehen sind* , mit vom *Benutzer installierbaren Bibliotheken* und ist für *mehrere Pythons sicher* . *Neu,* da virtuelle Umgebungen nur mit den Standardbibliotheken beginnen, die im Lieferumfang von Python enthalten sind, müssen Sie alle anderen Bibliotheken erneut installieren, 
```
pip install
```
während die virtuelle Umgebung aktiv ist. *Sandboxed,* da keine dieser neuen Bibliotheksinstallationen außerhalb der virtuellen Umgebung sichtbar ist. Sie können also die gesamte Umgebung löschen und erneut starten, ohne sich Gedanken über die Auswirkungen auf Ihre Basis-Python-Installation machen zu müssen. *Vom Benutzer installierbare Bibliotheken,* da der Zielordner der virtuellen Umgebung ohne erstellt wird
```
sudo
```
In einem Verzeichnis, das Sie bereits besitzen, benötigen Sie keine 
```
sudo
```
Berechtigungen, um Bibliotheken darin zu installieren. Schließlich ist es *Multi-Python-sicher* , da bei der Aktivierung virtueller Umgebungen in der Shell nur die Python-Version (3.4, 3.5 usw.) angezeigt wird, die zum Erstellen dieser virtuellen Umgebung verwendet wurde. 

```
pyenv
```
ähnelt darin, 
```
venv
```
dass Sie damit mehrere Python-Umgebungen verwalten können. Jedoch mit 
```
pyenv
```
Sie können nicht bequem Rollback - Bibliothek installiert zu einem gewissen Startzustand und Sie werden wahrscheinlich brauchen 
```
admin
```
Privilegien zu einem bestimmten Zeitpunkt zu aktualisieren Bibliotheken. Daher denke ich, dass es auch am besten ist, es zu verwenden 
```
venv
```
. 

In den letzten Jahren habe ich viele Probleme bei Build-Systemen (Emacs-Pakete, eigenständige Python-Anwendungs-Builder, Installer ...) festgestellt, die letztendlich auf Probleme mit zurückzuführen sind 
```
virtualenv
```
. Ich denke, Python wird eine bessere Plattform sein, wenn wir diese zusätzliche Option eliminieren und nur verwenden 
```
venv
```
.









—
[Riaz Rizvi](https://stackoverflow.com/users/213307/riaz-rizvi)


[
quelle
](https://stackoverflow.com/programming/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe/47559925#47559925)









3









```
add2virtualenv
```
Optimiert Ihre 
```
PYTHONPATH
```
durch Hinzufügen einer benutzerdefinierten 
```
_virtualenv_path_extensions.pth
```
Datei unter 
```
site-packages
```
. Alternativ können Sie die 
```
PYTHONPATH
```
Umgebungsvariable in der 
```
bin/activate
```
Datei aktualisieren, die Sie bei jeder Aktivierung der virtuellen Umgebung aufrufen. Oder Sie können Symlinks unter hinzufügen 
```
site-packages
```
, um auf die zusätzlichen Verzeichnisse zu verweisen. Beide Alternativen sind transparenter für die herkömmlichen Befehlszeilentools, die Entwickler häufig zur Fehlerbehebung verwenden. Die Verwendung eines Brauchs 
```
.pth
```
mit einem undokumentierten Namen lässt es magischer erscheinen, IMO.



—
[Riaz Rizvi](https://stackoverflow.comhttps://stackoverflow.com/users/213307/riaz-rizvi)










15








Okay, ich habe auf [stackoverflow.com/questions/48130371/…](https://qastack.com.de/programming/48130371/python-venv-modulenotfounderror) bestätigt, dass ein korrektes Update 
```
PYTHONPATH
```
die Notwendigkeit überflüssig macht 
```
add2virtualenv
```
. In Bezug auf den Mangel an Hilfe zu SO aus Ihrem ersten Kommentar ist mein einziger Vorschlag, Antworten zu verbessern, wenn sie Ihr Problem beheben, um die Leute zu motivieren, beim Posten für Sie Fehler zu beheben? Eine halbe Stunde Nachforschungen + Zuschreibung im Austausch für einen Mausklick? Klingt nach einem guten Handel ...



—
[Riaz Rizvi](https://stackoverflow.comhttps://stackoverflow.com/users/213307/riaz-rizvi)










7








Nein, Sie haben Recht - ich versuche, gut zu stimmen. Wenn du in meiner Nähe wärst, würde ich dir ein Bier kaufen. Ich werde mein Versprechen einhalten und sehen, ob die Python-Doc-Leute mir erlauben, die Änderung aus Gründen der Klarheit zu / bin / die offiziellen Docs hinzuzufügen. Obwohl ich nicht großartig bin, bin ich nicht schrecklich in Python. Wenn es mir schwer gefallen ist ... Wie auch immer, danke für deine Zeit - wünsche dir alles Gute.



-
[SteveJ](https://stackoverflow.comhttps://stackoverflow.com/users/2338323/stevej)










9








@ MalikA.Rumi Der Segen wurde leicht reduziert auf "den Pipenv-Schöpfer, der fleißig an uns und andere vermarktet wird, weshalb wir Pipenv erwähnen".



—
[Rob Grant ](https://stackoverflow.comhttps://stackoverflow.com/users/61938/rob-grant)










6








@AndreaMoro Es ist das 
```
pyvenv
```
, was veraltet ist, nicht 
```
pyenv
```
. Es ist so leicht, mit den Namen dieser Tools verwechselt zu werden.



—
[Daniel Holmes ](https://stackoverflow.comhttps://stackoverflow.com/users/9663023/daniel-holmes)














24 










Ich bin in das 
```
pipenv
```
Kaninchenloch gegangen ( *es ist in der Tat ein tiefes und dunkles Loch ...* ) und ***da die letzte Antwort vor über 2 Jahren war*** , hielt ich es für nützlich, die Diskussion mit den neuesten Entwicklungen zum Thema Python Virtual Envelopes I zu aktualisieren habe gefunden.

## HAFTUNGSAUSSCHLUSS:

Bei dieser Antwort geht es **NICHT** darum, die ***heftige*** Debatte über die Vorzüge von ***pipenv**** versus * ***venv*** als Umschlaglösungen ***fortzusetzen -**** ich unterstütze dies auch nicht* . Es geht darum, dass ***PyPA*** widersprüchliche Standards befürwortet und wie die zukünftige Entwicklung von ***virtualenv*** verspricht, eine ***Entweder-Oder-*** Wahl ***überhaupt*** zu negieren . Ich habe mich genau deshalb auf diese beiden Werkzeuge konzentriert, weil sie von ***PyPA*** gesalbt wurden .

## venv

Wie das OP feststellt, ist ***venv*** ein Tool zur Virtualisierung von Umgebungen. ***KEINE*** Lösung von Drittanbietern, sondern ein natives Tool. ***PyPA*** unterstützt ***venv*** für die Erstellung von **VIRTUAL ENVELOPES** : " [In Version 3.5 geändert: Die Verwendung von venv wird jetzt für die Erstellung virtueller Umgebungen empfohlen](https://docs.python.org/3/library/venv.html) ."

## pipenv

***pipenv kann*** - wie*** venv*** - zum Erstellen virtueller Umschläge verwendet werden, bietet jedoch zusätzlichFunktionenfür die Paketverwaltung und die[ Überprüfung von Sicherheitslücken](https://pipenv-fork.readthedocs.io/en/latest/advanced.html#detection-of-security-vulnerabilities) . Anstelle der Verwendung
```
requirements.txt
```
,
```
pipenv
```
liefertPaketmanagement via[ Pipfile](https://github.com/pypa/pipfile) . Da[*** PyPA*** pipenv für **PACKAGE MANAGEMENT**](https://packaging.python.org/guides/tool-recommendations/)[ befürwortet](https://packaging.python.org/guides/tool-recommendations/) , scheint dies zu implizieren, dass es
```
pipfile
```
ersetzt wird
```
requirements.txt
```
.

**JEDOCH** : ***pipenv*** verwendet ***virtualenv*** als Werkzeug zum Erstellen virtueller Umschläge, **NICHT ** ***venv,*** das von ***PyPA*** als Go-to-Tool zum Erstellen virtueller Umschläge ***empfohlen*** wird .

## Widersprüchliche Standards:

Wenn es also nicht schwierig genug war, sich für eine Lösung für virtuelle Umschläge zu ***entscheiden,*** unterstützt ***PyPA*** jetzt zwei verschiedene Tools, die unterschiedliche Lösungen für virtuelle Umschläge verwenden. Die tobende Github-Debatte über ***venv vs virtualenv,*** die diesen Konflikt hervorhebt, finden Sie [hier](https://github.com/pypa/pipenv/issues/15) .

## Konfliktlösung:

Die Github-Debatte, auf die im obigen Link ***verwiesen wird, hat die*** Entwicklung von ***virtualenv*** in Richtung der ***Anpassung*** von ***venv*** in [zukünftigen Versionen](https://github.com/pypa/virtualenv/issues/1366) gelenkt :




lieber eingebautes venv: Wenn die Zielpython venv hat, erstellen wir die Umgebung damit (und führen dann nachfolgende Operationen durch, um andere von uns angebotene Garantien zu vereinfachen).



## Fazit:

Es sieht also so aus, als ob es in Zukunft eine gewisse Konvergenz zwischen den beiden konkurrierenden Lösungen für virtuelle Hüllkurven geben wird, aber ab sofort unterscheidet sich ***pipenv*** - das verwendet 
```
virtualenv
```
- ***erheblich*** von 
```
venv
```
.

Angesichts [der Probleme, die ***pipenv*** löst,](https://realpython.com/pipenv-guide/#problems-that-pipenv-solves) und der Tatsache, dass ***PyPA*** seinen Segen gegeben hat, ***scheint*** es eine glänzende Zukunft zu haben. Und wenn ***virtualenv*** auf seine vorgeschlagenen Entwicklungsziele liefert, sollte nicht mehr eine virtuelle Hülle Lösung der Wahl sein , ein Fall von beiden ***pipenv*** OR ***Venv*** .









—
[F1Linux](https://stackoverflow.com/users/10009950/f1linux)


[
quelle
](https://stackoverflow.com/programming/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe/59923461#59923461)









6








Soweit* ich verstanden habe: *Der* tatsächliche Wert von *pipenv* wurde bereits seit einiger Zeit diskutiert und seit über einem Jahr nicht mehr veröffentlicht. Viele Dinge haben sich seitdem geändert, und ich würde argumentieren, dass es für *pipenv* nur noch schlimmer wurde (Werkzeuge wie *Poesie* und *Pip-Werkzeuge* sind in einem viel besseren Zustand). Die *PyPA-* Seiten sind veraltet, und ich würde argumentieren, dass sie *pipenv herabstufen sollten* . *venv* ist ein Standardwerkzeug und als solches sehr effizient, verfügt jedoch nur über begrenzte Funktionen. *virtualenv* konkurriert nicht mit *venv,* sondern versucht, die Bereiche abzudecken, in die *venv* nicht *gehen* kann oder will (da es ein Standard ist).



—
[Sinoroc ](https://stackoverflow.comhttps://stackoverflow.com/users/11138259/sinoroc)
















@sinoroc Mein Beitrag war nicht über die Vorzüge oder pipenv., Es ging um die widersprüchlichen Führung von PyPA sowohl pipenv befürwortende UND** Venv machen die Wahl eines Umschlags Lösung schwieriger und wie es ein gewisses Maß an Converge erscheint die Notwendigkeit negieren zu wählen zwischen ihnen überhaupt. Beachten Sie, dass ich nichts unterstütze, sondern nur teile, was ich über die Entwicklung dieser beiden ***von PyPA empfohlenen*** Lösungen gelernt habe . PyPA Interesse an ihnen gegeben, ob ich mag sie oder nicht irrelevant: pipenv und Venv schien ***wahrscheinlich*** ein Teil der Landschaft geworden



—
[F1Linux ](https://stackoverflow.comhttps://stackoverflow.com/users/10009950/f1linux)










9








Ich würde sagen, *bleib* so oft wie möglich bei *venv* und *pip* . Diese beiden sind hier, um zu bleiben. *Venv* ist Teil der Standardbibliothek von Python und in gewisser Weise auch *pip,* da es in Python (über *surepip* ) verkauft wird. Die anderen Tools ( abgesehen von der *Pyenv-* Serie: etwas ganz anderes) scheinen sich entweder auf *venv* und *pip* zu stützen oder (mit mehr oder weniger Erfolg) zu *emulieren* . Was toll ist. Aber wenn die Dinge schlecht *laufen* , sind *Venv* und *Pip* der sichere Fallback. Das einzige andere Werkzeug, das ich benutze, ist *tox* (mit *tox-venv*), um die virtuellen Umgebungen zu erstellen und zu füllen (unkompliziert, keine Magie, seltsam, es wird noch nicht erwähnt).



—
[Sinoroc ](https://stackoverflow.comhttps://stackoverflow.com/users/11138259/sinoroc)










3








Dieser neueste Beitrag ist Gold wert, da er beim Ausbügeln der Falten großartige Arbeit geleistet hat. Ich halte mich an pip und venv, da ich Probleme mit baumelnden Binärdateien mit virtualenv hatte, als Systempython aktualisiert wurde.



—
[Codeviper ](https://stackoverflow.comhttps://stackoverflow.com/users/3861837/codeviper)










1








In der Vergangenheit bin ich auf Probleme mit pipenv nonverbose bei Fehlern gestoßen. Argl und Graben. Außerdem: [chriswarrick.com/blog/2018/07/17/…](https://chriswarrick.com/blog/2018/07/17/pipenv-promises-a-lot-delivers-very-little/)



—
[qrtLs ](https://stackoverflow.comhttps://stackoverflow.com/users/4933053/qrtls)














3 










**Update April 2020**

Ich habe danach gesucht, als ich auf [diesen Beitrag](https://packaging.python.org/tutorials/managing-dependencies/) gestoßen bin . Ich denke, diese Frage, welches Tool verwendet werden soll, ist für neue Python-Benutzer wie mich ziemlich verwirrend und schwierig. Dies ist direkt von der PyPA-Website in Bezug auf pipenv:




Während dieses Tutorial das pipenv-Projekt als Tool behandelt, das sich hauptsächlich auf die Anforderungen der Python-Anwendungsentwicklung und nicht auf die Entwicklung der Python-Bibliothek konzentriert, arbeitet das Projekt selbst derzeit an mehreren Prozess- und Wartungsproblemen, die verhindern, dass Fehlerkorrekturen und neue Funktionen veröffentlicht werden ( mit dem gesamten Jahr 2019 ohne Neuerscheinung). Dies bedeutet, dass pipenv kurzfristig immer noch unter mehreren Macken und Leistungsproblemen leidet, ohne dass ein klarer Zeitplan für die Lösung dieser Probleme vorliegt.




*Während dies weiterhin der Fall ist, möchten Projektbetreuer wahrscheinlich andere Tools für das Anwendungsabhängigkeitsmanagement zur Verwendung anstelle von oder zusammen mit pipenv untersuchen.*




Unter der Annahme, dass die Veröffentlichung von pipenv im April 2020 wie geplant durchgeführt wird und die Veröffentlichung danach ebenfalls auf Kurs bleibt, wird diese Einschränkung im Tutorial entfernt. Wenn diese Releases nicht auf dem richtigen Weg bleiben, wird das Lernprogramm selbst entfernt und durch eine Diskussionsseite zu den verfügbaren Optionen für das Abhängigkeitsmanagement ersetzt.










—
[Arnuld](https://stackoverflow.com/users/9814557/arnuld)


[
quelle
](https://stackoverflow.com/programming/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe/61981596#61981596)















Es sieht so aus, als ob sich pipenv derzeit (dh im Mai 2020) noch in der Vorabversion für die Veröffentlichung im April 2020 befindet. Siehe [hier](https://pypi.org/project/pipenv/#history) .



—
[Andrewjames ](https://stackoverflow.comhttps://stackoverflow.com/users/12567365/andrewjames)
















Dies beantwortet die Frage nicht.



—
[Flimm ](https://stackoverflow.comhttps://stackoverflow.com/users/247696/flimm)
















Ich denke, @Flimm hat die Fragen gut beantwortet. Ich antwortete auf die Antwort von



—
[F1Linux](https://stackoverflow.comhttps://stackoverflow.com/users/9814557/arnuld)










1








Ab 4. Juni 2020, das 
```
pipenv
```
hat Team 2 Versionen PyPI Freigabe: 
```
2020.5.28
```
und in jüngerer Zeit 
```
2020.6.2
```
: [pypi.org/project/pipenv/#history](https://pypi.org/project/pipenv/#history)



—
[Nichtsein ](https://stackoverflow.comhttps://stackoverflow.com/users/376240/nonbeing)
















##### Ähnliche Fragen:




- 
[Wie ist die Beziehung zwischen virtualenv und pyenv?](https://qastack.com.de/programming/29950300/what-is-the-relationship-between-virtualenv-and-pyenv)
 175



- 
[Was ist der Unterschied zwischen Pyenv, Virtualenv, Anaconda?](https://qastack.com.de/programming/38217545/what-is-the-difference-between-pyenv-virtualenv-anaconda)
 140



- 
[Installieren Sie Pakete nach dem Upgrade der Python-Hauptversion automatisch in der virtuellen Umgebung neu](https://qastack.com.de/programming/59859095/reinstall-packages-automatically-into-virtual-environment-after-python-major-ver)
 10



- 
[So verlassen / beenden / deaktivieren Sie eine Python-Virtualenv](https://qastack.com.de/programming/990754/how-to-leave-exit-deactivate-a-python-virtualenv)
 1607



- 
[Verwenden Sie eine andere Python-Version mit virtualenv](https://qastack.com.de/programming/1534210/use-different-python-version-with-virtualenv)
 1115

















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





Lizenziert unter [cc by-sa 3.0](https://creativecommons.org/licenses/by-sa/3.0/) 
mit Namensnennung.









![media-DbVAwR](../../media/media-DbVAwR.png)

# Originaltext
Bessere Übersetzung vorschlagen