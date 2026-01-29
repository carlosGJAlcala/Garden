---
title: "Ssrf"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---
### **¿Qué es un ataque SSRF (Server-Side Request Forgery)?**

Un ataque de **SSRF (Server-Side Request Forgery)** es una vulnerabilidad incluida en el [[owasp|OWASP Top 10]] que ocurre cuando un atacante abusa de una aplicación para que esta realice solicitudes HTTP o de otro protocolo hacia recursos internos o externos, que el atacante no podría acceder directamente. La solicitud se origina desde el servidor de la aplicación, lo que permite al atacante interactuar con servicios internos de la red del servidor o incluso acceder a recursos protegidos.

> **Relacionado**: Similar a [[XXE]] en cuanto a acceso a recursos internos. Detectable con [[Burp-suite|Burp Suite]] o [[owasp-zap|OWASP ZAP]].

---

### **¿Cómo funciona un SSRF?**

1. **Entrada controlada por el atacante:**
    
    - Una aplicación acepta una entrada del usuario que se utiliza para formar una solicitud hacia otro recurso, como una URL.
    - Ejemplo típico: carga de una imagen remota (`http://ejemplo.com/image`) o integración con APIs externas.
2. **Manipulación de la solicitud:**
    
    - El atacante introduce una URL o dirección maliciosa en la entrada controlada.
    - Esto fuerza al servidor a realizar solicitudes hacia recursos inesperados o sensibles.
3. **El servidor realiza la solicitud:**
    
    - Como la solicitud proviene del servidor de la aplicación, puede acceder a recursos internos de la red del servidor o realizar interacciones no autorizadas.
4. **Impacto:**
    
    - El atacante puede leer datos internos, interactuar con servicios internos (como bases de datos, servidores de administración, APIs internas), o incluso realizar escaneos en la red interna.

---

### **Ejemplo básico de un ataque SSRF**

#### **Escenario vulnerable:**

Una aplicación web permite a los usuarios proporcionar una URL para descargar una imagen. Supongamos que el backend toma la URL ingresada y realiza la solicitud para descargar la imagen y mostrarla.

**Código vulnerable:**

```python
import requests
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/fetch-image', methods=['POST'])
def fetch_image():
    image_url = request.json.get('url')
    response = requests.get(image_url)  # Solicitud directa
    return response.content
```

#### **Ataque SSRF:**

El atacante proporciona una URL maliciosa en la entrada:

```json
{
  "url": "http://127.0.0.1:8080/admin"
}
```

- El servidor hace la solicitud a `http://127.0.0.1:8080/admin`, un recurso interno que el atacante no podría acceder directamente desde su navegador.
- Si este recurso interno devuelve información confidencial, el atacante podría obtenerla a través de la respuesta del servidor.

---

### **Impactos de un ataque SSRF**

1. **Acceso a recursos internos:**
    
    - El atacante puede interactuar con servicios internos como bases de datos, APIs internas, servidores de administración o almacenamiento.
2. **Filtración de información:**
    
    - Recursos internos como `/etc/passwd` en servidores locales o credenciales de servicios expuestos a través de APIs pueden ser filtrados.
3. **Denegación de servicio:**
    
    - Al abusar de la capacidad del servidor para realizar solicitudes, un atacante puede sobrecargarlo o forzarle a interactuar con recursos pesados.
4. **Ejecución de ataques adicionales:**
    
    - Un SSRF puede ser un punto de partida para otros ataques, como:
        - Escaneo de la red interna.
        - Explotación de vulnerabilidades en servicios internos.
        - Ataques basados en metadatos, como robar credenciales desde servicios en la nube (por ejemplo, AWS IMDS - Instance Metadata Service).

---

### **Ejemplo avanzado: Ataque a AWS IMDS**

En servidores alojados en AWS, un atacante puede usar SSRF para acceder a los metadatos de la instancia. Si la aplicación vulnerable se ejecuta en una instancia EC2:

#### **Solicitud SSRF:**

```json
{
  "url": "http://169.254.169.254/latest/meta-data/iam/security-credentials/"
}
```

#### **Resultado:**

El servidor podría devolver credenciales temporales de IAM, que el atacante puede usar para acceder a los recursos de AWS (como S3, DynamoDB, etc.).

---

### **Cómo prevenir un ataque SSRF**

1. **Validación estricta de entradas:**
    
    - Valida las entradas proporcionadas por el usuario para asegurarte de que solo se permitan URLs confiables.
    - Usa listas blancas de dominios permitidos.
    
    Ejemplo en Python:
    
    ```python
    allowed_domains = ['ejemplo.com']
    
    def is_valid_url(url):
        parsed_url = urlparse(url)
        return parsed_url.hostname in allowed_domains
    ```
    
2. **Evitar solicitudes directas:**
    
    - En lugar de permitir que la aplicación realice solicitudes directamente basadas en entradas del usuario, utiliza un proxy o servicios intermediarios que validen las solicitudes.
3. **Restringir la conectividad del servidor:**
    
    - Configura el servidor para que no pueda acceder a recursos internos como `127.0.0.1` o `169.254.169.254`.
    - En servidores en la nube, utiliza servicios como **AWS IMDSv2** para proteger los metadatos.
4. **Usar bibliotecas seguras:**
    
    - Algunas bibliotecas pueden ayudar a prevenir SSRF mediante la validación de URLs y restricciones en las solicitudes.
5. **Implementar cortafuegos de aplicaciones web (WAF):**
    
    - Un WAF puede detectar patrones comunes de SSRF y bloquear solicitudes maliciosas.

---

### **Conclusión**

Un ataque SSRF aprovecha la capacidad de un servidor para realizar solicitudes en nombre de un atacante. Esto puede tener consecuencias graves, especialmente si el servidor tiene acceso a recursos internos o servicios sensibles. La mejor forma de prevenir SSRF es validar estrictamente las entradas, limitar el acceso a la red interna y usar configuraciones seguras para servicios en la nube y metadatos.