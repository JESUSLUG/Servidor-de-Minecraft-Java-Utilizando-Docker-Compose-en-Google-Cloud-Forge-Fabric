# Servidor de Minecraft-Forge utilizando-Docker Compose en Google Cloud - Para Forge, Fabric o Vanilla. 
Despliegue de un Servidor de Minecraft Modificado con Forge, Fabric o Vanilla utilizando Docker-Compose en Google Cloud (En este caso, BetterMC Forge: BMC3)

---

### Uso de la imagen de Docker de itzg para Minecraft

En este repo, utilizamos la imagen de Docker proporcionada por itzg, la cual es muy completa y facilita el despliegue de un servidor de Minecraft vanilla o con mods. itzg explica de manera clara cómo montar un servidor de Minecraft vanilla utilizando esta imagen en su propio repositorio y en su sitio web.

Sin embargo, es importante señalar que aunque la documentación es detallada, pueden perderse algunos detalles, especialmente cuando se trata de montar un servidor con mods, forge o fabric. Aunque esta funcionalidad está explicada, puede ser un poco confusa para aquellos que son nuevos en estas tecnologías.

Dicho esto, todo el crédito por la imagen de Docker debe ir a itzg. Puedes encontrar más información sobre la imagen y su funcionamiento en el repositorio oficial:
[Perfil de Github de itzg](https://github.com/itzg)
[Repo de itzg](https://github.com/itzg/docker-minecraft-server)
[Documentación](https://docker-minecraft-server.readthedocs.io/en/latest/)

Dicho esto, en este repositorio busca explicar desde cómo montar el servidor en el servicio de Google Cloud hasta las configuraciones del docker-compose para instalar el paquete de mods de tu elección. Esa clase de cosas que no las encuentras en un mismo repositorio :) 

--- 


---

Actualizamos el sistema desplegado.

```
sudo apt-get update
```

Luego instalamos docker.

```
sudo apt-get install docker.io --yes
```

Nos ponemos como usuario root.

```
sudo su
```
e instalamos docker-compose.

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

---
