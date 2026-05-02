Arquitectura y Desarrollo de SV.Services
SV.Services es una plataforma web moderna e integral diseñada para la gestión operativa y técnica de servicios. Está concebida como una aplicación de página única (SPA - Single Page Application) que consolida múltiples herramientas en una interfaz cohesiva y profesional.

A continuación, se detalla cómo está estructurado y desarrollado el sistema a nivel técnico:

1. Tecnologías Principales
El proyecto se desarrolla bajo el concepto de "Vanilla Web Development" (sin frameworks pesados de frontend como React o Angular), priorizando el rendimiento, la carga rápida y la simplicidad en el mantenimiento.

Estructura y Lógica Base: HTML5 y Vanilla JavaScript (ES6+).
Estilos (UI/UX): Vanilla CSS. Se emplea un robusto sistema de variables CSS (:root) para definir temas, colores, tipografías (como Bricolage Grotesque) y dimensiones (espaciados, radios de borde). Esto permite un diseño "Cyber-Pro" / moderno con soporte para temas oscuros (Dark Mode) y personalización de la marca (colores primarios ajustables).
Backend as a Service (BaaS): Firebase (v8 Compat). La plataforma utiliza Firebase como su núcleo de backend, integrando específicamente:
Firebase Authentication: Para el manejo de sesiones de usuario de forma segura.
Cloud Firestore: Como base de datos NoSQL en tiempo real, almacenando información de usuarios, tareas, notificaciones y configuraciones.
Firebase Storage: Para el almacenamiento de documentos, reportes o imágenes de la plataforma.
2. Arquitectura del Software
La aplicación sigue una arquitectura centralizada en un archivo principal (index.html), el cual contiene tanto la estructura DOM, como los estilos integrados y la lógica de negocio en JavaScript. Aunque está en un solo archivo, la lógica está modularizada internamente:

A. Capa de Interfaz de Usuario (Views/Renderers)
El sistema utiliza funciones de JavaScript para inyectar dinámicamente el contenido HTML en un contenedor principal (#mainContent). Las funciones principales de renderizado incluyen:

renderDash(): Panel de control (diferente según el rol del usuario).
renderTasks(): Gestión de servicios/tareas.
renderTechs() y renderClients(): Gestión de usuarios.
renderConfig(): Ajustes de la plataforma.
renderApprovals(): Flujo de solicitudes y aprobaciones.
B. Capa de Lógica y Estado
Gestión de Estado Local: Utiliza un objeto global API que mantiene en memoria las colecciones principales (configuraciones, usuarios, tareas, notificaciones).
Persistencia Local: Hace uso de localStorage (sv.services.config.v1) para guardar configuraciones visuales (como el color primario de la marca o los logos) de forma local, asegurando que la interfaz cargue rápidamente antes de sincronizar con la nube.
C. Sincronización en Tiempo Real
La plataforma implementa escuchadores en tiempo real (onSnapshot de Firestore) mediante la función setupRealtimeListeners(). Esto asegura que cualquier cambio en la base de datos (por ejemplo, cuando un técnico actualiza el estado de una tarea) se refleje inmediatamente en las pantallas de todos los usuarios conectados sin necesidad de recargar la página.

3. Control de Acceso Basado en Roles (RBAC)
El sistema soporta una lógica de roles bien definida para adaptar la interfaz y los permisos según el tipo de usuario (CU.role):

Administrador (admin): Tiene acceso total al sistema. Puede gestionar clientes, técnicos, asignar tareas, ver reportes financieros y modificar la configuración global.
Técnico (tech): Accede a "Mi Panel" y "Mis Tareas". Puede ver las tareas que tiene asignadas, cambiar su estado (En Progreso, Finalizado) y gestionar su propio flujo de trabajo, pero no tiene acceso a configuraciones globales o finanzas.
Cliente (client): Tiene una vista restringida donde solo puede observar los servicios contratados por su empresa ("Mis servicios"), ver el estado actual del servicio y realizar aprobaciones.
4. Estructura de Módulos (Características Principales)
Módulo de Autenticación: Interfaz de login con validación de credenciales a través de Firebase.
Dashboard (Panel Principal): Muestra métricas clave (estadísticas de tareas completadas, servicios activos, valor financiero) de forma visual.
Gestor de Tareas / Tablero Kanban: Permite visualizar los servicios en estados (Pendiente, En Progreso, Aprobación, Finalizado). Incluye barras de progreso, cálculo de prioridad y fechas estimadas.
Gestión de Usuarios: Mantenimiento (CRUD) completo de perfiles de Técnicos y Clientes (especialidades, datos de contacto, NIT de empresas, etc.).
Módulo de Notificaciones: Sistema integrado de alertas que informa a los usuarios sobre cambios en las tareas o solicitudes pendientes.
Configuración: Permite al administrador ajustar parámetros de la empresa, colores de la interfaz, información de contacto y enlaces a redes sociales.
5. Decisiones de Diseño y UX
El desarrollo puso un fuerte énfasis en la experiencia de usuario (UX):

Diseño Dinámico: Se aplican micro-interacciones, efectos hover, transiciones suaves, y "Glassmorphism" (efectos de desenfoque de fondo en modales y tarjetas) para dar un aspecto "Premium".
Responsividad: La aplicación utiliza Grid y Flexbox de forma intensiva, con "Media Queries" configuradas para asegurar que el sistema sea completamente funcional tanto en monitores grandes como en dispositivos móviles (el menú lateral se convierte en un menú tipo hamburguesa en pantallas pequeñas).
Sistema de Alertas (Toasts): Se implementó un sistema de notificaciones en pantalla no invasivo para informar al usuario sobre éxitos, errores o advertencias en sus acciones.
Resumen
SV.Services está desarrollado como una plataforma web ligera pero sumamente capaz. Al acoplar el stack de tecnologías web nativas (Vanilla JS/CSS) con el ecosistema de Firebase en el backend, el programa logra ser una herramienta en tiempo real, escalable y muy enfocada en ofrecer un entorno visual atractivo y fluido para el control operativo.
