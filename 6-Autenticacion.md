# 🔒 Actividad 6: Autenticación y Seguridad – Protegiendo la API con JWT 

## 🎯 Propósito 
En esta actividad agregarás **autenticación y autorización** a tu API de tareas para que solo usuarios autorizados puedan acceder a los endpoints. Esto implica implementar un mecanismo de login que entregue un token de seguridad (usaremos **JWT**, JSON Web Tokens) y exigir ese token en las rutas de la API. El objetivo es que experimentes cómo GitHub Copilot puede asistirte en incorporar medidas de seguridad en tu aplicación sin perder fluidez de desarrollo. *Existen varios métodos comunes para asegurar APIs* (como **Autenticación Básica**, **API Keys**, **OAuth 2.0** y **JWT**, entre otros), pero en este laboratorio nos centraremos en JWT por ser una solución moderna, **stateless** y ampliamente usada para APIs web. Un **JWT** es un token firmado digitalmente que el servidor genera tras verificar las credenciales de un usuario, y que el cliente debe enviar en cada petición subsecuente (típicamente en la cabecera **Authorization**) para acceder a rutas protegidas. 

Al finalizar, tendrás tu backend protegido con autenticación JWT y el frontend ajustado para usarlo, manteniendo una buena experiencia de usuario. ¡Vamos a agregar seguridad a nuestra aplicación! 🔐

## 🧱 Punto de partida 
Antes de comenzar, asegúrate de contar con:  
- **Backend listo** con las rutas CRUD de tareas funcionando (resultado de actividades previas). Si has hecho la Actividad 5, tu backend ya persiste tareas en disco.  
- **Frontend funcional** (Angular o Next.js) capaz de listar, crear y marcar tareas (de la Actividad 3).  
- **GitHub Copilot** y **Copilot Chat** activos en tu editor para que te asistan.  
- El paquete de JWT instalado en el backend. Desde la terminal en el proyecto backend, ejecuta:  
  ```bash
  npm install jsonwebtoken @types/jsonwebtoken
  ``` 
  Esto instala la librería **jsonwebtoken**, popular para crear y verificar JWT en Node.js.  

Además, piensa en alguna credencial de prueba para el login. Por simplicidad, usaremos un usuario *hardcoded* (por ejemplo, usuario `"admin"` con contraseña `"admin123"`), ya que no tenemos gestión de usuarios ni base de datos de credenciales en este proyecto de hackathon. 

## 🛠️ Paso a paso con Copilot 

### 1. Configura un secreto y middleware básico de JWT en el backend  
Abre tu archivo principal del servidor (por ejemplo, `index.ts`). Vamos a configurar un **“secreto”** para firmar los tokens. Escribe un comentario:  
```ts
// Configurar secreto JWT y middleware de verificación
```  
💡 **Copilot** debería sugerir la creación de una constante con la clave secreta (por ejemplo, `const JWT_SECRET = "algoMuySecreto";`). En un entorno real, esta clave debe almacenarse en variables de entorno y nunca en el código fuente público, pero para este ejercicio puedes definirla directamente. Copilot también podría empezar a esbozar una función middleware para verificar tokens en las solicitudes. Si no ves sugerencias, pídele ayuda en Copilot Chat:  
> *“¿Cómo configuro un middleware en Express para validar un JWT?”*  

Acepta la sugerencia si ves que crea una función, quizás llamada `verifyToken` o similar, que use `jsonwebtoken`. En esencia, este **middleware** debe: obtener el token del header `Authorization`, verificarlo con `jwt.verify(token, JWT_SECRET)`, manejar errores si el token es inválido o expiró, y llamar a `next()` si todo está bien. Asegúrate de que retorne un **401 Unauthorized** si no hay token o es inválido. Copilot podría sugerir algo así: 

```ts
function verifyToken(req, res, next) {
  const authHeader = req.headers['authorization'];
  const token = authHeader && authHeader.split(' ')[1];
  if (!token) {
    return res.sendStatus(401);
  }
  try {
    const decoded = jwt.verify(token, JWT_SECRET);
    req.user = decoded;  // guardar info del usuario si fuera necesario
    next();
  } catch (err) {
    return res.sendStatus(403);
  }
}
``` 

Si la sugerencia no aparece completa, guíala añadiendo detalles en comentarios (por ejemplo: `// usar jwt.verify para validar el token`). Preguntas útiles para Copilot Chat podrían ser:  
> *“¿Cómo obtengo el token JWT del header Authorization en Express?”*  

> *“¿Qué respuesta doy si el token no es válido?”*  

### 2. Crea una ruta de **login** que emita un token JWT  
Ahora implementaremos la ruta para **iniciar sesión**. Esta ruta recibirá credenciales (usuario y contraseña) y, si son correctas, devolverá un token JWT firmado. En tu servidor Express, escribe un comentario para que Copilot lo reconozca, por ejemplo:  
```ts
// Ruta POST /login que valida credenciales y devuelve un JWT
```  
✋ **Detente y observa** si Copilot te sugiere código para la ruta. Idealmente, debería: 1) leer `req.body` para usuario y contraseña, 2) comprobar que coinciden con nuestro usuario de prueba (ej. `"admin"/"admin123"`), y 3) si son válidos, generar un token con `jwt.sign`. Si Copilot no completa la lógica, puedes guiarlo paso a paso. Escribe por ejemplo:  
```ts
// Si las credenciales son válidas, generar token JWT con jwt.sign
```  
Copilot podría entonces sugerir algo utilizando `jwt.sign({ userId: ... }, JWT_SECRET, { expiresIn: '1h' })`[3](https://dev.to/ilyasgaraad/secure-your-rest-api-with-jwt-authentication-beginner-friendly-2e5f). Usa un **payload** sencillo, por ejemplo el ID o nombre de usuario. Para nuestro demo, podríamos hacer:  
```ts
const token = jwt.sign({ username: user }, JWT_SECRET, { expiresIn: '1h' });
```  
Esto crea un token válido por **1 hora**. Establecer expiración es importante para limitar el tiempo en que un token robado sería útil. Si las credenciales no coinciden, la ruta debe responder con un error (401 o 403). Copilot puede sugerir un mensaje de error como *"Credenciales inválidas"* en ese caso. 

> 🗒️ *Nota:* Normalmente las contraseñas no se comparan en texto plano, se almacenarían cifradas y se verificarían con hashing seguro. Pero en este contexto simplificado aceptaremos una comparación directa para enfocarnos en JWT. Aun así, es bueno preguntar a Copilot Chat por curiosidad: *“¿Cómo debería almacenar y verificar contraseñas de usuarios de forma segura?”*.

### 3. Protege las rutas de tareas con el middleware de autenticación  
Con la ruta de login lista, vamos a **restringir el acceso** a las demás rutas (las de tareas) usando el middleware `verifyToken` creado en el paso 1. Es probable que tus rutas CRUD de tareas estén registradas algo como:  
```ts
app.get('/tasks', ...);
app.post('/tasks', ...);
``` 
y así sucesivamente. Para asegurarlas, inserta el middleware de dos formas posibles: 

- **Opción 1:** Usar el middleware en cada ruta, por ejemplo:  
  ```ts
  app.get('/tasks', verifyToken, (req, res) => { ... });
  ``` 
  de manera que antes de ejecutar la lógica de la ruta se valide el token. 

- **Opción 2:** Usar `app.use` en el router de tareas para aplicar el middleware a todas las subrutas. Por ejemplo, si tienes algo como `app.use('/tasks', tasksRouter)`, puedes aplicar `tasksRouter.use(verifyToken)` o directamente `app.use('/tasks', verifyToken, tasksRouter)`. 

Elige el enfoque según cómo esté estructurado tu código. Si todas las rutas están en el mismo archivo, quizás la opción 1 sea más sencilla añadiendo `verifyToken` como segundo argumento en cada ruta. 

Escribe en tu código un comentario sobre proteger las rutas, por ejemplo:  
```ts
// Proteger rutas /tasks/* con el middleware de autenticación
```  
Copilot puede automáticamente insertar el middleware en cada ruta definida debajo. Revisa que efectivamente ahora **todas las operaciones CRUD de tareas requieren haber enviado un token válido**. Para verificarlo, puedes intentar arrancar el servidor y hacer una petición a `/tasks` sin token: debería responder **401 Unauthorized** (o 403 Forbidden si token inválido). Si en lugar de eso tienes acceso libre, repasa si colocaste bien el middleware. Ante dudas, pregunta a Copilot Chat:  
> *“¿Cómo protejo mis rutas Express usando un middleware de JWT?”*  

### 4. Actualiza el **frontend**: flujo de Login y almacenamiento del token  
Con el backend seguro, necesitamos modificar el frontend para que pueda **obtener y usar el token JWT**. Esto implica dos tareas principales en la aplicación cliente: **iniciar sesión** (pedir credenciales al usuario y llamar al nuevo endpoint `/login`) y luego **adjuntar el token** en las peticiones a la API. 

#### a) Añadir interfaz de inicio de sesión  
En tu aplicación frontend (ya sea Angular o Next.js/React), crea un simple formulario de login. Por ejemplo: un campo de texto para “usuario”, otro para “contraseña” y un botón “Ingresar”. No es necesario gestionar registros de usuarios; solo autenticaremos al usuario de prueba conocido. 

En Angular, podrías generar un componente de login o simplemente agregar el formulario en el componente existente que lista tareas (condicionalmente mostrando uno u otro). En Next.js/React, puedes crear un pequeño componente o usar el estado local para condicionar la vista. **Usa Copilot para acelerar esto**: Por ejemplo, en Angular abre el HTML relevante y escribe un comentario:  
```html
<!-- Formulario de login con inputs de usuario, password y botón --> 
``` 
Copilot debería sugerir un snippet de formulario (por ejemplo usando `[(ngModel)]` para enlazar dos variables en el componente TS, y un `(ngSubmit)` o click en el botón para llamar a una función de login). Acepta la sugerencia y luego ve al archivo TypeScript correspondiente y escribe un comentario como:  
```ts
// Método login() que envía credenciales al backend y maneja el token
``` 
Copilot puede autocompletar la lógica: usar HttpClient (Angular) o fetch (Next.js) para hacer un **POST** a `http://localhost:3000/login` con el usuario y contraseña, y recibir el token en la respuesta. Asegúrate de **guardar el token** cuando llegue. Por ejemplo, en Angular podrías almacenarlo en `localStorage`:  
```ts
localStorage.setItem('token', receivedToken);
``` 
En React, podrías usar `localStorage` igualmente o manejarlo en un estado global/contexto. Puedes preguntar a Copilot Chat:  
> *“¿Cómo guardo un token JWT en el navegador de forma segura?”*  

Copilot puede mencionar que **localStorage** es sencillo pero susceptible a ataques XSS, mientras que usar **cookies HttpOnly** es más seguro. Para este ejercicio, usaremos localStorage por simplicidad, pero **ten en cuenta las implicaciones de seguridad**. 

Una vez almacenado el token, tu frontend debería saber que el usuario “está logueado”. Puedes, por ejemplo, mantener un estado booleano `isLoggedIn` en el componente (true después de login exitoso) o simplemente checar la existencia de `localStorage.getItem('token')`. Usa esa condición para mostrar la lista de tareas solo si hay token; si no, mostrar el formulario de login. De esta manera forzamos al usuario a loguearse antes de acceder a las tareas. 

#### b) Incluir el token en las peticiones desde el frontend  
Ahora viene la parte crucial: el frontend debe enviar el token al backend en cada llamada a la API de tareas. Esto suele hacerse agregando un header **Authorization: Bearer \<token\>** en las solicitudes HTTP. 

- **En Angular**: Si usas un servicio (`HttpClient`) para obtener las tareas, modifica la llamada GET (y las POST/PUT/DELETE) para añadir el header. Por ejemplo:  
  ```ts
  const token = localStorage.getItem('token');
  this.http.get('/tasks', {
      headers: new HttpHeaders().set('Authorization', `Bearer ${token}`)
  });
  ``` 
  Puedes guiar a Copilot escribiendo un comentario en el servicio:  
  ```ts
  // Incluir el header Authorization con Bearer token si existe
  ``` 
  Es probable que sugiera el código adecuado para adjuntar el token. Otra forma más elegante es implementar un **HttpInterceptor** que agregue automáticamente el header a cada petición. Esto es opcional; si tienes tiempo en el hackathon, podrías intentar que Copilot cree un interceptor (preguntando: *“¿Cómo implemento HttpInterceptor para JWT en Angular?”*), pero no es obligatorio. 

- **En Next.js/React**: Si en la actividad anterior usaste `fetch` para las peticiones, ahora deberás incluir el header en cada fetch. Podrías centralizarlo, pero quizá lo más directo es modificar las funciones que hacían fetch. Por ejemplo:  
  ```jsx
  const token = localStorage.getItem('token');
  fetch('http://localhost:3000/tasks', {
    headers: { 'Authorization': 'Bearer ' + token }
  })
  ``` 
  Haz algo similar para POST/PUT/DELETE. Una técnica común en React es guardar el token en un Context o en estado global (usando Redux o similar) para accederlo fácilmente, pero para no complicar el laboratorio, leer de `localStorage` cuando se necesite está bien. Asegúrate de que este código solo se ejecute cuando el token exista (es decir, después de login). 

Después de estos cambios, tu aplicación cliente enviará el JWT en cada solicitud. Gracias a nuestro middleware en el backend, **solo** si el token es válido las operaciones se completarán. 

### 5. Prueba la funcionalidad segura end-to-end  
¡Hora de probar! 🎉 Inicia tu backend (por ejemplo, `npm start` o `npx ts-node-dev index.ts`) y tu frontend (Angular: `ng serve`, Next: `npm run dev`). Abre tu aplicación en el navegador: 

- Si todo está bien, inicialmente debería aparecer el **formulario de login**. Intenta acceder a la lista de tareas sin loguearte (por ejemplo, si tu app muestra la lista vacía automáticamente, debería haber fallos en la consola de las peticiones a `/tasks` con **401**). 
- Ingresa las credenciales de prueba (por ejemplo *admin/admin123*) y envíalas. Si la autenticación fue exitosa, tu frontend recibió un token JWT y lo guardó. Ahora la vista debería actualizarse para mostrar la interfaz de tareas (lista, formulario de nueva tarea, etc.). 
- Prueba crear, marcar y borrar tareas como antes. Todas esas peticiones ahora van con el token; deberían funcionar como antes si el token es válido. Si modificas el token manualmente o lo borras de `localStorage`, las peticiones volverán a fallar con 401/403. 

También puedes verificar el flujo vía herramientas externas: en **Postman** o **curl**, haz primero un POST a `/login` con las credenciales correctas y toma el token que recibes; luego intenta un GET a `/tasks` sin token (debe fallar) y luego con el header `Authorization: Bearer <tuToken>` (debe tener éxito). 

En caso de problemas:  
- Si el login falla, revisa que el usuario/contraseña enviados coincidan con los codificados en el backend. 
- Si el login funciona pero luego todas las peticiones siguen fallando, asegura que el token se está adjuntando correctamente en los headers. Observa en la pestaña Network del navegador si el request lleva la cabecera Authorization. 
- Si ves errores de CORS al hacer la petición `/login` desde el frontend, quizá necesites habilitar CORS en el backend Express (con el paquete `cors`). Copilot te puede ayudar si preguntas: *“¿Cómo habilito CORS en Express?”*. 

## 🧪 Validación 
Para dar por completada la actividad, verifica los siguientes puntos: 

1. **El endpoint `/login` funciona correctamente**: Cuando le envías las credenciales válidas, responde con un token JWT. Con credenciales inválidas, responde con un código de error (401 o 403) apropiado.  
2. **Las rutas de tareas requieren autenticación**: Si intentas acceder a cualquier ruta de tareas (GET/POST/PUT/DELETE `/tasks`) **sin** enviar el token, el servidor responde con **401 Unauthorized**. En cambio, al incluir un token válido en el header, la operación procede con normalidad.  
3. **El frontend tiene un flujo de login** visible y funcional: No permite acceder a la lista de tareas sin antes haber ingresado las credenciales. Después de login, la aplicación muestra y permite operar las tareas como antes, usando el token en cada petición.  
4. **Manejo de expiración**: Si quieres probar la expiración del token, puedes temporariamente reducir `expiresIn` a un valor corto (ej. `"10s"`) en el backend y recompilar. Inicia sesión y espera 10 segundos; el siguiente intento de acción debería fallar con 403, obligando a loguearte de nuevo. En un escenario real, implementaríamos un **refresh token** para renovar el acceso sin pedir credenciales tan frecuentemente, pero eso está fuera del alcance de este laboratorio.  

Si todas estas condiciones se cumplen, ¡felicidades! Tu API ahora está securizada. Si encuentras algún error, no dudes en consultar a Copilot Chat con el mensaje de error o una descripción del problema. Por ejemplo: *“El token no se adjunta correctamente, ¿qué podría estar mal?”*. Copilot puede darte pistas útiles. 

## 💡 Sugerencias de uso de Copilot Chat 
- *“¿Cómo implemento autenticación JWT en Express de manera segura?”* – Puedes pedir un resumen teórico o ejemplo de código; Copilot te recordará que debes verificar el token en cada solicitud y no exponer la clave secreta.  
- *“¿Cómo agrego el header Authorization en las peticiones HTTP desde Angular?”* – Útil si necesitas ayuda con HttpHeaders o interceptores en Angular.  
- *“¿Dónde debo guardar el JWT en el frontend?”* – Para discutir sobre **LocalStorage vs Cookies** y las implicaciones de seguridad de cada uno (por ejemplo, LocalStorage es vulnerable a XSS).  
- *“¿Cómo manejar tokens expirados y renovar el JWT automáticamente?”* – Si te interesa saber sobre **refresh tokens** y estrategias para mantener sesiones activas sin molestar al usuario. Copilot te puede explicar cómo funciona un flujo con `/refresh` usando cookies HttpOnly para el refresh token.  

## ✅ Resultado esperado 
Al completar esta actividad, deberías contar con: 

- 🔐 **Seguridad implementada** en tu API: solo usuarios autenticados (que tengan un JWT válido) pueden acceder a las rutas de tareas.  
- 🔑 **Endpoint de login** funcionando, que entrega un JWT al validar usuario y contraseña.  
- 🛡️ **Middleware de protección** en el backend que verifica el token en cada petición protegida.  
- 🤝 **Frontend actualizado** con una pantalla de login y envío del token en las peticiones subsecuentes.  
- 📖 **Experiencia** en el uso de Copilot para implementar características de seguridad. Vislumbraste cómo la IA puede acelerar tareas complejas como la autenticación, pero también aprendiste la importancia de entender y verificar cuidadosamente esas sugerencias en temas sensibles.  

## 🚀 Reflexión final 
Integrar autenticación y autorización es un paso crucial para llevar tu aplicación a un entorno real. En esta actividad, **aprendiste a combinar las sugerencias de Copilot con buenas prácticas de seguridad**, manteniendo el control sobre el código. Viste cómo Copilot puede generar rápidamente el esqueleto de un sistema de login JWT y ayudarte a propagar el uso del token en el cliente, pero también comprobaste que **como desarrollador debes revisar y ajustar** esas sugerencias para garantizar que no haya brechas de seguridad. 

Algunas lecciones clave: utiliza **tokens de corta duración** para minimizar riesgos, **almacena los tokens de forma segura** (idealmente en cookies HttpOnly para evitar accesos vía JavaScript malicioso), y nunca expongas tu **secreto JWT** en el cliente ni en repos públicos. Ten en cuenta que la autenticación robusta suele requerir más consideraciones (manejo de **refresh tokens** para una mejor UX, revocación de tokens, cifrado de datos sensibles, etc.), pero ahora tienes una base sólida sobre cómo proteger una API. 

Con la API de tareas autenticada y persistente, y un frontend dinámico, ¡tu proyecto de hackathon ha incorporado todos los elementos esenciales de una aplicación web segura y moderna! Mantén estos aprendizajes presentes en futuros desarrollos. **¡Excelente trabajo asegurando tu aplicación!** 🔒🚀 

