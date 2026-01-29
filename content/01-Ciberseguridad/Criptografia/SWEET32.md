---
title: "Sweet32"
date: 2026-01-26
tags:
  - ciberseguridad
  - criptografia
---
**SWEET32** es una vulnerabilidad de **seguridad** que afecta a ciertos algoritmos de cifrado utilizados en las conexiones **TLS (Transport Layer Security)** y **SSL (Secure Sockets Layer)**, especialmente aquellos basados en el algoritmo de **cifrado de bloque 3DES (Triple DES)**. La vulnerabilidad fue descubierta en 2016 y está relacionada con la **longitud de la clave** y la **tamaño del bloque** de 3DES, lo que lo hace susceptible a **ataques de colisión de bloque** cuando se utiliza en entornos de **conexiones de largo tiempo** o con **mucho tráfico**.

###  **¿Qué es SWEET32?**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Redes/Nginx|Nginx]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Criptografia/OpenSSL|OpenSSL]].

**SWEET32** se refiere a un ataque de **colisión de bloque** que puede ser utilizado para comprometer la seguridad de las conexiones TLS/SSL que usan el algoritmo **3DES**. El ataque se basa en la **limitación de tamaño de bloque de 64 bits** del algoritmo 3DES, lo que lo hace vulnerable a un tipo de **colisión** cuando se cifra una cantidad suficiente de datos.

###  **¿Cómo funciona el ataque SWEET32?**

1. **Problema con 3DES**:
    
    - **3DES** utiliza un **tamaño de bloque de 64 bits**, que es relativamente pequeño en comparación con otros algoritmos de cifrado modernos, como **AES** (Advanced Encryption Standard), que usa un bloque de **128 bits**.
        
    - Cuando se cifra un volumen grande de datos con un algoritmo de **cifrado de bloques** como 3DES, existe la posibilidad de que el **mismo bloque de datos** sea cifrado varias veces, lo que aumenta la probabilidad de que se produzcan **colisiones** en el bloque de 64 bits.
        
2. **Colisión de bloques**:
    
    - En los **ataques de colisión**, el atacante puede observar suficientes bloques cifrados y, con el tiempo, ser capaz de inferir información sobre los datos originales. En particular, en **conexiones TLS** donde hay una gran cantidad de tráfico, el tamaño pequeño del bloque de 3DES permite a los atacantes identificar patrones repetidos en los bloques cifrados y **extraer** información sensible.
        
    - El ataque **SWEET32** se convierte en una amenaza cuando se cifra un volumen significativo de datos durante un largo período de tiempo, como ocurre en **sesiones HTTPS prolongadas**.
        
3. **Vulnerabilidad en sesiones largas**:
    
    - El ataque se basa en la **observación del tráfico cifrado** y en el hecho de que en conexiones de larga duración o con grandes cantidades de datos, existe una alta probabilidad de que dos bloques cifrados sean idénticos, lo que se conoce como una **colisión de bloques**.
        
    - Un atacante podría, con el tiempo, obtener suficiente información sobre el contenido de la conexión y potencialmente **descifrar** parte de los datos enviados, lo que **compromete la seguridad** de la comunicación.
        

###  **Impacto de SWEET32**:

- **Exposición de datos sensibles**: Un atacante que explote SWEET32 podría ser capaz de obtener **información sensible**, como contraseñas, números de tarjetas de crédito, o incluso datos cifrados completos.
    
- **Ataques de intercepción**: Los atacantes pueden **interceptar** y **analizar** las comunicaciones cifradas y, a través del ataque, descubrir patrones o incluso datos completos, lo que puede llevar a la **filtración de información confidencial**.
    
- **Compromiso de integridad**: Aunque el ataque no necesariamente compromete la integridad de los datos, en algunos casos puede permitir a un atacante **modificar** o manipular la información cifrada, dependiendo de la implementación.
    

###  **¿Cómo prevenir el ataque SWEET32?**

1. **Deshabilitar 3DES en configuraciones TLS/SSL**:
    
    - **Eliminación de 3DES**: La principal recomendación para mitigar este ataque es **deshabilitar el uso de 3DES** en configuraciones de **servidores SSL/TLS**. Los algoritmos de cifrado modernos como **AES** (preferiblemente con claves de 128 bits o más) deben ser habilitados en su lugar, ya que tienen un tamaño de bloque de **128 bits**, lo que hace que sea mucho más difícil realizar un ataque de colisión como el de SWEET32.
        
2. **Uso de cifrados con mayor seguridad**:
    
    - **Actualizar cifrados**: Configurar el servidor para usar **AES con claves de 128 bits** o más, que es mucho más seguro y eficiente que 3DES.
        
    - **Preferir suites de cifrado modernas**: Asegúrate de usar suites de cifrado que no incluyan algoritmos obsoletos como **3DES** o **RC4**. Las suites de cifrado modernas como **ECDHE (Elliptic Curve Diffie-Hellman)** con **AES** son más seguras.
        
3. **Configurar límites de tiempo para sesiones TLS**:
    
    - En lugar de mantener largas sesiones TLS, se pueden configurar los servidores para **limitar la duración de las sesiones** y así reducir la cantidad de datos cifrados con el mismo bloque de 64 bits.
        
4. **Monitoreo de tráfico y auditoría de configuraciones**:
    
    - Monitorear los servidores y las conexiones para asegurarse de que no haya **tráfico TLS** que utilice 3DES o cualquier otro algoritmo vulnerable.
        
    - Realizar **auditorías periódicas** de las configuraciones SSL/TLS para garantizar que se estén utilizando los **métodos de cifrado más seguros**.
        
5. **Actualización de bibliotecas SSL/TLS**:
    
    - Asegúrate de que las **bibliotecas y servidores TLS** estén siempre **actualizados**. Los **parches de seguridad** y las **nuevas configuraciones** implementadas en versiones recientes pueden ayudar a mitigar vulnerabilidades como SWEET32.
        

###  **Configuración recomendada (en Nginx, Apache, etc.)**

- **Deshabilitar 3DES y habilitar AES**: A continuación se muestra un ejemplo de cómo deshabilitar 3DES en un servidor web:
    

#### **En Nginx**:

```nginx
ssl_ciphers 'ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:AES128-SHA256';
ssl_protocols TLSv1.2 TLSv1.3;
```

#### **En Apache**:

```apache
SSLCipherSuite ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:AES128-SHA256
SSLProtocol TLSv1.2 TLSv1.3
```

Esto asegura que solo se utilizarán **cifrados modernos y seguros** y **se eliminará el soporte para 3DES**.

###  **Resumen:**

**SWEET32** es una vulnerabilidad de seguridad que afecta a **cifrados de bloque con un tamaño de 64 bits** como **3DES** en conexiones TLS/SSL. Los ataques SWEET32 se explotan aprovechando el **tamaño pequeño del bloque de 64 bits** en 3DES, lo que facilita la **colisión de bloques** en conexiones largas. La **prevención** de este ataque implica **deshabilitar 3DES** y utilizar **cifrados más seguros** como **AES** con bloques de 128 bits. Asegurarse de tener configuraciones seguras y actualizadas de **TLS/SSL** es esencial para mitigar los riesgos de SWEET32.