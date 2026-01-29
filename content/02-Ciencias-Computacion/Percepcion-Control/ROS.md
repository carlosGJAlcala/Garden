---
title: "Ros"
date: 2026-01-26
tags:
  - ciencias-computacion
  - percepcion-control
---
**ROS (Robot Operating System)** no es un sistema operativo en el sentido clásico (como Linux o Windows), sino un **framework** o **middleware** para el desarrollo de aplicaciones robóticas. Proporciona herramientas, bibliotecas y convenciones que permiten a los desarrolladores **crear sistemas robóticos modulares, escalables y reutilizables**.

---

###  ¿Qué es ROS?


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/ONOS|ONOS]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

ROS es una **plataforma de software de código abierto** que facilita el desarrollo de **sistemas robóticos complejos**. Se construye sobre Linux (generalmente Ubuntu) y proporciona servicios como:

- Comunicación entre procesos (nodos).
    
- Control de sensores y actuadores.
    
- Representación del entorno (mapas, modelos 3D).
    
- Planificación de movimientos.
    
- Visión artificial, navegación, manipulación, etc.
    

---

###  Componentes Clave de ROS

1. **Nodos (`nodes`)**:
    
    - Son los procesos que ejecutan tareas. Cada nodo se encarga de una función específica: leer un sensor, controlar un motor, procesar imagen, etc.
        
    - Pueden estar escritos en C++ (`roscpp`) o Python (`rospy`).
        
2. **Tópicos (`topics`)**:
    
    - Son canales de comunicación **asíncronos** entre nodos. Un nodo puede publicar datos (como imágenes de cámara) y otro puede suscribirse para recibirlos.
        
3. **Mensajes (`messages`)**:
    
    - Estructuras de datos que se intercambian por los tópicos. Ejemplo: un mensaje `geometry_msgs/Twist` puede contener velocidades lineales y angulares.
        
4. **Servicios (`services`)**:
    
    - Comunicación **sincrónica** entre nodos: un nodo hace una petición y espera la respuesta (por ejemplo, pedir al robot que se mueva a cierta posición).
        
5. **Acciones (`actions`)**:
    
    - Para tareas que toman tiempo (como navegar a un punto), permiten iniciar la acción, seguir su progreso y cancelarla si es necesario.
        
6. **Launch files**:
    
    - Archivos `.launch` que permiten **iniciar múltiples nodos** con configuraciones específicas.
        
7. **ROS Master (`roscore`)**:
    
    - Es el servidor central que mantiene registro de los nodos y facilita su descubrimiento y conexión.
        

---

###  Ejemplo de arquitectura básica

Imagina un robot móvil con ROS:

- `camera_node` publica imágenes por el tópico `/camera/image_raw`.
    
- `image_processing_node` se suscribe a ese tópico y detecta obstáculos.
    
- `navigation_node` publica comandos de movimiento en `/cmd_vel`.
    
- `motor_controller_node` se suscribe a `/cmd_vel` y controla los motores.
    

Toda esta comunicación ocurre **de manera modular y descentralizada**, sin que los nodos se conozcan directamente.

---

### ️ Ejemplo simple en Python

```python
import rospy
from geometry_msgs.msg import Twist

def mover_robot():
    pub = rospy.Publisher('/cmd_vel', Twist, queue_size=10)
    rospy.init_node('robot_mover', anonymous=True)
    rate = rospy.Rate(10)  # 10 Hz
    vel_msg = Twist()
    vel_msg.linear.x = 0.2
    vel_msg.angular.z = 0.1
    while not rospy.is_shutdown():
        pub.publish(vel_msg)
        rate.sleep()
```

Este nodo hace que el robot se mueva hacia adelante con un ligero giro.

---

###  ROS y Ciberseguridad

ROS fue diseñado **para investigación**, no para entornos hostiles, por lo que tiene debilidades importantes si no se protege:

1. **No tiene autenticación ni cifrado por defecto**.
    
2. Cualquier nodo conectado a la red puede:
    
    - Publicar comandos falsos (`/cmd_vel`).
        
    - Escuchar datos sensibles (cámaras, sensores).
        
    - Detener nodos o incluso reiniciar el sistema.
        

️ Para mitigar esto, se usa:

- **ROS 2**, que implementa seguridad con DDS (Data Distribution Service): autenticación, cifrado, control de acceso.
    
- **VPNs** o redes privadas para aislar el robot.
    
- Firewalls y segmentación de red.
    

---

###  Casos de uso reales

- **Robots de reparto autónomos** (TurtleBot, Tiago).
    
- **Brazos robóticos** industriales.
    
- **Drones** con navegación autónoma.
    
- **Coches autónomos** en fases de prototipo (ROS se integra con simuladores como Gazebo o CARLA).
    
- **Robots quirúrgicos** y aplicaciones médicas (I+D).
    

---

###  Herramientas útiles en ROS

- `rqt_graph`: visualiza los nodos y conexiones activas.
    
- `rviz`: visualización 3D de sensores, trayectorias, etc.
    
- `rosbag`: graba y reproduce datos para pruebas.
    
- `tf`: gestiona transformaciones entre sistemas de coordenadas (muy útil en robótica móvil y brazos robóticos).
    

---

###  Conclusión

**ROS** es el estándar de facto en desarrollo de sistemas robóticos. Su arquitectura modular, soporte de múltiples lenguajes y comunidad lo hacen ideal para prototipos, investigación y desarrollo industrial. Eso sí, **requiere protección activa** si se despliega en entornos reales debido a sus vulnerabilidades en versiones anteriores a ROS 2.

¿Quieres que te muestre un ejemplo práctico de un sistema completo en ROS o cómo integrarlo con sensores reales?