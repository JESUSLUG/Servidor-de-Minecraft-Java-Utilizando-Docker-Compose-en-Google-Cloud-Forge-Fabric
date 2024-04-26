# Servidor de Minecraft-Forge utilizando-Docker Compose en Google Cloud - Para Forge, Fabric o Vanilla. 
Despliegue de un Servidor de Minecraft Modificado con Forge, Fabric o Vanilla utilizando Docker-Compose en Google Cloud (En este caso, BetterMC Forge: BMC3)

Actualizamos el sistema desplegado.

```
sudo apt-get update
```

Luego instalamos docker

```
sudo apt-get install docker.io --yes
```

Nos podemos como usario root

```
sudo su
```
e instalamos docker-compose

```
curl -L https://github.com/docker/compose/releases/download/1.28.5/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

Verificamos que todo esté instalado. Si Docker y Docker-compose están instalados, al ejecutar los siguientes comandos, obtendremos un listado de comandos disponibles.

```
docker 
```

```
docker-compose
```
