---
title: "Konversation"
date: 2026-01-26
tags:
  - ciberseguridad
  - comunicaciones-seguras
  - konversation
---
 Te explico paso a paso cómo conectarte a un servidor IRC usando **Konversation** para que puedas empezar a chatear enseguida.

---

### 1️⃣ Abrir Konversation y crear conexión


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

- Abre **Konversation**.
    
- Si es la primera vez que lo usas, te aparecerá el asistente de conexión. Si no, ve a **Servidor → Conectar a servidor…**.
    
- Elige **Añadir** para crear una nueva conexión.
    

---

### 2️⃣ Configurar el servidor

- **Servidor**: por ejemplo, para Libera Chat escribe `irc.libera.chat`.
    
- **Puerto**: `6697` (recomendado) o `6667`.
    
- Marca la opción **SSL/TLS** si usas el puerto 6697 para conexión segura.
    

---

### 3️⃣ Poner tu apodo

- En **Nickname** pon el nombre con el que quieras aparecer.
    
- Opcional: añade un segundo y tercer nick por si el primero está ocupado.
    

---

### 4️⃣ (Opcional) Registrar tu nick

Si quieres que nadie más pueda usar tu apodo:

1. Conéctate al servidor.
    
2. Escribe:
    
    ```
    /msg NickServ REGISTER contraseña email@example.com
    ```
    
3. Luego confirma el registro siguiendo las instrucciones que te enviarán por correo.
    

La próxima vez que te conectes, autentícate con:

```
/msg NickServ IDENTIFY contraseña
```

---

### 5️⃣ Unirte a un canal

- Una vez conectado, para entrar a un canal escribe:
    
    ```
    /join #nombre_del_canal
    ```
    
    Ejemplo:
    
    ```
    /join #kde
    ```
    

---

### 6️⃣ Guardar la conexión

- En el menú de Konversation, guarda tu perfil de servidor para que no tengas que configurarlo cada vez.
    
- Incluso puedes marcar canales para que se abran automáticamente al conectarte.
    

---

Si quieres, te puedo hacer **un ejemplo ya configurado para Libera Chat en Konversation** para que solo tengas que importarlo y empezar a hablar.