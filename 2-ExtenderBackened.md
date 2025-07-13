# 🧩 Actividad 2: Nueva Característica – Autocompletado de Tareas tras 24 Horas

## 🎯 Propósito

En esta actividad vas a extender el backend que creaste en la Actividad 1, agregando una funcionalidad de negocio: marcar automáticamente como completadas las tareas que tengan más de 24 horas desde su creación. El objetivo es que explores cómo Copilot puede ayudarte a implementar lógica personalizada, no solo código repetitivo.

---

## 🧱 Punto de partida

Antes de comenzar, asegúrate de que:

- Tu backend esté funcionando correctamente.
- El modelo de tarea incluya un campo `fechaCreacion`.
- GitHub Copilot y Copilot Chat estén activos en tu editor.

---

## 🧠 ¿Qué vas a construir?

Una función que revise las tareas existentes y marque como completadas las que tengan más de 24 horas desde su creación. Esta función puede ejecutarse:

- Cada cierto intervalo (por ejemplo, cada minuto).
- O justo antes de devolver las tareas al cliente (cuando se hace un GET a `/tasks`).

Para este laboratorio, usaremos la segunda opción por simplicidad.

---

## 🛠️ Paso a paso con Copilot

### 1. Asegúrate de tener `fechaCreacion` en el modelo

Abre el archivo donde defines las tareas y escribe:

```ts
// Agregar campo fechaCreacion al modelo de tarea
```

Observa lo que Copilot sugiere. ¿Te propone un campo `fechaCreacion: Date`? ¿Lo incluye al crear una nueva tarea? Si no, puedes guiarlo con:

```ts
// Al crear una nueva tarea, asignar fechaCreacion con new Date()
```

Si tienes dudas, pregunta en Copilot Chat:

> “¿Cómo agrego un timestamp al crear un objeto en TypeScript?”

---

### 2. Crear la función de autocompletado

En el archivo donde manejas las rutas o lógica de negocio, escribe:

```ts
// Función que marca tareas como completadas si tienen más de 24 horas
```

Copilot debería sugerirte una función que recorra las tareas, compare la fecha actual con `fechaCreacion` y actualice el campo `completado`.

Si no lo hace, puedes guiarlo con:

```ts
// Si Date.now() - fechaCreacion > 86400000, marcar como completada
```

Y si necesitas ayuda con la lógica de fechas, pregunta en Copilot Chat:

> “¿Cómo comparo fechas en JavaScript para saber si pasaron 24 horas?”

---

### 3. Invocar la función en la ruta GET `/tasks`

Ve a la ruta que devuelve las tareas y escribe:

```ts
// Antes de devolver las tareas, actualizar las vencidas
```

Copilot debería sugerirte llamar a la función que acabas de crear. Si no lo hace, puedes escribir el nombre manualmente y dejar que complete los argumentos.

---

## 🧪 Validación

Para probar sin esperar 24 horas reales:

- Crea una tarea con `fechaCreacion` manualmente ajustada a más de 24 horas atrás.
- O modifica temporalmente la condición a 10 segundos (`10000` ms) para ver el efecto inmediato.

Haz una petición GET a `/tasks` y verifica si la tarea aparece como completada.

Si algo no funciona, copia el fragmento de código y pregunta en Copilot Chat:

> “¿Ves algún error en esta lógica de tiempo?”

---

## 💬 Sugerencias de uso de Copilot Chat

- “¿Cómo recorro un array y actualizo objetos en JavaScript?”
- “¿Cómo convierto una fecha a milisegundos?”
- “¿Cómo ejecuto una función cada minuto en Node.js?”

---

## ✅ Resultado esperado

Al finalizar esta actividad deberías tener:

- Una función que marca automáticamente como completadas las tareas vencidas.
- Una ruta GET que actualiza el estado de las tareas antes de devolverlas.
- Una mejor comprensión de cómo guiar a Copilot para implementar lógica de negocio.

---

## 🚀 Reflexión final

Esta actividad demuestra que Copilot no solo sirve para escribir código repetitivo, sino también para ayudarte a pensar, planificar y resolver problemas reales. Aprendiste a dividir un problema, guiar a Copilot con buenos prompts y validar tu solución.

¡Vamos por la interfaz! 💡

Aquí tienes el contenido actualizado del archivo **2-ExtenderBackened.md**, incluyendo la sección de navegación al final:

---

## ➡️ Siguiente desafío

Continúa con la siguiente actividad: **[Actividad 3: Interfaz Frontend – Conectando el Backend con el Usuario](3-FrontEnd.md)**
