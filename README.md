#  Editor de Markdown - Uso de Promesas y Asincronía en JavaScript

##  Introducción
Este documento explica por qué la asincronía es clave en la lectura y exportación de archivos en un Editor de Markdown, los beneficios de usar Promesas frente a callbacks, y cómo manejar errores con `try/catch`. Además, cubre las diferencias entre `.then()` y `.catch()`.

---

##  Importancia de la Asincronía en un Editor de Markdown
JavaScript es un lenguaje de un solo hilo, lo que significa que solo puede ejecutar una tarea a la vez. Si realizamos la lectura de archivos de manera **sincrónica**, el programa se detendría hasta que la operación termine, lo que bloquearía la interfaz de usuario.

Con la **asincronía**, podemos leer el archivo sin bloquear la aplicación, permitiendo que siga respondiendo a otras interacciones del usuario.

---

##  Beneficios de Promesas frente a Callbacks
Antes de las Promesas, los callbacks eran la forma principal de manejar la asincronía, pero tenían problemas:

- **Callback Hell**: Código anidado difícil de leer y mantener.
- **Manejo de errores complicado**: Cada callback debe verificar errores manualmente.

Las **Promesas** solucionan estos problemas:
✅ Más legibles con `.then()`.  
✅ Separan el éxito (`.then()`) de los errores (`.catch()`).  
✅ Permiten combinaciones fáciles con `Promise.all()` o `async/await`.

---

## 🛡 Uso de `try/catch` en `async/await`
Cuando usamos `async/await`, el manejo de errores es más ordenado con `try/catch`:

```javascript
async function leerArchivo(ruta) {
    try {
        const respuesta = await fetch(ruta); // Simulación de lectura de archivo
        if (!respuesta.ok) throw new Error("No se pudo leer el archivo");
        const contenido = await respuesta.text();
        console.log("Contenido leído:", contenido);
        return contenido;
    } catch (error) {
        console.error("Error al leer el archivo:", error.message);
    }
}
```

Si la lectura falla, el error es capturado en `catch`, evitando que el programa se detenga abruptamente.

---

##  Diferencia entre `.then()` y `.catch()`
Ambos son métodos de Promesas, pero tienen usos distintos:

```javascript
fetch("archivo.md")
    .then(respuesta => {
        if (!respuesta.ok) throw new Error("Archivo no encontrado");
        return respuesta.text();
    })
    .then(contenido => console.log("Contenido:", contenido))
    .catch(error => console.error("Error:", error.message));
```

- `.then()` maneja el resultado exitoso de una Promesa.
- `.catch()` captura errores en la cadena de Promesas.

Esto es equivalente a `try/catch` en `async/await`, pero en el estilo basado en Promesas.

---

##  ¿Cuál usar? `.then().catch()` vs `async/await`
Ambos son válidos, pero:
- `async/await` es más limpio y fácil de leer.
- `.then().catch()` es útil para encadenar Promesas sin variables intermedias.

Para un **Editor de Markdown**, `async/await` hará que el código sea más claro y mantenible.

---

##  Conclusión
El uso de Promesas y `async/await` mejora la eficiencia de un Editor de Markdown al permitir la lectura de archivos sin bloquear la aplicación. Además, facilita el manejo de errores y hace el código más limpio y mantenible.

