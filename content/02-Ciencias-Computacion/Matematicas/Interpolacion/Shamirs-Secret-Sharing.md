---
title: " Shamir's Secret Sharing – Explicación y aplicación en programación"
date: 2026-01-26
tags:
  - ciencias-computacion
  - matematicas
  - interpolacion
---

# Shamir's Secret Sharing


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/ARIN|ARIN]]. [[02-Ciencias-Computacion/Matematicas/Interpolacion/Interpolacion|Interpolacion]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[02-Ciencias-Computacion/Matematicas/Interpolacion/Metodo-de-diferencias-divididas-y-polinomio-de-Newton|Metodo de diferencias divididas y polinomio de Newton]].

**Shamir's Secret Sharing (SSS)** es un algoritmo [[01-Ciberseguridad/Criptografia/Repaso-de-Matematicas|criptográfico]] que permite **dividir un secreto (por ejemplo, una clave privada) en múltiples partes** de modo que:

> **Fundamentos matemáticos**: Basado en [[Polinomio-de-Lagrange|interpolación de Lagrange]] y [[02-Ciencias-Computacion/Matematicas/Aritmetica-modular/Pequeno-Teorema-de-Fermat|aritmética modular]].

- Se necesitan al menos **tt de nn** partes para reconstruirlo.
    
- Con menos de tt partes **no se puede obtener ninguna información útil**.
    

---

##  ¿Para qué sirve?

- Almacenar claves de forma segura y distribuida.
    
- Dividir información crítica entre personas (ej. claves de empresa, bóvedas criptográficas).
    
- Mecanismos de recuperación seguros (por ejemplo, recuperación social de billeteras en Web3).
    
- **Aplicaciones de alta seguridad, como HSMs, DAOs o backup resiliente**.
    

---

##  ¿Cómo funciona?

La idea se basa en que **un polinomio de grado t−1t-1 queda determinado por tt puntos**.

Si el secreto es un número ss (por ejemplo, una clave), se construye un polinomio:

f(x)=a0+a1x+a2x2+⋯+at−1xt−1f(x) = a_0 + a_1 x + a_2 x^2 + \cdots + a_{t-1} x^{t-1}

donde:

- a0=sa_0 = s (el secreto),
    
- a1,...,at−1a_1, ..., a_{t-1} son coeficientes aleatorios,
    
- Los puntos f(1),f(2),...,f(n)f(1), f(2), ..., f(n) se reparten como **partes del secreto** (shares).
    

---

##  Propiedades

- Cualquier grupo de tt partes puede **reconstruir el secreto** usando **interpolación de Lagrange**.
    
- Cualquier grupo de <t< t partes **no puede inferir nada** sobre el secreto.
    
- Funciona en un **campo finito** (por ejemplo, módulo de un número primo grande pp).
    

---

## ️ Implementación práctica (simplificada)

### Generación de partes:

1. Elegimos:
    
    - Un número primo pp (por ejemplo, 208351617316091241234326746312124448251235562226470491514186331217050270460481).
        
    - Un secreto s<ps < p.
        
    - Grado t−1t - 1 y número total de partes nn.
        
2. Creamos un polinomio aleatorio de grado t−1t-1 con a0=sa_0 = s.
    
3. Evaluamos el polinomio en x=1,2,...,nx = 1, 2, ..., n.
    

### Reconstrucción (con al menos tt partes):

Usamos la fórmula de interpolación de Lagrange:

s=f(0)=∑i=1tyi⋅∏j≠i−xjxi−xjmod  ps = f(0) = \sum_{i=1}^{t} y_i \cdot \prod_{j \ne i} \frac{-x_j}{x_i - x_j} \mod p

---

##  Ejemplo ilustrativo (campo Z17\mathbb{Z}_{17})

Supongamos:

- Secreto: s=5s = 5
    
- Grado: 22 (umbral t=3t = 3)
    
- Polinomio aleatorio: f(x)=5+3x+2x2mod  17f(x) = 5 + 3x + 2x^2 \mod 17
    

Calculamos:

- f(1)=5+3(1)+2(1)2=10mod  17f(1) = 5 + 3(1) + 2(1)^2 = 10 \mod 17
    
- f(2)=5+3(2)+2(4)=5+6+8=19mod  17=2f(2) = 5 + 3(2) + 2(4) = 5 + 6 + 8 = 19 \mod 17 = 2
    
- f(3)=5+9+18=32mod  17=15f(3) = 5 + 9 + 18 = 32 \mod 17 = 15
    

Las partes son:  
→ (1,10),(2,2),(3,15)(1,10), (2,2), (3,15)

Con estas tres, podemos reconstruir f(0)=s=5f(0) = s = 5 mediante interpolación.

---

##  Aplicaciones en programación

|Área|Aplicación|
|---|---|
|**Criptografía**|División y recuperación segura de claves|
|**Blockchain / Web3**|Wallet recovery, multisig off-chain|
|**Sistemas distribuidos**|Claves compartidas en nodos|
|**Backups resistentes**|Sin punto único de fallo|
|**Firmas descentralizadas**|Threshold signatures (con variantes de SSS)|

---

##  Ventajas

- Seguridad matemática sólida.
    
- Flexibilidad en el número de participantes y umbral.
    
- Resistencia ante pérdidas parciales de datos.
    
- Compatible con otros sistemas criptográficos modulares.
    

---

## ️ Consideraciones

- Requiere operar en un **campo finito grande**, por lo tanto:
    
    - Aritmética modular (requiere inversos).
        
    - Uso de **números primos grandes**.
        
- No detecta si alguien entrega una parte falsa → para eso existe **verificación verificada** (VSS).
    

---

##  Herramientas y librerías

- `secretsharing` (Python)
    
- `sss` de `cryptography.io`
    
- `Shamir` en `libsodium`
    
- Ethereum / Solidity: `Shamir` + `bn256`
    

---