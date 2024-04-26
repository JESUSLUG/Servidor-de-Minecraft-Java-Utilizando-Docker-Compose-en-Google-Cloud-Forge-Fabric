# Servidor de Minecraft utilizando Docker Compose en Google Cloud - Para Forge, Fabric o Vanilla. 
Despliegue de un Servidor de Minecraft Modificado con Forge, Fabric utilizando Docker-Compose en Google Cloud (En este caso, BetterMC Forge: BMC3)

![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/872bd56d-8f71-4d93-905e-5c740a717b1a)


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
![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/49e7738b-108d-45e7-9860-a35c33723f86)

Al hacer click, tenemos varias opciones, pero por defecto debería abrirnos otra pestaña del navegador para acceder a la terminal de la VM.

---

### Dentro De La VM

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
### Montar el Docker Compose

Ahora, gracias al archivo de docker-compose que está en este repositorio, con darle un docker-compose up -d, ya tendrías básicamente el servidor montado, siendo BetterMC Forge: BMC3 en su versión 1.19.2. Así que explicaremos eso y luego nos iremos a los detalles.

Primero copiamos este repo, en la terminal de la vm con (esto para tener el docker-compose) 

```
git clone https://github.com/JESUSLUG/Servidor-de-Minecraft-Utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric.git
```
Usaremos la API de Curseforge, esto se debe a que el contenedor accederá a esta API para descargar los mods de esta página.
Accedemos a https://console.curseforge.com/?#/  Nos vamos a API KEY y copiamos.

![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/dc7dc027-b28e-42b6-b3fa-a9709e29e5c6)

Ya copiado, toca crear un archivo .env

```
nano .env
```

y pegamos CF_API_KEY=**TUAPIDECURSEFORGE**

Pulsamos Ctrl + X y luego Yes para guardar. Para confirmar si se guardó, volvemos a abrir el archivo con nano .env y lo que hemos escrito debería estar allí.


Ahora si. Levantamos el contenedor

```
docker-compose up -d
```

Esperamos... y escribimos lo siguiente para ver si está en nuestro listado de contenedores.

```
docker ps
```

Si todo está bien, debería salir algo así.

![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Forge-utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/e3a650f1-5b74-4481-bfc7-926cb3096852)

Ahora, como lo levantamos, este aún no estará listo. Pues está descargando los mods y toca la cosa. Así que para ver cómo va, copiamos el numero de CONTAINER ID y escribimos..

```
docker logs -f <nombre_del_contenedor_o_ID_del_contenedor> 
```

En esto, veremos qué está haciendo el contenedor, qué está descargando y cómo va. Este proceso tardará unos 5 a 10 minutos.

Cuando esto termine, podremos acceder dentro del contenedor para modificar ciertas cosas. Esto ya depende de lo que quieras modificar.

```
docker exec -it <nombre_del_contenedor_o_ID_del_contenedor> /bin/bash
```

Dentro de este esta los archivos del mundo, ajustes del servidor del juego, etc. 

![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/0edc40d1-7fbb-4d78-be6e-499c6b575c9a)


Ahora, solo entra a tu minecraft y accede con la IP, esta ip se encuentra en la plataforma de Google Cloud- Instancias VM. **IP EXTERNA**

![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/ccaa11c9-c941-4b78-b5e7-6c7689395cdc)

---

### Modificar docker-compose para Forge o Fabric.

Ahora, hay varios detalles a destacar de la estructura de nuestro docker-compose, primero lo abriremos con:

```
nano docker-compose.yml 
```

Éste contiene lo siguiente:
![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/c9c0e9e1-8425-4a8f-86b4-7cf4634a37d5)

Este nos sirve para declarar la versión deseada del juego, **VERSION: "1.19.2"**. Esto puede ser ignorado, ya que el Forge o Fabric que se descargue y la lógica de la imagen suelen saber qué versión se necesita. Sin embargo, lo agregué para evitar cualquier tipo de error. La versión del juego depende del Forge que vayas a usar.

Este, es lo que nos ayudo a llamar el .env para llamar la API de CuseForge **CF_API_KEY: ${CF_API_KEY}**.

Este nos sirve para declarar el nombre del paquete de mods que usarás **CF_SLUG: better-mc-forge-bmc3**, siendo el caso de Better Minecraft Forge BMC3.

El **CF_FILENAME_MATCHER: v20** nos sirve como versión del Matcher. Si usamos otra que no sea del pack que estés descargando, te dará error...

Y el **FORGE_VERSION: "43.3.5"**, nos sirve para declarar la versión que se descargará... el **TYPE: FORGE** depende de si es Forge o Fabric...

Toda esta información la sacarás del Forge o Fabric que vayas a usar, siempre y cuando esté descargado de **Curse Forge**.

Ejemplo, si queremos usar este:

![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/92d701ed-e686-4e9d-be93-70621338dcc9)


Tendremos que identificar ciertos apartados. El primero es la URL: https://www.curseforge.com/minecraft/modpacks/better-mc-forge-bmc3/files/4889399
Para poder llenar **CF_SLUG:** con lo que queremos descargar, tenemos que identificar en la URL algo como esto: **better-mc-forge-bmc3**
Siendo que en la URL, está aquí: https://www.curseforge.com/minecraft/modpacks/**better-mc-forge-bmc3**/files/4889399


Y la Version del juego, se identifica con el zip que hay para descargar, siendo **VERSION: "1.19.2"**, Better_MC_[FORGE]_**1.19.2**_v20.zip
Luego está el **CF_FILENAME_MATCHER: v20**. Como muestra la imagen, la versión se identifica al final del zip. Siendo en este caso, Better_MC_[FORGE]_1.19.2_**v20**.zip

![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/225c2d42-e206-470d-b436-03735f993729)

Ahora, para finalizar estos detalles, toca ver la versión del Forge. **FORGE_VERSION: "43.3.5"**, este se encuentra en la parte de abajo:
Recuerda que el **TYPE: FORGE** depende de si es Forge o Fabric. 

![image](https://github.com/JESUSLUG/Servidor-de-Minecraft-Utilizando-Docker-Compose-en-Google-Cloud-Forge-Fabric-Vanilla/assets/116361712/729b990f-e03b-47aa-97cb-e623e12fdcf6)


### ERRORES AL MONTAR 

Bien, para finalizar este repositorio, es importante explicar que algunos paquetes de mods tienden a modificar estos mods al descargarlos. El contenedor puede creer que necesita otras dependencias de mods que ya no están en el pack, lo que hace que falle al instalar y no se pueda montar correctamente.

Por ejemplo, el error al inicio de intentar montar este servidor era el siguiente:

```
Mod ID: 'spruceui', Requested by: 'ryoamiclights', Expected range: '*', Actual version: '[MISSING]'
Mod ID: 'jeresources', Requested by: 'jerintegration', Expected range: '[0.14.1.160,)', Actual version: '[MISSING]'
```

Lo que tenemos que hacer es decirle al contenedor que no queremos estos mods. Claro, para identificar qué mods son los que causan el error, tendremos que ejecutar el contenedor, revisar los logs y apuntar los nombres de esos mods. Luego, iremos al contenedor y en **CF_EXCLUDE_MODS** pondremos dichos mods que causan el problema.

```
      CF_EXCLUDE_MODS: |
        ryoamiclights
        jer-integration
      CF_FORCE_SYNCHRONIZE: "true"
```

Y para resolver el problema sin tener que detener y matar el contenedor, usamos **CF_FORCE_SYNCHRONIZE: "true"** para garantizar que se limpien las modificaciones excluidas.

DATOS

CUANDO HAGAS CAMBIOS EN EL COMPOSE, VUELVE A CORRERLO CON

```
docker-compose up -d
```

DOCKER SE EJECUTA DESDE SUPER USARIO, SI VUELVES A HACER CAMBIOS TIENES QUE ENTRAR COMO USARIO ROOT O SIEMPRE PONER **sudo docker ...** 


---
