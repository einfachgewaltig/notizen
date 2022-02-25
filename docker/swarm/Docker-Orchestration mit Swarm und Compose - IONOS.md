Docker-Orchestration mit Swarm und Compose - IONOS
========================================



<https://www.ionos.de/digitalguide/server/knowhow/docker-orchestration-mit-swarm-und-compose/>

## Die Bereitstellung von Multi-Container-Apps im Cluster erfolgt in fünf Schritten:

Lokale Docker-Registry erstellen
Multi-Container-App als Stack definieren
Multi-Container-App mit Compose testen
Image in die Registry laden
Stack im Cluster ausführen

<https://www.ionos.de/digitalguide/server/knowhow/docker-orchestration-mit-swarm-und-compose/>

### 1.1 Registry als Service im Cluster starten: Nutzen Sie den Befehl docker service create nach folgendem Schema, um einen lokalen Registry-Server als Service im Cluster zu starten.

docker service create --name registry --publish 5000:5000 registry:2
Der Befehl weist Docker an einen Service mit dem Namen registry zu starten, der an Port 5000lauscht. Der erste Wert hinter dem Flag --publish gibt den Host-Port an, der zweite den Port des Containers. Dem Service liegt das Image registry:2 zugrunde, das eine Implementierung der Docker Registry HTTP API V2 enthält und frei über das Docker-Hub bezogen werden kann.