---
title: "Preguntas"
date: 2026-01-26
tags:
  - ciberseguridad
  - ingenieria-inversa
---
<<<<<<< HEAD
=======
Autor Carlos Garrido
>>>>>>> origin/main
# Preguntas

> **Relacionado**: [[01-Ciberseguridad/Ingenieria-Inversa/objetos-COM|objetos COM]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

1- Dado el binario analízalo brevemente y describe por encima que simula este binario.  
2- Al igual que en la práctica anterior describe las funciones definidas por el programador.  
3- ¿En qué lenguaje crees que está escrito el binario?, en caso de ser un lenguaje  
orientado a objetos identifica al menos un constructor de clase.  
4 - En primer lugar consigue parchear la petición de licencia para evitarla. Describe el  
proceso  
5 - En segundo lugar parchea el nombre del jugador para que aparezca el tuyo. Describe  
el proceso  
6 - En tercer lugar intenta conseguir imprimir el mensaje “Has ganado” (parcheando el  
binario). Describe el proceso  
7 - Por último, obtén uno varios códigos de licencia correctos. En este caso, al describir el  
proceso deberás hacerlo usando el código ensamblador, sin usar el pseudocódigo  
proporcionado por el decompilador.

# Contenido
<<<<<<< HEAD
1- Dado el binario analízalo brevemente y describe por encima que simula este binario.  
2- Al igual que en la práctica anterior describe las funciones definidas por el programador.  
3- ¿En qué lenguaje crees que está escrito el binario?, en caso de ser un lenguaje  
orientado a objetos identifica al menos un constructor de clase.  
4 - En primer lugar consigue parchear la petición de licencia para evitarla. Describe el  
proceso  
5 - En segundo lugar parchea el nombre del jugador para que aparezca el tuyo. Describe  
el proceso  
6 - En tercer lugar intenta conseguir imprimir el mensaje “Has ganado” (parcheando el  
binario). Describe el proceso  
7 - Por último, obtén uno varios códigos de licencia correctos. En este caso, al describir el  
proceso deberás hacerlo usando el código ensamblador, sin usar el pseudocódigo  
proporcionado por el decompilador.

=======
#### 1- Dado el binario analízalo brevemente y describe por encima que simula este binario.  
Simula el funcionamiento de un casino en el que jugador inteta adividnar una casilla correcta para ir acumulando puntos hasta llegar a 10 000 puntos para poder ganar. El algoritmo es el siguiente. Primero inicializa el programa y pide una licencia para verificar si es valida , en el caso de que no lo sea termina el programa y si es valida crea un objeto que representa al casino y da la bienvenida al jugador. A continuación  entra en el bucle y empezaría el juego, cuando llegue a los 10.000 puntos se termina el juego indicando que ha ganado.
#### 2- Al igual que en la práctica anterior describe las funciones definidas por el programador.  
La función **sub_132D** es la que verifica si la licencia del jugador es correcta. para que sea valida el primer caracter(el menos signfiicativo) tiene que ser par en ascci, el cuarto 1,el quinto - , el sexto y el noveno tiene que ser 2.

La función **sub_1ACC** representa el constructor del casino, que inicializa la puntuación a cero y establece la casilla ganadora en 42.

**sub_1ACC** En está sección también esta la función saludar la cual se utilizar para dar la bienvenida al jugador cuando entra al juego.

La función **sub_1B32** Se encarga de imprimir las instrucciones al jugador. Muestra el siguiente mensaje: **Para ganar tienes que sumar 10.000 puntos**.

La función **sub_1B76** es la que simula el juego, en esta casilla se comprueba si el número que ha introducido el jugador corresponde con el número 42, si es así muestra que "has ganado" e incrementa el contador y devuelve 1 para indicar que siga jugando en el caso de que no es así devuelve 0 y termina el juego.

La función **sub_1C38** es la que comprueba si has ganado para ello compara tu puntación con 9999 si es mayor imprime el mensaje de vitoria.

**sub_1C86** esta función es un get que devuelve el valor acumulado de la puntación.

#### 3- ¿En qué lenguaje crees que está escrito el binario?, en caso de ser un lenguaje orientado a objetos identifica al menos un constructor de clase.  
Se ha hecho en c++ ya que es un lenguaje orientado a objetos como prueba de ello esta en el constructor que está definido en la función **sub_1ACC** .

#### 4 - En primer lugar consigue parchear la petición de licencia para evitarla. Describe el  proceso  
Para  parchear pues tenemos que cambiar la comprobación en la función sub_132D
hacemos un reverse jump en los jne que hay dentro de la función.
![[Pasted image 20250407233740.png]]
Quedando de resultado así.
![[Pasted image 20250407233913.png]]
Cerramos la aplicación y la ejecutamos para comprobar si ha funcionado.
![[Pasted image 20250407234209.png]]
#### 5 - En segundo lugar parchea el nombre del jugador para que aparezca el tuyo. Describe  el proceso  

Para el nombre primero tenemos que encontrar donde está USUARIO UAH 
Y nos fijamos en la posición de memoria.

![[Pasted image 20250407235222.png]]
Es la posición 203b, en un editor hexadecimal cambiamos el nombre por el nuestro.
He utilizado ghex y he cambiado usuario uah por carlos 
![[Pasted image 20250408001611.png]]
El cambio se ha hecho en la sección de data.
![[Pasted image 20250408001449.png]]
#### 6 - En tercer lugar intenta conseguir imprimir el mensaje “Has ganado” (parcheando el  binario). Describe el proceso  

Cambiamos el comparado de funcion que compara la puntación que es la sub_1C38 
![[Pasted image 20250408004034.png]]
He rellando el equals con nops  para que no salte y muestre el mensaje de que has ganado
![[Pasted image 20250408004408.png]]
![[Pasted image 20250408004728.png]]
#### 7 - Por último, obtén uno varios códigos de licencia correctos. En este caso, al describir el  proceso deberás hacerlo usando el código ensamblador, sin usar el pseudocódigo  proporcionado por el decompilador.
La función que se encarga de la validación de la licencia es la siguiente:
sub_132D.
![[Pasted image 20250407132236.png]]
Lo primero que hace para ver si es par el lsbl es fijarse si acaba en 0, para ello utiliza la operación and y luego hace un test. para el resto de operaciones se va desplazadando el registros eax y comprueba haciendo cmp con lo valores anteriromete descritos en  apartados anteriores.

Para ello utilizo el siguiente código para generar licencias hecho en python.

```python
import random
import string

def generar_licencia_valida():
    while True:
        licencia = list('X' * 9)

        # a1[0] debe tener bit menos significativo en 0 => ASCII par
        licencia[0] = random.choice([c for c in string.ascii_letters + string.digits if ord(c) % 2 == 0])
        
        # Fijamos las posiciones clave
        licencia[3] = '1'
        licencia[4] = '-'
        licencia[5] = '2'
        licencia[8] = '2'

        # Rellenamos los demás caracteres con letras o números aleatorios
        for i in range(9):
            if licencia[i] == 'X':
                licencia[i] = random.choice(string.ascii_uppercase + string.digits)

        return ''.join(licencia)

# Generar varias licencias válidas
for _ in range(10):
    print(generar_licencia_valida())
```
Probarnos una de las licencias que nos ha generado el programa:
![[Pasted image 20250407131612.png]]
Y nos da la bienvenida.
Otras licencias son:
t5C1-2I42  
40Y1-2JU2  
V8X1-2202  
h9N1-2X32  
r2W1-2QJ2  
T1T1-2UU2  
V3N1-2OB2  
8Q71-29I2  
h5S1-2CH2
>>>>>>> origin/main
# codigo 
Main  sub_1391
```c 
// bad sp value at call has been detected, the output may be wrong!
int __cdecl main(int argc, const char **argv, const char **envp)
{
  int v3; // eax
  Casino *v4; // edi
  int v5; // eax
  Casino *v6; // edi
  int Puntuacion; // eax
  int v8; // eax
  Casino *v9; // ebx
  int v11; // eax
  int v12; // [esp+10h] [ebp-50h] BYREF
  int v13; // [esp+14h] [ebp-4Ch]
  Casino *v14; // [esp+18h] [ebp-48h]
  char *s; // [esp+1Ch] [ebp-44h]
  int *v16; // [esp+20h] [ebp-40h]
  int v17[6]; // [esp+24h] [ebp-3Ch] BYREF
  char v18[4]; // [esp+3Ch] [ebp-24h] BYREF
  Casino *v19; // [esp+40h] [ebp-20h]
  int *p_argc; // [esp+50h] [ebp-10h]

  p_argc = &argc;
  v3 = std::operator<<<std::char_traits<char>>(&std::cout, &unk_2008);
  std::ostream::operator<<(v3, &std::endl<char,std::char_traits<char>>);
  std::operator>><char,std::char_traits<char>>(&std::cin, v18);
  if ( checkLicencia(v18) )
  {
    v4 = (Casino *)operator new(0x20u);
    Casino::Casino(v4);
    v14 = v4;
    s = "USUARIO UAH";
    v16 = &v12;
    std::string::basic_string<std::allocator<char>>((int)v17, "USUARIO UAH", (int)&v12);
    Casino::saludar((int)v4, (int)v17);
    std::string::~string(v17);
    std::__new_allocator<char>::~__new_allocator(&v12);
    v19 = v14;
    Casino::imprimirInstrucciones();
    v13 = 1;
    while ( v13 == 1 )
    {
      v12 = 0;
      v5 = std::operator<<<std::char_traits<char>>(&std::cout, "A que casilla quieres apostar: \n");
      std::ostream::operator<<(v5, &std::endl<char,std::char_traits<char>>);
      std::istream::operator>>(&std::cin, &v12);
      v13 = Casino::jugar(v14, v12);
      v6 = v14;
      Puntuacion = Casino::getPuntuacion(v14);
      Casino::hasGanado(v6, Puntuacion);
    }
    v8 = std::operator<<<std::char_traits<char>>(&std::cout, &unk_206C);
    std::ostream::operator<<(v8, &std::endl<char,std::char_traits<char>>);
    v9 = v14;
    if ( v14 )
    {
      Casino::~Casino(v14);
      operator delete(v9, 0x20u);
    }
    return 0;
  }
  else
  {
    v11 = std::operator<<<std::char_traits<char>>(
            &std::cout,
            "La licencia introducida para este programa no es correcta");
    std::ostream::operator<<(v11, &std::endl<char,std::char_traits<char>>);
    return 0;
  }

}
```
checkLicense sub_132D
```c
_BOOL4 __cdecl checkLicencia(const char *a1)
{
  int v2; // [esp+Ch] [ebp-4h]

  v2 = 0;
  if ( (*a1 & 1) == 0 && a1[4] == 45 && a1[3] == 49 && a1[5] == 50 )
    return a1[8] == 50;
  return v2;
}
```


Casino sub_1ACC
```c
void __cdecl Casino::Casino(Casino *this)
{
  _BYTE v1[5]; // [esp+17h] [ebp-11h] BYREF
  unsigned int v2; // [esp+1Ch] [ebp-Ch]

  v2 = __readgsdword(0x14u);
  *(_DWORD *)&v1[1] = v1;
  std::string::basic_string<std::allocator<char>>((int)this, "DEFAULT NAME", (int)v1);
  std::__new_allocator<char>::~__new_allocator(v1);
  *((_DWORD *)this + 6) = 0;
  *((_DWORD *)this + 7) = 42;
}
```
Saludar -> sub_1ACC
```c
int __cdecl Casino::saludar(int a1, int a2)
{
  int v2; // eax
  int v3; // eax

  std::string::operator=(a1, a2);
  v2 = std::operator<<<std::char_traits<char>>(&std::cout, "Bienvenido: ");
  v3 = std::operator<<<char>(v2, a1);
  return std::ostream::operator<<(v3, &std::endl<char,std::char_traits<char>>);
}
```
imprimirInstrucciones->sub_1B32
```c
int Casino::imprimirInstrucciones()
{
  int v0; // eax

  v0 = std::operator<<<std::char_traits<char>>(&std::cout, "Para ganar tienes que sumar 10.000 puntos\n");
  return std::ostream::operator<<(v0, &std::endl<char,std::char_traits<char>>);
}
```

jugar sub_1B76
```c 
int __cdecl Casino::jugar(Casino *this, int a2)
{
  int v2; // eax
  int v3; // eax
  int v4; // eax

  if ( a2 != *((_DWORD *)this + 7) )
    return 0;
  ++*((_DWORD *)this + 6);
  v2 = std::operator<<<std::char_traits<char>>(&std::cout, &unk_2157);
  v3 = std::ostream::operator<<(v2, *((_DWORD *)this + 6));
  std::ostream::operator<<(v3, &std::endl<char,std::char_traits<char>>);
  v4 = std::operator<<<std::char_traits<char>>(&std::cout, &unk_216B);
  std::ostream::operator<<(v4, &std::endl<char,std::char_traits<char>>);
  Casino::hasGanado(this, *((_DWORD *)this + 6));
  return 1;
}
```
has ganado sub_1C38
```c 
void __cdecl Casino::hasGanado(Casino *this, int a2)
{
  int v2; // eax

  if ( a2 > 9999 )
  {
    v2 = std::operator<<<std::char_traits<char>>(&std::cout, &unk_216D);
    std::ostream::operator<<(v2, &std::endl<char,std::char_traits<char>>);
  }
}
```
getPuntuación  sub_1C86
```c 
int __cdecl Casino::getPuntuacion(Casino *this)
{
  return *((_DWORD *)this + 6);
}
```