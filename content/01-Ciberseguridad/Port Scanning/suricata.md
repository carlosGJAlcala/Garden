# INSTALACIÓN

Primero, hay que añadir el repositorio para que pueda descargarse Suricata:

```bash
sudo add-apt-repository ppa:oisf/suricata-stable
```

Pasted image 20241104134911.png

Luego, hacemos un update:

```bash
sudo apt update
```

A continuación, podemos instalar Suricata:

```bash
sudo apt install suricata-dbg
```

Pasted image 20241104135044.png

Verificamos que no está creado el directorio `rules` dentro de `etc/suricata`:

Pasted image 20241104135240.png

Lo creamos con `mkdir`. Aquí se van a alojar las reglas:

Pasted image 20241104135352.png

Añadimos nuestra red en el `homenet`. Para ello, entramos en el archivo de configuración `suricata.yml`:

Pasted image 20241104135641.png

También indicamos la interfaz de red:

Pasted image 20241104135956.png

Especificamos dónde está la carpeta de reglas y también indicamos un nuevo archivo donde se leen las reglas:

Pasted image 20241104140415.png

Escribimos la siguiente regla:

Pasted image 20241104140644.png

Y ejecutamos Suricata, indicándole la interfaz de red.
