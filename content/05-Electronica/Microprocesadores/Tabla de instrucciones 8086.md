---
title: "Tabla de instrucciones 8086"
---

# Tabla de instrucciones 8086

## INSTRUCCIONES DE TRANSFERENCIA

| Mnemónico | Operandos (Destino, Fuente) | Flags | Descripción |
|---|---|---|---|
| MOV | REG,MEM/REG; MEM/REG,REG; MEM/REG,NUM | No altera flags | COPIA EL OPERANDO FUENTE EN EL OPERANDO DESTINO. Ambos operandos deben ser del mismo tipo (BYTE O PALABRA). RESTRICCIONES: No se pueden mover datos entre dos elementos de memoria. No se puede usar MOV para transferir un valor inmediato a un registro de segmento. Ante cualquiera de estos dos casos, si es necesario, se usará un registro auxiliar. El registro CS no puede ser usado como destino. |
| PUSH | REG 16; MEM 16 | No altera flags | METE EL OPERANDO EN LA PILA. Decrementa en dos unidades el contenido del Puntero de Pila (SP) y después almacena la palabra especificada por el operando en la posición indicada por el puntero de pila (SS:SP). RESTRICCIONES: Solo se pueden guardar en la pila operandos tipo palabra, y antes hay que inicializar los registros SS y SP. |
| POP | REG 16; MEM 16 | No altera flags | SACA UNA PALABRA DE LA PILA. Transfiere la palabra de la pila, direccionada por SS:SP al operando destino (tipo palabra), y después incrementa en dos unidades el registro SP. El contenido de la pila no se borra, sino que el puntero es modificado. RESTRICCIONES: El registro CS no puede ser especificado como destino. |
| XCHG | MEM/REG,REG | No altera flags | INTERCAMBIA EL CONTENIDO DE LOS DOS OPERANDOS. Pueden ser byte o palabra, pero los DOS del mismo tamaño. RESTRICCIONES: No se puede intercambiar dos posiciones de memoria. Para ello, se usa un registro auxiliar. No pueden ser operandos registros de segmento. |
| XLAT | (ninguno) | No altera flags | TRADUCE. Convierte caracteres de un código en otro. Reemplaza un byte contenido en AL, por un byte de una tabla de conversión (256 bytes de longitud máxima) creada por el usuario. AL es el índice de la tabla. BX apunta al comienzo de la tabla. AL=DS:BX+AL. |
| IN | AL,PORT; AL,DX; AX,PORT; AX,DX | No altera flags | COPIA EL CONTENIDO DE UN PUERTO DE ENTRADA EN EL ACUMULADOR. Tamaño byte o palabra, se almacena en AL o AX respectivamente. Si la dirección del puerto está entre 0 y 255, se especifica directamente en la instrucción. En general, para direcciones entre 0h y FFFFh, se carga en DX la dirección (variable). |
| OUT | PORT,AL; PORT,AX; DX,AL; DX,AX | No altera flags | TRANSFIERE UN BYTE O PALABRA (ubicado en AL o AX respectivamente) AL PUERTO DE SALIDA ESPECIFICADO. La dirección del puerto puede ser un valor fijo de un byte (de 0 a FFh), o un valor variable que puede ser modificado por el programa, almacenado en DX (de 0 a FFFFh). |
| LEA | REG 16,MEM | No altera flags | CARGA LA DIRECCIÓN EFECTIVA. Carga el desplazamiento (offset) de la dirección de memoria origen en el registro de 16 bits indicado como destino. RESTRICCIONES: No puede usarse como destino ningún registro de segmento. NOTA: (LEA=dirección, MOV=contenido de la dirección). |
| LDS | REG 16,MEM | No altera flags | CARGA EL SEGMENTO DE DATOS. Carga el registro de 16 bits especificado como destino con el contenido de la palabra almacenada en la dirección MEM. Las posiciones involucradas son: (byte bajo de REG16)=MEM, (byte alto de REG16)=MEM+1, (byte bajo de DS)=MEM+2, (byte alto de DS)=MEM+3. RESTRICCIONES: No se puede usar como destino un registro de segmento. NOTA: LDS se suele usar para inicializar SI y DS antes de usar instrucciones de cadena. |
| LES | REG 16,MEM | No altera flags | CARGA EL SEGMENTO EXTRA. Carga el registro de 16 bits especificado como destino con el contenido de la palabra almacenada en la dirección MEM. Las posiciones involucradas son: (byte bajo de REG16)=MEM, (byte alto de REG16)=MEM+1, (byte bajo de ES)=MEM+2, (byte alto de ES)=MEM+3. RESTRICCIONES: No se puede usar como destino un registro de segmento. NOTA: LES se suele usar para inicializar DI y ES antes de usar instrucciones de cadena. |
| PUSHF | (ninguno) | No altera flags | GUARDA EN LA PILA LA PALABRA DE ESTADO. Decrementa en dos unidades el registro SP, y guarda en la dirección de pila indicada por SS:SP el registro de flags PSW. |
| POPF | (ninguno) | OF,DF,IF,TF,SF,ZF,AF,PF,CF | SACA UNA PALABRA DE LA PILA AL REGISTRO PSW. Saca la palabra de la dirección más baja de la pila (SS:SP) y la copia sobre el registro de estado del procesador (PSW). Posteriormente incrementa en dos unidades el puntero de pila SP. |
| LAHF | (ninguno) | No altera flags | ALMACENA EL BYTE BAJO DE PSW (flags SF, ZF, AF, PF y CF) EN AH. Sirve para ejecutar correctamente sobre un 8088/86 programas escritos para un 8080 o un 8085. |
| SAHF | (ninguno) | SF,ZF,AF,PF,CF | ALMACENA EL REGISTRO AH EN EL BYTE MENOS SIGNIFICATIVO DE PSW. Sirve para ejecutar correctamente sobre un 8088/86 programas escritos para un 8080 o un 8085. |

## INSTRUCCIONES ARITMÉTICAS

| Mnemónico | Operandos (Destino, Fuente) | Flags | Descripción |
|---|---|---|---|
| ADD | REG,MEM/REG; MEM/REG,REG; MEM/REG,NUM | OF,SF,ZF,AF,PF,CF | SUMAR. Suma el operando fuente al operando destino, almacenando el resultado en el operando destino. Los operandos pueden ser de tipo byte o palabra, pero AMBOS DEL MISMO TIPO. RESTRICCIONES: No se permite la suma de dos posiciones de memoria. |
| ADC | REG,MEM/REG; MEM/REG,REG; MEM/REG,NUM | OF,SF,ZF,AF,PF,CF | SUMAR CON ACARREO. Suma el operando fuente al operando destino, almacenando el resultado en el operando destino. Los operandos pueden ser de tipo byte o palabra, pero AMBOS DEL MISMO TIPO. Si el flag de CARRY (CF) está activado, suma uno al resultado. RESTRICCIONES: No se permite la suma de dos posiciones de memoria. |
| INC | REG; MEM | OF,SF,ZF,AF,PF (no afecta a CF) | INCREMENTA EL DESTINO EN UNA UNIDAD. Suma uno a la dirección de memoria o registro especificado. Si dicho operando de destino era FFFFh, pasará a valer 0000h después de la ejecución de INC, y no se pondrá a '1' el flag CF. |
| AAA | (ninguno) | AF,CF (se activan si el nº en AL antes de AAA es > 9) | AJUSTE ASCII PARA LA SUMA. Sólo opera sobre el registro AL, corrigiendo el resultado de una suma de dos números BCD desempaquetados (cada nº BCD viene representado por 8 bits) y convirtiéndolo en un número BCD desempaquetado. |
| DAA | (ninguno) | SF,ZF,AF,PF,CF | AJUSTE DECIMAL PARA LA SUMA. Corrige el resultado almacenado en AL correspondiente a la suma de dos números BCD empaquetados, convirtiéndolo en un número BCD empaquetado. Si el nibble (cuatro bits) de menor peso es superior a 9 o bien la bandera AF se activó durante la suma, la instrucción DAA le suma 6. Si el nuevo valor del nibble de mayor peso es ahora mayor que 9 o bien el flag CF está a '1', se suma 60h al registro AL. |
| SUB | REG,MEM/REG; MEM/REG,REG; MEM/REG,NUM | OF,SF,ZF,AF,PF,CF | RESTAR. Resta el operando fuente del operando destino, almacenando el resultado en el operando destino. Los operandos pueden ser de tipo byte o palabra, pero AMBOS DEL MISMO TIPO. RESTRICCIONES: No se permite la resta de dos posiciones de memoria. |
| SBB | REG,MEM/REG; MEM/REG,REG; MEM/REG,NUM | OF,SF,ZF,AF,PF,CF | RESTA CON BORROW. Resta el operando fuente del operando destino, almacenando el resultado en el operando destino. Los operandos pueden ser de tipo byte o palabra, pero AMBOS DEL MISMO TIPO. Si la bandera de arrastre está activada (CF=1), se resta 1 al resultado. RESTRICCIONES: No se permite la resta de dos posiciones de memoria. |
| DEC | REG; MEM | OF,SF,ZF,AF,PF (no afecta a CF) | DECREMENTA EL DESTINO EN UNA UNIDAD. Resta uno al operando destino. Dicho operando puede estar almacenado en una posición de memoria o en un registro, y su tamaño puede ser byte o palabra. |
| NEG | REG; MEM | OF,SF,ZF,AF,PF,CF | FORMAR EL COMPLEMENTO A 2. Invierte el signo del operando destino. El operando puede ser una posición de memoria o un registro. |
| CMP | REG,MEM/REG; MEM/REG,REG; MEM/REG,NUM | OF,DF,SF,ZF,AF,PF,CF | COMPARAR DOS OPERANDOS. Lo hace mediante la resta del operando fuente del destino. El resultado NO es almacenado, y sólo se actualiza el contenido de los flags. Los operandos pueden ser de tipo byte o palabra, pero AMBOS DEL MISMO TIPO. RESTRICCIONES: No se permite la comparación entre dos posiciones de memoria. |
| AAS | (ninguno) | AF,CF (se activan si el nº en AL antes de AAS es > 9) | AJUSTE ASCII PARA LA RESTA. Corrige el resultado en AL de la resta de dos números decimales desempaquetados, convirtiéndolo en un valor decimal desempaquetado. |
| DAS | (ninguno) | SF,ZF,AF,PF,CF | AJUSTE DECIMAL PARA LA RESTA. Corrige el resultado almacenado en AL correspondiente a la resta de dos números BCD empaquetados, convirtiéndolo en un número BCD empaquetado. Si el nibble (4 bits) de menor peso es superior a 9 o bien el flag AF se activó durante la resta, la instrucción DAS le resta 6. Si el nuevo valor del nibble de mayor peso es ahora mayor que 9 o bien el flag CF está a 1, se resta 60h al registro AL. |
| MUL | REG; MEM | OF,CF (se activan cuando la mitad superior del resultado -en DX ó AH- no sea 0) | MULTIPLICAR SIN SIGNO. Multiplica un nº sin signo tamaño byte por un nº sin signo tamaño byte contenido en AL guardando el resultado en AX (AX=AL * operando byte) o multiplica un nº sin signo tamaño word por un nº sin signo tamaño word contenido en AX guardando el resultado en DX (palabra más significativa) y en AX (palabra menos significativa) (DX AX=AX * operando word). |
| IMUL | REG; MEM | OF,CF (se activan cuando la mitad superior del resultado -en DX ó AH- no sea 0) | MULTIPLICA CON SIGNO. Multiplica un nº con signo tamaño byte por un nº con signo tamaño byte contenido en AL guardando el resultado en AX (AX=AL * operando byte) o multiplica un nº con signo tamaño word por un nº con signo tamaño word contenido en AX guardando el resultado en DX (palabra más significativa) y en AX (palabra menos significativa) (DX AX=AX * operando word). |
| AAM | (ninguno) | SF,ZF,PF | AJUSTE ASCII PARA LA MULTIPLICACIÓN. Corrige el resultado en AX del producto de dos números decimales desempaquetados, convirtiéndolo en un valor desempaquetado. (AH=cociente de AL/10) y (AL=resto de AL/10). |
| DIV | REG; MEM | Todos los flags quedan INDEFINIDOS | DIVIDIR SIN SIGNO. Divide el contenido del acumulador y su extensión (AH AL si el operando es de tipo byte, o DX AX si el operando es de tipo word) entre el operando fuente. Hay dos posibilidades: Dividir 16 bits entre 8 bits (Dividendo=AX, Divisor=fuente 8bits, Cociente=AL, Resto=AH) o dividir 32 bits entre 16 bits (Dividendo=DX AX, Divisor=operando 16bits, Cociente=AX, Resto=DX). Se genera una interrupción de tipo 0 si el cociente supera FFh o FFFFh respectivamente. |
| IDIV | REG; MEM | Todos los flags INDEFINIDOS. Signo resto=signo dividendo | DIVIDIR CON SIGNO. Divide el contenido del acumulador y su extensión (AH AL si el operando es de tipo byte, o DX AX si el operando es de tipo word) entre el operando fuente. Hay dos posibilidades: Dividir 16 bits entre 8 bits (Dividendo=AX, Divisor=fuente 8bits, Cociente=AL, Resto=AH) o dividir 32 bits entre 16 bits (Dividendo=DX AX, Divisor=operando 16bits, Cociente=AX, Resto=DX). Interrupción de tipo 0 si 7Fh<cociente<81h ó 7FFFh<cociente<8001h respectivamente. |
| AAD | (ninguno) | SF,ZF,PF | AJUSTE ASCII PARA LA DIVISIÓN. Convierte dos dígitos en código BCD desempaquetado almacenados en AH y AL en el correspondiente nº binario. El resultado es almacenado en AL. |
| CBW | (ninguno) | No altera flags | CONVIERTE BYTE EN WORD. Copia el bit de signo del byte almacenado en AL sobre todos los bits de AH. A esta operación se denomina extensión del signo de AL. Si es sin signo, se rellena los bits más significativos con 0. Si es con signo, se rellena los bits más significativos con el bit de mayor peso. |
| CWD | (ninguno) | No altera flags | CONVIERTE WORD EN DOUBLEWORD. Copia el bit de signo de la palabra almacenada en AX sobre todos los bits de DX. A esta operación se denomina extensión del signo de AX en DX. |

## INSTRUCCIONES LÓGICAS

| Mnemónico | Operandos (Destino, Fuente) | Flags | Descripción |
|---|---|---|---|
| NOT | REG; MEM | No altera flags | NO LÓGICO. Forma el complemento a uno del operando, esto es, cambia los ceros por unos y los unos por ceros. El operando puede ser un registro o una posición de memoria de tamaño byte o word. |
| AND | REG,MEM/REG; MEM/REG,REG; MEM/REG,NUM | OF=0,SF,ZF,PF,CF=0 (AF indefinida) | Y LÓGICO. Realiza la operación lógica AND entre los operandos fuente y destino, realizada bit a bit y almacenada en el destino. RESTRICCIONES: No se puede realizar la operación entre dos posiciones de memoria. |
| OR | REG,MEM/REG; MEM/REG,REG; MEM/REG,NUM | OF=0,SF,ZF,PF,CF=0 (AF indefinida) | O LÓGICO. Realiza la operación OR inclusiva entre los operandos fuente y destino, realizada bit a bit y almacenada en el destino. RESTRICCIONES: No se puede realizar la operación entre dos posiciones de memoria. |
| XOR | REG,MEM/REG; MEM/REG,REG; MEM/REG,NUM | OF=0,SF,ZF,PF,CF=0 (AF indefinida) | O LÓGICO EXCLUSIVO. Realiza la operación lógica OR exclusiva entre los operandos fuente y destino, realizada bit a bit y almacenada en el destino. RESTRICCIONES: No se puede realizar la operación entre dos posiciones de memoria. |
| TEST | REG,MEM/REG; MEM/REG,REG; MEM/REG,NUM | OF=0,SF,ZF,PF,CF=0 (AF indefinida) | AND LÓGICA. Realiza la operación lógica AND entre los operandos fuente y destino, realizada bit a bit pero sin almacenar el destino. Se actualizan los flags. RESTRICCIONES: No se puede realizar la operación entre dos posiciones de memoria. |

## INSTRUCCIONES DE DESPLAZAMIENTO Y ROTACIÓN

| Mnemónico | Operandos (Destino, Fuente) | Flags | Descripción |
|---|---|---|---|
| ROL | MEM/REG,1; MEM/REG,CL | OF,CF | ROTAR A LA IZQUIERDA los bits del operando destino el número de veces especificado en el operando fuente (los bits se van moviendo una posición hacia la izquierda). Si el nº de veces es 1, se puede especificar directamente. Si no, hay que usar CL. CF copia en cada rotación el bit más significativo. (ver esquema de DESPLAZAMIENTOS) |
| RCL | MEM/REG,1; MEM/REG,CL | OF,CF | ROTA A LA IZQUIERDA USANDO EL ACARREO. Rota hacia la izquierda los bits del operando destino y la bandera de acarreo un número de veces especificado en el operando fuente. Si el nº de veces es 1, se puede especificar directamente. Si no, hay que usar CL. Los bits se van moviendo una posición hacia la izquierda. El bit más significativo se almacena en CF y el contenido de CF pasa a ser el bit menos significativo. (ver esquema de DESPLAZAMIENTOS) |
| ROR | MEM/REG,1; MEM/REG,CL | OF,CF | ROTAR A LA DERECHA los bits del operando destino el número de veces especificado en el operando fuente (los bits se van moviendo una posición hacia la derecha). Si el nº de veces es 1, se puede especificar directamente. Si no, hay que usar CL. CF copia en cada rotación el bit más significativo. (ver esquema de DESPLAZAMIENTOS) |
| RCR | MEM/REG,1; MEM/REG,CL | OF,CF | ROTA A LA DERECHA USANDO EL ACARREO. Rota hacia la derecha los bits del operando destino y la bandera de acarreo un número de veces especificado en el operando fuente. Si el nº de veces es 1, se puede especificar directamente. Si no, hay que usar CL. Los bits se van moviendo una posición hacia la derecha. El bit menos significativo se almacena en CF y el contenido de CF pasa a ser el bit más significativo. (ver esquema de DESPLAZAMIENTOS) |
| SAL | MEM/REG,1; MEM/REG,CL | OF,SF,ZF,PF,CF | DESPLAZAMIENTO ARITMÉTICO A LA IZQUIERDA. Desplaza hacia la izquierda los bits del operando destino el número de veces indicado por el operando fuente, siendo colocado un cero en el bit menos significativo en cada desplazamiento. Si el nº de veces es 1, se puede especificar directamente. Si no, hay que usar CL. (ver esquema de DESPLAZAMIENTOS). NOTA: SAL y SHL son la misma instrucción máquina. Actúan igual. |
| SHL | MEM/REG,1; MEM/REG,CL | OF,SF,ZF,PF,CF | DESPLAZAMIENTO LÓGICO A LA IZQUIERDA. Desplaza hacia la izquierda los bits del operando destino el número de veces indicado por el operando fuente, siendo colocado un cero en el bit menos significativo en cada desplazamiento. Si el nº de veces es 1, se puede especificar directamente. Si no, hay que usar CL. (ver esquema de DESPLAZAMIENTOS). NOTA: SAL y SHL son la misma instrucción máquina. Actúan igual. |
| SAR | MEM/REG,1; MEM/REG,CL | OF,SF,ZF,PF,CF | DESPLAZAMIENTO ARITMÉTICO A LA DERECHA. Desplaza hacia la derecha los bits del operando destino el número de veces indicado por el operando fuente, siendo colocado una copia del bit más significativo en el bit más significativo en cada desplazamiento. Así, el bit de signo inicial se mantiene. Si el nº de veces es 1, se puede especificar directamente. Si no, hay que usar CL. El bit que sale por la derecha va a CF. (ver esquema de DESPLAZAMIENTOS) |
| SHR | MEM/REG,1; MEM/REG,CL | OF,SF,ZF,PF,CF | DESPLAZAMIENTO LÓGICO A LA DERECHA. Desplaza hacia la derecha los bits del operando destino el número de veces indicado por el operando fuente, siendo colocado un cero en el bit más significativo en cada desplazamiento. Así, el bit de signo inicial se mantiene. Si el nº de veces es 1, se puede especificar directamente. Si no, hay que usar CL. El bit que sale por la derecha (el menos significativo) va a CF. (ver esquema de DESPLAZAMIENTOS) |

## INSTRUCCIONES DE CADENA

| Mnemónico | Operandos (Destino, Fuente) | Flags | Descripción |
|---|---|---|---|
| MOVSB | (ninguno) | No altera flags | MUEVE CADENAS de BYTES. Transfiere un byte de una dirección de memoria dada por DS:SI a otra posición de memoria dada por ES:DI. Tras la transferencia, SI y DI son automáticamente actualizados para apuntar al siguiente elemento de la cadena. Si el flag DF es '0', SI y DI incrementan una unidad. Si el flag DF es '1', SI y DI decrementan una unidad. NOTA: Se puede usar REP para conseguir transferencias múltiples, guardando en CX el nº de transferencias a realizar. |
| MOVSW | (ninguno) | No altera flags | MUEVE CADENAS de PALABRAS. Transfiere una palabra de una dirección de memoria dada por DS:SI a otra posición de memoria dada por ES:DI. Tras la transferencia, SI y DI son automáticamente actualizados para apuntar al siguiente elemento de la cadena. Si el flag DF es '0', SI y DI incrementan dos unidades. Si el flag DF es '1', SI y DI decrementan dos unidades. NOTA: usar REP para transferencias múltiples, guardando en CX el nº de transferencias a realizar. |
| CMPSB | (ninguno) | OF,SF,ZF,AF,PF,CF | COMPARA CADENAS BYTE A BYTE. Compara la cadena ubicada en la dirección de memoria dada por DS:SI con otra cadena situada en la posición de memoria dada por ES:DI. No se modifica ninguna cadena, sólo los flags. Tras la comparación, SI y DI son automáticamente actualizados para apuntar al siguiente elemento de la cadena. Si el flag DF es '0', SI y DI incrementan una unidad. Si el flag DF es '1', SI y DI decrementan una unidad. NOTA: Se puede usar REP para conseguir comparaciones múltiples, guardando en CX el nº de comparaciones a realizar. |
| CMPSW | (ninguno) | OF,SF,ZF,AF,PF,CF | COMPARA CADENAS WORD A WORD. Compara la cadena ubicada en la dirección de memoria dada por DS:SI con otra cadena situada en la posición de memoria dada por ES:DI. No se modifica ninguna cadena, sólo los flags. Tras la comparación, SI y DI son automáticamente actualizados para apuntar al siguiente elemento de la cadena. Si el flag DF es '0', SI y DI incrementan dos unidades. Si el flag DF es '1', SI y DI decrementan dos unidades. NOTA: Se puede usar REP para conseguir comparaciones múltiples, guardando en CX el nº de comparaciones a realizar. |
| SCASB; SCASW | (ninguno) | OF,SF,ZF,AF,PF,CF | EXPLORA UNA CADENA (DE BYTES O PALABRAS) COMPARANDO SUS ELEMENTOS CON EL ACUMULADOR. Compara la cadena ubicada en la dirección de memoria dada por ES:DI con el acumulador (AL si es byte, AX si es word). No se modifica la cadena, sólo los flags. Tras la comparación, DI es automáticamente actualizado para apuntar al siguiente elemento de la cadena. Si el flag DF es '0', DI incrementan y si el flag DF es '1', DI decrementa (una unidad si es byte, dos si es word). NOTA: Se puede usar REP para conseguir comparaciones múltiples, guardando en CX el nº de comparaciones a realizar. Al final, DI guardará la dirección siguiente a aquella en la que se encontró un elemento igual al acumulador. |
| LODSB; LODSW | (ninguno) | No altera flags | CARGA CADENA (DE BYTES O PALABRAS) EN EL ACUMULADOR. Transfiere un byte o word de la cadena ubicada en la dirección de memoria dada por DS:SI a AL o AX respectivamente. Tras la transferencia, SI es automáticamente actualizado para apuntar al siguiente elemento de la cadena. Si el flag DF es '0', SI incrementan y si el flag DF es '1', SI decrementa (una unidad si es byte, dos si es word). |
| STOSB; STOSW | (ninguno) | No altera flags | ALMACENA EL CONTENIDO DEL ACUMULADOR EN UNA CADENA. Transfiere el contenido del acumulador (AL o AX dependiendo de si la cadena es byte o word respectivamente) en la dirección de memoria dada por ES:DI. Tras la transferencia, DI es automáticamente actualizado para apuntar al siguiente elemento de la cadena. Si el flag DF es '0', DI incrementan y si el flag DF es '1', DI decrementa (una unidad si es byte, dos si es word). NOTA: Se puede usar REP para conseguir transferencias múltiples, guardando en CX el nº de transferencias a realizar. |
| REP | (ninguno) | No altera flags | REPITE LA INSTRUCCIÓN DE CADENA SIGUIENTE (instrucción de cadena). Se usa en combinación con el registro CX. Decrementa el contenido de CX en una unidad y se ejecuta la siguiente instrucción de cadena hasta que CX sea cero. NOTA: SÓLO ACTÚA SOBRE LA SIGUIENTE INSTRUCCIÓN DE CADENA. |
| REPE; REPZ | (ninguno) | No altera flags | REPITE LA INSTRUCCIÓN DE CADENA SIGUIENTE (instrucción de cadena). REPE y REPZ son dos nemónicos para la misma instrucción máquina. Se suelen usar con las instrucciones CMPS y SCAS. Repiten la instrucción de cadena mientras las cadenas sean iguales, ZF='1' y/o CX distinto de '0'. NOTA: SÓLO ACTÚA SOBRE LA SIGUIENTE INSTRUCCIÓN DE CADENA. PARA REPETIR UN BLOQUE DE INSTRUCCIONES SE USARÁ LOOP. |
| REPNE; REPNZ | (ninguno) | No altera flags | REPITE LA INSTRUCCIÓN DE CADENA SIGUIENTE (instrucción de cadena). REPNE y REPNZ son dos nemónicos para la misma instrucción máquina. Se suelen usar con las instrucciones CMPS y SCAS. Repiten la instrucción de cadena mientras las cadenas sean DISTINTAS, ZF='0' y/o CX distinto de '0'. NOTA: SÓLO ACTÚA SOBRE LA SIGUIENTE INSTRUCCIÓN DE CADENA. PARA REPETIR UN BLOQUE DE INSTRUCCIONES SE USARÁ LOOP. |

## INSTRUCCIONES DE CONTROL DE PROGRAMA

| Mnemónico | Operandos (Destino, Fuente) | Flags | Descripción |
|---|---|---|---|
| CALL | [ADR]; REG:OFFSET; REG (solo 127 posiciones arriba o abajo) | No altera flags | LLAMADA A SUBRUTINA. Transfiere la ejecución del programa principal a una subrutina. Se salva la dirección de la instrucción siguiente para continuar cuando termine la subrutina. Hay dos tipos de llamadas: NEAR y FAR. NEAR es para llamar a subrutinas en el mismo segmento de código (CALL NEAR decrementa SP en dos unidades y salva en la pila el IP correspondiente a la siguiente instrucción). FAR es para llamar a subrutinas en otro segmento (CALL FAR decrementa SP en dos unidades, salva en la pila el contenido del registro CS, decrementa SP otras dos unidades, y salva en la pila el IP de la siguiente instrucción (CS:IP que son 20 bits), y por último coloca en CS:IP la dirección de comienzo de la subrutina. RET termina la subrutina). |
| RET | (NUM) opcional | No altera flags | RETORNO DE SUBRUTINA. Devuelve el control al programa principal. Carga la dirección completa de la instrucción siguiente a la CALL que originó la llamada. Si la subrutina es NEAR, RET sustituye el contenido del registro IP por la palabra situada en la parte más baja de la pila (apuntada por SP). Tras esto, SP incrementa dos unidades. Si la subrutina es FAR, se sacan dos palabras de la pila. La primera se carga en el registro IP y la segunda en el CS. En total SP se incrementa en 4 unidades. Si se coloca un valor numérico tras RET, SP se incrementa de forma extra en la misma cantidad (esto es útil cuando se pasan parámetros a través de la pila). |
| JMP | DIRECCIÓN | No altera flags | SALTO INCONDICIONAL. Puede ser directo (lo que sigue a JMP es la dirección que se carga en IP) o indirecto (la dirección de salto está contenida en el registro o dirección que sigue a JMP). Dependiendo del segmento, es un salto NEAR o FAR. |
| JA; JNBE | DESPLAZAMIENTO | No altera flags | SALTO SI SUPERIOR. Salta si se cumple CF='0' y ZF='0'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. NOTA: Usaremos MAYOR Y MENOR con números con signo, y SUPERIOR e INFERIOR para números sin signo. |
| JAE; JNB; JNC | DESPLAZAMIENTO | No altera flags | SALTO SI SUPERIOR O IGUAL. Salta si se cumple CF='0'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. NOTA: Usaremos MAYOR Y MENOR con números con signo, y SUPERIOR e INFERIOR para números sin signo. |
| JB; JC; JNAE | DESPLAZAMIENTO | No altera flags | SALTO SI INFERIOR. Salta si se cumple CF='1'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. NOTA: Usaremos MAYOR Y MENOR con números con signo, y SUPERIOR e INFERIOR para números sin signo. |
| JNA; JBE | DESPLAZAMIENTO | No altera flags | SALTO SI NO SUPERIOR (inferior o igual). Salta si se cumple CF='0'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. NOTA: Usaremos MAYOR Y MENOR con números con signo, y SUPERIOR e INFERIOR para números sin signo. |
| JCXZ | DESPLAZAMIENTO | No altera flags | SALTO SI CX ES CERO. Salta si se cumple CX='0'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. NOTA: Usaremos MAYOR Y MENOR con números con signo, y SUPERIOR e INFERIOR para números sin signo. |
| JE; JZ | DESPLAZAMIENTO | No altera flags | SALTO SI IGUAL. Salta si se cumple ZF='1'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. NOTA: Usaremos MAYOR Y MENOR con números con signo, y SUPERIOR e INFERIOR para números sin signo. |
| JG; JNLE | DESPLAZAMIENTO | No altera flags | SALTO SI MAYOR. Salta si se cumple ZF='0' y SF=OF. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. (El número 00000011 es mayor que 11111000). NOTA: Usaremos MAYOR Y MENOR con números con signo, y SUPERIOR e INFERIOR para números sin signo. |
| JGE; JNL | DESPLAZAMIENTO | No altera flags | SALTO SI MAYOR O IGUAL. Salta si se cumple SF=OF. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. (El número 00000011 es mayor que 11111000). NOTA: Usaremos MAYOR Y MENOR con números con signo, y SUPERIOR e INFERIOR para números sin signo. |
| JL; JNGE | DESPLAZAMIENTO | No altera flags | SALTO SI MENOR. Salta si se cumple SF distinto de OF. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. (El número 00000011 es mayor que 11111000). NOTA: Usaremos MAYOR Y MENOR con números con signo, y SUPERIOR e INFERIOR para números sin signo. |
| JLE; JNG | DESPLAZAMIENTO | No altera flags | SALTO SI MENOR O IGUAL. Salta si se cumple ZF='1' o SF distinto de OF. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. (El número 00000011 es mayor que 11111000). NOTA: Usaremos MAYOR Y MENOR con números con signo, y SUPERIOR e INFERIOR para números sin signo. |
| JNE; JNZ | DESPLAZAMIENTO | No altera flags | SALTO SI NO IGUAL. Salta si se cumple ZF='0'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. NOTA: Usaremos MAYOR Y MENOR con números con signo, y SUPERIOR e INFERIOR para números sin signo. |
| JNO | DESPLAZAMIENTO | No altera flags | SALTO SI NO HAY DESBORDAMIENTO. Salta si se cumple OF='0'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. |
| JNP; JPO | DESPLAZAMIENTO | No altera flags | SALTO SI NO HAY PARIDAD, O SI ES PARIDAD IMPAR. Salta si se cumple PF='0'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. |
| JNS | DESPLAZAMIENTO | No altera flags | SALTO SI POSITIVO. Salta si se cumple SF='0'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. |
| JO | DESPLAZAMIENTO | No altera flags | SALTO SI HAY DESBORDAMIENTO. Salta si se cumple OF='1'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. |
| JP; JPE | DESPLAZAMIENTO | No altera flags | SALTO SI HAY PARIDAD. Salta si se cumple PF='1'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. |
| JS | DESPLAZAMIENTO | No altera flags | SALTO SI SIGNO. Salta si se cumple SF='1'. El salto está comprendido entre 128 posiciones hacia atrás y 127 hacia delante. |
| LOOP | DIRECCIÓN | No altera flags | BUCLE. Provoca la repetición de una serie de instrucciones un número determinado de veces, especificado por el registro contador CX. En cada iteración CX se decrementa en una unidad. Si CX es distinto de '0', salta a la dirección. Esa dirección debe estar entre 128 posiciones hacia atrás y 127 hacia delante. |
| LOOPE; LOOPZ | DIRECCIÓN | No altera flags | BUCLE SI IGUAL O CERO. Provoca la repetición de una serie de instrucciones un número determinado de veces, especificado por el registro contador CX. En cada iteración CX se decrementa en una unidad. Si CX es distinto de '0' y ZF='1', salta a la dirección. Esa dirección debe estar entre 128 posiciones hacia atrás y 127 hacia delante. |
| LOOPNE; LOOPNZ | DIRECCIÓN | No altera flags | BUCLE SI NO IGUAL O NO CERO. Provoca la repetición de una serie de instrucciones un número determinado de veces, especificado por el registro contador CX. En cada iteración CX se decrementa en una unidad. Si CX es distinto de '0' y ZF='0', salta a la dirección. Esa dirección debe estar entre 128 posiciones hacia atrás y 127 hacia delante. |
| INT | TIPO DE INTERRUPCIÓN | IF=0,TF=0 | INTERRUPCIÓN. Realiza una interrupción por software. Abandona el curso normal del programa para ejecutar la rutina de atención de la interrupción, salvando antes el contenido de PSW e IP en la pila. El vector de interrupción está ubicado en la posición de memoria (0000:4*int) a la (0000:4*int+3). |
| INTO | (ninguno) | IF=0,TF=0 | INTERRUPCIÓN SI OVERFLOW. Genera la interrupción interna tipo 4 en el caso de que la bandera de overflow OF='1'. |
| IRET | (ninguno) | TODAS LAS BANDERAS SON RESTAURADAS | RETORNO DE UNA INTERRUPCIÓN. Devuelve el control del programa a la instrucción siguiente a donde se había interrumpido, sacando su dirección de la pila. Se restauran los valores de CS, IP y PSW. Todas las banderas son restauradas con los valores que tenían antes de la interrupción. |

## INSTRUCCIONES DE MANIPULACIÓN DE FLAGS

| Mnemónico | Operandos (Destino, Fuente) | Flags | Descripción |
|---|---|---|---|
| CLC | (ninguno) | CF=0 | PONE A CERO EL FLAG DE CARRY. |
| CLD | (ninguno) | DF=0 | PONE A CERO EL FLAG DE DIRECCIÓN. |
| CLI | (ninguno) | IF | BORRA EL FLAG DE INTERRUPCIÓN. Desactiva el permiso de interrupción para las interrupciones enmascarables. Se seguirán tratando las interrupciones no enmascarables NMI y las software. |
| CMC | (ninguno) | CF | COMPLEMENTAR EL FLAG DE ACARREO. Si CF='0' lo pone a '1', si CF='1' lo pone a '0'. |
| STC | (ninguno) | CF=1 | PONER FLAG DE CARRY. Pone a '1' el flag de carry. |
| STD | (ninguno) | DF=1 | PONER FLAG DE DIRECCIÓN. Pone a '1' el flag de dirección. |
| STI | (ninguno) | IF | PONER FLAG DE INTERRUPCIÓN. Pone a uno el flag de interrupción, permitiendo las interrupciones enmascarables. No tiene efecto hasta que no se haya ejecutado la instrucción que sigue a la STI. |

## INSTRUCCIONES DE CONTROL DEL MICROPROCESADOR

| Mnemónico | Operandos (Destino, Fuente) | Flags | Descripción |
|---|---|---|---|
| ESC | COD. OP.; REG/MEM | (ninguno) | ESCAPE. Se usa para pasar instrucciones a un coprocesador. El primer operando es un código de operación. El segundo operando indica dónde se encuentra el dato que se le va a pasar. |
| HLT | (ninguno) | (ninguno) | PARADA DEL PROCESADOR. Cesa la actividad de búsqueda. Sólo saldrá de este estado mediante una petición de interrupción externa enmascarable, no enmascarable, o una señal RESET. Útil para diagnosticar equipos. |
| LOCK | (instrucción crítica) | (ninguno) | CIERRE DEL BUS. Usado en sistemas multiprocesador para compartir recursos. LOCK se usará delante de una instrucción crítica que deba tener prioridad absoluta en el control del bus. |
| NOP | (ninguno) | (ninguno) | NO OPERACIÓN. Sólo consume tres ciclos de reloj. Usado para ajustar retardos. |
| WAIT | (ninguno) | (ninguno) | ESPERA. El microprocesador entra en estado de letargo sin hacer nada. Se puede salir mediante la activación a nivel bajo de la entrada TEST, o con una petición de interrupción. Se usa para sincronizar. |

---

## INFORMACIÓN DE REFERENCIA

### Esquema de desplazamientos

```
- SAL/SHL:   CF │ 8 ó 16 bits │ 0 │ ROR
             8 ó 16 bits │ CF
- SAR - RCL
- CF - 8 ó 16 bits
- 8 ó 16 bits - CF
Signo
- SHR:   0 │ 8 ó 16 bits │ CF │ RCR
         8 ó 16 bits - CF
- ROL:   CF │ 8 ó 16 bits
```

### Palabra de estado PSW

```
15 14 13 │ 12 11 10 │ 9 │ 8 7 │ 6 5 │ 4 3 │ 2 1 │ 0
OF │ DF IF │ TF SF │ ZF AF │ PF │ CF
```

### Codificación de instrucciones

```
COD OP │ D │ W │ MOD │ REG │ R/M │ DESPLAZA. │ VALOR
D: 0 ......... REG = FUENTE
   1 .......... REG = DESTINO
W: 0 .......... TAMAÑO BYTE
   1 .......... TAMAÑO WORD
```

### Dirección de registros

```
REGISTRO │ W=1 │ W=0 │ Dirección de Registro │ Registro de Segmento
000      │ AX  │ AL  │ 00                    │ ES
001      │ CX  │ CL  │ 01                    │ CS
010      │ DX  │ DL  │ 10                    │ SS
011      │ BX  │ BL  │ 11                    │ DS
100      │ SP  │ AH  │
101      │ BP  │ CH  │
110      │ SI  │ DH  │
111      │ DI  │ BH  │
```

### MOD: Direccionamiento

```
MOD │ R/M (W=0) │ R/M (W=1) │
00  │ (BX)+(SI) │ (BX)+(SI) │ (BX)+(SI)+D8  │ (BX)+(SI)+D16 │ AL │ AX │ DS: DS: DS │
    │ (BX)+(DI) │ (BX)+(DI) │ (BX)+(DI)+D8  │ (BX)+(DI)+D16 │ CL │ CX │ DS: DS: DS │
    │ (BP)+(SI) │ (BP)+(SI) │ (BP)+(SI)+D8  │ (BP)+(SI)+D16 │ DL │ DX │ SS: SS: SS │
    │ (BP)+(DI) │ (BP)+(DI) │ (BP)+(DI)+D8  │ (BP)+(DI)+D16 │ BL │ BX │ SS: SS: SS │
    │ (SI)      │ (SI)      │ (SI)+D8       │ (SI)+D16      │ AH │ SP │ DS: DS: DS │
    │ (DI)      │ (DI)      │ (DI)+D8       │ (DI)+D16      │ CH │ BP │ DS: DS: DS │
    │ D16       │ (BP)+D8   │ (BP)+D16      │               │ DH │ SI │ DS: DS: DS │
    │ (BX)      │ (BX)+D8   │ (BX)+D16      │               │ BH │ DI │ DS: DS: DS │
```

### Uso de los registros de segmento

```
TIPO DE OPERACIÓN           │ SEGMENTO POR DEFECTO │ SEGMENTO OPCIONAL │ OFFSET
Búsqueda de instrucción     │ CS                   │ NINGUNO           │ IP
Operación con la pila       │ SS                   │ NINGUNO           │ SP
Operación con cadena fuente │ DS                   │ CS, ES, SS        │ SI
Operación con cadena destino│ ES                   │ NINGUNO           │ DI
Lectura/Escritura de datos  │ DS                   │ CS, ES, SS        │ DIRECCIÓN EFECTIVA
BP usado como registro base │ SS                   │ CS, DS, ES        │ DIRECCIÓN EFECTIVA
```

## Funciones de interrupción DOS/BIOS

*(Esta sección resume las funciones de interrupción software más empleadas, tal y como aparecían en el documento original. Es un resumen más breve que las notas dedicadas `INT 21H.md`, `INT 10H.md` e `INT 33H.md` de la carpeta padre, que cubren estas mismas interrupciones con mucho más detalle.)*

### Funciones de la interrupción 21h (DOS)

| AH | Función | Descripción |
|---|---|---|
| 01h | Entrada desde el teclado | Espera a que se teclee un carácter por teclado. Escribe el carácter en pantalla y devuelve el código ASCII en el registro AL. Modifica AL con el código ASCII del carácter leído. |
| 02h | Salida a la pantalla | Muestra un carácter en pantalla. Se debe guardar en DL el código ASCII del carácter que se desea sacar por pantalla. Devuelve en AL el código ASCII del carácter impreso. |
| 06h | Entrada/salida directa por consola | Envía carácter a la salida estándar sin comprobar ctrl-C. Se debe guardar en DL el código ASCII del carácter que se desea sacar por pantalla (distinto de 0FFh). Lee carácter de la entrada estándar sin esperar pulsación cuando DL=0FFh. Salida: si había algún carácter: ZF='0' y AL=código ASCII del carácter leído. Si no había carácter: ZF='1'. |
| 08h | Entrada desde el teclado sin eco | Lee un carácter por teclado pero no lo muestra por pantalla. Modifica AL con el código ASCII del carácter leído. |
| 09h | Muestra cadena | Muestra por pantalla la cadena a la que apunta la pareja de registros DS:DX. El final de la cadena se debe marcar con el carácter `$`. |
| 0Ah | Lee cadena | Lee una cadena desde el teclado. El buffer de almacenamiento debe estar apuntado por DS:DX. El primer byte del buffer debe contener el número máximo de caracteres a leer. En el segundo byte se devuelve el número real de caracteres pulsados (a excepción del retorno de carro) y a partir del segundo byte se encuentra la cadena de caracteres leída, finalizada con un retorno de carro (0Dh). |
| 25h | Cargar el vector de interrupción | Entradas: AL = tipo de interrupción; DS:DX apunta a la rutina de atención a la interrupción. |
| 2Ch | Obtener la hora del sistema | Devuelve: CH = horas (0-23), CL = minutos (0-59), DH = segundos (0-59), DL = centésimas de segundo (0-99). |
| 35h | Obtener vector de interrupción | Obtiene la dirección de la rutina de atención de la interrupción especificada. Entradas: AL = tipo de interrupción. Devuelve: ES:BX = segmento y desplazamiento de la rutina de atención a la interrupción. |
| 4Ch | Sale al DOS | Devuelve el control al DOS, igual que la interrupción 20h. Devuelve en AL el código de retorno al DOS que se desee. Modifica AL con el valor que se desea devolver al DOS para ser usado con el IF ERRORLEVEL. |

### Funciones de la interrupción 10h (BIOS de vídeo)

| AH | Función | Descripción |
|---|---|---|
| 00h | Establece el modo de la pantalla | Modos de pantalla seleccionables por AL: |

| AL | Modo |
|---|---|
| 0 | 40x25 blanco y negro alfanumérico |
| 1 | 40x25 color (16) alfanumérico |
| 2 | 80x25 blanco y negro alfanumérico |
| 3 | 80x25 blanco y negro alfanumérico |
| 4 | 320x200 color (4) gráfica |
| 5 | 320x200 blanco y negro gráfica |
| 6 | 640x200 blanco y negro gráfica |
| 0Eh | 640x200 color (16) gráfica |
| 12h | 640x480 color (16) gráfica |
| 13h | 320x200 color (256) gráfica |

| AH | Función | Descripción |
|---|---|---|
| 01h | Establecer las líneas del cursor | CH (bits 0-4) = línea inicial, bits 5-7 deben ser 0. CL (bits 0-4) = línea final, bits 5-7 deben ser 0. |
| 02h | Posición del cursor | DH = Fila (0-24), DL = Columna (0-79). |
| 03h | Leer posición del cursor | BH = número de página (0 en modo gráfico). Devuelve: DH (fila), DL (columna), CH (bits 0-4 línea inicial, bits 5-7 = 0), CL (bits 0-4 línea final, bits 5-7 = 0). |
| 06h | Desplazamiento (scroll) hacia arriba | AL = número de líneas (si AL=0 se borra la ventana). CH = fila esquina superior izquierda, CL = columna esquina superior izquierda, DH = fila esquina inferior derecha, DL = columna esquina inferior derecha, BH = relleno. |
| 07h | Desplazamiento (scroll) hacia abajo | Mismos parámetros que la función 06h, mostrando el texto hacia abajo. |
| 08h | Leer carácter y atributo de la posición actual | BH = número de página. Devuelve: AL = carácter leído, AH = atributo del carácter leído. |
| 09h | Escribir el carácter y el atributo en la posición actual del cursor | BH = número de página, CX = número de caracteres a escribir, BL = atributo del carácter o color, AL = carácter a escribir. |
| 0Eh | Escribir el carácter en la pantalla y avanzar el cursor | AL = carácter a escribir, BL = color del carácter o su atributo, BH = número de la página. |
| 0Fh | Leer el estado actual de la pantalla | Devuelve: AL = modo, AH = número de columnas de la pantalla, BH = número de página activa. |

### Funciones de la interrupción 16h (BIOS de teclado)

| AH | Función | Descripción |
|---|---|---|
| 00h | Leer pulsación del teclado | Espera tecla; elimina la tecla del buffer al leerla. Salida: AH = código BIOS de rastreo, AL = código ASCII de la tecla. Sólo reconoce 84 teclas; elimina del buffer las del teclado extendido. |
| 01h | Comprobar pulsación del teclado | No espera tecla, no reconoce teclado extendido, no elimina la tecla del buffer. Salida: si no hay tecla en el buffer → flag de cero activado; si hay tecla → flag de cero desactivado, AH = código BIOS de rastreo, AL = código ASCII de la tecla. |
| 02h | Obtener estado del teclado | Salida: AL = estado del teclado. |
| 10h | Leer pulsación del teclado extendido | Espera tecla; elimina la tecla del buffer. Salida: AH = código BIOS de rastreo, AL = código ASCII de la tecla. |
| 11h | Comprobar pulsación del teclado extendido | No elimina la tecla del buffer. Salida: si no hay tecla en el buffer → flag de cero activado; si hay tecla → flag de cero desactivado, AH = código BIOS de rastreo, AL = código ASCII de la tecla. |
| 12h | Obtener estado del teclado extendido | Salida: AH = estado del teclado extendido, AL = estado del teclado. |

## Interfaces de E/S: 8255A (PPI) y 8251A (USART)

*(Esta sección del documento original describe los registros y formatos de control de dos circuitos integrados de E/S auxiliares del PC: el 8255A (Programmable Peripheral Interface, interfaz paralela) y el 8251A (interfaz serie USART). El contenido original combina varios diagramas de bits (figuras) con las etiquetas de sus campos, y la extracción OCR entremezcló el orden de las etiquetas de bit con el texto explicativo de forma que no se puede reconstruir con confianza total la posición exacta de cada campo dentro de cada figura. Se transcribe a continuación la información que sí se pudo agrupar con confianza razonable por tabla/figura; donde el orden de los bits es incierto, se preserva la agrupación de etiquetas tal y como aparecía, sin inventar una disposición de bits que no se pueda verificar.)*

### 8255A — Tablas de operación de la PPI

**Tabla 1. Operación de lectura en la PPI**

| A1 | A0 | RD# | WR# | CS# | Operación de entrada (lectura) |
|---|---|---|---|---|---|
| 0 | 0 | 0 | 1 | 0 | Puerto A → Bus de Datos |
| 0 | 1 | 0 | 1 | 0 | Puerto B → Bus de Datos |
| 1 | 0 | 0 | 1 | 0 | Puerto C → Bus de Datos |
| 1 | 1 | 0 | 1 | 0 | Palabra de control → Bus de datos |

**Tabla 2. Operaciones de escritura en la PPI**

| A1 | A0 | RD# | WR# | CS# | Operación de salida (escritura) |
|---|---|---|---|---|---|
| 0 | 0 | 1 | 0 | 0 | Bus de Datos → Puerto A |
| 0 | 1 | 1 | 0 | 0 | Bus de Datos → Puerto B |
| 1 | 0 | 1 | 0 | 0 | Bus de Datos → Puerto C |
| 1 | 1 | 1 | 0 | 0 | Bus de Datos → Palabra de control |

**Tabla 3. Selección de la PPI**

| A1 | A0 | RD# | WR# | CS# | Estado |
|---|---|---|---|---|---|
| x | x | x | x | 1 | Bus de datos en Three-State (deshabilitado) |
| x | x | 1 | 1 | 0 | Bus de datos en Three-State (deshabilitado) |

**Figura 1. Registro de control / Figura 2. Palabra de control (Set/Reset de los bits del puerto C):**

*(disposición de bits no reconstruible con confianza; etiquetas identificadas en el original: PUERTO A, PUERTO B, PUERTO C (parte alta) y PUERTO C (parte baja) con selección de dirección 1=ENTRADA/0=SALIDA por cada puerto; SELECCIÓN DE MODO con 0=MODO 0, 1=MODO 1 (grupo A) y 00=MODO 0, 01=MODO 1, 1X=MODO 2 (grupo B); FORMATO SET/RESET con 1=ACTIVO/0=PUESTA A CERO y PUESTA A UNO; SELECCIÓN DEL BIT numerada D1-D3 y otros bits D0-D7)*

**Formato del puerto C en modo 1 — entrada:**

`I/O I/O IBFa INTEa INTRa INTEb IBFb INTRb` (bits D7 a D0)

**Formato del puerto C en modo 1 — salida:**

`OBFa INTEa I/O I/O INTRa INTEb OBFb INTRb` (bits D7 a D0)

**Formato de la palabra de estado / puerto C en modo 2:**

`OBFa INTE1 IBFa INTE2 INTRa X X X` (bits D7 a D0)

### 8251A — Registro de modo y registro de control (USART)

**Figura 4. Formato del registro de modo** (aplica tras un reset, para el primer byte escrito en el registro de modo):

- Bits D1-D0 — Factor de relación de baudios: `00` = Modo síncrono, `01` = Asíncrono x1, `10` = Asíncrono x16, `11` = Asíncrono x64
- Bits D3-D2 — Longitud de carácter: `00` = 5 bits, `01` = 6 bits, `10` = 7 bits, `11` = 8 bits
- Bits D5-D4 — Control de paridad: `X0` = Sin paridad, `01` = Paridad impar, `11` = Paridad par
- Bits D7-D6 — Longitud de bit de stop (modo asíncrono): `00` = Inválido, `01` = 1 bit stop, `10` = 1,5 bits stop, `11` = 2 bits stop

*(en modo síncrono, los bits D7-D6 tienen un significado distinto relacionado con el número de caracteres de sincronismo (1 o 2) y si SYNDET es entrada o salida (sincronización interna/externa); el original no permite reconstruir con confianza la correspondencia exacta bit a bit para este caso)*

**Figura 5. Palabra de control** (registro de control, C/D=1, escritura):

| Bit | Nombre | Significado |
|---|---|---|
| D0 | TxEN | Habilitación de transmisión. `1` = Habilitada, `0` = Deshabilitada |
| D1 | DTR | Terminal de Datos Dispuesto. `1` = Fuerza DTR a nivel bajo |
| D2 | RxE | Habilitación de recepción. `1` = Habilitada, `0` = Deshabilitada |
| D3 | SBRK | Envío del carácter BREAK. `1` = Fuerza TxD a nivel bajo, `0` = Operación normal |
| D4 | ER | Borrado de errores. `1` = Puesta a cero de los flags de error PE, OE y FE |
| D5 | RTS | Solicitud de envío. `1` = Fuerza RTS a nivel bajo |
| D6 | IR | Reset interno. `1` = Coloca al 8251A en formato de instrucción de modo |
| D7 | EH | Entrada en modo captura. `1` = Permite la espera de caracteres de sincronismo |

**Figura 6. Registro de estado** (lectura, mismo nombre que el registro de control, C/D=1):

| Bit | Nombre | Significado |
|---|---|---|
| D0 | TxRDY | Transmisor listo |
| D1 | RxRDY | Receptor listo |
| D2 | TxEMPTY | Transmisor vacío |
| D3 | PE | Error de paridad (Parity Error) |
| D4 | OE | Error de sobreescritura (Overrun Error) |
| D5 | FE | Error de bloque, asíncrono (Framing Error) |
| D6 | SYNDET/BRKDET | Detección de sincronismo o de BREAK |
| D7 | DSR | Estado del terminal. `0` = DSR a nivel alto, `1` = DSR a nivel bajo |

**Otros registros internos de la USART:**

- Registro de transmisión: dirección C/D=0, escritura
- Registro de recepción: dirección C/D=0, lectura
- Registro de modo: dirección C/D=1, primera escritura tras reset
- Registro de control: dirección C/D=1, escritura
- Registro de estado: dirección C/D=1, lectura
