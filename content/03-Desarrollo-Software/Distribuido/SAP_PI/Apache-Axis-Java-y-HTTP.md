---
title: "Apache Axis Java Y Http"
date: 2025-01-01
tags:
  - desarrollo-software
---

##  Apache Axis (Java) y HTTP


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[03-Desarrollo-Software/Distribuido/SAP_PI/STUB|STUB]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

### 1. ¿Qué es Apache Axis?

Apache Axis es un **framework de código abierto en Java** creado por la Apache Software Foundation para trabajar con **servicios web basados en SOAP**.  
Su función principal es permitir:

- **Publicar** servicios web SOAP en Java (lado servidor).
    
- **Consumir** servicios web SOAP de otros sistemas (lado cliente).
    

Se considera el sucesor de **Apache SOAP** y fue uno de los frameworks más utilizados en la primera generación de servicios web empresariales en Java.

---

### 2. Relación con HTTP

Aunque SOAP puede funcionar sobre distintos protocolos de transporte, el más común y el que usa Axis por defecto es **HTTP**.

- Los mensajes SOAP se **encapsulan dentro de peticiones HTTP POST**.
    
- El servidor Axis recibe la petición, procesa el XML y responde también en formato SOAP/XML dentro de la respuesta HTTP.
    

Por eso se habla de **Axis HTTP**: el framework implementa SOAP sobre HTTP, que es el medio más estándar para la comunicación cliente-servidor.

---

### 3. Componentes principales de Axis en Java

- **Cliente (Stub):**  
    Código generado a partir de un **WSDL**. Permite llamar a métodos del servicio web remoto como si fueran métodos locales de Java.
    
- **Servidor (Skeleton):**  
    Código que recibe las peticiones SOAP, las traduce a objetos Java, ejecuta la lógica del servicio y devuelve la respuesta en SOAP.
    
- **Motor de Axis:**  
    Es el núcleo del framework. Se encarga de:
    
    - Procesar mensajes SOAP.
        
    - Manejar Handlers (filtros que procesan mensajes antes o después).
        
    - Gestionar la comunicación sobre HTTP.
        
- **WSDL2Java:**  
    Herramienta que genera el código Java necesario (stubs y skeletons) a partir de un archivo WSDL.
    

---

### 4. Flujo de funcionamiento sobre HTTP

1. **El cliente genera un stub** a partir del WSDL del servicio.
    
2. El programador en Java llama un método del stub, por ejemplo:
    

```java
int r = servicio.suma(2, 3);
```

3. El stub convierte esa llamada en un **mensaje SOAP XML**.
    
4. Ese XML se envía en una petición **HTTP POST** al servidor Axis.
    
5. El servidor Axis (skeleton + motor) recibe el mensaje, lo interpreta y ejecuta el método Java real.
    
6. El resultado se convierte en un XML SOAP de respuesta y se devuelve en la respuesta HTTP.
    
7. El stub procesa el XML recibido y lo devuelve como un resultado nativo en Java (`5`).
    

---

### 5. Ejemplo de comunicación SOAP/HTTP en Axis

**Petición del cliente (HTTP + SOAP):**

```http
POST /axis/services/Calculadora HTTP/1.1
Host: servidor.com
Content-Type: text/xml; charset=utf-8
SOAPAction: "suma"

<?xml version="1.0"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ns1:suma xmlns:ns1="http://ejemplo.com/calculadora">
      <a>2</a>
      <b>3</b>
    </ns1:suma>
  </soap:Body>
</soap:Envelope>
```

**Respuesta del servidor (HTTP + SOAP):**

```http
HTTP/1.1 200 OK
Content-Type: text/xml; charset=utf-8

<?xml version="1.0"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ns1:sumaResponse xmlns:ns1="http://ejemplo.com/calculadora">
      <resultado>5</resultado>
    </ns1:sumaResponse>
  </soap:Body>
</soap:Envelope>
```

---

### 6. ¿Por qué fue importante?

- Fue uno de los **primeros frameworks estándar para SOAP en Java**.
    
- Permitía la **interoperabilidad** entre aplicaciones en diferentes lenguajes y plataformas.
    
- Automatizaba la parte más compleja: manejo de XML, generación de WSDL, transporte HTTP.
    

---

### 7. Estado actual

- Apache Axis 1.x y 2.x fueron muy utilizados, pero hoy están casi obsoletos.
    
- Fueron reemplazados por frameworks más modernos como **Apache CXF**, **JAX-WS (Java EE)** o directamente por **servicios REST/JSON**, que son más ligeros.
    
- Aun así, **Axis sigue presente en entornos empresariales antiguos**, especialmente en banca, seguros y administración pública.
    

---

En resumen: **Apache Axis (Java)** es un framework que permite crear y consumir servicios web basados en **SOAP**, funcionando principalmente sobre **HTTP POST**, y gestionando automáticamente la traducción entre llamadas Java y mensajes XML.

---

## Ejemplo: Consumir servicio SOAP con Apache Axis

Ejemplo de cómo funciona **Apache Axis en Java** para consumir un servicio SOAP a través de HTTP. Simularemos un servicio web de **calculadora** con una operación `suma(a, b)`.

### 1. Preparar el WSDL

El servicio web tiene un archivo **WSDL** (Web Services Description Language) que describe el servicio, cómo funciona y qué métodos ofrece. En este caso, nuestro servicio de **Calculadora** tiene una operación `suma(a, b)` que devuelve el resultado de sumar dos números.

Este archivo WSDL tiene más o menos esta estructura (simplificada):

```xml
<definitions xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/"
             xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/"
             targetNamespace="http://ejemplo.com/calculadora">
    <message name="sumaRequest">
        <part name="a" type="xsd:int"/>
        <part name="b" type="xsd:int"/>
    </message>
    <message name="sumaResponse">
        <part name="resultado" type="xsd:int"/>
    </message>

    <portType name="CalculadoraPortType">
        <operation name="suma">
            <input message="tns:sumaRequest"/>
            <output message="tns:sumaResponse"/>
        </operation>
    </portType>

    <binding name="CalculadoraBinding" type="tns:CalculadoraPortType">
        <soap:binding style="rpc" transport="http://schemas.xmlsoap.org/soap/http"/>
        <operation name="suma">
            <soap:operation soapAction="suma"/>
            <input>
                <soap:body use="literal"/>
            </input>
            <output>
                <soap:body use="literal"/>
            </output>
        </operation>
    </binding>

    <service name="CalculadoraService">
        <port name="CalculadoraPort" binding="tns:CalculadoraBinding">
            <soap:address location="http://ejemplo.com/axis/services/Calculadora"/>
        </port>
    </service>
</definitions>
```

### 2. **Generación de Stubs con WSDL2Java**

Para trabajar con este servicio en tu código Java, usas la herramienta **WSDL2Java** de Axis. Esta herramienta genera las clases **stubs** (cliente) que podrás usar para interactuar con el servicio SOAP de manera sencilla.

Ejecutas el siguiente comando para generar el código Java:

```bash
wsdl2java -o /path/to/output -p com.ejemplo.calculadora http://ejemplo.com/axis/services/Calculadora?wsdl
```

Esto generará varias clases Java dentro del paquete `com.ejemplo.calculadora`, incluyendo las clases que representan las solicitudes y respuestas, y la clase `CalculadoraService` que es el stub del cliente.

### 3. **Código Java para Consumir el Servicio**

Ahora que tenemos los **stubs**, podemos escribir el código Java para **llamar al servicio de la calculadora**. Suponiendo que ya has generado los stubs, el código sería algo como esto:

```java
import com.ejemplo.calculadora.Calculadora;
import com.ejemplo.calculadora.CalculadoraServiceLocator;
import com.ejemplo.calculadora.suma;

public class ClienteCalculadora {

    public static void main(String[] args) {
        try {
            // Crear el objeto del servicio (stub generado)
            CalculadoraServiceLocator serviceLocator = new CalculadoraServiceLocator();
            Calculadora calculadora = serviceLocator.getCalculadora();

            // Crear la solicitud (SOAP request)
            suma request = new suma();
            request.setA(2);  // Primer número
            request.setB(3);  // Segundo número

            // Llamar al servicio
            int resultado = calculadora.suma(request);  // Llamada al método 'suma' del servicio

            // Imprimir el resultado
            System.out.println("Resultado de la suma: " + resultado);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 4. **Explicación del Flujo**

1. **Cliente crea el stub**: `CalculadoraServiceLocator` es el locator que obtiene el objeto `Calculadora` que contiene el método `suma`. Este método es un stub generado automáticamente a partir del WSDL.
    
2. **Solicitud SOAP (request)**: El objeto `suma` es una clase generada que se usa para representar el mensaje SOAP. Aquí asignamos los valores de `a` y `b` a los parámetros que la operación `suma` necesita.
    
3. **Llamada al servicio**: La llamada a `calculadora.suma(request)` envía la solicitud SOAP (con los valores de `a` y `b`) al servidor web. Axis se encarga de empaquetar esta solicitud como un mensaje SOAP, enviarlo por HTTP y esperar la respuesta.
    
4. **Respuesta SOAP**: El servidor procesa la solicitud, realiza la operación de suma (2 + 3 = 5) y devuelve el resultado dentro de un mensaje SOAP.
    
5. **Procesar respuesta**: El cliente (el stub generado) deserializa la respuesta SOAP, extrayendo el valor `resultado` (5) y lo devuelve como un valor Java nativo.
    
6. **Mostrar resultado**: Finalmente, el cliente imprime el resultado en consola.
    

---

### 5. **Estructura del Mensaje SOAP**

Cuando el cliente envía la solicitud SOAP, el mensaje tiene esta forma:

**SOAP Request (petición de cliente)**:

```xml
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ns1:suma xmlns:ns1="http://ejemplo.com/calculadora">
      <a>2</a>
      <b>3</b>
    </ns1:suma>
  </soap:Body>
</soap:Envelope>
```

Y cuando el servidor responde, el mensaje SOAP será:

**SOAP Response (respuesta del servidor)**:

```xml
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ns1:sumaResponse xmlns:ns1="http://ejemplo.com/calculadora">
      <resultado>5</resultado>
    </ns1:sumaResponse>
  </soap:Body>
</soap:Envelope>
```

### 6. **Conclusión**

- **Apache Axis** maneja el trabajo pesado de construir y analizar los mensajes SOAP en XML.
    
- **Los stubs** generados a partir del WSDL hacen que la interacción con el servicio sea fácil, llamando métodos como si estuvieras trabajando con objetos locales en Java, pero en realidad estás llamando a métodos remotos en un servidor.
    
- **HTTP** es el medio de transporte que se utiliza para enviar y recibir los mensajes SOAP entre el cliente y el servidor.
    

Este es un ejemplo básico de cómo consumir un servicio web SOAP usando **Apache Axis** en **Java**. Si necesitas detalles adicionales sobre el servidor o la configuración avanzada, ¡avísame!