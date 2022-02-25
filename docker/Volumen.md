Volumen
========================

## Volumes erstellen und verwalten 

Im Gegensatz zu einem Bind-Mount können Sie Volumes außerhalb des Geltungsbereichs eines Containers erstellen und verwalten.

### Erstellen Sie ein Volume :
 docker volume create my-vol


### Auflisten von Bänden :
 docker volume ls
  
  
### Überprüfen Sie ein Volume :
docker volume inspect my-vol

###Entfernen Sie ein Volume :
docker volume rm my-vol