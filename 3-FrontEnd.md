# 🖥️ Actividad 3: Interfaz Frontend – Conectando el Backend con el Usuario

## 🎯 Propósito

En esta actividad vas a construir una interfaz web que se conecte con el backend de tareas que creaste en la Actividad 1. El objetivo es que experimentes cómo GitHub Copilot puede ayudarte a generar componentes, formularios y llamadas HTTP de forma rápida y fluida, tanto en Angular como en Next.js.

---

## 🧱 Preparación del Proyecto Base

Antes de comenzar, asegúrate de tener un proyecto frontend funcional. Puedes elegir entre Angular o Next.js, según tu experiencia o preferencia.

### 🔧 Opción A: Angular

1. Abre tu terminal y ejecuta:
   ```bash
   npm install -g @angular/cli
   ng new tareas-frontend
   cd tareas-frontend
   ng serve
   ```

2. Abre `http://localhost:4200` en tu navegador.

3. Verifica que Copilot esté activo en archivos `.ts` y `.html`.

### ⚙️ Opción B: Next.js

1. En la terminal:
   ```bash
   npx create-next-app@latest tareas-frontend --typescript
   cd tareas-frontend
   npm run dev
   ```

2. Abre `http://localhost:3000` en tu navegador.

3. Verifica que Copilot esté activo en archivos `.tsx`.

---

## 🛠️ Construcción de la Interfaz con Copilot

### 1. Crear un servicio o función para obtener tareas

Abre el archivo donde quieras definir la lógica para obtener tareas (por ejemplo, `task.service.ts` en Angular o un hook en Next.js) y escribe:

```ts
// Obtener todas las tareas desde el backend
```

✋ Detente un momento y observa lo que Copilot sugiere. ¿Te propone una función con `fetch` o `HttpClient`? ¿Está usando la URL correcta (`http://localhost:3000/tasks`)? Si no es lo que esperas, ajusta el comentario o usa Copilot Chat para preguntar:

> “¿Cómo hago una petición GET en Angular/React para obtener datos de una API?”

Acepta la sugerencia si es útil, o edítala según lo que necesites.

---

### 2. Mostrar la lista de tareas

En tu componente principal, escribe un comentario como:

```ts
// Mostrar una lista de tareas con su estado
```

Copilot debería sugerirte un bucle `*ngFor` (Angular) o `.map()` (React). Asegúrate de que cada tarea muestre su título y si está completada (`✅` o `⌛`).

Si no aparece nada útil, prueba en Copilot Chat:

> “¿Cómo muestro una lista de objetos en Angular/React?”

---

### 3. Crear un formulario para agregar tareas

En tu componente, escribe:

```ts
// Crear un formulario para agregar una nueva tarea
```

Copilot debería sugerirte un input y un botón, y una función para enviar la tarea al backend. Si no lo hace, puedes guiarlo con más contexto:

```ts
// Formulario con input para título y botón que llama a addTask()
```

Y si necesitas ayuda con el binding o el estado, pregunta en Copilot Chat:

> “¿Cómo hago binding con ngModel en Angular?”  
> “¿Cómo manejo el estado de un input en React?”

---

### 4. (Opcional) Marcar tareas como completadas

Agrega un comentario como:

```ts
// Botón para marcar una tarea como completada
```

Copilot debería sugerirte una función que haga un `PUT` o `PATCH` al backend. Si no lo hace, puedes escribir:

```ts
// PUT a /tasks/:id para actualizar el campo completado
```

Y dejar que Copilot complete la lógica.

---

## ✅ Validación

- Crea una tarea y verifica que aparezca en la lista.
- Marca una tarea como completada y revisa que cambie su estado.
- Refresca la página y asegúrate de que los datos persisten correctamente.

---

## 💬 Sugerencias de uso de Copilot Chat

Si en algún momento te atascas, Copilot Chat está para ayudarte. Aquí algunos ejemplos útiles:

- “¿Cómo creo un servicio HTTP en Angular?”
- “¿Cómo uso useEffect para obtener datos en React?”
- “¿Cómo conecto un formulario a una función en Angular/React?”

Recuerda: cuanto más claro y específico seas en tu prompt, mejores serán las sugerencias.

---

## 🧠 Resultado esperado

Al finalizar esta actividad deberías tener una interfaz web funcional que:

- Se conecta con tu backend.
- Permite crear y visualizar tareas.
- (Opcional) Permite marcarlas como completadas.

Y lo más importante: habrás usado GitHub Copilot como un verdadero copiloto, guiándolo con tus ideas y refinando sus sugerencias.

---

## 🚀 Reflexión final

Esta actividad no se trata solo de escribir código, sino de aprender a colaborar con una IA que te asiste. Copilot no reemplaza tu criterio: lo potencia. Aprendiste a guiarlo con buenos prompts, a validar sus sugerencias y a construir una interfaz completa sin escribir cada línea desde cero.

¡Vamos por la siguiente actividad! 💡

---