<link rel="stylesheet" href="../static/style/personalizaciones.css">

# Node.js <!-- omit from toc -->

![Cabecera](../static/images/ghibli/omohide1.jpg)

**Node es un entorno de ejecución de JavaScript.**  
Es monohilo, asíncrono y está orientado a eventos.

<blockquote class="comentario">
    Usa V8, el mismo motor que Chrome para ejecutar JavaScript.
</blockquote>

<div id="table-of-contents">

## Tabla de Contenido <!-- omit from toc -->

- [Historia](#historia)
- [REPL](#repl)
- [globalThis](#globalthis)
- [Patrones de Diseño Módulo](#patrones-de-diseño-módulo)
  - [CommonJS o CJS](#commonjs-o-cjs)
  - [ES Modules](#es-modules)
- [Módulos nativos](#módulos-nativos)
  - [Importar módulos nativos](#importar-módulos-nativos)
  - [os](#os)
    - [Ejemplos](#ejemplos)
  - [fs](#fs)
    - [/promises](#promises)
  - [Modulo HTTP](#modulo-http)
    - [HTTP Header](#http-header)
    - [req argument](#req-argument)
- [NPM](#npm)
  - [Registro](#registro)
  - [Línea de comandos](#línea-de-comandos)
    - [yarn](#yarn)
  - [Uso](#uso)
    - [init](#init)
      - [entrypoint](#entrypoint)
      - [testing](#testing)
      - [keywords](#keywords)
      - [license](#license)
    - [Dependecias de producción vs desarrollo](#dependecias-de-producción-vs-desarrollo)
- [Eventos](#eventos)
  - [EventEmitter](#eventemitter)
  - [Métodos de EventEmitter](#métodos-de-eventemitter)
  - [Pasar Argumentos a los Eventos](#pasar-argumentos-a-los-eventos)
  - [Herencia de EventEmitter](#herencia-de-eventemitter)
  - [Uso en Módulos Nativos](#uso-en-módulos-nativos)

</div>

## Historia

Creado por Ryan Dall en **2009** como alternativa a **Apache HTTP server**, que no era capaz de manejar muchas consexiones de forma concurrente.

Ahora es parte de la **Open Source Foundation**.

## REPL

REPL son siglas para Read-Eval-Print Loop que se inicia ejecutando `node` en el terminal.

Es un entorno interactivo, similar a la consola de un navegador, que permite ejecutar comandos de JavaScript en tiempo real.

<blockquote class="comentario">

    Es útil para probar fragmentos de código, depurar y explorar las características de Node.js.

</blockquote>

## globalThis

Un objeto global the JavaScript común para todos los entornos.

Es equivalente al objeto `window` del navegador y `global` de NodeJS.

## Patrones de Diseño Módulo

Para programar en NodeJS vamos a usar módulos. Así encapsulamos y reutilizamos código.

### CommonJS o CJS

Forma clásica de utilizar módulos.

<blockquote class="nota">

**NOTA:** Está casi deprecated.

</blockquote>

Es necesario exportarlo en un módulo e importarlo en otro.

**EXPORTAMOS:**

```js
// math.js
// math.cjs
const sum = (a, b) => a + b;
const subtract = (a, b) => a - b;

module.exports = {
  sum,
  subtract,
};
```

**IMPORTAMOS:**

```js
// app.js
// app.cjs
const math = require("./math.js");

console.log(math.sum(5, 3)); // 8
console.log(math.subtract(5, 3)); // 2
```

### ES Modules

Es la forma **moderna y estándar** de trabajar con módulos en JavaScript.

Para usar ES Modules en Node.js, necesitas:

1. Usar la extensión `.mjs`
2. O añadir `"type": "module"` en el package.json

**EXPORTAMOS:**

```js
// math.mjs
export const sum = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// También podemos exportar por defecto
export default function multiply(a, b) {
  return a * b;
}
```

**IMPORTAMOS:**

```js
// app.mjs
import { sum, subtract } from "./math.mjs";
import multiply from "./math.mjs";

console.log(sum(5, 3)); // 8
console.log(subtract(5, 3)); // 2
console.log(multiply(5, 3)); // 15
```

## Módulos nativos

La ventaja de NodeJS es la biblioteca de módulos nativos que tiene.

### Importar módulos nativos

Lo recomendable es, no poner el nombre del módulo sino `node:nombre`.

```js
const os = require("node:os");
```

### os

Permite interactuar con el sistema operativo subyacente.

<blockquote class="comentario">

Podemos obtener información como el tipo de sistema, la arquitectura, la memoria disponible...

</blockquote>

#### Ejemplos

1. Obtener el **tipo de sistema** operativo:

   ```javascript
   const os = require("os");
   console.log(os.type()); // 'Linux', 'Darwin', 'Windows_NT', etc.
   ```

2. Obtener la **cantidad de memoria libre** en el sistema:

   ```javascript
   const os = require("os");
   console.log(os.freemem()); // Devuelve la memoria libre en bytes
   ```

3. Obtener la información de la **CPU**:

   ```javascript
   const os = require("os");
   console.log(os.cpus()); // Devuelve un array de objetos que contienen información sobre cada CPU/núcleo
   ```

### fs

Permite interactuar con el sistema de archivos.

<blockquote class="comentario">

Podemos leer, escribir, actualizar y eliminar archivos.

</blockquote>

**EJEMPLOS:**

1. **Leer** un archivo de **forma síncrona**:

    ```javascript
    const fs = require("fs");
    const data = fs.readFileSync("/path/to/file", "utf8");
    console.log(data);
    ```

2. **Escribir** en un archivo de **forma asíncrona**:

   ```javascript
   const fs = require("fs");
   fs.writeFile("/path/to/file", "Hello, world!", (err) => {
     if (err) throw err;
     console.log("El archivo ha sido guardado!");
   });
   ```

3. Crear un directorio:

   ```javascript
   const fs = require("fs");
   fs.mkdir("/path/to/directory", { recursive: true }, (err) => {
     if (err) throw err;
     console.log("El directorio ha sido creado!");
   });
   ```

#### /promises

En vez de usar callbacks para utilizar funciones del módulo de forma asíncrona, tenemos el submódulo `fs/promises`, que da un API basado en promesas.

Esto permite utilizar `async/await` para manejar operaciones de archivos de manera más limpia y manejable.

**EJEMPLOS:**

1. **Leer** un archivo usando promesas:

   ```javascript
   const fs = require("fs/promises");

   async function readFile() {
     try {
       const data = await fs.readFile("/path/to/file", "utf8");
       console.log(data);
     } catch (err) {
       console.error(err);
     }
   }
   readFile();
   ```

2. **Escribir** en un archivo usando promesas:

   ```javascript
   const fs = require("fs/promises");
   async function writeFile() {
     try {
       await fs.writeFile("/path/to/file", "Hello, world!");
       console.log("El archivo ha sido guardado!");
     } catch (err) {
       console.error(err);
     }
   }
   writeFile();
   ```

3. **Eliminar** un archivo usando promesas:

   ```javascript
   const fs = require("fs/promises");
   async function deleteFile() {
     try {
       await fs.unlink("/path/to/file");
       console.log("El archivo ha sido eliminado!");
     } catch (err) {
       console.error(err);
     }
   }
   deleteFile();
   ```

### Modulo HTTP

Un servidor puede **recibir** y **responder** a peticiones. 

```js
const http = require('node:http')

const server = http.createServer((req,res) =>{
    console.log('request received') 
    res.end('Hola Mundo')
})
```

<blockquote class="comentario">

  console.log() se ve en la consola del **servidor**, no la del **navegador**
</blockquote>


Debemos especificar donde debe escuchar el servidor.

```js

server.listen(0, () => {
    console.log('server listening on port http://localhost${server.adress().port}')
})
```

<blockquote class="nota">

**NOTA:** Al poner puerto 0 busca el primer puerto abierto. Esto en modo desarrollo es de utilidad.

**NUNCA NUNCA USAR EN MODO PRODUCCIÓN.** Lo querremos redireccionar al puerto 80, que siempre estará abierto.

</blockquote>

#### HTTP Header

Si la respuesta del servidor debe mostrarse como html le añadimos una cabecera.

```js
var http = require('http');

http.createServer(function (req,res){
    res.writeHead(200,{'Content-Type':'text/html'});
    res.write('Hello World!');
    res.end();
}).listen(8080);
```

#### req argument

The request object has a property called "url" with the part of the url after the domain name.

Hay algunos módulos que permiten dividir la petición en partes legibles, como el módulo url.

```js
var http = require('http')
var url = require('url')

http.createServer(function (req, res) {
    res.writeHead(200,{'Content-Type':'text/html'});
    let q = url.parse(req.url,true).query
    let txt = q.year+" "+q.month
    res.end(txt)
}).listen(8080);

// La petición http://localhost:8080/?year=2017&?month=July
// Produce: 2017 July
```

## NPM

NPM (Node Package Manager) surgió poco después de node.

### Registro

El registro de NPM  es una **base de datos pública** de paquetes de JavaScript.

<blockquote class="comentario">

  Los desarrolladores pueden publicar sus paquetes en el registro para que otros puedan instalarlos y utilizarlos en sus proyectos.
</blockquote>

**EJEMPLOS:**

1. **Publicar** un paquete en el registro de NPM:

    ```bash
    npm publish
    ```

2. **Instalar** un paquete desde el registro de NPM:

    ```bash
    npm install nombre-del-paquete
    ```

### Línea de comandos

Como hemos visto en los ejemplos anteriores, `NPM` proporciona una utilidad de línea de comandos que permite a los desarrolladores gestionar paquetes y dependencias en sus proyectos de Node.js.

Podemos listarlas con sus versiones en un archivo `package.json` que se genera al iniciar `npm`.

**EJEMPLOS:**

1. **Instalar** todas las dependencias listadas en `package.json`:

    ```bash
    npm install
    ```

2. **Actualizar** todas las dependencias a sus últimas versiones:

    ```bash
    npm update
    ```

#### yarn

`Yarn` es un gestor de paquetes alternativo a NPM, desarrollado por Facebook.

<blockquote class="comentario">

  Ofrece mejoras en la velocidad, seguridad y consistencia de las instalaciones de paquetes.
</blockquote>

**EJEMPLOS:**

1. **Instalar** todas las dependencias listadas en `package.json` usando Yarn:

    ```bash
    yarn install
    ```

2. **Agregar una nueva dependencia** a un proyecto usando Yarn:

    ```bash
    yarn add nombre-del-paquete
    ```

### Uso

`NPM` y `Yarn` se utilizan para gestionar las dependencias de los proyectos de `Node.js`, permitiendo a los desarrolladores instalar, actualizar y eliminar paquetes de manera eficiente.

#### init

El comando `init` se utiliza para crear un nuevo archivo `package.json`

<blockquote class="nota">

  Este es el archivo de configuración principal de un proyecto de Node.js.
</blockquote>

```plaintext
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (my-project)
version: (1.0.0)
description: My project description
entry point: (index.js)
test command:
git repository:
keywords:
author:
license: (ISC)
```

##### entrypoint

Especifica el archivo principal de la aplicación.

Por defecto, este campo se llama `main`.

```json
{
  "main": "index.js"
}
```

##### testing

Permite definir comandos personalizados que se pueden ejecutar usando `npm run`.

Esto incluye scripts de prueba.

```json
{
  "scripts": {
    "test": "mocha"
  }
}
```

##### keywords

Permite especificar palabras clave que describen el proyecto.

<blockquote class="comentario">
    Ayudan a otros desarrolladores a encontrar el paquete en el registro de NPM.
</blockquote>

```json
{
  "keywords": ["nodejs", "npm", "package"]
}
```

##### license

Especifica la licencia bajo la cual se distribuye el proyecto.

```json
{
  "license": "MIT"
}
```

#### Dependecias de producción vs desarrollo

1. **Instalar una dependencia de producción**:

    ```bash
    npm install nombre-del-paquete --save
    ```

    Esto añadirá el paquete a la sección `dependencies` en el archivo `package.json`.

2. **Instalar una dependencia de desarrollo**:

    ```bash
    npm install nombre-del-paquete --save-dev
    ```

    Esto añadirá el paquete a la sección `devDependencies` en el archivo `package.json`.

**EJEMPLO DE `package.json`**:

```json
{
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "mocha": "^8.2.1"
  }
}
```

## Eventos

Node.js utiliza un modelo de eventos para manejar operaciones asíncronas. Los eventos son una parte fundamental de Node.js y se gestionan mediante el módulo `events`.

### EventEmitter

La clase principal para manejar eventos en Node.js es `EventEmitter`. Puedes crear instancias de `EventEmitter` y registrar oyentes para eventos específicos.

**EJEMPLO BÁSICO:**

```javascript
const EventEmitter = require('events');
const myEmitter = new EventEmitter();

// Registrar un oyente para el evento 'event'
myEmitter.on('event', () => {
    console.log('Un evento ocurrió!');
});

// Emitir el evento 'event'
myEmitter.emit('event');
```

### Métodos de EventEmitter

- **on(event, listener):** Registra un oyente para el evento especificado.
- **emit(event, [arg1], [arg2], [...]):** Emite el evento especificado, pasando argumentos opcionales a los oyentes.
- **once(event, listener):** Registra un oyente que se ejecutará solo la primera vez que se emita el evento.
- **removeListener(event, listener):** Elimina un oyente específico para el evento especificado.

**EJEMPLO CON `once`:**

```javascript
const EventEmitter = require('events');
const myEmitter = new EventEmitter();

myEmitter.once('event', () => {
    console.log('Este evento se ejecuta solo una vez');
});

myEmitter.emit('event'); // Se ejecuta
myEmitter.emit('event'); // No se ejecuta
```

### Pasar Argumentos a los Eventos

Puedes pasar argumentos adicionales a los oyentes cuando emites un evento.

**EJEMPLO PASANDO ARGUMENTOS:**

```javascript
const EventEmitter = require('events');
const myEmitter = new EventEmitter();

myEmitter.on('event', (arg1, arg2) => {
    console.log(`Evento con argumentos: ${arg1}, ${arg2}`);
});

myEmitter.emit('event', 'arg1', 'arg2');
```

### Herencia de EventEmitter

Puedes hacer que tus propias clases hereden de `EventEmitter` para manejar eventos personalizados.

**EJEMPLO DE HERENCIA:**

```javascript
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {}

const myEmitter = new MyEmitter();

myEmitter.on('event', () => {
    console.log('Un evento personalizado ocurrió!');
});

myEmitter.emit('event');
```

### Uso en Módulos Nativos

Muchos módulos nativos de Node.js, como `fs`, `http` y `net`, utilizan `EventEmitter` para manejar eventos.

**EJEMPLO CON `fs`:**

```javascript
const fs = require('fs');

const readStream = fs.createReadStream('/path/to/file');

readStream.on('data', (chunk) => {
    console.log(`Recibido un chunk de datos: ${chunk}`);
});

readStream.on('end', () => {
    console.log('Lectura del archivo completada');
});
```
