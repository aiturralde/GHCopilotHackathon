# 🚀 ¡Bienvenid@ a la Hackathon de **GitHub Copilot**! 

¡Nos alegra muchísimo tenerte aquí! Este repositorio es tu punto de partida para una aventura de código asistida por IA. **Aquí encontrarás una serie de actividades prácticas diseñadas para que aprendas, experimentes y te diviertas** mientras desarrollas una aplicación paso a paso con la ayuda de GitHub Copilot. Recuerda que un buen README como este te dará una clara visión del proyecto desde el principio, por eso hemos preparado una bienvenida cálida y un índice útil. **Nuestra hackathon es inclusiva y amigable:** no necesitas ser un desarrollador experto para participar – ¡cualquiera con ganas de aprender puede lograr cosas increíbles!. Lo importante es la curiosidad y la motivación por crear. 

¿Por qué hacemos esto? Porque creemos en el poder de la colaboración entre humanos e inteligencia artificial para llevar la programación al siguiente nivel. Esta hackathon tiene como objetivo que **descubras nuevas formas de desarrollar software apoyándote en IA**, y te sientas parte de algo más grande: una comunidad que innova y rompe barreras. Cada actividad te acercará más a dominar GitHub Copilot y entender **cómo puede potenciar tu flujo de trabajo**. La idea es aprender haciendo, sin miedo a equivocarse y con mucho entusiasmo. *Recuerda:* las hackathons no se tratan solo de competir, sino de **creatividad, aprendizaje y trabajo en equipo**. 

## 📋 Pre-requisitos  

Antes de sumergirte en las actividades, asegúrate de preparar tu entorno de desarrollo con los siguientes requisitos mínimos:  

- **Node.js** y **npm** instalados en tu sistema. Se recomienda utilizar una versión LTS reciente de Node.js (por ejemplo, Node 16.x o superior) para garantizar compatibilidad. Node.js y npm son imprescindibles para ejecutar el backend y las herramientas de frontend del laboratorio.  
- **Visual Studio Code** actualizado, con la **extensión de GitHub Copilot** instalada y configurada correctamente. Asegúrate de haber iniciado sesión en VS Code con tu cuenta de GitHub que tenga una suscripción activa a Copilot (o acceso de prueba). Si dispones de **Copilot Chat**, actívalo también para aprovechar sus capacidades durante el laboratorio. *(Copilot es compatible con varios IDE, pero VS Code es el recomendado en este hackathon.)*  
- **Conexión a internet** estable. GitHub Copilot funciona mediante servicios en la nube, por lo que necesitarás Internet para que pueda generar sugerencias de código.  
- **Repositorio del laboratorio** clonado o descargado en tu máquina local. Es decir, este mismo repositorio con las guías debe estar accesible en tu entorno. La forma recomendada es clonar el repositorio usando **Git**.
- *(Opcional)* Una herramienta para probar APIs REST, como **Postman**, **Insomnia** o el comando `curl`. Esto puede ser útil para verificar manualmente los endpoints de tu API durante el desarrollo, aunque no es estrictamente obligatorio ya que en la Actividad 3 contarás con una interfaz web para interactuar con el backend. 

Teniendo estos pre-requisitos listos, tendrás todo preparado para abordar las actividades del laboratorio sin contratiempos 😉.  

## 📚 Actividades del Laboratorio 

El laboratorio se compone de **6 actividades secuenciales** (⬇️ listadas abajo). Te recomendamos realizarlas en orden, ya que cada una construye sobre lo aprendido en la anterior. A continuación te ofrecemos un breve resumen de cada actividad con un enlace a su guía detallada, a modo de índice para que navegues fácilmente por el contenido. ¡Prepárate para codear con una sonrisa! 😃💻

1. **[Actividad 1: API Backend – Construyendo la base con Copilot](1-ConfigurarAPIBackend.md)** – Construirás un servidor **API REST** básico para gestionar tareas con Node.js/Express, usando GitHub Copilot para generar rápidamente la estructura CRUD del backend y sentar las bases de tu aplicación.  
2. **[Actividad 2: Nueva Característica – Autocompletado de Tareas tras 24 Horas](2-ExtenderBackened.md)** – Extenderás tu backend agregando lógica de negocio: una función que marca automáticamente como completadas las tareas creadas hace más de 24 horas. Aprenderás cómo Copilot puede ayudarte incluso con funcionalidades personalizadas más allá del código repetitivo.  
3. **[Actividad 3: Interfaz Frontend – Conectando el Backend con el Usuario](3-FrontEnd.md)** – Desarrollarás una interfaz web (puede ser **Angular** o **Next.js**, ¡tú eliges!) conectada a tu API de tareas. Aprovecharás Copilot para generar componentes de UI, formularios y llamadas HTTP de forma ágil, creando la conexión entre tu frontend y backend.  
4. **[Actividad 4: Pruebas y Refactorización – Asegurando la Calidad con Copilot](4-PruebasAutomaticas.md)** – Escribirás **pruebas automatizadas** para tu backend y luego **refactorizarás** el código para mejorar su calidad y mantenibilidad. Utilizarás Copilot (y si está disponible, su modo Agente en Copilot Chat) como asistente en tareas de QA, viendo cómo su apoyo facilita detectar mejoras y mantener un código limpio.  
5. **[Actividad 5: Persistencia – Guardando tareas con node-persist](5-Persistencia.md)** – Implementarás **persistencia de datos** en el backend usando la librería `node-persist`, de modo que las tareas se almacenen en disco y no se pierdan al reiniciar el servidor. Copilot te guiará en la integración de esta solución, refactorizando tu código para leer y escribir datos persistentes.  
6. **[Actividad 6: Autenticación y Seguridad – Protegiendo la API con JWT](6-Autenticacion.md)** – Añadirás **autenticación y autorización JWT** a tu API para proteger tus rutas. Configurarás un flujo de login que emite un token de seguridad (JSON Web Token) y ajustarás el frontend para enviar ese token en cada petición. Verás cómo Copilot puede asistir incluso en temas críticos de seguridad, ayudándote a implementar protección de endpoints y manejo de credenciales de forma correcta. 

> **Nota:** La actividad 6 es complementaria para llevar tu proyecto más allá, añadiendo seguridad robusta a tu app.

## 🎉 ¡A divertirse! 

Ya tienes todo lo que necesitas para empezar. Cada actividad es una pequeña misión con instrucciones paso a paso, consejos y sugerencias de Copilot Chat para sacarle el máximo provecho. Si te atascas, **no dudes en apoyarte en Copilot Chat o en tus compañeros** – preguntar y compartir es parte del proceso de aprendizaje. Al final de la hackathon, habrás construido una aplicación completa, tocando front-end, back-end, pruebas, persistencia y seguridad, todo con el acompañamiento de una IA. 

**¡Manos a la obra y mucha suerte!** Estamos emocionados por ver lo que crearás en este viaje. Recuerda: lo importante es **aprender y pasarla bien**. ¡Inspírate, codea y sobre todo, disfruta cada paso del camino! Te espera una experiencia de desarrollo única, y quién sabe, quizás al finalizar te sorprendas de lo mucho que has logrado 🚀😃. 

¡Happy hacking! 💻🎈
