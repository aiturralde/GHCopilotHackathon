# 🧱 Actividad 1: API Backend – Construyendo la base con Copilot

## 🎯 Propósito

En esta primera actividad vas a construir un servidor API REST para gestionar tareas. El objetivo es que experimentes cómo GitHub Copilot puede ayudarte a generar rápidamente la estructura de un backend funcional, incluyendo rutas CRUD (Crear, Leer, Actualizar, Eliminar), usando Node.js con Express o Fastify y TypeScript.

---

## 🧱 Punto de partida

Antes de comenzar, asegúrate de tener:

- Node.js y npm instalados.
- Visual Studio Code con GitHub Copilot y Copilot Chat activos.
- Un proyecto vacío o una carpeta para trabajar.

---

## 🛠️ Paso a paso con Copilot

### 1. Inicializa tu proyecto

Abre la terminal y ejecuta:

```bash
npm init -y
npm install express typescript ts-node-dev @types/node @types/express
npx tsc --init
```

Crea un archivo `index.ts` y ábrelo en VS Code.

---

### 2. Configura el servidor con Copilot

En `index.ts`, escribe:

```ts
// Configurar un servidor Express que escuche en el puerto 3000
```

✋ Espera a que Copilot sugiera el código base: importar express, crear la app, usar `app.listen`, etc. Si no lo hace, presiona `Ctrl + Enter` para ver sugerencias o pregunta en Copilot Chat:

> “¿Cómo configuro un servidor Express básico en TypeScript?”

Acepta la sugerencia si es adecuada, o ajústala según tus necesidades.

---

### 3. Define el modelo de datos

Crea una interfaz para representar una tarea. Escribe:

```ts
// Definir la interfaz Task con id, titulo, descripcion, completado y fechaCreacion
```

Copilot debería sugerir una estructura como:

```ts
interface Task {
  id: number;
  titulo: string;
  descripcion?: string;
  completado: boolean;
  fechaCreacion: Date;
}
```

Si no lo hace, puedes guiarlo con más detalles o pedir ayuda en Copilot Chat:

> “¿Cómo defino una interfaz en TypeScript para una tarea con esos campos?”

---

### 4. Implementa las rutas CRUD

#### a) GET /tasks

Escribe:

```ts
// Ruta GET /tasks que devuelve todas las tareas
```

Copilot debería sugerir una función que devuelva un array de tareas. Asegúrate de tener una variable global `tasks` para almacenar las tareas en memoria.

#### b) POST /tasks

Escribe:

```ts
// Ruta POST /tasks que crea una nueva tarea
```

Copilot debería sugerir extraer `req.body`, crear una nueva tarea con `fechaCreacion: new Date()` y agregarla al array.

#### c) PUT /tasks/:id

Escribe:

```ts
// Ruta PUT /tasks/:id que actualiza una tarea existente
```

Copilot debería sugerir buscar la tarea por ID y actualizar sus campos.

#### d) DELETE /tasks/:id

Escribe:

```ts
// Ruta DELETE /tasks/:id que elimina una tarea
```

Copilot debería sugerir filtrar el array para eliminar la tarea correspondiente.

💡 Consejo: Si Copilot no sugiere lo que esperas, agrega más contexto en los comentarios o divide el problema en pasos más pequeños.

---

## 🧪 Validación

1. Ejecuta el servidor con:
   ```bash
   npx ts-node-dev index.ts
   ```

2. Usa Postman, Insomnia o `curl` para probar las rutas:
   - `GET /tasks` → debería devolver un array (vacío al inicio).
   - `POST /tasks` → crea una nueva tarea.
   - `PUT /tasks/:id` → actualiza una tarea.
   - `DELETE /tasks/:id` → elimina una tarea.

3. Si algo falla, copia el error y pregunta en Copilot Chat:

> “¿Qué significa este error en Express?”  
> “¿Por qué mi ruta POST no está funcionando?”

---

## 💬 Sugerencias de uso de Copilot Chat

- “¿Cómo valido que el título no esté vacío en una ruta POST?”
- “¿Cómo devuelvo un error 404 si no encuentro una tarea?”
- “¿Cómo uso middlewares en Express?”

---

## ✅ Resultado esperado

Al finalizar esta actividad deberías tener:

- Un servidor Express corriendo en `localhost:3000`.
- Rutas CRUD funcionales para gestionar tareas.
- Un modelo de datos en memoria con TypeScript.
- Experiencia guiando a Copilot con comentarios y prompts claros.

---

## 🚀 Reflexión final

Esta actividad te mostró cómo Copilot puede ayudarte a arrancar un proyecto desde cero. Aprendiste a guiarlo con comentarios, validar sus sugerencias y construir un backend funcional sin escribir cada línea manualmente.

¡Vamos por la siguiente funcionalidad! 💡

## ➡️ Siguiente desafío

Continúa con la siguiente actividad: **[Actividad 2: Nueva Característica – Autocompletado de Tareas tras 24 Horas](2-ExtenderBackened.md)**