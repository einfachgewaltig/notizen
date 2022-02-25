Portainer install 
========================

docker volume create portainer_data


docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer



docker run -d -p 8080:8080 --name=freqtrade_3503fdb4--restart=always -v /var/run/docker.sock:/var/run/docker.sock -v reqtrade_3503fdb4:/data hoanghnbk/freqtrade_3503fdb4
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce

docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
 freqtradeorg/freqtrade
