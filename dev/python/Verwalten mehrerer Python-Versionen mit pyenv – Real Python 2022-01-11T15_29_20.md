Verwalten mehrerer Python-Versionen mit pyenv – Real Python
========================================



<https://realpython.com/intro-to-pyenv/>

global
Der globalBefehl legt die globale Python-Version fest. Dies kann mit anderen Befehlen überschrieben werden, ist jedoch nützlich, um sicherzustellen, dass Sie standardmäßig eine bestimmte Python-Version verwenden. Wenn Sie dies 3.6.8standardmäßig verwenden möchten, können Sie Folgendes ausführen:

$ pyenv global 3.6.8
Dieser Befehl setzt die ~/.pyenv/versionauf 3.6.8. Weitere Informationen finden Sie im Abschnitt zum Angeben Ihrer Python-Version .

local
Der localBefehl wird häufig verwendet, um eine anwendungsspezifische Python-Version festzulegen. Sie können es verwenden, um die Version auf 2.7.15Folgendes einzustellen :

$ pyenv local 2.7.15