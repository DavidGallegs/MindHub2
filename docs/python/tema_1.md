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

Las cadenas en python usan `''` o `""`, tambien podemos colocar dentro saltos de linea `\n`

### GENERALIDADES

#### SIN VALOR EXISTENTE

La forma de colocar que no sabemos un valor es poniendo `Variable = None`

#### VERIFICAR TIPO DE DATO

Usamos la función `type()`, esta nos dira que tipo es

#### ASIGNACIÓN MÚLTIPLE

Podemos asignar valores múltples: `x,y,z = "Texto",2,-400

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

En las cadenas, las comillas `''` o `""`, si colocamos dentro de una variable o un print `"""texto"""` o `'''Texto'''` permite la multilínea.

### EXTRA

Para comentarios líneales usamos `#`, y multilínea usamos `""" Texto """` o `''' Texto '''`  
Luego tenemos el `\` que continua la línea  
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
Para convertir un valor complejo, cuya parte real es `x` y la pate imaginaria es `y`, utilizamos `complex(x,y)`

## ENTRADA Y SALIDA

Para mostrar datos usamos `print()` y usa un salto de línea por defecto.  
Por otro lado esta `print(f"")` que permite usar variables dentro de comillas.  
Si usamos la siguiente estructura: `print("",end="")` cancela el salo de línea.  

Para recibir datos utilizamos `input()` y puede estar dentro de conversores de tipos de datos.
