<link rel="stylesheet" href="../static/style/personalizaciones.css">

# Markdown <!-- omit from toc -->

![Cabecera](../static/images/ghibli/howl1.jpg)

Se utiliza a menudo en **documentación** de [GitHub](https://www.github.com), como `README` files.

<div id="table-of-contents">

## Tabla de Contenido <!-- omit from toc -->

- [Básico](#básico)
  - [Títulos](#títulos)
  - [Énfasis](#énfasis)
  - [Enlaces](#enlaces)
  - [Imágenes](#imágenes)
  - [Código](#código)
  - [Tablas](#tablas)
  - [Citas](#citas)
  - [Separadores](#separadores)
  - [Caracteres reservados](#caracteres-reservados)

</div>

## Básico

### Títulos

Como en HTML hay 6. Cuantos más # más pequeño.

```md
# Tu título 1
### Tu título 3
###### Tu título 6
```

### Énfasis

Podemos escribir en **negrita** o *cursiva*.

```md
**Negrita**
__Negrita__
*Cursiva*
_Cursiva_
```

### Enlaces

Se pueden incluir enlaces, como este a [Google](https://www.google.es)

```md
[Google](https://www.google.es)
```

### Imágenes

Se pueden incluir imágenes de forma similar añadiendo una exclamación
![El castillo Ambulante](../images/ghibli/howl1.jpg)

```md
![El castillo Ambulante](../images/ghibli/howl1.jpg)
```

### Código

Se pueden escribir fragmentos de código rodeándolos de ```

```md
    ```
    Y aquí el código
    ```
```

### Tablas

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

### Citas

Se pueden citar frases con >

>Hacer apuntes en markdown fue una gran idea - Inés

```md
>Hacer apuntes en markdown fue una gran idea - Inés
```

### Separadores

---
Una línea permite separar fácilmente.

>**CUIDADO:**
>Con texto inmediatamente encima lo trata como un título 2.

```md
---
***
___
```

### Caracteres reservados

Hay caracteres especiales en markdown cuyo efecto se puede anular utilizando `\` antes.  

**"De esa manera, puedo escribir \* sin problema."**

```md
"De esa manera, puedo escribir \* sin problema."
```
