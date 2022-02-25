Verwalten mehrerer Python-Versionen mit pyenv – Real Python
========================================



<https://realpython.com/intro-to-pyenv/>

Virtuelle Umgebungen erstellen
Das Erstellen einer virtuellen Umgebung ist ein einzelner Befehl:

$ pyenv virtualenv <python_version> <environment_name>
Technisch gesehen ist das <python_version>optional, aber Sie sollten erwägen, es immer anzugeben, damit Sie sicher sind, welche Python-Version Sie verwenden.

Das <environment_name>ist nur ein Name für Sie, um Ihre Umgebungen getrennt zu halten. Es empfiehlt sich, Ihre Umgebungen mit dem gleichen Namen wie Ihr Projekt zu benennen. Wenn Sie beispielsweise myprojectan Python 3.6.8 arbeiten und dagegen entwickeln möchten, führen Sie Folgendes aus:

$ pyenv virtualenv 3.6.8 myproject