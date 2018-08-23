# Instrucciones de instalación y configuración

1. Bajamos el repositorio de Github parados en el directorio donde vamos a trabajar `~/documentos/`

```bash
> git clone git@github.com:CESIT-2018/crud-app-programacion3.git
```

2. El paso 1 nos creo una carpeta llamada crud-app-programacion3 en nuestor directorio, ingresamos a ella

```bash
> cd crud-app-programacion3
```

3. Instalamos las dependencias para el servidor, para ello ejecutamos el siguiente comando parados en `~/documentos/crud-app-programacion3`

```bash
> npm install
```

4. Nos movemos a la carpeta del cliente e instalamos las dependencias

```bash
> cd client
> npm install
```

5. Volvemos al directorio `~/documentos/crud-app-programacion3` y ejecutamos la aplicación. Una vez ejecutada la aplicación nos queda el servidor en el puerto 5000 (ver configuración) y el cliente en el puerto 3000.

```bash
> cd ~/documentos/crud-app-programacion3
> npm run dev
```

6. De no funcionar el paso 5 que ejecuta el cliente y el servidor en forma concurrente, lo que haremos es levantaros por separado. Para ello abrimos dos consolas y ejecutamos los siguientos comandos

```bash
> # en la cosnola 1
> cd ~/documentos/crud-app-programacion3
> npm run start
```

```bash
> # en la cosnola 2
> cd ~/documentos/crud-app-programacion3/client
> npm run start
```


> Cuando actualicemos nuestro código debemos verificar que las dependencias siguen actualizadas. El siguiente es un ejemplo de como actualizar el código e verificar las dependencias.

```bash
> cd ~/documentos/crud-app-programacion3
> git pull
> npm install # actualizamos dependencias para el servidor
> cd client
> npm install # actualizamos dependencias para el cliente
```

> en el siguiente link encontramos un ejemplo similar al nuestro
https://github.com/sitepoint-editors/redux-crud-example