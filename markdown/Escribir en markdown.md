# MARKDOWN

>Se utiliza a menudo en documentación de GitHub, como README files.

## BÁSICO

### TÍTULOS

Como en HTML hay 6. Cuantos más # más pequeño.

```md
# Tu título 1
### Tu título 3
###### Tu título 6
```

### ÉNFASIS

Podemos escribir en **negrita** o *cursiva*.

```md
**Negrita**
__Negrita__
*Cursiva*
_Cursiva_
```

### ENLACES

Se pueden incluir enlaces, como este a [Google](https://www.google.es)

```md
[Google](https://www.google.es)
```

### IMÁGENES

Se pueden incluir imágenes de forma similar añadiendo una exclamación
![El castillo Ambulante](../images/howl1.jpg)

```md
![El castillo Ambulante](../images/howl1.jpg)
```

### CÓDIGO

Se pueden escribir fragmentos de código rodeándolos de ```

```md
    ```
    Y aquí el código
    ```
```

### TABLAS

Separando una lista de elementos con guiones - y pipes | se pueden hacer tablas

| Columna 1 | Columna 2 | Columna 3 |
|-----------|-----------|-----------|
| fila1     | fila1     | fila1     |
| fila2     | fila2     | fila2     |

```md
| Columna 1 | Columna 2 | Columna 3 |
|-----------|-----------|-----------|
| fila1     | fila1     | fila1     |
| fila2     | fila2     | fila2     |
```

### CITAS

Se pueden citar frases con >

>Hacer apuntes en markdown fue una gran idea - Inés

```md
>Hacer apuntes en markdown fue una gran idea - Inés
```

### SEPARADORES

---
Una línea permite separar fácilmente.

>CUIDADO:
>Con texto inmediatamente encima lo trata como un título 2.

```md
---
***
___
```

### CARACTERES RESERVADOS

Hay caracteres especiales en markdown cuyo efecto se puede anular utilizando \ antes.
"De esa manera, puedo escribir \* sin problema."

```md
"De esa manera, puedo escribir \* sin problema."
```
