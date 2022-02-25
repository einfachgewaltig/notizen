# pyenv
source https://realpython.com/intro-to-pyenv/

## install 
curl https://pyenv.run | bash

>  pyenv install 3.6.8

------

### install pyenv (optinal ?!?!?!)

pyenv shell 3.6.8
> echo $PYENV_VERSION

## Creating Virtual Environments
Creating a virtual environment is a single command:

> $ pyenv virtualenv <python_version> <environment_name>
>> pyenv virtualenv 3.6.8 myproject

 pyenv local myproject
 
 ### Aktivieren Ihrer Versionen
Nachdem Sie nun Ihre virtuelle Umgebung erstellt haben, ist deren Verwendung der nächste Schritt. Normalerweise sollten Sie Ihre Umgebungen aktivieren, indem Sie Folgendes ausführen:

$ pyenv local myproject

>> $ pyenv which pip <br>
/home/realpython/.pyenv/versions/myproject/bin/pip

### Wenn Sie die eval "$(pyenv virtualenv-init -)"Ausführung in Ihrer Shell nicht konfiguriert haben , können Sie Ihre Python-Versionen damit manuell aktivieren/deaktivieren:

§ pyenv activate <environment_name>  <br>
§  pyenv deactivate

## Arbeiten mit mehreren Umgebungen
Wenn Sie alles, was Sie gelernt haben, zusammenfassen, können Sie effektiv mit mehreren Umgebungen arbeiten. Nehmen wir an, Sie haben die folgenden Versionen installiert:

$ pyenv versions
 <br>
* system (set by /home/realpython/.pyenv/version) <br>
  2.7.15 <<br>>
  3.6.8 <br>
  3.8-dev <br>
Jetzt möchten Sie an zwei verschiedenen, treffend benannten Projekten arbeiten:

project1 unterstützt Python 2.7 und 3.6. <br>
project2 unterstützt Python 3.6 und experimentiert mit 3.8-dev. <br>
Sie können sehen, dass Sie standardmäßig das System Python verwenden, was durch das *in der pyenv versionsAusgabe angezeigt wird . Erstellen Sie zunächst eine virtuelle Umgebung für das erste Projekt: <br>

$ cd project1/ <br>
$ pyenv which python <br>
/usr/bin/python <br>
$ pyenv virtualenv 3.6.8 project1 <br>
...
$ pyenv local project1
<br>
$ python -V 
<br>
/home/realpython/.pyenv/versions/project1/bin/python <br>


###############################
------
------

souce virtualenv 
========================

# create virtualenv in directory /freqtrade/.env
 

# run virtualenv
source .env/bin/activate

 pipenv shell

--------------
## virtualenv
pyvenv env
source env/bin/active

--------------
## venv / quelle ubuntu
python3-m venv /home/Benutzer/venv-test
### activieren

source /home/Benutzer/venv-test/bin/active 