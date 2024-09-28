# ☀️ solana-docker-dev

![docker](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)
![Solana](https://img.shields.io/badge/Solana-9945FF?style=for-the-badge&logo=solana&logoColor=fff)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

- 🐙by: [@byNestorCode](https://github.com/byNestorCode) ***#elSoftwareNoConoceFronteras***
- 📷 Instagram: [@rocketmx_](https://www.instagram.com/rocketmx_/)

***Este 🐙 repo es para ayudar a los devs en su entorno de desarollo en 🪟 windows***

***Este repo está inspirado en:***
- 🐙 Checa este repo si quieres aprender Solana y desarrollar en Web3 ➡️ [Click aqui](https://github.com/buildspace/buildspace-projects/blob/main/Solana_And_Web3/es/Section_0/Lesson_1_What_Are_We_Building.md)
    - Es un proyecto muy increible de Buildspace [ve a darles una 🌟](https://github.com/buildspace/buildspace-projects)
    - 📐 [@buildspace](https://github.com/buildspace/) gracias desde México 🌎

- 🌐 También hay una solución más sencilla, checa esto ➡️ [replit](https://replit.com/@adilanchian/gif-portal-starter-project?v=1#src/App.jsx), pero vamos, date oportunidad de intentar este pequeño tutorial.

# 🤠🚀 Bienvenidx

¿Has tenido problemas con tu CMD o Powershell, incluso de tu WSL al momento de crear tu entorno de desarrollo para Solana? Así como tú traje muchos dolores de cabeza, y la solución parece sencilla, cambiarnos totalmente a Linux, y la verdad amo a Linux y todo esto grandioso que hemos creado como comunidad, el Open Source y Open Harware, pero el orgullo no me dejaba dormir, no quería cambiarme de OS, así que como siempre recurrí a mi mejor amigo, 🐋 docker.

Recuerda una cosa importante, este solo es un repositorio, de tí depende generar lo más importante, la curiosidad 🧠. Ella te permitirá adenrarte en todos los conocimientos teóricos y prácticos para formarnos como súper Devs. 🖥️

¿Listx para comenzar?

# 📊 ¿Qué necesitamos para empezar?

1. Clonar este repositorio

2. Tener docker instalado en nuestra máquina (de preferencia la mas reciente versión):
    - 🐋 Da click aquí ➡️ [Docker Desktop](https://www.docker.com/products/docker-desktop/)
    - 🚢 Aquí esta la documentació paso a paso para instalarla, te pedirá WSL ➡️ [Documentación](https://docs.docker.com/desktop/install/windows-install/#install-docker-desktop-on-windows)

3. De preferencia utilizar ♾️ vscode para trabajar nuestro código:
    - ♾️ Da click aquí ➡️ [Visual Studio Code](https://code.visualstudio.com/download)


# 🛑 Alto aquí

Se que tienes muchas ganas de comenzar, pero vamos a configurar nuestro proyecto antes.
Para este punto de la historia te recomiendo hacer lo siguiente desde tú `vscode` 

1. Dentro de nuestra carpeta `Docker` debemos de crear un archivo .env
    - Dentro de este archivo vamos a colocar nuestra variable de entorno, esta variable es nuestra password para conectarnos por SSH a nuestro contenedor
        - ROOT_PASSWORD=
        - Ahí arriba ⬆️ coloca despues del signo `=` lo que quieras sin espacios

2.  Crearemos una carpeta con el nombre de `solana-dev`
    - Esta carpeta es súper necesaria, aquí se mapea el volumen de nuestro contenedor y nuesta maquina local

3. Crearemos un archivo en el directorio raíz de nuestro repo llamado `key.json`
    - Este archivo es muy importante, creeme, en las pruebas tuve muchos errores al momento de buscar mi public key de Solana.
    - Recuerda que este archivo es confidencial 🤫🚓

# 🐋 Sobre el contenido de Docker 

Te invito a darle una revisada al contenido de los ficheros `Dockerfile` y `docker-compose.yaml`. No es necesario que ahorita te conviertas en master de Docker, para eso hice este repo, para darte una herramienta y comiences lo antes posible.

Sin embargo quiero que tengas en cuenta algo dentro de `docker-compose.yaml`:
```yaml
        ports:
            - "2222:22"  # Mapea el puerto SSH
            - "8899:8899" # RPC URL
            - "8900:8900" # WebSocket URL
```

- Estos puertos nos ayudarán a acceder a nuestro contenedor por SSH o poder ver lo que desarollemos localmente con nuestro navegador preferido. 

# 📬 Ahora sí, vamos a continuar
Una vez hechos los pasos anteriores, vamos a utilizar Powershell o CMD, el que te guste más y vamos a hacer lo siguiente:

1. Vamos a dirigirnos a nuestro directorio, busca la ruta donde clonaste el repositorio, en mi caso me encuentro en la siguiente ruta:
    -   ```bash
        cd /Documents/Github/Docker
        ```
2. Desde aquí mismo de la terminal, vamos a ejecutar nuestro archivo docker-compose.yaml
    -  ```bash
        docker-compose up -d --build
        ```
        - ⌛ En este punto te pido un poco de paciencia, estará realizando las intalaciones necesarias, puede tardar un ratito.
        - ✅ Sí todo sale bien, solamente verás un mensaje de confirmación en tu consola.
        - ✖️ De lo contrario hazmelo saber, allá arriba te dejé mi contacto de IG o genera un nuevo issue.

3. ¿Recuerdas que creamos un directorio llamado `solana-dev` ahí dentro es donde más adelante encontrarás tus proyectos para trabajarlos. Para acceder realiza algo similar al paso número uno:
    -   ```bash
        cd /ruta_al_proyecto/solana-dev
        ```

# 🚀 ¿Cómo creo mi proyecto?
¿Recuerdas que anteriormente te hablé de los puertos de Docker? Bueno, es momento de utilizarlos

1. Accederemos a nuestro contenedor por SSH ¿Cómo hacemos esto? Para esto puedes abrir otra ventana de Powershell o de CMD, o en la misma, no pasa nada y después colocar el siguiete comando tal como está ahí:
    -   ```powershell
        ssh root@localhost -p 2222
        ```

2. A continuación te hará una pregunta que si quieres guardar el fingerprint, por favor respondé que sí:
    -   ```powershell
        yes
        ```
Lo anterior solo te lo pedirá la primera vez, así que la siguiente que quieras conectarte solo te pedira la contraseña, hablando de ¿Cúal contraseña? Bueno, vamos a continuar

3. La contraseña es la que configuramos dentro de nuestro archivo .env ¿Recuerdas? está dentro de la carpeta de Docker y su contenido es el siguiente:
    - `ROOT_PASSWORD=`
    - Ahí arriba ⬆️ coloca despues del signo `=` estará tu password, solo copia y pega en tu consola

Listo, tendremos acceso a nuestro 🐋 contenedor de Docker desde nuestra consola

4. Ahora nos dirigiremos a la ruta donde crearemos nuestro proyecto
-   ```bash
    cd /home/root/solana-dev/
    ```

⚠️ NOTA: recuerda que cualquier cosa que coloques aquí mágicamente aparecerá en tu carpeta solana-dev dentro del repositorio

También usaremos el módulo npm de Anchor y Solana Web3 JS; ¡ambos nos ayudarán a conectar nuestra aplicación web a nuestro programa Solana!

5. Ejecutaremos el siguiente comando:
-   ```bash
    npm install @project-serum/anchor @solana/web3.js
    ```

6. Lo siguiente que vamos a hacer es generar una cartera digital Solana local para trabajar. No te preocupes por crear una frase de contraseña (passphrase) por ahora, simplemente da click a "enter" cuando te pregunte.
-   ```bash
    solana-keygen new --outfile /root/.config/solana/id.json --force
    ```

Éste comando lo que hará es crear un keypair Solana local, que es algo así como nuestra cartera local que es lo que vamos a usar para comunicarnos con nuestros programas a través de la línea de comando.

Te invito a revisar tu archivo llamado `key.json`, ahí encontrarás el keipair.

7. Ahora ya solo nos queda crear nuestro proyecto:
-   ```bash
    anchor init nombre_del_proyecto
    ```

8. Accedemos al proyecto una vez generado:
-   ```bash
    cd nombre_del_proyecto
    ```

9. En este punto, yo tuve que hacer una modificación dentro del archivo `Anchor.toml` que se encuentra dentro de nuestro proyecto:
-   ```bash
    wallet = '/root/.config/solana/id.json'
    ```
Esto lo hice porque me daba problemas al encontrar mi keypair, así que solo puse la ruta absoluta

Y ahora se viene lo chido mis Devs:

10. Vamos a ejecutarlo, para ello ejecutaremos el siguiente comando:
-   ```bash
    anchor test
    ```

⌛ ¡Este comando puede tomar un tiempo la primera vez que lo ejecutas! Siempre y cuando obtengas las palabras verdes en la parte inferior que te confirmen que todo esta correcto

Ahora te invito a volver a ♾️ `vscode`, y observa, mágicamente el proyecto también estará en local. Cada que modifiques algo se clonará en ambos lugares.

Ahora sí, a darle ¡Éxito Devs! 🚀

# ⚠️ Como recomendación personal
Para trabajar mejor mis proyectos de solana en web3, descargué aún así todo lo anterior para 🪟 windows, esto para trabajar más cómodo en mi ♾️ `vscode`, si quieres hacerlo tambíen, te invito a ver el siguiente tutorial, no te llevará mucho timempo hacerlo y será una mejor experiencia.

- Es el repo de Buildspace que te mecioné desde el inicio: 🐙[Click aqui](https://github.com/buildspace/buildspace-projects/blob/main/Solana_And_Web3/es/Section_2/Lesson_1_Get_Local_Solana_Env_Running.md)
