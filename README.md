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

### Creando la instancia de Google Cloud.

En primer lugar, me gustaría mencionar que entre las opciones de servicios en la nube disponibles actualmente, casi todas ofrecen una prueba gratuita por un cierto período de tiempo o proporcionan créditos para utilizar su plataforma. En el caso de Google Cloud, ofrecen una prueba de $300 dólares, lo que equivale aproximadamente a 6300 pesos mexicanos. El costo mensual varía dependiendo de la instancia que utilices y de cuánto la emplees. Es importante destacar que la configuración de la instancia que se utiliza en Google Cloud tiende a ser similar en otros servicios de nube.

Con estos $300 dólares, podrías financiar aproximadamente 8 meses de servidor para el juego, más o menos. **Desde mi perspectiva**, considero que esta es una excelente oportunidad para comenzar a utilizar Google Cloud, Docker y Docker Compose y aprender algo nuevo en el proceso y ya más adelante usar esos créditos en otra cosa:). 
Sin embargo, cada persona tiene su propia perspectiva;).

Ahora que hemos explicado esto, continuemos.

Lo primero es crear una cuenta en Google.... acceder a Google Cloud y registrarte para obtener los créditos. Es necesario agregar una tarjeta de crédito, pero no se realizará ningún cargo; puedes eliminarla más adelante si lo deseas.

Si todo salió bien, estarás en una interfaz como esta:

![Captura1](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/06a2b027-eea7-4bfb-a788-1157893f8d02)

Ahora, crearemos un proyecto nuevo (ponle el nombre que gustes). 
![Captura desde 2024-04-26 09-02-11](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/b45f6bdf-eb9f-40e7-af69-ee6616135146)

Al terminar nos quedara una interfaz como esta: 
![Captura desde 2024-04-26 09-05-30](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/5439d6fd-b8b3-4d7a-b576-e2edeb608265)


Luego, nos dirigimos a Compute Engine y hacemos clic en Instancias de VM (Virtual Machine (Máquina Virtual en español))  .
![Forma 1](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/bb20458b-d187-4d13-adb6-0048c2eb5a89)

O puedes acceder a las instancias de VM desde la interfaz después de crear el proyecto.
![Forma 1](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/e6ae4105-aab8-4828-86e7-15006614efec)


Tendremos que activar esta API "Compute Engine API", para crear y ejecutar máquinas virtuales en Google Cloud Platform.
![Captura desde 2024-04-26 09-03-44](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/2f30960c-d10c-4a9b-92cd-dc3f910fcaf8)







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
