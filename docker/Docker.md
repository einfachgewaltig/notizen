Docker 
======================== 
https://docker-curriculum.com/
# Docker Compose .yml

## docker build . -t

## docker-compose up -d
## docker exec -it
command line




# Docker STANDART
---------------------------------
## docker pull
--------------------------
 ## docker images
 ----------------------------------------------------
 ##  docker run
haben wir keinen Befehl bereitgestellt, also wurde der Container hochgefahren, ein leerer Befehl ausgeführt und dann beendet. Nun ja - irgendwie schade. Versuchen wir etwas Spannenderes.
##
### $ docker run busybox echo "hello from busybox"

hello from busybox

-------------------------------------------------------
 ## docker ps -a

STATUSS palte anzeigt, dass diese Container vor einigen Minuten beendet wurden.


## docker run -it ~~busybox~~ bash
/ # ls
bin   dev   etc   home  proc  root  sys   tmp   usr   var
/ # uptime
 05:45:21 up  5:58,  0 users,  load average: 0.00, 0.01, 0.04
Wenn Sie den runBefehl mit den -itFlags ausführen, werden wir an ein interaktives tty im Container angehängt. Jetzt können wir **so viele Befehle im Container ausführen, wie wir möchten**. Nehmen Sie sich etwas Zeit, um Ihre Lieblingsbefehle auszuführen.

## docker port static-site
80/tcp -> 0.0.0.0:32769
443/tcp -> 0.0.0.0:32768


##  docker run -p 8888:80 prakhar1989/static-site
Sie können auch einen benutzerdefinierten Port angeben, an den der Client Verbindungen zum Container weiterleitet.







docker volume *create portainer_data*

docker run -d -p 9000:9000 --name portainer --restart always 
-v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer