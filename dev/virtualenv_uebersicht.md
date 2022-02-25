Verwalten mehrerer Python-Versionen mit pyenv – Real Python 2022-01-11T15.36.51
========================================



<https://realpython.com/intro-to-pyenv/>

Virtuelle Umgebungen erstellen
Das Erstellen einer virtuellen Umgebung ist ein einzelner Befehl:

$ pyenv virtualenv <python_version> <environment_name>
Technisch gesehen ist das <python_version>optional, aber Sie sollten erwägen, es immer anzugeben, damit Sie sicher sind, welche Python-Version Sie verwenden.

Das <environment_name>ist nur ein Name für Sie, um Ihre Umgebungen getrennt zu halten. Es empfiehlt sich, Ihre Umgebungen mit dem gleichen Namen wie Ihr Projekt zu benennen. Wenn Sie beispielsweise myprojectan Python 3.6.8 arbeiten und dagegen entwickeln möchten, führen Sie Folgendes aus:

$ pyenv virtualenv 3.6.8 myproject
Die Ausgabe enthält Nachrichten , die ein paar zusätzlichen zeigen Python - Pakete installiert zu werden , und zwar wheel, pipund setuptools. Dies dient ausschließlich der Bequemlichkeit und richtet lediglich eine Umgebung mit umfassenderen Funktionen für jede Ihrer virtuellen Umgebungen ein.

Aktivieren Ihrer Versionen
Nachdem Sie nun Ihre virtuelle Umgebung erstellt haben, ist deren Verwendung der nächste Schritt. Normalerweise sollten Sie Ihre Umgebungen aktivieren, indem Sie Folgendes ausführen:

$ pyenv local myproject
Sie haben den pyenv localBefehl schon einmal gesehen , aber diesmal geben Sie eine Umgebung an, anstatt eine Python-Version anzugeben. Dadurch wird eine .python-versionDatei in Ihrem aktuellen Arbeitsverzeichnis erstellt und da Sie eval "$(pyenv virtualenv-init -)"in Ihrer Umgebung ausgeführt wurden, wird die Umgebung automatisch aktiviert.

Sie können dies überprüfen, indem Sie Folgendes ausführen:

$ pyenv which python
/home/realpython/.pyenv/versions/myproject/bin/python
Sie können sehen, dass eine neue Version erstellt wurde myprojectund die pythonausführbare Datei auf diese Version verweist. Wenn Sie sich eine ausführbare Datei ansehen, die diese Umgebung bereitstellt, werden Sie dasselbe sehen. Nehmen Sie zum Beispiel pip:

$ pyenv which pip
/home/realpython/.pyenv/versions/myproject/bin/pip
Wenn Sie die eval "$(pyenv virtualenv-init -)"Ausführung in Ihrer Shell nicht konfiguriert haben , können Sie Ihre Python-Versionen damit manuell aktivieren/deaktivieren:

$ pyenv activate <environment_name>
$ pyenv deactivate