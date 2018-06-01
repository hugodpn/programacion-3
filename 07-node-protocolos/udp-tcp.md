# UDP

El protocolo de datagramas de usuario (en inglés: User Datagram Protocol o UDP) es un protocolo del nivel de transporte basado en el intercambio de datagramas. Permite el envío de datagramas a través de la red sin que se haya establecido previamente una conexión, ya que el propio datagrama incorpora suficiente información de direccionamiento en su cabecera. Tampoco tiene confirmación ni control de flujo, por lo que los paquetes pueden adelantarse unos a otros; y tampoco se sabe si ha llegado correctamente, ya que no hay confirmación de entrega o recepción. Su uso principal es para protocolos como DHCP, BOOTP, DNS y demás protocolos en los que el intercambio de paquetes de la conexión/desconexión son mayores, o no son rentables con respecto a la información transmitida, así como para la transmisión de audio y vídeo en real, donde no es posible realizar retransmisiones por los estrictos requisitos de retardo que se tiene en estos casos.


## Las características principales de este protocolo son:

1. Trabaja sin conexión, es decir que no emplea ninguna sincronización entre el origen y el destino.

2. Trabaja con paquetes o datagramas enteros, no con bytes individuales como TCP. Una aplicación que emplea el protocolo UDP intercambia información en forma de bloques de bytes, de forma que por cada bloque de bytes enviado de la capa de aplicación a la capa de transporte, se envía un paquete UDP.

3. No es fiable. No emplea control del flujo ni ordena los paquetes.

4. Su gran ventaja es que provoca poca carga adicional en la red ya que es sencillo y emplea cabeceras muy simples.

## Ejemplo Servidor

Creamos una carpeta en la que almacenaremos nuestro programa, luego creamos el archivo para el servidor `servidorUDP.js`

```javascript

const dgram = require('dgram');

const server = dgram.createSocket('udp4');

server.on('error', (err) => {
  console.log(`Error en el servidor:\n${err.stack}`);
  server.close();
});

server.on('message', (msg, rinfo) => {
  console.log(`Recibiendo: ${msg} desde ${rinfo.address}:${rinfo.port}`);
});

server.on('listening', () => {
  const address = server.address();
  console.log(`El servidor está escuchando en ${address.address}:${address.port}`);
});

server.bind(41234);

```
> node servidorUDP.js

## Ejemplo Cliente

En la misma carpeta que creamos el programa servidor, creamos un archivo `clienteUDP.js`

```javascript

const dgram = require('dgram');

const message = Buffer.from('Mensaje de prueba... Yo soy USUARIO!');
const client = dgram.createSocket('udp4');

client.send(message, 41234, 'localhost', (err) => {
  client.close();
});

```
> node clienteUDP.js

## Fuentes

> https://es.wikipedia.org/wiki/Protocolo_de_datagramas_de_usuario

> https://nodejs.org/api/dgram.html

> https://www.hacksparrow.com/node-js-udp-server-and-client-example.html


# TCP

Protocolo de control de transmisión (Transmission Control Protocol o TCP), es uno de los protocolos fundamentales en Internet. Muchos programas dentro de una red de datos compuesta por redes de computadoras, pueden usar TCP para crear “conexiones” entre sí a través de las cuales puede enviarse un flujo de datos. El protocolo garantiza que los datos serán entregados en su destino sin errores y en el mismo orden en que se transmitieron. También proporciona un mecanismo para distinguir distintas aplicaciones dentro de una misma máquina, a través del concepto de puerto.

TCP da soporte a muchas de las aplicaciones más populares de Internet (navegadores, intercambio de ficheros, clientes FTP, etc.) y protocolos de aplicación HTTP, SMTP, SSH y FTP.

## Características

* Permite colocar los segmentos nuevamente en orden cuando vienen del protocolo IP.
* Permite el monitoreo del flujo de los datos y así evita la saturación de la red.
* Permite que los datos se formen en segmentos de longitud variada para "entregarlos" al protocolo IP.
* Permite multiplexar los datos, es decir, que la información que viene de diferentes fuentes (por ejemplo, aplicaciones) en la misma línea pueda circular simultáneamente.
* Por último, permite comenzar y finalizar la comunicación amablemente.

## UDP vs TCP

**UDP:** proporciona un nivel de transporte no fiable de datagramas, ya que apenas añade la información necesaria para la comunicación extremo a extremo al paquete que envía al nivel inferior. Lo utilizan aplicaciones como NFS (Network File System) y RCP (comando para copiar ficheros entre computadores remotos), pero sobre todo se emplea en tareas de control y en la transmisión de audio y vídeo a través de una red. No introduce retardos para establecer una conexión, no mantiene estado de conexión alguno y no realiza seguimiento de estos parámetros. Así, un servidor dedicado a una aplicación particular puede soportar más clientes activos cuando la aplicación corre sobre UDP en lugar de sobre TCP.

**TCP:** es el protocolo que proporciona un transporte fiable de flujo de bits entre aplicaciones. Está pensado para poder enviar grandes cantidades de información de forma fiable, liberando al programador de la dificultad de gestionar la fiabilidad de la conexión (retransmisiones, pérdida de paquetes, orden en el que llegan los paquetes, duplicados de paquetes...) que gestiona el propio protocolo. Pero la complejidad de la gestión de la fiabilidad tiene un coste en eficiencia, ya que para llevar a cabo las gestiones anteriores se tiene que añadir bastante información a los paquetes a enviar. Debido a que los paquetes para enviar tienen un tamaño máximo, cuanta más información añada el protocolo para su gestión, menos información que proviene de la aplicación podrá contener ese paquete (el segmento TCP tiene una sobrecarga de 20 bytes en cada segmento, mientras que UDP solo añade 8 bytes). Por eso, cuando es más importante la velocidad que la fiabilidad, se utiliza UDP. En cambio, “TCP asegura la recepción en destino de la información para transmitir”.

## Ejemplo de servidor TCP

Creamos una carpeta en la que almacenaremos nuestro programa TCP, luego creamos el archivo para el servidor `servidor.js`

```javascript

const PORT = '5050';

// obtenomos la librería de red
const net = require('net');

// creamos un servidor
const server = net.createServer((c) => {
  // 'connection' listener -> conexion escuchando
  console.log('cliente conectado');

  let clientName = `${c.remoteAddress}:${c.remotePort}`;
  
  // si hay error lo loguea
  c.on('end', () => {
    console.log('Cliente desconectado');
  });

  c.on('data', (data) => { 
    let m = data.toString().replace(/[\n\r]*$/, '');

    console.log(`${clientName} nos dice: \n\n${m}`);

    // le escribimos una respuesta al cliente
    c.write(`Usted envio (${m}). Muchas Gracias!\n`);
  });

  // escribe una respuesta a la conexíon
  // c.write(`Hola te hablo a las ${new Date()} \r\n`);
  c.pipe(c);
});

server.on('error', (err) => {
  throw err;
});

server.listen(PORT, () => {
  console.log(`Servidor escuchando en localhost:${PORT}`);
});

```
> node servidorTCP.js

## Ejemplo cliente TCP

En la misma carpeta que creamos el programa TCP servidor, creamos un archivo `cliente.js`

```javascript

const PORT = 5050;

// obtenomos la librería de red
const net = require('net');

// creamos una conexión a un puerto específico
const client = net.createConnection({ port: PORT }, () => {
  // 'connect' listener -> conexion escuchando
  console.log('conectándose al servidor!');
  client.write('USUARIO!\r\n'); 
});

// evento cuando se recibe data del servidor
client.on('data', (data) => {

  console.log("> Data recibida");
  console.log(data.toString());
  client.end();
});

// evento cuando se desconecta del servidor
client.on('end', () => {
  console.log('Desconectando del servidor');
});


```

> node clienteTCP.js

# Fuentes

> https://es.wikipedia.org/wiki/Protocolo_de_control_de_transmisi%C3%B3n

