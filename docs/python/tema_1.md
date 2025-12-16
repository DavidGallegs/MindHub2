# TEMA 1

## TIPOS DE DATOS

### BOLEANOS

Tenemos los valores **verdaderos** como `True` o `1`  
Y los que son valores **negativos** como `False` o `0`  

### NUMÉRICOS

| TIPO             | VALOR        |
|------------------|--------------|
| Entero (+)       | 12, 50, 200  |
| Entero (-)       | -12, -50, -20|
| Binario (0b)     | 0b10111      |
| Octal (0o)       | 0o377        |
| Hexadecimal (0x) | 0xaf1a       |
| Reales           | 3.1478       |
| Complejos        | 2+2j         |

### STRINGS

Las cadenas en python usan `''` o `""`  
Tambien podemos colocar dentro saltos de linea `\n`

## GENERALIDADES

### SIN VALOR EXISTENTE

La forma de colocar que no sabemos un valor es poniendo `Variable = None`

### VERIFICAR TIPO DE DATO

Usamos la función `type()`, esta nos dira que tipo es la variable.

### ASIGNACIÓN MÚLTIPLE

Podemos asignar valores múltples: `x,y,z = "Texto",2,-400.

## OPERADORES

### GENERALES

| TIPO        | OPERADORES                                               |
|-------------|----------------------------------------------------------|
| ARITMETICOS | +, -, *, /, //, %, **                                    |
| COMPARACIÓN | ==, !=, >, <, <=, >=                                     |
| LÓGICOS     | and, or, not                                             |
| PERTENENCIA | in, not in → ('a' in/not in 'casa')                      |
| IDENTIDAD   | is, is not                                               |
| AGRUPACIÓN Y ACCESO | (), [], {}, ., [:] → (Sublistas o subStrings), : → (Bloques) |

### CADENAS

En las cadenas, las comillas `''` o `""`, sí colocamos dentro de una variable o un print `"""texto"""` o `'''Texto'''` permite la multilínea.

Tenemos carácteres especiales como `\n`, `\'` o `\"`  
Y para usar `\` ponemos `r` delante de la cadena.

Podemos acceder los carácteres de una cadena usando índices `[n]` ya sean positivos o negativos.  

Podemos obtener subcadenas de las cadenas, paa ello usamos `cadena[start:end]`  

- Ejemplos:  
  
~~~python
texto ="Python"

print(texto[0:4]) # Pyth (índices de 0 a 3)
print(texto[::2]) # Pto (caràcteress del 0 al 5 de 2 en 2)
print(texto[1:4:2]) # yh (caràcteress 1 al 3 de 2 en 2)
print(texto[:3]) # Hol (desde el índice 0 al índice 2)
print(texto[::-1]) # invierte la cadena
~~~

Tambien podemos ver la longitud de una cadena con `len()`  

### EXTRA

Para comentarios líneales usamos `#` y multilínea usamos `""" Texto """` o `''' Texto '''`  
Luego tenemos el `\` que continua la línea.  
Y el `@` que sirve como decorador.

## FUNCIONES MATEMÁTICAS PREDEFINIDAS

- `abs(x)` → Devuelve el valor absoluto.
- `hex(x)` → Devuelve el valor hexadecimal.
- `oct(x)` → Devuelve un valor octal.
- `bin(x)` → Devuelve un valor binario.
- `pow(x,y)` → Devuelve una potencia elevada a un exponente
- `round(x,None)` → Deuvuelve un redondeo a `None` o a `N` decimales
- `max(x)` → Devuelve el valor máximo de una lista.
- `min(x)` → Devuelve el valor mínimo de una lista.
  
## CONVERSIÓN DE TIPOS DE DATOS

Tenemos los primitivos como `bool(x)`, `int(x)`, `float(x)`, `str(x)`  
Para convertir a valores complejos sin parte imaginaria usamos `complex(x)`  
Para convertir un valor complejo, cuya parte real es `x` y la pate imaginaria es `y` utilizamos `complex(x,y)`

## ENTRADA Y SALIDA

Para mostrar datos usamos `print()` y usa un salto de línea por defecto.  
Por otro lado esta `print(f"")` que permite usar variables dentro de comillas.  
Si usamos la siguiente estructura: `print("",end="")` cancela el salo de línea.  

Para recibir datos utilizamos `input()` y puede estar dentro de conversores de tipos de datos.

## FUNCIONES DE STRINGS

`cadena.upper()` → Convierte a mayúsculas.  
`cadena.lower()` → Convierte a minúsculas.  
`cadena.capitalize()` → Devuelve la primera letra en mayúscula.  
`cadena.title()` →  Devuelve la primera letra en mayúscula de cada palabra.  
`cadena.strip()` →  Elimina espacios en blanco al inicio y final de la cadena.  
`cadena.replace("Laura","Olivia")` → Ssutituye partes de la cadena.  
`cadena.split(" ")` → Divide la cadena en una lista, usando un 'separador'.  
`texto = " ".join(lista)` → Devuelve una lista a una cadena usando un 'separador'.  
`cadena.find("D")` → Devuelve la posición en la que encuentra esa subcadena , -1 si no está.  
`cadena.index("D")` → Igual que find, pero lanza una exepción si no está.  
`cadena.startswith("Buenos")` → Devuelve true si empieza por ese substring.  
`cadena.endswith("Laura")` → Devuelve true si termina por ese substring.  
`cadena.isalpha()` → Devuelve true si todos los carácteres son letras.  
`cadena.isdigit()` → Devuelve true si todos los carácteres son números.  
`cadena.isalnum()` → Devuelve true si todos los carácteres son letras o números.  
`cadena.isspace()` → Devuelve true si todos los carácteres son espacios en blanco.  
`cadena.count("a")` → Devuelve el números de apariciones de esa subcadena en la cadena.  
`cadena.zfill(3)` → Llena de zeros el inicio de la cadena hasta alcanzar la longitud deseada.  
