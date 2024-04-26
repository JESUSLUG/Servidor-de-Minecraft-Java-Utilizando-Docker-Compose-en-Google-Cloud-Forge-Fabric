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

![Forma 2](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/e6ae4105-aab8-4828-86e7-15006614efec)


Tendremos que activar esta API "Compute Engine API", para crear y ejecutar máquinas virtuales en Google Cloud Platform.
![Captura desde 2024-04-26 09-03-44](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/2f30960c-d10c-4a9b-92cd-dc3f910fcaf8)


Ahora, creamos la instancia. Le damos click en **CREAR INSTANCIA**
Ponemos el nombre que gustemos y seleccionamos la regios y zona que mas nos convenga. 
Luego en configuracion de la maquina, elegimos una instancia EC2
![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/48a85f65-ee3b-4e16-a491-c9ac72c774c4)

Luego personalizamos el procedor y la ram, en este caso, usamos 4 nucleos y 8 gb de ram 
![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/6acc8fdf-2cd7-4e9f-bd3f-9f042976ef03)


Luego nos vamos a Disco de arranque y le damos en **CAMBIAR**, esto es importante para que la generacion de mundo sea rapido tanto para el sever, como para tus jugadores. 

![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/d22daa67-67ef-4668-8b5e-49d747d3cab4)

Nos mandará a esta interfaz, en la cual elegiremos el espacio de disco que consideremos. En este caso, lo dejé en 10 GB. Elige el sistema operativo Ubuntu, la versión 24.04 LTS y el tipo de disco de arranque "Disco persistente estándar".
![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/b05a127e-e816-493e-8bbd-25f71ed0a35c)

Luego bajamos más y nos vamos a Firewall y marcamos con un check Permitir tráfico HTTP y Permitir tráfico HTTPS. El balanceo de cargas nos podría servir si mostráramos más de un servidor en la misma instancia, pero en este caso pasaremos de ello. 
![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/0aadc63b-3594-412e-aa0b-f1f4d2ef5915)

Ahora nos vamos en opciones en avanzadas

![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/c61f293f-adfd-4395-afbb-2ba96ed83e39)

Herramientas de redes y ponemos una etiqueta de red que nos servirá más adelante.
![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/77d5d203-dbcd-486d-9bae-fb4e05aa7052)

Le damos en Crear. Esto tomará un poco de tiempo, ya que quede, debería verse algo así.
![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/56e409c0-4d55-44c6-a24c-9e94df698a96)

Ahora, nos vamos en configurar reglas de Firewall.
![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/fe704d9c-5be2-46ae-80d7-976f63487eb5)

Le pondremos un nombre significativo, para que no olvidemos para qué sirve.

![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/36faa605-5c67-4354-9c26-b3bb1748fd13)

Prioridad en 1000, etiqueta de destino, le ponemos la misma etiqueta que pusimos en "Herramientas de redes". (Sé que la de la captura de pantalla anterior es diferente a esta, así que calma).
Luego en Filtro de origen, seleccionamos rangos de de IPv4 y 
Rangos de IPv4 de origen 0.0.0.0/4, esto significa que cualquier dirección IP puede acceder al servidor de Minecraft. 
![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/d5ab7db1-ec4b-47f8-a917-bf24043fb476)

Y ahora, para que estas IPs accedan, es importante activar el protocolo TCP en el puerto 25565. Este puerto en particular se elige porque es el puerto predeterminado al montar el servidor (esto en las configuraciones del contenedor y el archivo server.properties ).

![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/f8e93e8c-0f0a-4ae1-9acb-ebe83b158109)

Una vez que hayas terminado de hacer los ajustes, simplemente guarda los cambios y espera un momento mientras se aplican.

Luego de que estas se apliquen, regresaremos al apartado de instancias VM. Y le daremos en SSH (Secure Shell) para conectarnos a la Maquina virtual.  
<img src="https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/49e7738b-108d-45e7-9860-a35c33723f86" alt="imagen" style="width: 200px; height: 150px;">

Al hacer clic, tenemos varias opciones, pero por defecto debería abrirnos otra pestaña del navegador para acceder a la terminal de la VM.

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
