# 💾 Actividad 5: Persistencia – Guardando tareas con node-persist

## 🎯 Propósito

Hasta ahora, tu backend ha estado guardando las tareas en memoria. Eso significa que si reinicias el servidor, ¡todo se pierde! En esta actividad vas a integrar un sistema de almacenamiento persistente usando `node-persist`, una librería simple y efectiva para guardar datos localmente en disco.

El objetivo es que explores cómo Copilot puede ayudarte a refactorizar tu backend para que las tareas se guarden y recuperen automáticamente, incluso después de reiniciar el servidor.

---

## 🧱 Punto de partida

Antes de comenzar, asegúrate de tener:

- Tu backend funcional con rutas CRUD.
- GitHub Copilot y Copilot Chat activos.
- El paquete `node-persist` instalado:

```bash
npm install node-persist
```

---

## 🛠️ Paso a paso con Copilot

### 1. Inicializa node-persist

Abre tu archivo principal (`index.ts`) y escribe:

```ts
// Inicializar node-persist para guardar tareas en disco
```

Copilot debería sugerirte algo como:

```ts
import * as storage from 'node-persist';

await storage.init();
```

Si no lo hace, puedes guiarlo con:

```ts
// Importar node-persist y llamar a storage.init()
```

Y si tienes dudas, pregunta en Copilot Chat:

> “¿Cómo uso node-persist para guardar datos en un proyecto Node.js?”

---

### 2. Reemplaza el array en memoria

Hasta ahora probablemente tenías algo como:

```ts
let tasks: Task[] = [];
```

Escribe un comentario como:

```ts
// Reemplazar el array en memoria por almacenamiento persistente
```

Copilot debería sugerirte usar `storage.getItem('tasks')` y `storage.setItem('tasks', updatedTasks)`.

💡 Consejo: puedes crear funciones auxiliares como `loadTasks()` y `saveTasks()` para mantener tu código limpio.

---

### 3. Refactoriza las rutas CRUD

#### GET /tasks

Escribe:

```ts
// Obtener tareas desde node-persist
```

Copilot debería sugerir usar `await storage.getItem('tasks')`.

#### POST /tasks

Escribe:

```ts
// Agregar una nueva tarea y guardarla en node-persist
```

Copilot debería sugerir cargar las tareas, agregar la nueva, y volver a guardarlas.

Haz lo mismo para PUT y DELETE.

---

## 🧪 Validación

1. Ejecuta tu servidor.
2. Crea una tarea con `POST /tasks`.
3. Reinicia el servidor.
4. Haz un `GET /tasks` y verifica que la tarea sigue ahí.

Si algo falla, copia el error y pregunta en Copilot Chat:

> “¿Por qué node-persist no está guardando mis datos?”

---

## 💬 Sugerencias de uso de Copilot Chat

- “¿Cómo guardo un array de objetos con node-persist?”
- “¿Cómo actualizo un objeto dentro de un array y lo vuelvo a guardar?”
- “¿Cómo manejo errores si el archivo de persistencia no existe?”

---

## ✅ Resultado esperado

Al finalizar esta actividad deberías tener:

- Un backend que guarda las tareas en disco.
- Rutas CRUD que leen y escriben usando `node-persist`.
- Un código más robusto y listo para producción local.

---

## 🚀 Reflexión final

Esta actividad te mostró cómo pasar de un backend temporal a uno persistente. Aprendiste a integrar una librería externa, guiar a Copilot para refactorizar tu código y validar que los datos se mantengan entre reinicios.

¡Tu backend ahora tiene memoria! 🧠

---