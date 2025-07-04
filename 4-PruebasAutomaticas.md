# 🧪 Actividad 4: Pruebas y Refactorización – Asegurando la Calidad con Copilot

## 🎯 Propósito

En esta última actividad del laboratorio, vas a enfocarte en dos aspectos clave del desarrollo profesional: **escribir pruebas automatizadas** y **refactorizar tu código** para que sea más limpio, mantenible y robusto. Lo harás con la ayuda de GitHub Copilot y, si lo tienes habilitado, también con Copilot Chat y el modo Agente.

---

## 🧱 Requisitos previos

- Tu backend y frontend deben estar funcionando correctamente.
- Debes tener GitHub Copilot activo en VS Code.
- Idealmente, también deberías tener acceso a **Copilot Chat** y al **modo Agente** (si tu versión de VS Code lo permite).

---

## 🧪 Parte 1: Escribir pruebas automatizadas

### 1. Configura el entorno de pruebas

#### Si estás usando Node.js con TypeScript:
- Abre la terminal y ejecuta:
  ```bash
  npm install --save-dev jest ts-jest @types/jest
  npx ts-jest config:init
  ```

- Crea un archivo llamado `tasks.test.ts`.

### 2. Guía a Copilot para escribir tu primer test

Abre el archivo de prueba y escribe:

```ts
// Prueba que cree una tarea y luego la recupere
```

✋ Espera a que Copilot sugiera un bloque `describe` e `it`. Si no lo hace, escribe:

```ts
describe('API de Tareas', () => {
  it('debería crear y luego obtener una tarea nueva', async () => {
```

Copilot debería completar el resto. Si no lo hace, puedes preguntarle en Copilot Chat:

> “¿Cómo escribo una prueba con Jest para una API REST en Express?”

Asegúrate de que la prueba:
- Cree una tarea con `POST /tasks`.
- Luego haga un `GET /tasks` y verifique que la tarea esté presente.

### 3. Ejecuta las pruebas

En la terminal:

```bash
npx jest
```

Si algo falla, copia el error y pregúntale a Copilot Chat:

> “¿Qué significa este error en Jest?”  
> “¿Cómo soluciono este fallo en la prueba?”

---

## 🔁 Parte 2: Refactorización con Copilot

### 1. Identifica código repetido o confuso

Abre tu archivo principal (`index.ts`, `app.ts`, etc.) y busca funciones largas, duplicadas o difíciles de leer.

### 2. Usa comentarios para guiar a Copilot

Por ejemplo, escribe:

```ts
// Extraer esta lógica a una función separada
```

Copilot debería sugerir una función auxiliar. Si no lo hace, selecciona el bloque de código y pregunta en Copilot Chat:

> “¿Puedes ayudarme a refactorizar esta función para que sea más clara?”

### 3. Mejora la legibilidad

Agrega comentarios como:

```ts
// Agregar JSDoc para esta función
```

Copilot puede generar automáticamente la documentación. También puedes pedirle:

> “Agrega comentarios explicativos a este archivo”

---

## 🤖 (Opcional) Usa el Modo Agente de Copilot

Si tienes acceso al modo Agente:

1. Abre la vista de Copilot Chat.
2. Cambia el modo de “Chat” a “Agente”.
3. Escribe una instrucción como:

> “Refactoriza el archivo index.ts para separar responsabilidades y agregar comentarios JSDoc”

El agente analizará tu proyecto y propondrá un plan. Puedes aceptar o ajustar los pasos.

---

## ✅ Validación

- Ejecuta todas las pruebas y asegúrate de que pasen.
- Verifica que el código refactorizado siga funcionando.
- Usa `git diff` o tu control de versiones para revisar los cambios.

---

## 🧠 Resultado esperado

Al finalizar esta actividad deberías tener:

- Una suite de pruebas automatizadas que valida tu backend.
- Un código más limpio, modular y documentado.
- Experiencia usando Copilot como asistente de calidad, no solo de generación.

---

## 🚀 Reflexión final

Esta actividad cierra el ciclo completo de desarrollo asistido por IA: desde la generación inicial, pasando por la implementación de lógica de negocio, hasta la validación y mejora del código. Aprendiste a usar Copilot no solo para escribir más rápido, sino para pensar mejor, validar tus ideas y mantener tu código en forma.

¡Felicidades por completar el laboratorio! 🎉

---