---
title: "Socket Python"
date: 2026-01-26
tags:
  - ciencias-computacion
  - lenguajes-programacion
  - python
---
Son la base de las comunicaciones, en el siguiente documento se redactará en que consite y como hacerlos
## Comprender los sockets


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/ELPSCRK/DICCIONARIOS|DICCIONARIOS]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]].

### ¿Qué es un socket?

Un socket es una interfaz (puerta) para la comunicación entre distintos procesos situados en la misma máquina o en máquinas diferentes. En este último caso, hablamos de sockets de red.

Los conectores de red eliminan la gestión de las conexiones. Puedes pensar en ellos como gestores de conexión. En los sistemas Unix, en particular, los sockets son simplemente archivos que admiten las mismas operaciones de escritura-lectura, pero que envían todos los datos a través de la red.

Cuando un socket está en estado de escucha o conexión, siempre está vinculado a una combinación de una dirección IP más un número de puerto que identifica al host (máquina/dispositivo) y al proceso.

### Cómo funcionan las conexiones de socket

Los sockets pueden escuchar las conexiones entrantes o realizar ellos mismos las conexiones salientes. Cuando se establece una conexión, el socket de escucha (socket del servidor) se vincula adicionalmente a la IP y al puerto de la parte que se conecta.

O, alternativamente, se crea un nuevo socket que ahora está vinculado a dos pares de direcciones IP y números de puerto de un oyente y un solicitante. De esta forma, dos sockets conectados en máquinas diferentes pueden identificarse entre sí y compartir una única conexión para la transmisión de datos sin bloquear el socket de escucha que, mientras tanto, sigue escuchando otras conexiones.

En el caso del socket de conexión (socket cliente), se vincula implícitamente a la dirección IP del dispositivo y a un número de puerto accesible aleatoriamente al iniciar la conexión. Después, al establecer la conexión, se produce un enlace con la IP y el puerto del otro lado de la comunicación, de forma muy similar a la de un socket de escucha, pero sin crear un nuevo socket.

Cuando se establece una nueva conexión que se hace por el puerto que escucha se crea una nueva combinación de socket con la misma ip pero con un puerto distinto aunque este socket es manejado por el sistema operativo para el cliente sigue siendo el mismo el que escucha el sistema operativo sabe cual es gracias al seq_number

### Los sockets en el contexto de las redes

En este tutorial, no nos ocupamos de la implementación de los sockets, sino de lo que significan los sockets en el contexto de las redes.

Se puede decir que un socket es un punto final de conexión (destino del tráfico) que, por un lado, está asociado a la dirección IP de la máquina anfitriona y al número de puerto de la aplicación para la que se creó el socket y, por otro, está asociado a la dirección IP y al puerto de la aplicación que se ejecuta en otra máquina con la que se establece la conexión.

### Programación de sockets

Cuando hablamos de programación de sockets, instanciamos objetos socket en nuestro código y realizamos operaciones sobre ellos (escuchar, conectar, recibir, enviar, etc.). En este contexto, los sockets son simplemente objetos especiales que creamos en nuestro programa y que tienen métodos especiales para trabajar con conexiones y tráfico de red.

Internamente, esos métodos llaman al núcleo de tu sistema operativo o, más concretamente, a la pila de red, que es una parte especial del núcleo responsable de gestionar las operaciones de red.

### Sockets y comunicación cliente-servidor

Ahora bien, también es importante mencionar que los sockets aparecen a menudo en el contexto de la comunicación cliente-servidor.

La idea es sencilla: los sockets se relacionan con las conexiones; son gestores de conexiones. En la web, siempre que quieras enviar o recibir algún dato, inicias una conexión (que se inicia a través de la interfaz llamada sockets).

Ahora, tú o la parte a la que intentas conectarte actuáis como servidor y otra parte como cliente. Mientras un servidor sirve datos a los clientes, los clientes se conectan proactivamente y solicitan datos a un servidor. Un servidor escucha a través de un socket de escucha nuevas conexiones, las establece, recibe las peticiones del cliente y comunica los datos solicitados en su respuesta al cliente.

Por otra parte, un cliente crea un socket utilizando la dirección IP y el puerto del servidor al que desea conectarse, inicia una conexión, comunica su petición al servidor y recibe datos como respuesta. Este intercambio fluido de información entre los sockets del cliente y del servidor constituye la columna vertebral de diversas aplicaciones de red.

### Los sockets como base de los protocolos de red

El hecho de que los sockets formen una columna vertebral también significa que hay varios protocolos construidos y utilizados sobre ellos. Los más comunes son UDP y TCP, de los que ya hemos hablado brevemente. Los sockets que utilizan uno de estos protocolos de transporte se denominan sockets UDP o TCP.

### Sockets IPC

Aparte de los sockets de red, también hay otros tipos. Por ejemplo, los sockets IPC (comunicación entre procesos). Los sockets IPC están pensados para transferir datos entre procesos de la misma máquina, mientras que los sockets de red pueden hacer lo mismo a través de la red.

Lo bueno de los sockets IPC es que evitan gran parte de la sobrecarga de construir paquetes y resolver las rutas para enviar los datos. Como en el contexto de la IPC el emisor y el receptor son procesos locales, la comunicación a través de sockets IPC suele tener una latencia menor.

### Sockets Unix

Un buen ejemplo de sockets IPC son los sockets Unix que son, como todo en Unix, simples archivos en el sistema de archivos. No se identifican por la dirección IP y el puerto, sino por la ruta del archivo en el sistema de archivos.

### Sockets de red como sockets IPC

Ten en cuenta que también puedes utilizar sockets de red para las comunicaciones entre procesos si tanto el servidor como el receptor están en localhost (es decir, tienen una dirección IP 127.0.0.1).

Por supuesto, por un lado, esto añade latencia adicional debido a la sobrecarga asociada al procesamiento de tus datos por la pila de red, pero por otro lado, esto nos permite no preocuparnos del sistema operativo subyacente, ya que los sockets de red están presentes y funcionan en todos los sistemas, a diferencia de los sockets IPC, que son específicos de un SO o familia de SO determinados.

## Biblioteca de sockets Python

Para programar sockets en Python, utilizamos la biblioteca oficial de sockets incorporada en Python, que consta de funciones, constantes y clases que se utilizan para crear, gestionar y trabajar con sockets. Algunas de las funciones más utilizadas de esta biblioteca son

- **socket()**: crea un nuevo socket.
- **bind()**: asocia el socket a una dirección y puerto concretos.
- **listen()**: inicia la escucha de conexiones entrantes en el socket.
- **accept()**: acepta una conexión de un cliente y devuelve un nuevo socket para la comunicación.
- **connect()**: establece una conexión con un servidor remoto.
- **send()**: envía datos a través del socket.
- **recv()**: recibe datos del socket.
- **close()**: cierra la conexión del socket.

## Ejemplo de socket en Python

Echemos un vistazo a la programación de sockets con un ejemplo práctico escrito en Python. Aquí, nuestro objetivo es conectar dos aplicaciones y hacer que se comuniquen entre sí. Utilizaremos la biblioteca de sockets de Python para crear una aplicación de servidor de sockets que se comunicará e intercambiará información con un cliente a través de una red.

### Consideraciones y limitaciones

No obstante, ten en cuenta que, con fines educativos, nuestro ejemplo está simplificado, y las aplicaciones se ejecutarán localmente y no hablarán a través de la red real: utilizaremos una dirección localhost de bucle invertido para conectar el cliente con el servidor.

Esto significa que tanto el cliente como el servidor se ejecutarán en la misma máquina y que el cliente iniciará una conexión con la misma máquina en la que se está ejecutando, aunque con un proceso distinto que representa al servidor.

### Ejecución en máquinas diferentes

Alternativamente, podrías tener tus aplicaciones en dos dispositivos diferentes y tenerlos ambos conectados al mismo enrutador Wi-Fi, lo que formaría una red de área local. Así, el cliente que se ejecuta en un dispositivo podría conectarse al servidor que se ejecuta en otra máquina.

En este caso, sin embargo, necesitarías conocer las direcciones IP que tu enrutador asignó a tus dispositivos y utilizarlas en lugar de la dirección IP de loopback localhost (127.0.0.1) (para ver las direcciones IP, utiliza el comando `ifconfig` terminal para sistemas tipo Unix o `ipconfig` - para Windows). Después de obtener las direcciones IP de tus aplicaciones, puedes cambiarlas en el código en consecuencia, y el ejemplo seguirá funcionando.

De todos modos, vamos a empezar con nuestro ejemplo. Por supuesto, necesitarás tener [instalado Python](https://www.datacamp.com/es/blog/how-to-install-python) si quieres seguir el proceso.

### Crear un servidor de sockets en Python

Empecemos por crear un servidor de sockets (servidor TCP de Python, en concreto, ya que trabajará con sockets TCP, como veremos), que intercambiará mensajes con los clientes. Para aclarar la terminología, aunque técnicamente cualquier servidor es un servidor de sockets, ya que los sockets siempre se utilizan internamente para iniciar conexiones de red, utilizamos la expresión "servidor de sockets" porque nuestro ejemplo hace uso explícito de la programación de sockets.

Por tanto, sigue los pasos que se indican a continuación:

#### Crear un archivo Python con texto reutilizable

- Crea un archivo llamado `server.py`
- Importa el módulo `socket` en tu script de Python.

`import socket`

[Powered By](https://www.datacamp.com/datalab) 

- Añade una función llamada `run_server`. Allí añadiremos la mayor parte de nuestro código. Cuando añadas tu código a la función, no olvides aplicar la sangría adecuada:

`def run_server():     # your code will go here`

[Powered By](https://www.datacamp.com/datalab) 

#### Instanciar un objeto socket

Como siguiente paso, en `run_server`, crea un objeto socket utilizando la función `socket.socket()`.

El primer argumento (`socket.AF_INET`) especifica la familia de direcciones IP para IPv4 (otras opciones son: `AF_INET6` para la familia IPv6 y `AF_UNIX` para sockets de Unix)

El segundo argumento (`socket.SOCK_STREAM)` indica que estamos utilizando un socket TCP.

En caso de utilizar TCP, el sistema operativo creará una conexión fiable con entrega de datos en orden, detección y retransmisión de errores y control de flujo. No tendrás que pensar en poner en práctica todos esos detalles.

También hay una opción para especificar un socket UDP: `socket.SOCK_DGRAM`. Esto creará un socket que implementa todas las características de UDP de forma interna.

En caso de que quieras ir más allá y construir tu propio protocolo de capa de transporte sobre el protocolo de capa de red TCP/IP que utilizan los sockets, puedes utilizar el valor `socket.RAW_SOCKET` para el segundo argumento. En este caso, el sistema operativo no gestionará por ti ninguna función de protocolo de nivel superior y tendrás que implementar tú mismo todas las funcionalidades de cabeceras, confirmación de conexión y retransmisión, si las necesitas. También hay otros valores que puedes consultar en [la documentación](https://docs.python.org/2/library/socket.html#socket.SOCK_STREAM).

`# create a socket object     server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)`

[Powered By](https://www.datacamp.com/datalab) 

#### Vincular el socket del servidor a la dirección IP y al puerto

Define el nombre de host o la IP del servidor y el puerto para indicar la dirección desde la que se podrá acceder al servidor y dónde escuchará las conexiones entrantes. En este ejemplo, el servidor está a la escucha en la máquina local - esto se define mediante la variable `server_ip` establecida en `127.0.0.1` (también llamada localhost).

La variable `port` se establece en `8000`, que es el número de puerto con el que el sistema operativo identificará la aplicación del servidor (se recomienda utilizar valores superiores a 1023 para tus números de puerto, a fin de evitar colisiones con los puertos utilizados por los procesos del sistema).

`server_ip = "127.0.0.1"     port = 8000`

[Powered By](https://www.datacamp.com/datalab) 

Prepara el socket para recibir conexiones vinculándolo a la dirección IP y al puerto que hemos definido antes.

`# bind the socket to a specific address and port     server.bind((server_ip, port))`

[Powered By](https://www.datacamp.com/datalab) 

#### Escucha las conexiones entrantes

Configura un estado de escucha en el socket del servidor utilizando la función `listen` para poder recibir conexiones entrantes de clientes.

Esta función acepta un argumento llamado `backlog` que especifica el número máximo de conexiones en cola no aceptadas. En este ejemplo, utilizamos el valor `0` para este argumento. Esto significa que sólo un cliente puede interactuar con el servidor. Se rechazará el intento de conexión de cualquier cliente realizado mientras el servidor está trabajando con otro cliente.

Si especificas un valor mayor que `0`, digamos `1`, le indica al sistema operativo cuántos clientes se pueden poner en la cola antes de que se llame al método `accept` sobre ellos.

Una vez que se llama a `accept`, el cliente se elimina de la cola y ya no se tiene en cuenta para este límite. Esto te quedará más claro cuando veas más partes del código, pero lo que hace esencialmente este parámetro puede ilustrarse de la siguiente manera: una vez que tu servidor de escucha reciba la solicitud de conexión, añadirá a este cliente a la cola y procederá a aceptar su solicitud. Si antes de que el servidor haya podido llamar internamente a `accept` en el primer cliente, recibe una solicitud de conexión de un segundo cliente, empujará a este segundo cliente a la misma cola siempre que haya espacio suficiente en ella. El tamaño exacto de esta cola se controla con el argumento de trabajos pendientes. En cuanto el servidor acepta al primer cliente, éste se retira de la cola y el servidor empieza a comunicarse con él. El segundo cliente sigue en la cola, esperando a que el servidor se libere y acepte la conexión.

Si omites el argumento de trabajos pendientes, se establecerá el valor por defecto de tu sistema (en Unix, normalmente puedes ver este valor por defecto en el archivo `/proc/sys/net/core/somaxconn` ).

`# listen for incoming connections     server.listen(0)     print(f"Listening on {server_ip}:{port}")`

[Powered By](https://www.datacamp.com/datalab) 

#### Aceptar conexiones entrantes

A continuación, espera y acepta las conexiones entrantes de los clientes. El método `accept` detiene el hilo de ejecución hasta que se conecte un cliente. A continuación, devuelve un par de tuplas `(conn, address)`, donde "address" es una tupla de la dirección IP y el puerto del cliente, y `conn` es un nuevo objeto socket que comparte una conexión con el cliente y puede utilizarse para comunicarse con él.

`accept` crea un nuevo socket para comunicarse con el cliente en lugar de vincular el socket de escucha (llamado `server` en nuestro ejemplo) a la dirección del cliente y utilizarlo para la comunicación, porque el socket de escucha necesita escuchar más conexiones de otros clientes, de lo contrario se bloquearía. Por supuesto, en nuestro caso, sólo gestionamos un único cliente y rechazamos todas las demás conexiones mientras lo hacemos, pero esto será más relevante cuando lleguemos al ejemplo del servidor multihilo.

`# accept incoming connections     client_socket, client_address = server.accept()     print(f"Accepted connection from {client_address[0]}:{client_address[1]}")`

[Powered By](https://www.datacamp.com/datalab) 

#### Crear un bucle de comunicación

En cuanto se haya establecido una conexión con el cliente (tras llamar al método `accept` ), iniciamos un bucle infinito para comunicarnos. En este bucle, realizamos una llamada al método `recv` del objeto `client_socket`. Este método recibe del cliente el número de bytes especificado, en nuestro caso 1024.

1024 bytes es sólo una convención común para el tamaño de la carga útil, ya que es una potencia de dos que es potencialmente mejor a efectos de optimización que cualquier otro valor arbitrario. Sin embargo, eres libre de cambiar este valor como quieras.

Como los datos recibidos del cliente en la variable `request` están en forma binaria bruta, los transformamos de una secuencia de bytes a una cadena utilizando la función `decode`.

Luego tenemos una declaración if, que sale del bucle de comunicación en caso de que recibamos un mensaje `”close”`. Esto significa que, en cuanto nuestro servidor recibe una cadena `”close”` en la solicitud, devuelve la confirmación al cliente y finaliza su conexión con él. En caso contrario, imprimimos en la consola el mensaje recibido. La confirmación en nuestro caso es simplemente enviar una cadena `”closed”` al cliente.

Observa que el método `lower` que utilizamos en la cadena `request` en la declaración if, simplemente la convierte a minúsculas. De este modo, no nos importa si la cadena `close` se escribió originalmente con mayúsculas o minúsculas.

`# receive data from the client     while True:         request = client_socket.recv(1024)         request = request.decode("utf-8") # convert bytes to string                  # if we receive "close" from the client, then we break         # out of the loop and close the conneciton         if request.lower() == "close":             # send response to the client which acknowledges that the             # connection should be closed and break out of the loop             client_socket.send("closed".encode("utf-8"))             break          print(f"Received: {request}")`

[Powered By](https://www.datacamp.com/datalab) 

#### Enviar respuesta al cliente

Ahora debemos manejar la respuesta normal del servidor al cliente (es decir, cuando el cliente no desea cerrar la conexión). Dentro del bucle "while", justo después de `print(f"Received: {request}")`, añade las siguientes líneas, que convertirán una cadena de respuesta (`”accepted”` en nuestro caso) en bytes y la enviarán al cliente. De este modo, cuando el servidor reciba un mensaje del cliente que no sea `”close”`, enviará como respuesta la cadena `”accepted”`:

`response = "accepted".encode("utf-8") # convert string to bytes # convert and send accept response to the client client_socket.send(response)`

[Powered By](https://www.datacamp.com/datalab) 

#### Liberar recursos

Una vez que salimos del bucle "while" infinito, la comunicación con el cliente ha finalizado, así que cerramos el socket del cliente utilizando el método `close` para liberar recursos del sistema. También cerramos el socket del servidor utilizando el mismo método, lo que efectivamente apaga nuestro servidor. En un escenario del mundo real, probablemente querríamos que nuestro servidor siguiera escuchando a otros clientes y no se cerrara tras comunicarse con uno solo, pero no te preocupes, llegaremos a otro ejemplo más adelante.

De momento, añade las siguientes líneas después del bucle "while" infinito:

`# close connection socket with the client     client_socket.close()     print("Connection to client closed")     # close server socket     server.close()`

[Powered By](https://www.datacamp.com/datalab) 

**Nota:** no olvides llamar a la función `run_server` al final de tu archivo `server.py`. Sólo tienes que utilizar la siguiente línea de código:

`run_server()`

[Powered By](https://www.datacamp.com/datalab) 

#### Ejemplo completo de código de socket de servidor

Aquí tienes el código fuente completo de `server.py`:

`import socket  def run_server():     # create a socket object     server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)      server_ip = "127.0.0.1"     port = 8000      # bind the socket to a specific address and port     server.bind((server_ip, port))     # listen for incoming connections     server.listen(0)     print(f"Listening on {server_ip}:{port}")      # accept incoming connections     client_socket, client_address = server.accept()     print(f"Accepted connection from {client_address[0]}:{client_address[1]}")      # receive data from the client     while True:         request = client_socket.recv(1024)         request = request.decode("utf-8") # convert bytes to string                  # if we receive "close" from the client, then we break         # out of the loop and close the conneciton         if request.lower() == "close":             # send response to the client which acknowledges that the             # connection should be closed and break out of the loop             client_socket.send("closed".encode("utf-8"))             break          print(f"Received: {request}")          response = "accepted".encode("utf-8") # convert string to bytes         # convert and send accept response to the client         client_socket.send(response)      # close connection socket with the client     client_socket.close()     print("Connection to client closed")     # close server socket     server.close()  run_server()`

[Powered By](https://www.datacamp.com/datalab) 

Ten en cuenta que, para no convolucionar y complicar este ejemplo básico, hemos omitido el tratamiento de errores. Por supuesto, deberías añadir bloques try-except y asegurarte de que siempre cierras los sockets en la cláusula `finally`. Sigue leyendo y veremos un ejemplo más avanzado.

### Crear un socket cliente en Python

Después de configurar tu servidor, el siguiente paso es configurar un cliente que se conecte y envíe peticiones a tu servidor. Así que, empecemos con los pasos que se indican a continuación:

#### Crear un archivo Python con texto reutilizable

- Crea un nuevo archivo llamado `client.py`
- Importa la biblioteca de sockets:

`import socket`

[Powered By](https://www.datacamp.com/datalab) 

- Define la función `run_client` donde colocaremos todo nuestro código:

`def run_client():     # your code will go here`

[Powered By](https://www.datacamp.com/datalab) 

#### Instanciar un objeto socket

A continuación, utiliza la función `socket.socket()` para crear un objeto socket TCP que sirva como punto de contacto del cliente con el servidor.

`# create a socket object     client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)`

[Powered By](https://www.datacamp.com/datalab) 

#### Conexión al socket del servidor

Especifica la dirección IP y el puerto del servidor para poder conectarte a él. Estos deben coincidir con la dirección IP y el puerto que estableciste antes en `server.py`.

    `server_ip = "127.0.0.1"  # replace with the server's IP address     server_port = 8000  # replace with the server's port number`

[Powered By](https://www.datacamp.com/datalab) 

Establece una conexión con el servidor utilizando el método `connect` en el objeto socket cliente. Ten en cuenta que no hemos vinculado el socket cliente a ninguna dirección IP ni a ningún puerto. Esto es normal para el cliente, porque `connect` elegirá automáticamente un puerto libre y tomará una dirección IP que proporcione la mejor ruta al servidor desde las interfaces de red del sistema (`127.0.0.1` en nuestro caso) y enlazará el socket del cliente a ellas.

    `# establish connection with server     client.connect((server_ip, server_port))`

[Powered By](https://www.datacamp.com/datalab) 

#### Crear un bucle de comunicación

Una vez establecida la conexión, iniciamos un bucle infinito de comunicación para enviar varios mensajes al servidor. Obtenemos la entrada del usuario utilizando la función incorporada de Python `input`, luego la codificamos en bytes y la recortamos para que tenga 1024 bytes como máximo. Después enviamos el mensaje al servidor utilizando `client.send`.

   `while True:         # input message and send it to the server         msg = input("Enter message: ")         client.send(msg.encode("utf-8")[:1024])`

[Powered By](https://www.datacamp.com/datalab) 

#### Manejar la respuesta del servidor

Una vez que el servidor recibe un mensaje del cliente, le responde. Ahora, en el código de nuestro cliente, queremos recibir la respuesta del servidor. Para ello, en el bucle de comunicación, utilizamos el método `recv` para leer 1024 bytes como máximo. A continuación convertimos la respuesta de bytes en una cadena utilizando `decode` y luego comprobamos si es igual al valor `”closed”`. Si es así, salimos del bucle que, como veremos más adelante, terminará la conexión del cliente. En caso contrario, imprimimos la respuesta del servidor en la consola.

       `# receive message from the server         response = client.recv(1024)         response = response.decode("utf-8")          # if server sent us "closed" in the payload, we break out of the loop and close our socket         if response.lower() == "closed":             break          print(f"Received: {response}")`

[Powered By](https://www.datacamp.com/datalab) 

#### Liberar recursos

Por último, tras el bucle "while", cierra la conexión del socket cliente utilizando el método `close`. Esto garantiza que los recursos se liberan correctamente y que la conexión finaliza (es decir, cuando recibimos el mensaje `“closed”` y salimos del bucle while).

   `# close client socket (connection to the server)     client.close()     print("Connection to server closed")`

[Powered By](https://www.datacamp.com/datalab) 

**Nota**: De nuevo, no olvides llamar a la función `run_client`, que hemos implementado anteriormente, al final del archivo de la siguiente manera:

`run_client()`

[Powered By](https://www.datacamp.com/datalab) 

#### Ejemplo de código completo de socket cliente

Aquí tienes el código completo de `client.py`:

`import socket  def run_client():     # create a socket object     client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)      server_ip = "127.0.0.1"  # replace with the server's IP address     server_port = 8000  # replace with the server's port number     # establish connection with server     client.connect((server_ip, server_port))      while True:         # input message and send it to the server         msg = input("Enter message: ")         client.send(msg.encode("utf-8")[:1024])          # receive message from the server         response = client.recv(1024)         response = response.decode("utf-8")          # if server sent us "closed" in the payload, we break out of the loop and close our socket         if response.lower() == "closed":             break          print(f"Received: {response}")      # close client socket (connection to the server)     client.close()     print("Connection to server closed")  run_client()`

[Powered By](https://www.datacamp.com/datalab) 

### Prueba tu cliente y tu servidor

Para probar la implementación del servidor y el cliente que escribimos anteriormente, realiza lo siguiente:

- Abre dos ventanas de terminal simultáneamente.

- En una ventana de terminal, navega hasta el directorio donde se encuentra el archivo `server.py` y ejecuta el siguiente comando para iniciar el servidor:

   `python server.py`

[Powered By](https://www.datacamp.com/datalab) 

Esto vinculará el socket del servidor a la dirección localhost (127.0.0.1) en el puerto 8000 y empezará a escuchar las conexiones entrantes.

- En el otro terminal, navega hasta el directorio donde se encuentra el archivo `client.py` y ejecuta el siguiente comando para iniciar el cliente:

   `python client.py`

[Powered By](https://www.datacamp.com/datalab) 

Esto solicitará la entrada del usuario. A continuación, puedes escribir tu mensaje y pulsar Intro. Esto transferirá tu entrada al servidor y la mostrará en su ventana de terminal. El servidor enviará su respuesta al cliente y éste te pedirá de nuevo la entrada. Esto continuará hasta que envíes la cadena `”close”` al servidor.

## Trabajar con varios clientes - Multihilo

En el ejemplo anterior hemos visto cómo responde un servidor a las peticiones de un solo cliente, sin embargo, en muchas situaciones prácticas, numerosos clientes pueden necesitar conectarse a un solo servidor a la vez. Aquí es donde entra en juego el multihilo. El multihilo se utiliza en situaciones en las que necesitas manejar varias tareas (por ejemplo, ejecutar varias funciones) de forma concurrente (al mismo tiempo).

La idea es generar un hilo, que es un conjunto independiente de instrucciones que puede manejar el procesador. Los hilos son mucho más ligeros que los procesos, porque en realidad viven dentro de un proceso y no tienes que asignarles muchos recursos.

### Limitaciones del multihilo en Python

Ten en cuenta que el multihilo en Python es limitado. La implementación estándar de Python (CPython) no puede ejecutar hilos realmente en paralelo. Sólo se permite la ejecución de un único hilo a la vez, debido al bloqueo global del intérprete (GIL). Sin embargo, éste es un tema aparte, que no vamos a tratar. Por el bien de nuestro ejemplo, utilizar hilos CPython limitados es suficiente y consigue el objetivo. Sin embargo, en el mundo real, si vas a utilizar Python, deberías considerar la programación asíncrona. No vamos a hablar de ello ahora, porque es un tema aparte y suele abstraer algunas operaciones de socket de bajo nivel en las que nos centramos específicamente en este artículo.

### Ejemplo de servidor multihilo

Veamos en el siguiente ejemplo cómo añadir multihilo a tu servidor para gestionar un gran número de clientes. Ten en cuenta que esta vez también añadiremos un tratamiento básico de errores mediante los bloques try-except-finally. Para empezar, sigue los pasos que se indican a continuación:

#### Crear función de servidor de generación de hilos

En tu archivo de Python, importa los módulos `socket` y `threading` para poder trabajar tanto con sockets como con hilos:

`import socket import threading`

[Powered By](https://www.datacamp.com/datalab) 

Define la función `run_server` que, como en el ejemplo anterior, creará un socket de servidor, lo enlazará y escuchará las conexiones entrantes. Luego llama a `accept` en un bucle while infinito. Esto hará que siempre estés a la escucha de nuevas conexiones. Después de que `accept` obtenga una conexión entrante y regrese, crea un hilo utilizando el constructor `threading.Thread`. Este hilo ejecutará la función `handle_client`, que definiremos más adelante, y le pasará `client_socket` y `addr` como argumentos (la tupla`addr` contiene una dirección IP y un puerto del cliente conectado). Una vez creado el hilo, llamamos a `start` sobre él para que comience su ejecución.

Recuerda que la llamada a `accept` es bloqueante, por lo que en la primera iteración del bucle while, cuando llegamos a la línea con `accept`, nos detenemos y esperamos una conexión del cliente sin ejecutar nada más. En cuanto el cliente se conecte, vuelve el método `accept`, y continuamos la ejecución: generamos un hilo, que se encargará de dicho cliente y pasamos a la siguiente iteración, donde volveremos a detenernos en la llamada `accept` a la espera de que se conecte otro cliente.

Al final de la función, tenemos un tratamiento de errores que garantiza que el socket del servidor se cierre siempre en caso de que ocurra algo inesperado.

`def run_server():     server_ip = "127.0.0.1"  # server hostname or IP address     port = 8000  # server port number     # create a socket object     try:         server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)         # bind the socket to the host and port         server.bind((server_ip, port))         # listen for incoming connections         server.listen()         print(f"Listening on {server_ip}:{port}")          while True:             # accept a client connection             client_socket, addr = server.accept()             print(f"Accepted connection from {addr[0]}:{addr[1]}")             # start a new thread to handle the client             thread = threading.Thread(target=handle_client, args=(client_socket, addr,))             thread.start()     except Exception as e:         print(f"Error: {e}")     finally:         server.close()`

[Powered By](https://www.datacamp.com/datalab) 

Ten en cuenta que el servidor de nuestro ejemplo sólo se detendrá en caso de que se produzca un error inesperado. De lo contrario, escuchará a los clientes indefinidamente, y tendrás que matar el terminal si quieres detenerlo.

#### Crear una función de gestión de clientes que se ejecute en un hilo independiente

Ahora, encima de la función `run_server`, define otra llamada `handle_client`. Esta función será la que se ejecute en un hilo independiente para cada conexión de cliente. Recibe como argumentos el objeto socket del cliente y la tupla `addr`.

Dentro de esta función, hacemos lo mismo que en el ejemplo de un solo hilo, más algún tratamiento de errores: iniciamos un bucle para obtener mensajes del cliente utilizando `recv`.

Luego comprobamos si recibimos un mensaje de cierre. Si es así, respondemos con la cadena `”closed”` y cerramos la conexión saliendo del bucle. En caso contrario, imprimimos la cadena de solicitud del cliente en la consola y pasamos a la siguiente iteración del bucle para recibir el mensaje del siguiente cliente.

Al final de esta función, tenemos un tratamiento de errores para casos inesperados (cláusula`except` ), y también una cláusula `finally` en la que liberamos `client_socket` utilizando `close`. Esta cláusula `finally` siempre se ejecutará pase lo que pase, lo que garantiza que el socket del cliente siempre se libere correctamente.

`def handle_client(client_socket, addr):     try:         while True:             # receive and print client messages             request = client_socket.recv(1024).decode("utf-8")             if request.lower() == "close":                 client_socket.send("closed".encode("utf-8"))                 break             print(f"Received: {request}")             # convert and send accept response to the client             response = "accepted"             client_socket.send(response.encode("utf-8"))     except Exception as e:         print(f"Error when hanlding client: {e}")     finally:         client_socket.close()         print(f"Connection to client ({addr[0]}:{addr[1]}) closed")`

[Powered By](https://www.datacamp.com/datalab) 

Cuando `handle_client` regrese, el hilo que lo ejecuta también se liberará automáticamente.

**Nota**: No olvides llamar a la función `run_server` al final de tu archivo.

#### Ejemplo completo de código de servidor multihilo

Ahora, vamos a montar el código completo del servidor multihilo:

`import socket import threading  def handle_client(client_socket, addr):     try:         while True:             # receive and print client messages             request = client_socket.recv(1024).decode("utf-8")             if request.lower() == "close":                 client_socket.send("closed".encode("utf-8"))                 break             print(f"Received: {request}")             # convert and send accept response to the client             response = "accepted"             client_socket.send(response.encode("utf-8"))     except Exception as e:         print(f"Error when hanlding client: {e}")     finally:         client_socket.close()         print(f"Connection to client ({addr[0]}:{addr[1]}) closed")  def run_server():     server_ip = "127.0.0.1"  # server hostname or IP address     port = 8000  # server port number     # create a socket object     try:         server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)         # bind the socket to the host and port         server.bind((server_ip, port))         # listen for incoming connections         server.listen()         print(f"Listening on {server_ip}:{port}")          while True:             # accept a client connection             client_socket, addr = server.accept()             print(f"Accepted connection from {addr[0]}:{addr[1]}")             # start a new thread to handle the client             thread = threading.Thread(target=handle_client, args=(client_socket, addr,))             thread.start()     except Exception as e:         print(f"Error: {e}")     finally:         server.close()  run_server()`

[Powered By](https://www.datacamp.com/datalab) 

**Nota**: En un código del mundo real, para evitar posibles problemas como situaciones de carrera o incoherencias de datos al tratar con servidores multihilo, es vital tener en cuenta la seguridad de los hilos y las técnicas de sincronización. Sin embargo, en nuestro sencillo ejemplo esto no supone ningún problema.

### Ejemplo de cliente con tratamiento básico de errores

Ahora que tenemos una implementación de servidor capaz de gestionar varios clientes simultáneamente, podríamos utilizar la misma implementación de cliente que vimos anteriormente en los primeros ejemplos básicos para iniciar la conexión, o podríamos actualizarla ligeramente y añadir algún tratamiento de errores. A continuación puedes encontrar el código, que es idéntico al del ejemplo de cliente anterior con una adición de bloques try-except:

`import socket  def run_client():     # create a socket object     client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)      server_ip = "127.0.0.1"  # replace with the server's IP address     server_port = 8000  # replace with the server's port number     # establish connection with server     client.connect((server_ip, server_port))      try:         while True:             # get input message from user and send it to the server             msg = input("Enter message: ")             client.send(msg.encode("utf-8")[:1024])              # receive message from the server             response = client.recv(1024)             response = response.decode("utf-8")              # if server sent us "closed" in the payload, we break out of             # the loop and close our socket             if response.lower() == "closed":                 break              print(f"Received: {response}")     except Exception as e:         print(f"Error: {e}")     finally:         # close client socket (connection to the server)         client.close()         print("Connection to server closed")  run_client()`

[Powered By](https://www.datacamp.com/datalab) 

### Probar el ejemplo multihilo

Si quieres probar la implementación multicliente, abre varias ventanas de terminal para los clientes y una para el servidor. Primero inicia el servidor con `python server.py`. Después, inicia un par de clientes utilizando `python client.py`. En las ventanas del terminal del servidor verás cómo se conectan los nuevos clientes al servidor. Ahora puedes proceder a enviar mensajes desde distintos clientes introduciendo texto en los respectivos terminales y todos ellos serán tratados e impresos en la consola del lado del servidor.

## Aplicaciones de la programación de sockets en la ciencia de datos

Aunque todas las aplicaciones de red utilizan sockets creados por el SO de forma interna, hay numerosos sistemas que dependen en gran medida de la programación de sockets específicamente, ya sea para determinados casos de uso especiales o para mejorar el rendimiento. Pero, ¿cómo es exactamente útil la programación de sockets en el contexto de la ciencia de datos? Sin duda, desempeña un papel importante cuando es necesario recibir o enviar grandes cantidades de datos con rapidez. De ahí que la programación de sockets se utilice principalmente para la recogida de datos y el procesamiento en tiempo real, la informática distribuida y la comunicación entre procesos. Pero veamos más de cerca algunas aplicaciones concretas en el campo de la ciencia de datos.

### Recogida de datos en tiempo real

Los sockets se utilizan ampliamente para recoger datos en tiempo real de distintas fuentes para su posterior procesamiento, reenvío a una base de datos o a un canal de análisis, etc. Por ejemplo, se puede utilizar un socket para recibir instantáneamente datos de un sistema financiero o de una API de redes sociales para su posterior procesamiento por los científicos de datos.

### Informática distribuida

Los científicos de datos pueden utilizar la conectividad de socket para distribuir el procesamiento y el cálculo de enormes conjuntos de datos entre varias máquinas. La programación de sockets se utiliza habitualmente en Apache Spark y otros marcos de computación distribuida para la comunicación entre los nodos.

### Despliegue del modelo

La programación de sockets puede utilizarse al servir modelos de machine learning a los usuarios, permitiendo la entrega instantánea de predicciones y sugerencias. Para facilitar la toma de decisiones en tiempo real, los científicos de datos pueden utilizar aplicaciones de servidor basadas en sockets de alto rendimiento que reciben grandes cantidades de datos, los procesan utilizando modelos entrenados para proporcionar predicciones y, a continuación, devuelven rápidamente los resultados al cliente.

### Comunicación entre procesos (IPC)

Los sockets pueden utilizarse para IPC, lo que permite que distintos procesos que se ejecutan en la misma máquina se comuniquen entre sí e intercambien datos. Esto es útil en la ciencia de datos para distribuir cálculos complejos y que consumen muchos recursos entre varios procesos. De hecho, la biblioteca de subprocesamiento de Python se utiliza a menudo con este fin: genera varios procesos para utilizar varios núcleos del procesador y aumentar el rendimiento de la aplicación al realizar cálculos pesados. La comunicación entre estos procesos puede realizarse mediante sockets IPC.

### Colaboración y comunicación

La programación de sockets permite la comunicación y colaboración en tiempo real entre los científicos de datos. Para facilitar la colaboración eficaz y el intercambio de conocimientos, se utilizan aplicaciones de chat basadas en sockets o plataformas colaborativas de análisis de datos.

Vale la pena decir que en muchas de las aplicaciones anteriores, los científicos de datos podrían no estar directamente implicados en el trabajo con sockets. Normalmente utilizarían bibliotecas, marcos y sistemas que abstraen todos los detalles de bajo nivel de la programación de sockets. Sin embargo, internamente, todas esas soluciones se basan en la comunicación por sockets y utilizan la programación por sockets.

## Retos y buenas prácticas de la programación de sockets

Dado que los sockets son un concepto de bajo nivel de gestión de conexiones, los desarrolladores que trabajan con ellos tienen que implementar toda la infraestructura necesaria a su alrededor para crear aplicaciones robustas y fiables. Por supuesto, esto conlleva muchos retos. Sin embargo, hay algunas buenas prácticas y directrices generales que se pueden seguir para superar estos problemas. A continuación se exponen algunos de los problemas más frecuentes en la programación de sockets, junto con algunos consejos generales:

### Gestión de la conexión

Trabajar con muchas conexiones a la vez, gestionar varios clientes y garantizar una gestión eficaz de las solicitudes concurrentes puede ser, sin duda, un reto no trivial. Requiere una gestión cuidadosa de los recursos y coordinación para evitar cuellos de botella

#### Buenas prácticas

- Haz un seguimiento de las conexiones activas utilizando estructuras de datos como listas o diccionarios. O utiliza técnicas avanzadas como la agrupación de conexiones, que también ayudan a la escalabilidad.
- Utiliza hilos o técnicas de programación asíncrona para gestionar varias conexiones de clientes al mismo tiempo.
- Cierra las conexiones correctamente para liberar recursos y evitar fugas de memoria.

### Tratamiento de errores

Hacer frente a los errores, como los fallos de conexión, los tiempos de espera y los problemas de transmisión de datos, es crucial. Gestionar estos errores y proporcionar la información adecuada a los clientes puede ser un reto, especialmente cuando se realiza programación de sockets de bajo nivel.

#### Buenas prácticas

- Utiliza bloques try-except-finally para capturar y gestionar tipos específicos de errores.
- Proporciona mensajes de error informativos y considera la posibilidad de emplear el registro para ayudar en la resolución de problemas.

### Escalabilidad y rendimiento

Garantizar un rendimiento óptimo y minimizar la latencia son preocupaciones clave cuando se trata de flujos de datos de gran volumen o aplicaciones en tiempo real.

#### Buenas prácticas

- Optimiza el rendimiento de tu código minimizando el procesamiento innecesario de datos y la sobrecarga de la red.
- Aplica técnicas de almacenamiento en búfer para gestionar eficazmente las transferencias de datos de gran tamaño.
- Considera las técnicas de equilibrio de carga para distribuir las peticiones de los clientes entre varias instancias del servidor.

### Seguridad y autenticación

Asegurar la comunicación basada en sockets e implantar mecanismos de autenticación adecuados puede ser difícil. Garantizar la privacidad de los datos, impedir el acceso no autorizado y proteger contra actividades malintencionadas requiere una cuidadosa consideración y aplicación de protocolos seguros.

#### Buenas prácticas

- Utiliza los protocolos de seguridad SSL/TLS para garantizar una transmisión segura de los datos mediante la encriptación de la información.
- Garantiza la identidad del cliente aplicando métodos de autenticación seguros, como la autenticación basada en tokens, la criptografía de clave pública o el nombre de usuario/contraseña.
- Asegúrate de que los datos confidenciales, como contraseñas o claves API, están protegidos y encriptados o, idealmente, no se almacenan en absoluto (sólo sus hashes si es necesario).

### Fiabilidad y resistencia de la red

Hacer frente a las interrupciones de la red, las fluctuaciones del ancho de banda y las conexiones poco fiables puede plantear problemas. Mantener una conexión estable, gestionar las desconexiones con elegancia e implantar mecanismos de reconexión son esenciales para que las aplicaciones en red sean robustas.

#### Buenas prácticas

- Utiliza mensajes de mantenimiento de conexión para detectar conexiones inactivas o caídas.
- Implementa tiempos de espera para evitar bloqueos indefinidos y garantizar la gestión de respuestas a tiempo.
- Implementa la lógica de reconexión exponencial backoff para volver a establecer una conexión si se pierde.

### Mantenibilidad del código

Por último, pero no por ello menos importante, hay que mencionar la mantenibilidad del código. Debido a la naturaleza de bajo nivel de la programación de sockets, los desarrolladores se encuentran escribiendo más código. Esto podría convertirse rápidamente en un código espagueti imposible de mantener, por lo que es esencial organizarlo y estructurarlo lo antes posible y dedicar un esfuerzo adicional a planificar la arquitectura de tu código.

#### Buenas prácticas

- Divide tu código en clases o funciones que, idealmente, no deberían ser demasiado largas.
- Escribe pruebas unitarias desde el principio burlándote de tus implementaciones de cliente y servidor
- Considera la posibilidad de utilizar más bibliotecas de alto nivel para tratar las conexiones, a menos que sea absolutamente necesario utilizar la programación de sockets.

## Resumen Programación de sockets en Python

Los sockets son parte integrante de todas las aplicaciones de red. En este artículo hemos analizado la programación de sockets en Python. Estos son los puntos clave que debes recordar:

- Los sockets son interfaces que abstraen la gestión de las conexiones.
- Los sockets permiten la comunicación entre distintos procesos (normalmente un cliente y un servidor) localmente o a través de una red.
- En Python, el trabajo con sockets se realiza a través de la biblioteca `socket`, que entre otras cosas, proporciona un objeto socket con varios métodos como `recv`, `send`, `listen`, `close`.
- La programación de sockets tiene varias aplicaciones útiles en la ciencia de datos, como la recopilación de datos, la comunicación entre procesos y la informática distribuida.
- Los retos de la programación de sockets incluyen la gestión de conexiones, la integridad de los datos, la escalabilidad, la gestión de errores, la seguridad y el mantenimiento del código.

Con conocimientos de programación de sockets, los desarrolladores pueden crear aplicaciones de red eficaces y en tiempo real. Dominando los conceptos y las mejores prácticas, podrán aprovechar todo el potencial de la programación de sockets para desarrollar soluciones fiables y escalables.

Sin embargo, la programación de sockets es una técnica de muy bajo nivel, difícil de utilizar porque los ingenieros de aplicaciones tienen que tener en cuenta hasta el más mínimo detalle de la comunicación entre aplicaciones.

Hoy en día, muy a menudo no necesitamos trabajar con sockets directamente, ya que suelen gestionarlos las bibliotecas y los marcos de trabajo de nivel superior, a menos que sea realmente necesario exprimir el rendimiento de la aplicación o escalarla.

Sin embargo, comprender los sockets y tener algunas nociones de cómo funcionan las cosas internamente mejora la conciencia general como desarrollador o científico de datos y siempre es una buena idea.

Para saber más sobre el papel de Python en el análisis de redes, consulta nuestro curso [Análisis Intermedio de Redes en Python](https://www.datacamp.com/es/courses/intermediate-network-analysis-in-python). También puedes seguir nuestro programa de [habilidades de programación en Python](https://www.datacamp.com/es/tracks/python-programming) para mejorar tus conocimientos de programación en Python