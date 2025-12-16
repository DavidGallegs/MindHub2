# MARKDOWN

## PÁRRAFOS Y SALTOS  DE LÍNEA

Los párrafos son como en cualquier otro lenguaje.  
Los saltos de línea se hacen con `2 espacios en blanco` en la línea anterior.

## ENCABEZADOS

Para hacer los títulos  usamos desde 1 a 6: `#`  
Para que sea estético los podemos poner a ambos lados.

- Si ponemos Un texto y un `-` o `=` debajo, se crea un encabezado nivel 1 o nivel 2.
- Solo funciona para esos 2 niveles.

## CITAS

Las citas se crean unsando un `>`  
Las citas anidadas son colocando debajo un `>>`, `>>>`, etc…

## LISTAS

Las listas ordenadas y desordenadas se pueden anidadar y mezclar.  
  **DESORDENADAS:** Usamos los simbolos `*`, `-` o `+`  
  **ORDENADAS:** Se crean poniendo `número`.

## CÓDIGO BLOQUE

Abres y cierras con  `~~~`, todo el texto interior se comportará como código.

## REGLAS HORIZONTALES

Crear espacios en blanco lineas, usamos `***`, `—-` , `___`.  
Con estetica puede añadir espacios en blanco entre los simbolos

## ELEMENTOS EN LÍNEA

*Cursiva* → `*texto*` o `_texto_`
**Negrita** → `**Texto**` o `__Texto__`

## LINKS Y ENLACES

**FORMA 1:**  
Usamos `[Texto Clikeable](URL)`

**FORMA 2:**  
En un texto ponemos una [PALABRA] entre `[]`  
Luego asociamos esa palabra con el link con la siguiente estructura: `[PALABRA]: link/url`  
Esta forma permite usar [PALABRA] varias veces.

## CÓDIGO PURO

Para escribir líneas de código dentro un texto usamos ``` `` ```

## TEXTO PREFORMATADO

Usamos `4 espacios en blanco` para crear una línea de código.

## IMAGENES

Podemos poner imagenes de 2 formas:  

**FORMA 1:**  
Usando la siguiente estructura: `![Texto alternativo](/ruta/a/la/imagen.jpg)`  

![Imagen](./images/fondo7.jpg)

**FORMA 2**  
Usando la estructura `![HOLA][img]`.  
Y luego poniendo la asociación: `[img]: ./images/fondo7.jpg`  
Se pueden mostrar imagenes:  

![hola][img]

[img]: ./images/fondo7.jpg

## LINKS AUTOMÁTICOS

`<link/url>` pone el link con la url y todo.  
Ejemplo: <https://youtube.com>

## CANCELAR MK

Poniendo una `\` delante del Markdown, lo cancela.

## CREAR TABLAS

Colocando `|` podemos crear tablas, donde poniendo `|-----|` creamos las cabezeras.  
Y las filas se crean extensiendo la tabla en las siguientes líneas con `|`  
