---
title: "Guía Rápida — Introducción a ROS"
tags: [universidad, 4anyo, robots]
date: 2026-08-13
lang: es
---

# Guía Rápida — Introducción a ROS

Robot Operating System o ROS es una plataforma de desarrollo robótico que permite crear aplicaciones con múltiples sensores y actuadores de forma flexible. Es una colección de herramientas, bibliotecas y convenciones que tiene como objetivo simplificar la tarea de crear un comportamiento de robot complejo y robusto en una amplia variedad de plataformas robóticas.

ROS se creó desde cero para fomentar el desarrollo de software de robótica colaborativa. Por ejemplo, un laboratorio podría tener expertos en el mapeado de ambientes interiores y contribuir con un sistema de clase mundial para producir mapas. Otro grupo podría tener expertos en el uso de mapas para navegar, y otro grupo podría haber descubierto un enfoque de visión por computadora que funciona bien para reconocer pequeños objetos en desorden. ROS fue diseñado específicamente para que grupos de trabajo como estos colaboren y construyan sobre el trabajo de cada uno.

Esta guía rápida pretende ser un punto de partida en el desarrollo de las prácticas de laboratorio de diferentes asignaturas, para que se puedan crear fácilmente aplicaciones tanto en modo nativo ( C++, Python) como en Matlab.

Se puede encontrar más información sobre ROS en su página oficial: www.ros.org

Se recomienda utilizar la máquina virtual proporcionada en la asignatura, en la que ya se encuentra realizada una preinstalación de ROS Noetic y los paquetes más importantes a utilizar en las prácticas ( usuario: alumno; contraseña: alumno).

Si por el contrario se desea instalar ROS Noetic sobre Ubuntu 20.04 en modo nativo ( no se recomienda para la asignatura), deben seguirse las instrucciones dadas en la página http://wiki.ros.org/Installation/Ubuntu ( Desktop-full install, instalación recomendada).

Una vez instalado ROS, ha de configurarse el entorno para poder generar código. Es necesario crear un espacio de trabajo ( workspace) donde se guardarán y compilarán los archivos de los diferentes paquetes creados[^1].

Para ello, desde un terminal de Ubuntu, se realizarán los siguientes pasos:

> Nota: cuidado al copiar y pegar texto en el terminal, ya que algunos caracteres especiales (-, ~), espacios, etc. pueden dar problemas al no copiarse correctamente.

Creación del espacio de trabajo:

```
mkdir –p ~/robotica_movil_ws/src
```

Inicialización del espacio de trabajo:

```
cd ~/robotica_movil_ws/src/
catkin_init_workspace
cd ~/robotica_movil_ws
catkin_make
```

Añadir el espacio de trabajo al path por defecto:

```
sudo gedit ~/.bashrc
```

Añadir al final del fichero estas dos líneas:

```
source ~/robotica_movil_ws/devel/setup.bash
export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/robotica_movil_ws/
```

Cada vez que se modifica el fichero .bashrc se deben cerrar todas las ventanas de terminales abiertas y volver a abrirlas para que se ejecute de nuevo el fichero .bashrc actualizado con las modificaciones.

[^1]: Tutorial de creación de un workspace: http://wiki.ros.org/catkin/Tutorials/create_a_workspace

Se trata de un simulador específicamente creado para ROS ( stdr_simulator[^2]), que permite modelar y simular diferentes robots y sistemas sensoriales dentro de un entorno de movimiento bidimensional.

[^2]: Tutoriales de STDR: http://wiki.ros.org/stdr_simulator

## 3.1 Instalación del simulador

Para instalar el simulador desde las fuentes, se pueden descargar de la página: https://github.com/stdr-simulator-ros-pkg/stdr_simulator.

En caso de usar la máquina virtual, la descarga ya está realizada en la carpeta Downloads. Para instalarlo ha de descomprimirse dentro del directorio robotica_movil_ws/src y a continuación ejecutar:

```
cd ~/robotica_movil_ws
catkin_make
```

Para probar que la instalación es correcta se puede ejecutar la siguiente instrucción:

```
roslaunch stdr_launchers server_with_map_and_gui_plus_robot.launch
```

Deberá aparecer una ventana mostrando el GUI del simulador, con un mapa y un robot cargados.

Para cerrar el simulador, además de cerrar la ventana de la aplicación, es necesario pulsar Ctrl+C en el terminal desde el cual se lanzó.

> Nota: el simulador también puede instalarse desde los repositorios de ROS para Ubuntu con la siguiente instrucción:
> ```
> sudo apt-get install ros-noetic-stdr-simulator
> ```
> Sin embargo, esta versión tiene unos bugs por solucionar, por lo que es aconsejable instalar el simulador a partir de las fuentes como se ha indicado anteriormente.

## 3.2 Creación de un robot

A continuación se muestran los pasos para crear un robot AmigoBot con sus sensores asociados ( iguales a los que utiliza el robot real), que se utilizará en prácticas posteriores:

- Lanzar el simulador, utilizando para ello cualquiera de los ficheros .launch que vienen con la instalación. Por ejemplo, el que carga solo la GUI y un mapa:
  ```
  roslaunch stdr_launchers server_with_map_and_gui.launch
  ```
- Crear un nuevo robot, pulsando en "Create robot" ( tercer botón de la barra de herramientas superior). Por defecto los robots creados tienen forma circular, aunque se pueden definir formas poligonales utilizando la opción "Footprint" para definir los vértices. En este caso, por simplicidad de diseño se creará el robot circular, con las dimensiones del AmigoBot real, que son 33 x 28 cm ( definiendo un radio de 15 cm como aproximación).
- Añadir un sensor láser, pulsando en el botón + en la sección "Lasers". Esto añadirá un láser llamado "laser_1". Seleccionando el botón de edición se pueden modificar sus parámetros. Los robots disponibles en laboratorio tienen instalado un sensor láser de uno de estos dos modelos, cuyos parámetros se indican a continuación ( cada puesto debe configurar el láser del modelo que le corresponda):

  Para simular un láser RPLIDAR-A2:

  - Number of Rays: 400
  - Max distance ( m): 8.0
  - Min distance ( m): 0.15
  - Angle span ( degrees): 360
  - Translation – x ( m): 0.09

  Para simular un láser Hokuyo URG 04LX:

  - Number of Rays: 672
  - Max distance ( m): 5.6
  - Min distance ( m): 0.06
  - Angle span ( degrees): 240
  - Translation – x ( m): 0.09

  Finalmente, pulsar en "update" y guardar el laser_1 en la carpeta "laser_sensors" con el nombre "rplidar_a2.xml" o "hokuyo_urg04lx.xml" ( nota: comprobar que se dispone de permisos de escritura en esa carpeta, ya que dependiendo de la instalación pueden no estar concedidos por defecto).

- Añadir un sensor de ultrasonidos ( sonar), pulsando en el botón + de la sección "Sonars". Esto añadirá un sonar llamado "sonar_1". Seleccionando el botón de edición se pueden configurar los siguientes parámetros para que simule los sónares del robot AmigoBot:
  - Max distance ( m): 5.0
  - Min distance ( m): 0.1
  - Con span ( degrees): 15
  - Frequency: 20
  - Translation – x ( m): 0.076
  - Translation – y ( m): 0.1
  - Orientation: 90

  Finalmente, pulsar en "update" y guardar el sonar_1 en la carpeta "range_sensors" con el nombre "sonar_amigobot.xml".

- Crear el anillo de ultrasonidos, añadiendo otros 7 sonares más ( de sonar_2 a sonar_8). Para ello, se puede cargar para cada sonar los datos de "sonar_amigobot.xml" y a continuación modificar el parámetro de orientación y posición según la siguiente tabla:

| Sónar | X | Y | Orientación (º) | Orientación ( rad) |
|---|---|---|---|---|
| 0 | 0.076 | 0.1 | 90 | 1.5708 |
| 1 | 0.125 | 0.075 | 41 | 0.715585 |
| 2 | 0.150 | 0.03 | 15 | 0.261799 |
| 3 | 0.150 | -0.03 | -15 | -0.261799 |
| 4 | 0.125 | -0.075 | -41 | -0.715585 |
| 5 | 0.076 | -0.1 | -90 | -1.5708 |
| 6 | -0.14 | -0.058 | -145 | -2.53073 |
| 7 | -0.14 | 0.058 | 145 | 2.53073 |

- Guardar el robot con el nombre "amigobot.xml" en la sección "Robot".
- Añadir el robot, pulsando en el segundo botón de la barra de herramientas ( Load robot), seleccionando el robot recién creado y a continuación pulsando en la posición del mapa en la que se quiere que se posicione. ( Nota: si se obtiene un error al cargar el robot, editar el archivo amigobot.xml y eliminar la sección `<kinematics>` completa.)
- Modificar el robot: una vez generado, el archivo .xml puede modificarse de forma sencilla. Por coherencia con la numeración de sensores del AmigoBot se recomienda modificar el archivo para que los sonar vayan desde sonar_0 a sonar_7.

## 3.3 Simulador: mapa

Los mapas en ROS vienen definidos por un archivo de imagen ( habitualmente en formato png) y un archivo de descripción .yaml. Un ejemplo de archivo de descripción típico es el siguiente:

- `image: sparse_obstacles.png` : indica el archivo de imagen a cargar.
- `resolution: 0.02` : en metros por píxel.
- `origin: [0.0, 0.0, 0.0]` : origen del mapa ( x, y, orientación).
- `occupied_thresh: 0.6` : los píxeles con más de esta ocupación ( escala de grises) se consideran ocupados.
- `free_thresh: 0.3` : los píxeles por debajo de esta ocupación ( escala de grises) se consideran libres.
- `negate: 0` : si está a 0, los píxeles que tienden a blanco son libres y los negros ocupados; si está a 1, se invierte esta consideración.

En este apartado se explican algunos de los conceptos básicos para comenzar a trabajar con ROS.

## 4.1 Roscore

ROS necesita un nodo maestro en ejecución continuamente. Este nodo se encarga de coordinar y sincronizar todo el sistema de nodos/topics/servicios. Para ejecutarlo, debe teclearse en un terminal:

```
roscore
```

Nota: si se ejecuta algún programa mediante roslaunch ( se verá más adelante), este se encargará de ejecutar roscore automáticamente.

## 4.2 Nodos

Cada programa en ejecución dentro de ROS se considera un nodo. Los nodos se comunican entre sí mediante "topics" y "servicios".

Para monitorizar y obtener información de los nodos que están en ejecución en un determinado momento, se dispone de la herramienta `rosnode`. A modo de ejemplo, mientras se ejecuta el simulador con la prueba de instalación, se puede hacer uso de esta herramienta en otro terminal. Los comandos más utilizados son:

- `rosnode list` : devuelve una lista de los nodos que están activos. En el ejemplo que nos ocupa, `rosnode list` devuelve:
 ```
 /robot_manager
 /rosout
 /stdr_gui_node_c3po_12711_4502575229393065819
 /stdr_server
 /world2map
 ```
- `rosnode info "nombre_nodo"` : devuelve información de ese nodo, como sus publicaciones, sus subscripciones, los servicios que ofrece y sus conexiones con los demás nodos.
- `rosnode kill "nombre_nodo"` : elimina un nodo de la ejecución.

Una forma cómoda de visualizar todos los nodos que se encuentran en ejecución en un determinado momento es ejecutar la herramienta `rqt` en un terminal y a continuación cargar el plugin "plugin/introspection/node_graph" con la vista "nodes only", obteniéndose un grafo con los nodos activos.

## 4.3 Topics

Los topics son canales de comunicación que utilizan un tipo de mensaje determinado para enviar información de un nodo a otro. La conexión puede ser de tipo n:m ( varios a varios), es decir que varios nodos pueden escribir en el mismo topic y varios nodos pueden leer el mismo topic. La única limitación es que cada topic solamente admite datos de un único tipo, por lo que si se quieren transmitir varios tipos de datos entre dos nodos habrá que crear un topic para cada uno de ellos.

La herramienta `rostopic` permite inspeccionar estos canales de comunicación. Sus comandos más útiles son:

- `rostopic list` : lista todos los topics activos en el sistema.
- `rostopic info "nombre_topic"` : muestra la información del topic indicado: tipo de dato que transmite, nodos que están publicando en el topic y nodos que están leyendo de él.
- `rostopic type "nombre_topic"` : muestra la información del tipo de dato que se transmite por el topic.
- `rostopic echo "nombre_topic"` : crea un "subscriber" desde línea de comandos y vuelca a pantalla los datos que se están transmitiendo por ese topic.
- `rostopic pub "topic" "tipo de dato" "datos"` : permite publicar datos en un topic desde consola, generando un "publisher". Por ejemplo:
 ```
 rostopic pub --once /robot0/cmd_vel geometry_msgs/Twist '{ linear : { x : 0.2} }'
 ```

  publicará durante 3 segundos una velocidad lineal de 0.2 m/s al robot.

Al igual que con los nodos, se puede realizar una inspección visual de los topics mediante la herramienta `rqt`, en este caso seleccionando el plugin "plugin/introspection/node_graph" y la vista "node/topics ( active)", que muestra en elipses los nodos y en cuadrados los topics con los que se comunican.

La herramienta `rqt` también permite visualizar el valor de los campos numéricos de los topics. Para ello se ejecuta el plugin "plugin/Visualization/plot" y se añade el campo que se quiera mostrar gráficamente. Por ejemplo, se puede representar la posición en coordenadas cartesianas del robot añadiendo los campos "/robot0/odom/pose/pose/position/x" y "/robot0/odom/pose/pose/position/y"; se visualiza de manera continua, con el eje y como valor del campo y el eje x como el instante en que se ha recibido ( aunque los datos se reciben en tiempos discretos).

## 4.4 Servicios

Los servicios proporcionan otra manera de comunicación entre nodos. Esta comunicación, en vez de ser continua, es del tipo "llamada-respuesta", por lo que suele utilizarse para eventos especiales como resetear una simulación, etc.

La herramienta que permite gestionar los servicios en modo comando es `rosservice`, y sus opciones más utilizadas son:

- `rosservice list` : lista los servicios que hay activos.
- `rosservice info "nombre_servicio"` : muestra la información de un servicio: su tipo y qué nodo lo publica.
- `rosservice call "nombre_servicio" "argumentos"` : sirve para llamar a un servicio desde consola de comandos. Por ejemplo:
 ```
 rosservice call /robot_manager/list "{}"
 ```

  Este servicio proporciona como respuesta cuántos robots hay activos en el simulador.

## 4.5 Rosbag

Rosbag es un conjunto de herramientas que permite guardar datos durante la ejecución de un programa para posteriormente poder reproducirlos de nuevo. Las instrucciones más importantes de esta herramienta son:

- `rosbag record –a` : guarda en un archivo toda la información ( topics) en ejecución en el programa.
- `rosbag record "nombre de topics"` : guarda solamente la información de los topics indicados. Es conveniente salvar siempre el topic "tf" para mantener la información sobre el estado del sistema.
- `rosbag play "archivo.bag"` : vuelve a ejecutar los datos guardados en un archivo. Útil para la depuración y análisis de resultados a posteriori.

## 4.6 TF ( Transformadas)

`/tf` es un topic especial de ROS que está siempre presente y sirve para relacionar los distintos marcos de coordenadas que existen en el sistema. Es gestionado por un paquete llamado TF, que incluye múltiples utilidades para trabajar con los marcos de coordenadas y gestionar sus transformaciones ( se verá en detalle en prácticas posteriores). La relación entre los sistemas de coordenadas, incluso cuando es constante a lo largo del tiempo, ha de publicarse de forma continua en el topic `/tf` para que el resto de nodos pueda utilizar esta información.

Usualmente, cada topic contiene información referida a un sistema de coordenadas. Este sistema de coordenadas se encuentra indicado explícitamente en la cabecera del tipo de datos ( campo `frame_id`), con excepción de algunos tipos de datos que no están referidos a ningún marco de referencia y carecen de ese campo ( por ejemplo, los datos de tipo entero).

Para visualizar el árbol de transformadas se puede utilizar la herramienta `rqt`, plugin "plugins/visualization/TF Tree", que mostrará la relación entre los distintos marcos de coordenadas, así como quién genera cada transformada y con qué frecuencia la actualiza.

En el ejemplo que nos ocupa, existe un marco base de coordenadas llamado "world" relacionado con otro marco de coordenadas llamado "map". Esta relación la realiza el nodo "world2map", que publica una transformada estática entre ambos. A su vez, el marco "map" está relacionado por una transformada estática enviada por el simulador ( stdr_server) con el marco de coordenadas "map_static". Los marcos de coordenadas del mapa ( map_static) y el robot ( robot0) están relacionados por la odometría del mismo, relación que cambia conforme se mueve el robot y está publicada por el simulador ( nodo robot_manager). También existen una serie de transformadas entre el robot y sus diferentes sensores, publicadas igualmente por el simulador.

Hay que tener en cuenta una restricción importante a la hora de crear un árbol de transformadas en ROS: un marco de referencia puede tener varios "hijos" pero solamente un único "padre". De tal forma que siempre existirá un único elemento raíz ( comúnmente "world" o "map" en sistemas de robots móviles) del que irán colgando los distintos elementos que existen en el entorno ( distintos robots, sensores del entorno, etc.).

## 4.7 Ejecución de un programa

Para la ejecución de un programa en ROS existen dos maneras: el comando `rosrun` y el comando `roslaunch`.

**Rosrun**: este comando permite ejecutar un único nodo siempre que exista un nodo "roscore" activo. Su formato es el siguiente:

```
rosrun "nombre_paquete" "nombre_nodo" "argumentos"
```

Los argumentos que se pueden pasar a un programa son de tres tipos:

- Redirecciones: se puede modificar el nombre de los topics en los que un nodo escucha o publica. El formato para ello es `nombre_topic:=nuevo_nombre_topic`.
- Parámetros: algunos nodos aceptan parámetros de configuración ( publicados en el servidor de parámetros de ROS, gestionable mediante las instrucciones `rosparam`). Para indicar estos parámetros ha de escribirse `_nombre_parámetro:=valor_parámetro`.
- Argumentos clásicos: algunos nodos aceptan parámetros en el formato clásico de C/C++. Para incluirlos simplemente hay que escribir estos parámetros ( dependiendo del parser del nodo en cuestión) a continuación del nombre del nodo.

Como ejemplo, se puede ejecutar un nodo que permite teleoperar el robot en el simulador:

```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py cmd_vel:=/robot0/cmd_vel _speed:=0.3 _turn:=0.5
```

Esta instrucción ejecuta el nodo "teleop_twist_keyboard.py" que se encuentra dentro del paquete "teleop_twist_keyboard". Se realiza una redirección de topics cambiando el topic en el que escribe por defecto ( cmd_vel) al del robot (/robot0/cmd_vel). También se modifican dos parámetros ( speed y turn), limitando la velocidad máxima comandada a 0.3 m/s de velocidad lineal y 0.5 rad/s de velocidad angular.

**Roslaunch**: dada la complejidad que puede conllevar la ejecución de ROS, se utilizan los comandos roslaunch a modo de "script" para lanzar distintos nodos en una única instrucción. Un detalle importante es que el archivo .launch ejecuta automáticamente un nodo "roscore" en caso de que el mismo no se encuentre activo.

El formato de ejecución es el siguiente:

```
roslaunch "nombre_paquete" "fichero.launch"
```

Para que un archivo pueda ser ejecutado ha de encontrarse dentro de la carpeta /launch del paquete correspondiente. El fichero roslaunch puede ejecutar distintos nodos, incluir ficheros de configuración de parámetros e incluso incluir otros ficheros .launch.

En los siguientes apartados se explica cómo crear un nodo de ROS y cómo lanzar aplicaciones formadas por uno o más nodos a través de ficheros .launch.

## 5.1 Creación de un paquete

Los programas en ROS se agrupan en paquetes. Un paquete puede contener múltiples nodos, ficheros de configuración, etc., destinados todos ellos a conseguir una aplicación final concreta.

Como ejemplo, se va a crear a continuación un paquete para realizar la práctica 1. Los paquetes deben crearse dentro del directorio "/src" del espacio de trabajo, del siguiente modo:

```
cd ~/robotica_movil_ws/src
catkin_create_pkg practica_1 std_msgs rospy roscpp tf
```

De esta manera se ha creado un paquete de nombre "practica_1" que depende de varios paquetes estándar de ROS ( mensajes estándar, librerías de C++ y Python, y paquete de transformadas).

Un paquete por defecto contiene los siguientes directorios y archivos de importancia:

- `src/`: directorio donde se encontrarán los archivos fuente pertenecientes al paquete.
- `include/`: directorio donde se encontrarán las cabeceras de los archivos pertenecientes al paquete.
- `msg/`: directorio donde se encontrarán los tipos de mensaje definidos en el paquete.
- `srv/`: directorio donde se encontrarán los servicios definidos en el paquete.
- `launch/`: directorio donde se encontrarán los scripts de lanzamiento ( archivos .launch) pertenecientes al paquete.
- `package.xml`: archivo de descripción del paquete requerido para poder compilarlo. Incluye una descripción del paquete así como sus dependencias.
- `CMakeLists.txt`: archivo para poder compilar haciendo uso de CMake.

## 5.2 Creación de un fichero .launch

Los ficheros .launch permiten lanzar simultáneamente un conjunto de nodos. A modo de ejemplo, se va a crear a continuación un archivo "amigobot.launch", basado en el fichero "server_with_map_and_gui.launch", que permitirá lanzar el simulador con el robot amigobot creado en un apartado previo.

Para poder ejecutar el archivo correctamente ha de encontrarse dentro de la carpeta /launch de un paquete, por lo que se crea el directorio "~/robotica_movil_ws/src/practica_1/launch/" y dentro de él el archivo amigobot.launch de la siguiente manera:

```xml
<launch>
 <!-- Inclusión de otro archivo .launch el cual lanza un nodo que proporciona la descripción del robot a ROS -->
 <include file="$( find stdr_robot)/launch/robot_manager.launch" />
 <!-- Nodo que lanza el mapa con el que trabajarán ROS y STDR. Se pasa la descripción del mapa (.yaml) como
 parámetro clásico ( campo args). Se modifica el mapa respecto al original para representar un mapa
 de tipo laberinto. -->
 <node type="stdr_server_node" pkg="stdr_server" name="stdr_server"
 output="screen" args="$( find stdr_resources)/maps/robocup.yaml"/>
 <!-- Nodo que genera la relación entre los marcos de coordenadas map ( mapa del simulador) y world ( marco
 de coordenadas raíz). Se indica esta relación como argumentos del nodo, siguiendo el formato
 "x y z yaw pitch roll frame_origen frame_destino frecuencia" -->
 <node pkg="tf" type="static_transform_publisher" name="world2map"
 args="0 0 0 0 0 0 world map 100" />
 <!-- Inclusión de archivo .launch que lanza la interfaz gráfica del simulador -->
 <include file="$( find stdr_gui)/launch/stdr_gui.launch"/>
 <!-- Nodo que carga el robot Amigobot creado en la posición ( 4,8,0) -->
 <node pkg="stdr_robot" type="robot_handler" name="$( anon robot_spawn)"
 args="add $( find stdr_resources)/resources/robots/ amigobot.xml 4 8 0" />
</launch>
```

Para lanzar esta simulación, se ejecuta el fichero .launch anterior del siguiente modo:

```
roslaunch practica_1 amigobot.launch
```

y se observará la pantalla del simulador con el robot cargado.

## 5.3 Esqueleto genérico de un programa ( nodo)

A continuación se muestra el esqueleto básico de programación de un nodo en C++, con los comentarios necesarios para su comprensión. Este esqueleto puede descargarse de la página web de la asignatura ("esqueleto.cpp"). Básicamente, este programa crea una clase ("practica_1_node") que contiene, además de los "subscribers" y "publishers" para los diferentes topics, las llamadas ( callbacks) a las funciones que se ejecutan cada vez que se lee un dato en alguno de estos topics. Además, se crea un reloj relacionado con una llamada ("spin"), el cual de forma periódica lleva a cabo la tarea principal de procesamiento del nodo.

```cpp
// INCLUIR LA LIBRERIA DE ROS
// INCLUIR LOS TIPOS DE DATOS A USAR
```

Para cada tipo de dato que se quiera utilizar se necesita añadir el include de la librería que lo contiene. En este ejemplo no se utilizan todos los que aparecen arriba. El listado de los tipos de datos más comunes se encuentra en: estándar http://wiki.ros.org/std_msgs; sensores http://wiki.ros.org/sensor_msgs; navegación ( mapas, planificadores) http://wiki.ros.org/nav_msgs. Por otro lado, "tf.h" es la librería de transformadas por si fuera necesaria.

```cpp
// INCLUIR RESTO DE LIBRERIAS A UTILIZAR
// DECLARAR LA CLASE
class practica_1_node{
public:
 // DECLARAR EL CONSTRUCTOR
 practica_1_node ();
 // DECLARAR LAS FUNCIONES Y CALLBACKS A UTILIZAR
 void odomCallback ( const boost::shared_ptr<nav_msgs::Odometry const>& msg);
```

Este callback se asociará ( en el constructor de la clase) al subscriber "odom_sub", de manera que se ejecutará cada vez que llegue un nuevo dato de odometría al topic subscrito. En la declaración del callback ha de indicarse explícitamente el tipo de dato que va a escuchar, en este caso de tipo odometría.

```cpp
 // DECLARAR EL CALLBACK CON TEMPORIZADOR
 void spin ( const ros::TimerEvent& e);
```

Este callback se asociará ( en el constructor de la clase) al timer "timer_", de manera que se ejecutará periódicamente con la frecuencia indicada.

```cpp
private:
 // DECLARAR LOS SUBSCRIBER Y PUBLISHER
 ros::Subscriber odom_sub_;
```

Declaración del "subscriber" que se suscribirá al topic de odometría.

```cpp
 ros::Publisher cmd_vel_pub_;
```

Declaración del "publisher" que publicará en el topic de velocidad.

```cpp
 // DECLARAR EL TIMER
 ros::Timer timer_;
```

Declaración de un "timer" de ROS.

```cpp
};
// CALLBACK
void practica_1_node::odomCallback ( const boost::shared_ptr<nav_msgs::Odometry const>& msg)
{
 // En este callback hay que escribir lo que se desea que se ejecute cada vez que llegue un
 // dato nuevo al topic de odometría.
}
// CALLBACK DEL TIMER
void practica_1_node::spin ( const ros::TimerEvent& e)
{
 // En este callback hay que escribir lo que se desea que se ejecute cada vez que llegue un
 // nuevo tic del timer. Aquí suele ejecutarse la base del programa, si se desea que esta sea
 // periódica.
}
// CONSTRUCTOR DE LA CLASE
practica_1_node::practica_1_node (){
 // MANEJADOR DE NODOS DE ROS
 ros::NodeHandle n ("~");
```

Instrucción de ROS necesaria para crear un manejador del nodo de ROS.

```cpp
 // SUBSCRIBERS
 odom_sub_ = n.subscribe<nav_msgs::Odometry> ("/robot0/odom", 1,
 &practica_1_node::odomCallback, this);
```

Esta instrucción inicializa el subscriber "odom_sub_" para el nodo "n". Este subscriber permite escuchar un topic ( en este caso "/robot0/odom") y le asocia un callback que se ejecutará cuando lleguen mensajes al mismo ( en este caso "odomCallback"). Debe indicarse el tipo de mensaje del topic, que en este caso es "nav_msgs::Odometry". El tamaño de la cola de escucha en este caso es 1, lo cual significa que se queda solo con el último dato. Si se aumenta este número se pueden almacenar más datos para el caso de que no dé tiempo a procesarlos.

```cpp
 // PUBLISHERS
 cmd_vel_pub_ = n.advertise<geometry_msgs::Twist> ("/robot0/cmd_vel", 1, true);
```

Esta instrucción inicializa el publisher "cmd_vel_pub_" para el nodo "n". Este publisher permite publicar mensajes en un topic ( en este caso "/robot0/cmd_vel") cuyo tipo se indica ("geometry_msgs::Twist"). El tamaño de la cola de publicación en este caso es 1, lo cual significa que solo se almacena el último dato publicado.

```cpp
 // TIMER
 timer_ = n.createTimer ( ros::Duration ( 0.1), &practica_1_node::spin, this);
```

Esta instrucción inicializa el timer "timer_" para el nodo "n". Este timer tendrá una frecuencia de 10 Hz ("ros::Duration ( 0.1)") y ejecutará el callback "spin" cada vez que se cumpla un periodo del mismo.

```cpp
 // INICIALIZAR VARIABLES
}
// PROGRAMA PRINCIPAL
int main ( int argc, char **argv)
{
 // INICIALIZAR ROS
 ros::init ( argc, argv, "practica_1_node");
```

Creación del nodo de ROS, con nombre "practica_1_node".

```cpp
 // CARGAR LA CLASE
 practica_1_node pr1_node;
```

Se declara e inicializa la clase creada. En este momento se ejecuta el constructor de la clase, que crea los subscribers, publishers y timers, y los asocia a sus callbacks.

```cpp
 // LANZAR EL NODO
 ros::spin ();
```

Al llegar a esta instrucción el programa queda ejecutándose de manera indefinida, leyendo los topics suscritos.

```cpp
}
```

## 5.4 Ejemplo de programa: mover el robot un metro hacia adelante

En este apartado, y basándose en el esqueleto anterior, se va a crear un nodo de nombre "practica_1_node" que haga avanzar el robot un metro en línea recta. El código de la aplicación debe guardarse en un archivo, dentro de la carpeta "~/robotica_movil_ws/src/practica_1/src", con nombre "practica_1_node.cpp".

```cpp
// INCLUIR LA LIBRERIA DE ROS
// INCLUIR LOS TIPOS DE DATOS A USAR
// INCLUIR RESTO DE LIBRERIAS A UTILIZAR
// DECLARAR LA CLASE
class practica_1_node{
public:
 // DECLARAR EL CONSTRUCTOR
 practica_1_node ();
 // DECLARAR LAS FUNCIONES Y CALLBACKS A UTILIZAR
 void odomCallback ( const boost::shared_ptr<nav_msgs::Odometry const>& msg);
 // DECLARAR EL CALLBACK CON TEMPORIZADOR
 void spin ( const ros::TimerEvent& e);
private:
 // DECLARAR LOS SUBSCRIBER Y PUBLISHER
 ros::Subscriber odom_sub_;
 ros::Publisher cmd_vel_pub_;
 // DECLARAR EL TIMER
 ros::Timer timer_;
 // DECLARAR LAS VARIABLES A USAR
 nav_msgs::Odometry actualOdom, initOdom;
 geometry_msgs::Twist cmd_vel;
 int init;
 double dist;
 // Declaramos las variables que vamos a utilizar para esta aplicación
};
// CALLBACK
void practica_1_node::odomCallback ( const boost::shared_ptr<nav_msgs::Odometry const>& msg)
{
 // SALVAR LA ULTIMA ODOMETRÍA LEIDA
 actualOdom=*msg;
 // CUANDO LA PRIMERA ODOMETRÍA HAYA SIDO LEIDA, ACTIVAR FLAG
 if (!init)
 {
 init=1;
 }
}
```

En el callback de la odometría simplemente se almacena el mensaje de odometría recibido en la variable "actualOdom", para que esté actualizada y pueda usarse en otros lugares del programa. Además, la primera vez que se recibe un dato de odometría se pone la variable "init" a 1 para gestionar una máquina de estados que controla la ejecución del programa dentro del callback del timer "spin".

```cpp
// CALLBACK DEL TIMER
void practica_1_node::spin ( const ros::TimerEvent& e)
{
 // SI SE HA LEIDO AL MENOS UNA ODOMETRÍA, TOMARLA COMO POSICIÓN DE INICIO
 if ( init==1)
 {
 initOdom=actualOdom;
 init=2;
 }
 // SI YA TENEMOS LA POSICION DE INICIO, COMENZAMOS EL CONTROL
 if ( init==2)
 {
 // CALCULAR LA DISTANCIA RECORRIDA
 dist=sqrt ( pow ( initOdom.pose.pose.position.x - actualOdom.pose.pose.position.x,2) +
 pow ( initOdom.pose.pose.position.y - actualOdom.pose.pose.position.y,2));
 // MOSTRAR POR PANTALLA LA POSICIÓN ACTUAL Y LA DISTANCIA RECORRIDA
 ROS_INFO ("ACTUAL POSITION X %f Y %f THETA %f DISTANCE TRAVELLED %f \n",
 actualOdom.pose.pose.position.x, actualOdom.pose.pose.position.y,
 tf::getYaw ( actualOdom.pose.pose.orientation), dist);
 // SI SE HA RECORRIDO MENOS DE UN METRO, MOVER EL ROBOT. EN CASO CONTRARIO, DETENER EL ROBOT
 if ( dist<1)
 {
 cmd_vel.linear.x=0.2;
 cmd_vel.linear.y=0.0;
 cmd_vel.angular.z=0.0;
 cmd_vel_pub_.publish ( cmd_vel);
 }
 else
 {
 cmd_vel.linear.x=0.0;
 cmd_vel.linear.y=0.0;
 cmd_vel.angular.z=0.0;
 cmd_vel_pub_.publish ( cmd_vel);
 }
 }
}
```

En el callback del timer se realiza el control real del programa, gestionado generalmente mediante una máquina de estados. En este caso, hasta que no se ha leído un mensaje de odometría ( init=0) no se realiza ninguna acción. Una vez que se ha leído un mensaje de odometría ( init=1), se almacena como posición inicial del robot y se pasa al estado init=2, en el cual periódicamente ( cada vez que sucede un evento en el timer) se calcula la distancia avanzada por el robot ( distancia entre actualOdom e initOdom); si esta distancia es menor que un metro, se publica un mensaje de velocidad lineal de 0.2 m/s en el topic "cmd_vel". En caso contrario, se detiene el robot publicando una velocidad lineal de 0 m/s.

```cpp
// CONSTRUCTOR
practica_1_node::practica_1_node (){
 // MANEJADOR DE NODOS DE ROS
 ros::NodeHandle n ("~");
 // SUBSCRIBERS
 odom_sub_ = n.subscribe<nav_msgs::Odometry> ("/robot0/odom", 1,
 &practica_1_node::odomCallback, this);
 // PUBLISHERS
 cmd_vel_pub_ = n.advertise<geometry_msgs::Twist> ("/robot0/cmd_vel", 1, true);
 // TIMER
 timer_ = n.createTimer ( ros::Duration ( 0.1), &practica_1_node::spin, this);
 // INICIALIZAR VARIABLES
 init=0; // El estado inicial de la máquina de estados se pone a 0
 dist=0; // Inicialmente la distancia recorrida es 0
}
// PROGRAMA PRINCIPAL
int main ( int argc, char **argv)
{
 // INICIALIZAR ROS
 ros::init ( argc, argv, "practica_1_node");
 // CARGAR LA CLASE
 practica_1_node pr1_node;
 // LANZAR EL NODO
 ros::spin ();
}
```

## 5.5 Compilación y ejecución del nodo

Para poder compilar un paquete ( con todos los nodos que contenga) se hace uso de la herramienta catkin. Esta herramienta de ROS ejecuta distintos comandos CMake en cada uno de los paquetes dentro de un workspace.

Para poder compilar nodos es necesario modificar el archivo "CMakeLists.txt" dentro del directorio del paquete. Para compilar el primer programa de ejemplo habrá que descomentar las siguientes líneas:

```
add_executable ( practica_1_node src/practica_1_node.cpp)
```

Se indica la creación del ejecutable practica_1_node a partir del archivo fuente src/practica_1_node.cpp.

```
target_link_libraries ( practica_1_node ${catkin_LIBRARIES})
```

Se indica que compile el ejecutable practica_1_node haciendo uso de las librerías catkin por defecto.

Esto permitirá compilar el nodo "practica_1_node" haciendo uso de la instrucción "catkin_make" desde el directorio raíz del espacio de trabajo. Para añadir nuevos nodos habría que crear más líneas en el archivo de manera similar.

Por lo tanto, para compilar el nodo se ejecutará:

```
cd ~/robotica_movil_ws
catkin_make
```

Y tras compilarlo, para ejecutarlo ( estando ya el simulador abierto), se escribirá:

```
rosrun practica_1 practica_1_node
```

RViz es un programa que sirve para visualizar los distintos datos que existen dentro de una ejecución de ROS. Este programa está dotado de plugins que permiten representar los tipos de datos más comunes, tales como odometría, láser, sónar, mapas, etc.

Para ejecutar RViz, con una ejecución de ROS iniciada ( nodo roscore activo), solamente ha de teclearse `rosrun rviz rviz`. En caso de que la máquina sobre la que se esté ejecutando no soporte el software de aceleración OpenGL, habría que añadir antes el comando `export LIBGL_ALWAYS_SOFTWARE=1`.

Una vez abierto el programa se puede dividir la pantalla en cinco secciones:

- Barra superior: permite cambiar entre herramientas para mover la visualización, obtener datos de la misma o incluso enviar algunos comandos de posición.
- Barra inferior: muestra el tiempo de ROS.
- Barra izquierda: en ella se añaden los distintos datos a representar.
- Barra derecha: permite cambiar el punto de vista de la visualización.
- Ventana central: muestra la visualización como tal. Por defecto se muestra una rejilla vacía.

En la sección "Displays", un parámetro importante que se puede modificar es Fixed Frame, que indica el marco de coordenadas que se va a utilizar en la visualización. En el caso de nuestra simulación, si se quiere representar el mapa, se puede elegir "world", "map" o "map_static".

Para visualizar los distintos datos hay que pulsar el botón Add. Si se conoce el tipo de dato a representar se puede añadir "By Type", pero es más sencillo añadirlo con la opción "By Topic", puesto que solamente aparecerán los topics activos en el sistema en ese momento.

Algunos de los tipos de datos que se pueden visualizar son los siguientes:

**Map**: representación de un mapa de tipo rejilla de ocupación. Permite representar los datos en dos formatos:

- Map: en negro se representan las celdas ocupadas, en gris claro las celdas libres y en gris oscuro las celdas desconocidas.
- Costmap: se visualiza la ocupación de cada celda en distintos colores.

**Odometría ( Odometry)**: permite representar la posición del robot dentro del mapa como una flecha. Para obtener el recorrido del robot se puede variar el número de posiciones acumuladas a representar ( variable Keep). También se pueden variar el tamaño y color de las flechas para representar distintos robots en el mismo mapa.

**Láser ( LaserScan)**: permite representar las medidas de un sensor láser. Haciendo uso de las transformadas entre marcos de coordenadas, pinta sobre el mapa los impactos del láser ( no representa las medidas máximas del mismo). Mediante sus parámetros se puede modificar el tamaño de los impactos a representar, así como colorearlos de distintas maneras ( en colores planos, dependiendo del valor en alguno de sus ejes, por intensidad, etc.).

**Sensores de distancia ( Range)**: se pueden añadir sensores de distancia sónar o ultrasonidos a la visualización. Se representan como un cono dependiendo de su apertura, con una distancia proporcional a su medida.

**Árbol de transformadas ( TF)**: representa el eje de coordenadas de cada uno de los marcos de coordenadas del sistema, así como las relaciones entre ellos.

Una vez añadidos los topics a mostrar y modificado el punto de vista al deseado, se puede guardar esta configuración mediante el comando "file/save config as" y cargarla de nuevo al abrir el visualizador con:

```
rosrun rviz rviz -D "nombre guardado"
```

RViz posee además por defecto algunas herramientas con las que se puede interactuar, como "2D Pose Estimate" o "2D Nav Goal", que interactúan con los paquetes de navegación que se verán en prácticas posteriores.

Por otra parte, RViz tiene sus limitaciones y no permite visualizar todos los tipos de datos por defecto. Un dato muy habitual es el tipo "posewithcovariancestamped", que no puede ser visualizado directamente, por lo que se suelen desarrollar nodos intermedios para la visualización, o plugins que convierten estos datos a otros que pueda manejar RViz.

Tal y como se ha mostrado en los apartados anteriores, ROS presenta una arquitectura de programación distribuida, en la que diferentes nodos se comunican entre sí a través de mensajes enviados a los topics. Yendo un poco más allá, ROS permite que estos nodos se distribuyan en diferentes máquinas comunicadas por una red, para ajustarse a los recursos disponibles. Configurar ROS en un sistema multimáquina es sencillo, teniendo en cuenta los siguientes aspectos:

- Solo es necesario un Master de ROS ( roscore), que se ejecutará en una de las máquinas.
- Todas las máquinas deben conocer dónde se ejecuta el Master, lo cual se indica configurando en todas ellas ( incluida la propia máquina en la que se ejecuta) la variable de entorno ROS_MASTER_URI, del siguiente modo:
 ```
 export ROS_MASTER_URI=http://IP_ROSMASTER_MACHINE:11311
 ```

  donde IP_ROSMASTER_MACHINE es la dirección IP de la máquina que ejecuta el Máster.

- Si existe conectividad completa entre las máquinas a través de la red, los topics creados por cada una de ellas serán accesibles a todas las demás. Para ello, cada máquina debe comunicar su propia dirección de red dentro del sistema ROS a través de la variable de entorno ROS_IP, del siguiente modo:
 ```
 export ROS_IP=IP_LOCAL_MACHINE
 ```

  donde IP_LOCAL_MACHINE es la dirección IP de la propia máquina.

Se recomienda configurar las variables de entorno anteriores en el fichero .bashrc, editándolo y añadiéndolas al final.

Para comprobar que la conectividad es correcta, puede ejecutarse un `rostopic list` en todas las máquinas y comprobar que se tiene acceso a todos los topics creados por todos los nodos en cualquiera de las máquinas.

MATLAB dispone de la toolbox "Robotics System Toolbox", que permite crear nodos en Matlab/Simulink con conectividad al sistema ROS. Esto permite realizar aplicaciones sencillas de manera más rápida que programando en C++ y compilando en ROS nativo, por lo que se va a utilizar para desarrollar buena parte de las prácticas.

Para comprender la conexión entre Matlab y ROS y sus diferencias con la programación en ROS nativo, vamos a realizar el mismo programa que mueve el robot un metro en el entorno desde Matlab.

## 8.1 Configuración de la red

Si se está ejecutando Matlab ( con Robotics Toolbox instalada) y ROS en máquinas distintas ( en el caso del laboratorio, Matlab se ejecutará en el sistema operativo anfitrión Windows y ROS en una máquina virtual bajo Ubuntu), ha de configurarse la red de tal manera que exista conexión entre ellas. Para ello se recomienda comprobar que todos los ordenadores que se están empleando en el sistema ( incluida la máquina virtual) se encuentran en la misma red y todos son visibles entre sí ( emplear la herramienta ping para comprobar la visibilidad). Si se están empleando ordenadores que no son los propios del laboratorio, se recomienda conectarse a la red WiFi identificada como:

- Essid: AmigobotWiFi
- Password: Robotica1718!

El Máster de ROS ( roscore) se ejecutará únicamente en una de las máquinas ( en nuestro caso, en la máquina virtual con el simulador o en el robot real), y el resto de nodos deben conocer la dirección IP de la máquina en la que se ejecuta el máster.

Para conocer la dirección IP actual de la máquina virtual debe abrirse un terminal y ejecutarse el comando:

```
ifconfig
```

Se mostrará una tabla de información en la que la dirección IP se encuentra en ethX -> Direc. Inet.

Para configurar correctamente estas variables de entorno con la dirección IP actual de la máquina virtual debe editarse el fichero .bashrc:

```
cd
gedit .bashrc
```

Al final del fichero hay que añadir las siguientes líneas con la IP obtenida anteriormente:

```
export ROS_MASTER_URI=http://192.168.58.128:11311
export ROS_IP=192.168.58.128
```

## 8.2 Programa cliente

Una vez configurada la red, se ha de escribir el programa cliente en Matlab. Para ello se abre un editor ( comando edit) y se codifica el archivo ejemplo_1.m de la siguiente manera:

```matlab
%% INICIALIZACIÓN DE ROS
rosinit ('http://192.168.58.128:11311','NodeHost','IP_LOCAL_MACHINE')
% Inicialización de ROS con IP del master y puerto por defecto 11311, y la
% dirección IP de la máquina donde se ejecuta Matlab ( IP_LOCAL_MACHINE)
%% DECLARACIÓN DE SUBSCRIBERS
odom=rossubscriber ('/robot0/odom'); % Subscripción a la odometría
%% DECLARACIÓN DE PUBLISHERS
pub = rospublisher ('/robot0/cmd_vel', 'geometry_msgs/Twist');
%% GENERACIÓN DE MENSAJE
msg=rosmessage ( pub) % Creamos un mensaje del tipo declarado en "pub" ( geometry_msgs/Twist)
% Rellenamos los campos del mensaje para que el robot avance a 0.2 m/s
% Velocidades lineales en x,y y z ( velocidades en y o z no se usan en robots
% diferenciales y entornos 2D)
msg.Linear.X=0.2;
msg.Linear.Y=0;
msg.Linear.Z=0;
% Velocidades angulares ( en robots diferenciales y entornos 2D solo se utiliza el valor Z)
msg.Angular.X=0;
msg.Angular.Y=0;
msg.Angular.Z=0;
%% Definimos la periodicidad del bucle ( 10 hz)
r = robotics.Rate ( 10);
%% Nos aseguramos de recibir un mensaje relacionado con el robot "robot0"
while ( strcmp ( odom.LatestMessage.ChildFrameId,'robot0')~=1)
 odom.LatestMessage
end
%% Inicializamos la primera posición ( coordenadas x,y,z)
initpos=odom.LatestMessage.Pose.Pose.Position;
%% Bucle de control infinito
while ( 1)
 %% Obtenemos la posición actual
 pos=odom.LatestMessage.Pose.Pose.Position;
 %% Calculamos la distancia euclídea que se ha desplazado
 dist=sqrt (( initpos.X-pos.X)^2+( initpos.Y-pos.Y)^2)
 %% Si el robot se ha desplazado más de un metro, detenemos el robot ( velocidad
 %% lineal 0) y salimos del bucle
 if ( dist>1)
 msg.Linear.X=0;
 % Comando de velocidad
 send ( pub,msg);
 % Salimos del bucle de control
 break;
 else
 end
 % Comando de velocidad
 send ( pub,msg);
 % Temporización del bucle según el parámetro establecido en r
 waitfor ( r)
end
%% DESCONEXIÓN DE ROS
rosshutdown;
```

Algunas de las diferencias que se encuentran con la programación en ROS nativo en C++ son las siguientes:

- El programa es secuencial, sin necesidad de declaración de clases.
- El comando ros::init para conectar con el sistema ROS es sustituido por el comando rosinit () al inicio del programa.
- Se puede subscribir a un topic sin necesidad de generar un callback ( internamente Matlab genera el hilo correspondiente a la lectura de ese dato).
- Se puede generar un mensaje del tipo declarado en el topic mediante la instrucción rosmessage, añadiendo el subscriber/publisher de dicho topic.
- Los mensajes tienen los mismos campos que en ROS, pero el nombre de los mismos inicia en mayúscula.
- Se puede acceder al último dato leído en un Subscriber mediante la instrucción `subscriber.LatestMessage`.
- Para ejecutar un bucle de forma periódica se añaden las instrucciones `r=robotics.Rate ( ratio)` y `waitfor ( r)` dentro del bucle.
- La instrucción para enviar un mensaje en un publisher es `send ( publisher,mensaje)`.
- Al acabar el programa es necesario desconectarse del sistema ROS mediante la instrucción `rosshutdown`. En caso de que la ejecución haya quedado interrumpida o no pueda terminar, será necesario ejecutar ese comando en Matlab antes de iniciar una nueva conexión.

## 8.3 Ejecución

Para ejecutar este programa cliente será necesario lanzar el simulador en Ubuntu y, una vez lanzado, ejecutar el programa en Matlab. Matlab no necesita que se compile previamente el programa ni que se genere un paquete, lo que agiliza la creación de programas sencillos para ROS.

Se desea desarrollar un conjunto de scripts en Matlab que permitan teleoperar de forma sencilla el robot, así como leer y representar gráficamente las lecturas de los sensores proporcionadas por el simulador.

Para ello se pide:

1. Realizar dos scripts, de nombre conectar.m y desconectar.m, para iniciar y terminar respectivamente la conexión con el sistema ROS cuyo master se ejecuta en la VM.
2. Realizar un script de inicialización de variables, llamado ini_simulador.m, que realice las siguientes inicializaciones:
  - Declaración de subscribers ( a odometría, láser y sonares).
  - Declaración de publishers ( para envío de velocidades).
  - Declaración de los mensajes a utilizar.
  - Definir la periodicidad del timer.
  - Asegurarse de que se recibe algún mensaje del simulador.
3. Realizar un script de lectura de sensores, llamado lee_sensores.m, para realizar la lectura del láser y de los sonares:
  - En ambos casos, realizar la lectura utilizando la función 'receive'.
  - Mostrar gráficamente los datos del láser utilizando la función 'plot'.
  - Mostrar por pantalla las lecturas de los sónares.
4. Realizar un script llamado avanzar.m que haga avanzar el robot la distancia indicada en la variable 'd'. Para ello:
  - Es necesario crear un bucle que lea la odometría y compruebe la distancia avanzada hasta el momento.
  - Opcionalmente puede llamarse al script lee_sensores dentro del bucle para comprobar las lecturas realizadas.
5. Crear un script llamado girar.m que haga girar el robot el ángulo indicado en la variable 'th':
  - Necesario crear un bucle que lea la odometría y compruebe el ángulo girado hasta el momento.
  - Utilizar la función 'quat2eul' para obtener la orientación a partir del cuaternio que proporciona el topic.
  - Opcionalmente puede llamarse al script lee_sensores dentro del bucle para comprobar las lecturas realizadas.

Dada la naturaleza de ROS, hay que tener en cuenta que el código creado puede ser ejecutado en cualquier plataforma. Por lo tanto, el código creado para el simulador puede ejecutarse en un robot real siempre que se disponga del mismo tipo de sensores.

Para realizar las prácticas de laboratorio se dispone de un robot Amigobot de la familia Pioneer. Este robot, con sistema de tracción diferencial, incorpora encoders de 500 p/rev y 8 sensores de ultrasonidos con un rango de detección de 5 m. Además, incorpora un microcontrolador con sistema operativo propio ( ARCOS) que se encarga básicamente de procesar la información de estos sensores y gestionar la comunicación con un procesador externo a través de un puerto serie.

A cada robot se le ha incorporado, como procesador externo, una tarjeta Raspberry Pi con Linux y ROS, a la cual se ha conectado un sensor láser RPLIDAR-A2. La Raspberry Pi de cada robot tiene configurada una dirección IP fija para poder conectarse en red con cualquier otro ordenador externo ( puestos del laboratorio, ordenadores portátiles, etc.).

En el arranque del robot, el sistema operativo ejecuta un script que configura y lanza de forma automática un Master de ROS ( roscore), así como los drivers de ROS necesarios para controlar el robot y acceder a los datos de los sensores. Estos drivers son, principalmente:

- **p2os**: driver que gestiona la comunicación con el microcontrolador del Amigobot, para enviar comandos de velocidad y para leer la odometría y los sonares. Algunos de los topics más importantes creados por este driver son:
  - `/pose` — odometría
  - `/cmd_vel` — comandos de velocidad
  - `/cmd_motor_state` — habilitación de los motores
  - `/sonar_i` — datos del sonar i ( i desde 0 hasta 7)
- **rplidar**: driver que accede a los datos del láser, dejándolos en el topic `/scan` ( láser).

Finalmente, se van a probar los scripts de teleoperación y lectura de sensores que se programaron en el apartado 9 sobre el robot real.

Para ello, los únicos cambios que hay que realizar son los siguientes:

1. Configurar correctamente el sistema distribuido ( variables de entorno y función 'rosinit' de Matlab).
2. Sustituir el fichero 'ini_simulador.m' por otro llamado 'ini_robot.m' que se suscriba a los topics creados por el robot. Además, en el robot real es necesario habilitar los motores antes de empezar a desplazarse por el entorno, para lo cual habrá que crear un Publisher y un mensaje de enable/disable de los motores, como se muestra a continuación:
 ```matlab
 %publisher
 pub_enable=rospublisher ('/cmd_motor_state','std_msgs/Int32');
 %declaración mensaje
 msg_enable_motor=rosmessage ( pub_enable);
 %activar motores enviando enable_motor = 1
 msg_enable_motor.Data=1;
 send ( pub_enable,msg_enable_motor);
 ```
3. El resto de scripts no necesitan ser modificados.

**Recomendaciones para la máquina virtual Ubuntu con ROS**

Configuración de red:

- Para evitar conflictos de red, hay que cambiar la MAC ( con las flechas que generan una MAC aleatoria) varias veces, evitando así que coincidan varias máquinas virtuales con la misma MAC en la red.
- Comprobar que está configurada como "Bridge".
- Dar permisos a Matlab en el Firewall de Windows en redes públicas y privadas.

Para un mejor rendimiento de la máquina virtual, se recomienda:

- Aumentar la RAM a 2-3 Gb.
- Aumentar los procesadores a 2 o 4.
- Aumentar la memoria gráfica a 128-256 Mb.
- Bajar la resolución de la pantalla una vez arrancado Ubuntu: 1024x768 suele ser suficiente.

Activar el portapapeles bidireccional, para poder copiar y pegar entre la máquina virtual y el sistema operativo nativo. Para poder usar esta función es necesario instalar "Guest Additions" en la máquina virtual.

A continuación se incluye más información sobre estas recomendaciones:

**Cambiar la dirección MAC de la máquina virtual**

Debido a que VirtualBox genera la misma dirección MAC para todas las instancias de la máquina virtual, varios ordenadores pueden terminar teniendo la misma dirección IP, provocando problemas importantes de diversa índole en la red. Para resolver este problema es necesario entrar en la configuración de red de VirtualBox, en la sección Avanzadas, y generar una nueva dirección MAC al azar.

**Aumentar la memoria de vídeo por encima de 128 Mb**

Para mejorar el rendimiento de la máquina virtual es recomendable aumentar la memoria de vídeo. Para aumentarla por encima de 128 Mb debe abrirse el archivo "Ubuntu16_04_ROS.vbox" ( que se genera una vez importada la máquina virtual) con un editor de texto y cambiar el valor de la etiqueta:

```xml
<Display VRAMSize="128"/>
```

por ejemplo a 256:

```xml
<Display VRAMSize="256"/>
```

Este archivo se encuentra en el siguiente directorio según el sistema operativo anfitrión:

- Linux y Oracle Solaris: `$HOME/.config/VirtualBox`.
- Windows: `$HOME/.VirtualBox`.
- Mac OS X: `$HOME/Library/VirtualBox`.

**Instalar "Guest Additions"**

- Dentro de la máquina virtual, seleccionar en el menú superior Dispositivos / Insertar imagen de CD de las "Guest Additions".
- Seleccionar "Run".

**Dar permisos a Matlab en el Firewall de Windows en redes públicas y privadas**

Algunos usuarios han experimentado problemas al publicar topics como la velocidad ( cmd_vel). En estos casos es posible leer desde Matlab los topics publicados por el robot o el simulador, pero no publicar topics ( como la velocidad del robot o el simulador, por ejemplo). Esta situación se ha detectado en ordenadores con Windows 10, y el problema lo genera el Firewall de Windows Defender. Para resolverlo es necesario dar permiso a Matlab para comunicar a través del firewall tanto en redes privadas como públicas.

**Cambiar la resolución de la pantalla dentro de la máquina virtual**

Para un mejor funcionamiento de la máquina virtual es recomendable disminuir la resolución de la pantalla. Una resolución de 1024x768 puede ser suficiente.

1. Seleccionar "System Settings".
2. Seleccionar "Displays".
3. Cambiar la resolución en el desplegable "Resolution".
