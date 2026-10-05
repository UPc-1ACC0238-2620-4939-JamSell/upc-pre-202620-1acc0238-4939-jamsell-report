# Capítulo III: Solution UI/UX Design

## 3.1. Product Design

### 3.1.1. Style Guidelines

Esta sección establece las bases visuales de uso común para todo el equipo (branding, tipografía, colores, spacing e íconos), de modo que la aplicación móvil y el Landing Page mantengan una presentación consistente.

#### 3.1.1.1. General Style Guidelines

Las directrices de estilo general establecen los principios visuales que guían el desarrollo de Gethics Mobile, tanto en la aplicación móvil como en el Landing Page. El objetivo es transmitir una identidad confiable, técnica y cercana al trabajo de campo, que responda a las necesidades de ganaderos y veterinarios que gestionan información sanitaria de su ganado desde el celular, muchas veces en condiciones de baja conectividad.

El concepto visual parte del isotipo ya validado por el equipo: un toro en silueta sobre fondo granate, que asocia directamente la marca con el sector pecuario y con el nombre "Gethics" (genética + ética en el manejo del ganado). A partir de ahí, la paleta, la tipografía y los componentes de Gethics se mantienen deliberadamente acotados (pocos colores, una sola familia tipográfica, íconos de trazo simple) para que la aplicación se lea clara y profesional incluso en pantallas pequeñas y bajo el sol, condición habitual de uso en campo.

<div align="center">
  <img src="images/GethicsIcon.png" alt="Logo Gethics" width="200">
</div>

**Colores principales:**

| Código HEX | Color | Uso |
|---|---|---|
| #722A2E | <img src="images/3-1-1-1-color-722A2E.png" alt="722A2E" width="50px"> | Color primario — botones principales, elementos de énfasis (fecha seleccionada, barra de progreso, textos destacados) |
| #1E1E1E | <img src="images/3-1-1-1-color-1E1E1E.png" alt="1E1E1E" width="50px"> | Texto principal — títulos y contenido de mayor jerarquía |
| #FFFFFF | <img src="images/3-1-1-1-color-FFFFFF.png" alt="FFFFFF" width="50px"> | Fondo principal de pantallas y tarjetas |

**Colores secundarios:**

| Código HEX | Color | Uso |
|---|---|---|
| #444444 | <img src="images/3-1-1-1-color-444444.png" alt="444444" width="50px"> | Texto secundario — subtítulos, labels y metadatos |
| #E8F3E8 | <img src="images/3-1-1-1-color-E8F3E8.png" alt="E8F3E8" width="50px"> | Superficie neutra — fondos de chips e íconos circulares |
| #E4CBB4 | <img src="images/3-1-1-1-color-E4CBB4.png" alt="E4CBB4" width="50px"> | Acento cálido — badges de estado positivo (p. ej. "Saludable") |

**Colores de estado:**

| Código HEX | Color | Uso |
|---|---|---|
| #FFF4E0 | <img src="images/3-1-1-1-color-FFF4E0.png" alt="FFF4E0" width="50px"> | Fondo de alertas y urgencias (badge "Urgente", notificaciones del sensor) |
| #BB7B1C | <img src="images/3-1-1-1-color-BB7B1C.png" alt="BB7B1C" width="50px"> | Texto/ícono sobre alertas y urgencias |

Gethics no utiliza un color de "éxito" o "error" saturados independientes: el granate se reutiliza como color de énfasis en toda la interfaz y el ámbar cubre exclusivamente alertas y urgencias. Esto mantiene la paleta reducida y consistente con los mock-ups ya construidos por el equipo para la aplicación móvil, en vez de introducir tonos adicionales.

**Typography:**

La tipografía utilizada es **Roboto**, confirmada directamente en los nodos de texto de los mock-ups de Mateo en Figma (peso Medium para títulos y botones, Regular para texto de cuerpo). Es una sans-serif neutra y de alta legibilidad en pantallas pequeñas, apropiada para una app que se consulta rápido y muchas veces al aire libre, con el ganado por delante. Se usa una sola familia en distintos pesos para toda la interfaz (no se introduce una segunda tipografía para títulos), lo que simplifica la lectura y refuerza la coherencia visual entre el Landing Page y la aplicación móvil.

<div align="center">
  <p>
    <b>Gráfico</b>: Pesos de Roboto utilizados en Gethics
  </p>
  <img src="images/3-1-1-1-typography-roboto.png" alt="Roboto" width="500">
  <p>
    <i><b>Fuente</b>: Elaboración propia, a partir de los text styles verificados en el Figma del equipo.</i>
  </p>
</div>

**Icons:**

Gethics utiliza un set de íconos de línea simple, de trazo uniforme y esquinas redondeadas (en la línea de **Lucide Icons**), consistente con los íconos ya presentes en los mock-ups del equipo: la navegación inferior (Inicio, Inventario, Tareas, Perfil), las notificaciones y los íconos de evento dentro de la ficha de salud del animal. Este estilo minimalista refuerza la lectura rápida de la interfaz y evita la sobrecarga visual en pantallas pequeñas.

<div align="center">
  <p>
    <b>Gráfico</b>: Íconos utilizados en los mock-ups de Gethics
  </p>
  <img src="images/3-1-1-1-icons-reference.png" alt="Iconos Gethics" width="600">
  <p>
    <i><b>Fuente</b>: Capturas de los mock-ups del equipo (Figma).</i>
  </p>
</div>

**Tono de comunicación:**

El tono de Gethics es serio, respetuoso y directo, con un nivel de formalidad intermedio. El producto maneja información sanitaria del ganado, por lo que el lenguaje evita el humor o la informalidad excesiva que podría restarle seriedad al contenido, pero tampoco recurre a tecnicismos innecesarios: busca que tanto el ganadero como el veterinario entiendan de inmediato qué está pasando con el animal y qué acción deben tomar. La redacción prioriza etiquetas breves y accionables ("Registrar Tratamiento", "Ver todo", "Guardar Registro") por sobre textos largos, y reserva un tono más sereno para el uso diario, con momentos puntuales de mayor claridad visual (colores y badges) cuando una situación requiere atención prioritaria.

**Spacing:**

El espaciado sigue una base de 8px (8 · 16 · 24 · 32 · 48px), visible en los mock-ups en la separación entre tarjetas, el padding interno de los chips de estado y los márgenes entre secciones de la ficha del animal. En pantallas pequeñas esto permite agrupar la información en bloques claramente separados (datos generales, signos vitales, chequeos recientes) sin saturar la vista, priorizando que el usuario pueda escanear la pantalla rápido mientras trabaja en campo.

---

## 3.1.2. Information Architecture

Gethics está pensada para usarse desde el celular durante el trabajo diario con el ganado, así que su arquitectura de información se diseñó alrededor de una idea: que el ganadero llegue rápido a lo que necesita, con la menor cantidad de pasos posible. Por eso la estructura se organiza según las tareas que los pequeños y medianos ganaderos realizan con más frecuencia: revisar el estado general del hato, buscar un animal, registrar información nueva, dar seguimiento sanitario, consultar vacunas y controlar las actividades pendientes.

Para lograrlo se optó por una estructura jerárquica y orientada a tareas. Desde la navegación principal el usuario entra a cuatro módulos (**Inicio**, **Inventario**, **Tareas** y **Perfil**) y, a partir de ellos, se despliegan niveles secundarios según lo que quiera hacer en ese momento. Esta decisión evita mostrar todas las funciones a la vez en una pantalla pequeña y mantiene cada módulo enfocado en un solo tipo de actividad.

Entre pantallas se conservan los mismos elementos de navegación, etiquetas cortas y acciones principales visibles. La consistencia tiene un propósito práctico: el usuario aprende una sola vez cómo moverse por la aplicación y no tiene que volver a buscar dónde está cada función, algo clave cuando la usa en medio de otras labores.

---

### 3.1.2.1. Organization Systems

Gethics utiliza un sistema de organización **jerárquico y orientado a tareas**. En lugar de agrupar la información por tipo de dato (por ejemplo, todas las tablas juntas), se agrupa según la actividad que el usuario viene a realizar. Así, quien quiere revisar una vacuna no necesita saber en qué parte del sistema se guarda ese dato: entra al animal y la encuentra dentro de su ficha.

La navegación de primer nivel está compuesta por cuatro módulos:

- **Inicio:** resume el estado del ganado, muestra los indicadores relevantes y las alertas recientes. Es el punto de entrada, pensado para que el usuario tenga una visión general del hato antes de pasar a un módulo especializado.
- **Inventario:** concentra el registro y la consulta de los animales del hato.
- **Tareas:** organiza las actividades sanitarias, los controles y los eventos programados a través de un calendario.
- **Perfil:** reúne lo relacionado con la cuenta, el personal, los reportes y la configuración.

Cada módulo tiene su propia organización secundaria, definida por el contexto de uso.

**Inventario** presenta los animales como una lista de registros individuales. Cada elemento muestra solo lo necesario para identificarlo de un vistazo (número de arete, raza, peso y estado sanitario) y, al seleccionarlo, se accede a su ficha detallada. De esta forma la lista sirve para ubicar rápido al animal y la ficha para profundizar, sin mezclar ambos propósitos en una misma pantalla.

La ficha individual divide la información en tres categorías:

- **Información:** datos generales del animal.
- **Salud:** signos vitales, controles, tratamientos y eventos sanitarios.
- **Vacunas:** historial de vacunación y desparasitación.

Separar **Salud** y **Vacunas** responde a que se consultan con propósitos distintos: una describe el estado clínico y los eventos del animal, y la otra funciona como un historial preventivo que el ganadero revisa para saber qué le corresponde aplicar.

**Tareas** organiza las actividades por fecha y prioridad. El usuario selecciona un día en el calendario, ve las tareas de esa fecha y puede distinguir cuáles están pendientes, cuáles son próximas y cuáles están marcadas como urgentes. El calendario funciona como eje de la sección porque la mayoría de estas actividades dependen de cuándo deben realizarse.

La estructura completa de la aplicación se representa de la siguiente manera:

```text
Gethics
│
├── Autenticación
│   ├── Iniciar sesión
│   └── Crear cuenta
│
├── Inicio
│   ├── Salud general del hato
│   ├── Total de ganado
│   ├── Animales sanos
│   ├── Animales enfermos
│   ├── Animales en gestación
│   └── Alertas recientes
│
├── Inventario
│   ├── Buscar animales
│   ├── Listado de animales
│   ├── Registrar nueva res
│   └── Detalle del animal
│       ├── Información
│       ├── Salud
│       └── Vacunas
│
├── Tareas
│   ├── Calendario de salud
│   ├── Próximas tareas
│   └── Estado de actividades
│
└── Perfil
    ├── Editar perfil
    ├── Gestionar personal
    ├── Exportar reportes
    ├── Soporte
    └── Cerrar sesión
```

Como se observa en el diagrama, **Autenticación** es la puerta de entrada a la aplicación y no forma parte de la navegación principal. Una vez iniciada la sesión, el usuario se mueve entre los cuatro módulos y el punto más profundo de la estructura es la ficha del animal, a tres niveles de la navegación principal. Mantener la jerarquía poco profunda es una consecuencia directa del enfoque de la aplicación: reducir los pasos entre la intención del usuario y la información que busca. A cambio, funciones como la gestión de personal o la exportación de reportes quedan agrupadas dentro de **Perfil**, en un segundo plano respecto a las tareas de campo.

---

#### 3.1.2.2. Labelling Systems

El sistema de etiquetado de **Gethics** busca facilitar la comprensión de las funcionalidades mediante términos breves, descriptivos y relacionados con las actividades habituales de los usuarios del sector ganadero.

Las etiquetas utilizadas en la aplicación evitan términos técnicos innecesarios y priorizan palabras que permitan al usuario reconocer rápidamente qué información encontrará o qué acción realizará al seleccionar cada elemento.

La navegación principal utiliza cuatro etiquetas consistentes en las diferentes pantallas:

- **Inicio:** permite acceder al resumen general del estado del hato, indicadores y alertas recientes.
- **Inventario:** permite consultar, buscar y registrar animales.
- **Tareas:** permite consultar actividades y eventos programados dentro del calendario de salud.
- **Perfil:** permite gestionar la información personal, configuración y otras opciones relacionadas con la cuenta.

Además de las etiquetas de navegación principal, cada módulo utiliza términos específicos según su contexto.

| Etiqueta | Propósito |
|---|---|
| `Inicia sesión` | Identifica el proceso de acceso para usuarios registrados. |
| `Crear Cuenta` | Inicia el proceso de registro de un nuevo usuario. |
| `Ingresar` | Confirma las credenciales ingresadas y permite acceder a la aplicación. |
| `Registrarse` | Confirma la creación de una nueva cuenta. |
| `Inventario de Ganado` | Identifica el módulo donde se encuentran los animales registrados. |
| `Registrar Nueva Res` | Permite registrar un nuevo animal en el inventario. |
| `Número de Arete (Tag)` | Identifica al animal mediante su código o número de arete. |
| `Información` | Muestra los datos generales del animal seleccionado. |
| `Salud` | Agrupa signos vitales, controles, tratamientos y eventos sanitarios. |
| `Vacunas` | Presenta el historial de vacunación y desparasitación del animal. |
| `Registrar Tratamiento` | Permite añadir un nuevo tratamiento al historial sanitario. |
| `Calendario de Salud` | Organiza las actividades sanitarias y tareas programadas por fecha. |
| `Próximas Tareas` | Presenta las actividades pendientes próximas a realizarse. |
| `Alertas Recientes` | Muestra situaciones recientes que requieren la atención del usuario. |
| `Guardar Registro` | Confirma el almacenamiento de la información registrada. |
| `Editar Perfil` | Permite modificar los datos personales y de contacto. |
| `Gestionar Personal` | Permite administrar trabajadores, veterinarios y permisos asociados. |
| `Exportar Reportes de Salud` | Permite generar reportes relacionados con el estado del ganado. |
| `Soporte` | Permite acceder a opciones de ayuda y contacto con Gethics. |
| `Cerrar Sesión` | Finaliza la sesión activa del usuario. |

Gethics también utiliza etiquetas de estado para facilitar la interpretación rápida de la información. Estas etiquetas aparecen acompañadas de recursos visuales como colores e iconos para reforzar su significado.

Entre los principales estados utilizados se encuentran:

- **Sano:** indica que el animal no presenta incidencias sanitarias relevantes.
- **Enfermo:** indica la existencia de una condición que requiere atención.
- **Gestación:** identifica a los animales que se encuentran en periodo de gestación.
- **Saludable:** comunica un estado general favorable en la ficha individual del animal.
- **Urgente:** identifica actividades que requieren atención prioritaria.
- **En observación:** señala situaciones que necesitan seguimiento.
- **Aplicado:** indica que un tratamiento, vacuna o procedimiento ya fue realizado.

Para los animales se utiliza principalmente el **Número de Arete (Tag)** como identificador visible, debido a que permite relacionar la información digital con el identificador utilizado en el manejo del ganado.

Por ejemplo:

`Tag ID #8493`

Este formato permite que el usuario pueda reconocer rápidamente al animal tanto en el inventario como en su ficha individual.

En las acciones se utilizan principalmente verbos que indican claramente lo que ocurrirá al seleccionar una opción, como:

- `Registrar`
- `Guardar`
- `Editar`
- `Gestionar`
- `Exportar`
- `Ver todas`
- `Cerrar sesión`

El sistema de etiquetado mantiene consistencia entre las distintas pantallas para evitar que una misma funcionalidad sea representada con nombres diferentes. De esta manera, Gethics busca reducir la carga cognitiva del usuario y facilitar el aprendizaje progresivo de la aplicación.

---

#### 3.1.2.3. SEO Tags and Meta Tags

Las estrategias de **SEO Tags and Meta Tags** de Gethics se aplican principalmente a la **Landing Page**, debido a que las pantallas internas de la aplicación móvil no son indexadas directamente por los motores de búsqueda.

El objetivo de estas etiquetas es mejorar la identificación del producto en buscadores, describir correctamente el contenido de la página y optimizar la forma en que Gethics se presenta cuando el enlace es compartido en redes sociales o aplicaciones de mensajería.

Para la Landing Page se consideran las siguientes etiquetas principales:

```html
<title>Gethics | Gestión inteligente de ganado</title>

<meta
  name="description"
  content="Gethics es una aplicación móvil para pequeños y medianos ganaderos que permite gestionar animales, controlar eventos sanitarios, vacunas, tareas y reportes desde un solo lugar."
/>

<meta
  name="keywords"
  content="Gethics, gestión ganadera, ganado, aplicación ganadera, control de ganado, salud animal, gestión veterinaria, vacunas ganado, inventario ganadero"
/>

<meta name="author" content="JamSell" />

<meta name="robots" content="index, follow" />
```

---

#### 3.1.2.4. Searching Systems

El sistema de búsqueda de **Gethics** está diseñado para facilitar la localización rápida de animales registrados dentro del inventario.

La principal funcionalidad de búsqueda se encuentra en el módulo **Inventario de Ganado**, donde el usuario dispone de una barra de búsqueda con el texto:

`Buscar por arete o raza`

A partir de esta barra, el usuario puede localizar animales utilizando información directamente relacionada con su identificación dentro del sistema.

Los criterios de búsqueda visibles en el diseño son:

- Número de arete o Tag.
- Raza del animal.

Cada resultado del inventario se presenta mediante una tarjeta que resume la información principal del animal, permitiendo reconocerlo antes de ingresar a su ficha detallada.

La información mostrada en cada resultado incluye:

- Número de arete.
- Raza.
- Peso.
- Estado sanitario.
- Representación visual del animal.

El flujo principal de búsqueda puede representarse de la siguiente manera:

```text
Inventario
    ↓
Barra de búsqueda
    ↓
Ingresar número de arete o raza
    ↓
Mostrar registros coincidentes
    ↓
Seleccionar animal
    ↓
Ficha individual del animal
```

#### 3.1.2.5. Navigation Systems

El sistema de navegación de **Gethics** está diseñado para permitir que el usuario acceda de manera rápida y clara a las principales funcionalidades de la aplicación móvil.

La navegación principal se realiza mediante una barra inferior que agrupa los módulos principales visibles en la interfaz:

- `Inicio`
- `Inventario`
- `Tareas`
- `Perfil`

Esta barra permite al usuario cambiar entre las secciones principales de la aplicación sin necesidad de regresar constantemente a una pantalla inicial.

La opción seleccionada se diferencia visualmente del resto, permitiendo que el usuario identifique en qué módulo se encuentra actualmente.

#### Navegación principal

La estructura principal de navegación puede representarse de la siguiente manera:

```text
Inicio
  │
  ├── Inventario
  │
  ├── Tareas
  │
  └── Perfil
```

---

### 3.1.3. Landing Page UI Design

El Landing Page de Gethics traduce directamente las decisiones tomadas en Information Architecture y en los Style Guidelines: su navegación principal refleja los mismos cuatro conceptos de valor que organizan la aplicación (salud, registro, alertas y reportes), su etiquetado evita tecnicismos siguiendo el mismo sistema de labeling, y su jerarquía visual se apoya en los mismos principios de diseño: pocos colores, tipografía única, componentes simples definidos para toda la marca. A diferencia de la aplicación móvil, el Landing Page no requiere autenticación ni muestra datos reales del hato: su objetivo es comunicar la propuesta de valor del producto y convertir visitantes en usuarios, por lo que su arquitectura prioriza la narrativa (qué hace Gethics, para quién, por qué confiar en él) sobre la operación diaria. El sitio está desplegado en [gethics-landing-page.vercel.app](https://gethics-landing-page.vercel.app).

#### 3.1.3.1. Landing Page Wireframe

El wireframe del Landing Page se construyó en baja fidelidad (escala de grises, sin tipografía ni color final) para validar primero la estructura y jerarquía del contenido, antes de pasar al Mock-up con el Design System ya aplicado. Se presenta en dos versiones: Desktop Web Browser y Mobile Web Browser, ya que el Landing Page debe adaptarse correctamente a ambos tamaños de pantalla.

La estructura sigue un orden narrativo de arriba hacia abajo, alineado a la arquitectura de información ya definida:

- **Header/Nav:** logo y accesos directos a las secciones de la misma página (Vista previa, Para quién, Características, Cómo funciona, Modelo, Equipo), más el CTA principal "Descargar app". En mobile se colapsa a un menú hamburguesa para no saturar el ancho disponible.
- **Hero:** presenta la propuesta de valor con el mismo copy ya usado como tagline de la app ("Salud y manejo de tu ganado, en un solo lugar"), dos CTAs (acción primaria y secundaria) y tres cifras de respaldo (offline, monitoreo, roles de usuario), reforzando desde el primer scroll los diferenciales encontrados en la investigación de usuarios (trabajo sin conexión, seguimiento continuo).
- **Showcase:** tres pantallas ilustradas de la app (Inventario, Calendario de salud, Alertas) en formato mini-teléfono, para que un visitante entienda de un vistazo cómo se usa Gethics en el día a día, sin necesidad de descargarla primero.
- **Cifras de respaldo:** una franja con cuatro cifras provenientes directamente de la investigación de usuarios (porcentaje que hoy trabaja con cuaderno, tamaño promedio del hato entrevistado, módulos clave de la app, estudiantes detrás del proyecto), como transición entre el Showcase y los segmentos de usuario.
- **Para quién es Gethics:** dos perfiles de usuario, Ganaderos y Veterinarios/técnicos agropecuarios, cada uno con una fotografía de campo, un ícono y una lista de necesidades cubiertas, trasladando directamente los segmentos identificados en la investigación de usuarios a la narrativa del Landing Page.
- **Validado en campo:** tres citas atribuidas por rol (no por nombre, ya que corresponden a apreciaciones generales recogidas en las entrevistas de validación y no a citas textuales de un entrevistado específico), seguidas de un bloque comparativo "Hoy, sin Gethics" / "Con Gethics" que contrasta los problemas detectados en campo con la solución que propone la app.
- **Funcionalidades:** una grilla de 6 tarjetas que traduce directamente los módulos de la Information Architecture (Inventario, Calendario de Salud, Vacunas, Alertas, Offline, Reportes) a beneficios explicados en una línea, para que un visitante sin conocimiento técnico entienda qué hace la app sin leer todo el contenido.
- **Cómo funciona:** un flujo de 4 pasos conectados visualmente, que reduce la percepción de complejidad de adoptar una herramienta nueva —un criterio de diseño inclusivo pensado para usuarios con poca experiencia tecnológica, el mismo perfil identificado en la investigación de segmentos.
- **Modelo de negocio:** dos tarjetas (Para tu hato / Para instituciones) que describen el modelo real de monetización —suscripción ajustada al tamaño del hato y licencias institucionales— en vez de precios fijos inventados.
- **Equipo:** fotografías y nombres de los cinco integrantes del equipo responsable del proyecto, reforzando la transparencia sobre quién está detrás de Gethics.
- **CTA final y Footer:** cierre de conversión y enlaces de soporte, legales y de producto, consistentes con lo que un visitante espera encontrar al final de cualquier landing page.

En cuanto a diseño inclusivo, el wireframe privilegia bloques de alto contraste, etiquetas cortas y una sola columna en mobile (sin elementos uno al lado del otro que obliguen a hacer zoom), pensando en usuarios de campo que acceden desde el celular y, en muchos casos, con conexión limitada; el mismo criterio que fundamenta el modo offline de la aplicación.

<div align="center">
  <p><b>Gráfico</b>: Landing Page Wireframe — Desktop Web Browser</p>
  <img src="images/3-1-3-1-wireframe-desktop.png" alt="Wireframe Desktop Gethics" width="700">
  <p><i><b>Fuente</b>: Elaboración propia.</i></p>
</div>

<div align="center">
  <p><b>Gráfico</b>: Landing Page Wireframe — Mobile Web Browser</p>
  <img src="images/3-1-3-1-wireframe-mobile.png" alt="Wireframe Mobile Gethics" width="260">
  <p><i><b>Fuente</b>: Elaboración propia.</i></p>
</div>

#### 3.1.3.2. Landing Page Mock-up

El Mock-up del Landing Page aplica el Design System definido en los Style Guidelines sobre la estructura ya validada en el wireframe, extendiéndola con fotografía real, mayor peso tipográfico y componentes con profundidad (sombras y capas) que refuerzan la sensación de producto terminado y comercial, sin alterar el orden ni la jerarquía narrativa definidos en el wireframe.

- **Color:** el granate (#722A2E) se mantiene como color de énfasis en CTAs, números de paso, cifras de respaldo y los elementos destacados del Modelo de negocio, replicando su uso como color primario en la aplicación móvil. Se añade un tono gris cálido (#EFEDEA) como fondo de las tarjetas de testimonios, en lugar del verde usado originalmente, para que la fotografía de las personas destaque sin competir con el color de marca. Para el fondo general de la página se mantiene el tono casi blanco derivado del acento, #FBF4EC ("crema"), sobre el cual flota la tarjeta blanca del Hero; este tono no estaba documentado en los Style Guidelines originales (3.1.1.1) y se añade aquí como una variación tonal, no un color nuevo de marca. La tarjeta flotante "3 animales requieren atención" reutiliza el color de alerta (#FFF4E0 / #BB7B1C) definido para notificaciones, reforzando que el mismo lenguaje visual de la app ya anticipa, desde el Landing Page, el tipo de valor que el producto entrega.
- **Fotografía real:** el Hero usa como fondo a pantalla completa una fotografía de ganado en campo abierto, que se extiende detrás del header —el header pasa a transparente con texto blanco mientras el visitante está en la parte superior de la página, y adopta fondo sólido y texto oscuro apenas se hace scroll—. La misma fotografía real se usa en las tarjetas de los segmentos (Ganaderos / Veterinarios) y en los tres testimonios, donde los íconos genéricos se reemplazaron por fotografías representativas de cada rol (ganadero, veterinario, técnico agropecuario) dentro de un avatar circular. El equipo del proyecto también se presenta con fotografías reales de sus cinco integrantes en vez de iniciales o avatares genéricos.
- **Tipografía:** Roboto, con un salto de peso más marcado que en la versión anterior del mock-up: los títulos principales (H1 del Hero, H2 de cada sección) pasan a peso 900 (Black) y tamaños mayores, mientras el cuerpo de texto se mantiene en Regular/Medium, acentuando el contraste entre título contundente y texto explicativo, típico de un sitio comercial.
- **Iconografía:** íconos de trazo simple, en línea con el estilo Lucide definido para la app, aplicados a las tarjetas de Funcionalidades, Segmentos y Modelo de negocio, y a los indicadores de check/equis del bloque comparativo.
- **Componentes:** botones, tarjetas y badges mantienen el radio de esquina (18–32px) y la sombra suave de tono granate definidos previamente. Se suman dos componentes nuevos: el bloque **Showcase**, con tres mini-mockups de teléfono ilustrando pantallas reales de la app (Inventario, Calendario, Alertas), y el bloque comparativo **"Hoy sin Gethics" / "Con Gethics"**, construido como tarjetas con efecto 3D de "papeles apilados" (capas detrás de cada tarjeta, ligeramente rotadas) que se inclinan al pasar el cursor.

El bloque "Mockup de la app (pantalla real)" dentro del Hero queda como marcador de posición: es una ilustración de la interfaz, marcada explícitamente como tal en el texto alternativo de la imagen, y se reemplazará por una captura real una vez que los mock-ups de pantallas móviles estén terminados.

**Nota sobre el contenido de Testimonios:** la sección "Validado en campo" muestra los problemas concretos que los ganaderos y veterinarios describieron en las entrevistas exploratorias (cuadernos, doble digitación, historial no disponible en campo), atribuidos por rol y no por nombre, ya que las entrevistas de validación todavía no se han ejecutado. Las fotografías usadas en estos testimonios y en los segmentos de usuario son fotografías de stock representativas del rol (ganadero, veterinario, técnico), no de los entrevistados reales; se incorporaron por decisión del equipo para que el sitio luzca más cercano a un producto comercial terminado.

<div align="center">
  <p><b>Gráfico</b>: Landing Page Mock-up — Desktop Web Browser</p>
  <img src="images/3-1-3-2-mockup-desktop.png" alt="Mock-up Desktop Gethics" width="700">
  <p><i><b>Fuente</b>: Elaboración propia.</i></p>
</div>

<div align="center">
  <p><b>Gráfico</b>: Landing Page Mock-up — Mobile Web Browser</p>
  <img src="images/3-1-3-2-mockup-mobile.png" alt="Mock-up Mobile Gethics" width="260">
  <p><i><b>Fuente</b>: Elaboración propia.</i></p>
</div>

---


### 3.1.4. Mobile Applications UX/UI Design

Esta sección documenta el diseño de la aplicación móvil de Gethics, desde la estructura de baja fidelidad hasta el prototipo navegable. El proceso siguió una progresión deliberada, primero se definió la estructura de cada pantalla (wireframes), luego cómo se conectan entre sí (wireflows), después se aplicó el Design System de la sección 3.1.1 (mock-ups), se validaron los recorridos completos de cada tipo de usuario (user flows) y finalmente se construyó un prototipo interactivo para probar la experiencia antes de pasar al desarrollo.

Todas las decisiones parten de lo definido en Information Architecture: cuatro módulos en la navegación inferior (Inicio, Inventario, Tareas y Perfil), una jerarquía poco profunda cuyo punto más hondo es la ficha del animal, y acciones principales siempre visibles. Se diseñó para pantallas pequeñas, uso con una mano y condiciones de campo, tal como lo evidenció la investigación con ganaderos y veterinarios.

#### 3.1.4.1. Mobile Applications Wireframes

Los wireframes se elaboraron en baja fidelidad (escala de grises, sin color ni imágenes finales) para validar la estructura y jerarquía de cada pantalla antes de invertir tiempo en el acabado visual. En esta etapa interesa responder tres preguntas: qué información aparece, en qué orden y dónde está la acción principal.

<div align="center">
<img src="images/mobile-wireframe-01.png" alt="Mobile Wireframe 1" width="700">
</div>

<div align="center">
<img src="images/mobile-wireframe-02.png" alt="Mobile Wireframe 2" width="700">
</div>

<div align="center">
<img src="images/mobile-wireframe-03.png" alt="Mobile Wireframe 3" width="700">
</div>

<div align="center">
<img src="images/mobile-wireframe-04.png" alt="Mobile Wireframe 4" width="700">
</div>

<div align="center">
<img src="images/mobile-wireframe-05.png" alt="Mobile Wireframe 5" width="700">
</div>

<div align="center">
<img src="images/mobile-wireframe-06.png" alt="Mobile Wireframe 6" width="700">
</div>

<div align="center">
<img src="images/mobile-wireframe-07.png" alt="Mobile Wireframe 7" width="700">
</div>

<div align="center">
<img src="images/mobile-wireframe-08.png" alt="Mobile Wireframe 8" width="700">
  <p><i><b>Fuente</b>: Elaboración propia.</i></p>
</div>

Link de los Mobile Applications Wireframes: https://www.figma.com/design/ge1sEWNd24ywwpYcSb3bRX/GETHICS-%E2%80%94-Mobile-UX-UI?node-id=1-3&t=ef2OCrXj7Nzp0ImN-1
#### 3.1.4.2. Mobile Applications Wireflow Diagrams

Se elaboraron wireflows para las tareas más frecuentes identificadas en la User Task Matrix:

1. Registro de un animal: Inventario → botón "Registrar nueva res" → formulario → confirmación → regreso al listado con el animal ya agregado.

2. Consulta del historial de un animal: Inventario → búsqueda o selección en la lista → ficha del animal → pestaña Salud o Vacunas.

3. Revisión de tareas sanitarias: Tareas → selección de fecha en el calendario → lista de actividades del día → detalle o registro de tratamiento.

<div align="center">
<img src="images/wireflow01.png" alt="Wireflow 01" width="700">
</div>

<div align="center">
<img src="images/wireflow02.png" alt="Wireflow 02" width="700">
</div>

<div align="center">
<img src="images/wireflow03.png" alt="Wireflow 03" width="700">
</div>

<div align="center">
<img src="images/wireflow04.png" alt="Wireflow 04" width="700">
</div>

<div align="center">
<img src="images/wireflow05.png" alt="Wireflow 05" width="700">
</div>

<div align="center">
<img src="images/wireflow06.png" alt="Wireflow 06" width="700">
</div>

<div align="center">
<img src="images/wireflow07.png" alt="Wireflow 07" width="700">
</div>

<div align="center">
<img src="images/wireflow08.png" alt="Wireflow 08" width="700">
</div>

<div align="center">
<img src="images/wireflow09.png" alt="Wireflow 09" width="700">
</div>

<div align="center">
<img src="images/wireflow10.png" alt="Wireflow 10" width="700">
</div>

<div align="center">
<img src="images/wireflow11.png" alt="Wireflow 11" width="700">
</div>

<div align="center">
<img src="images/wireflow12.png" alt="Wireflow 12" width="700">
</div>

<div align="center">
<img src="images/wireflow13.png" alt="Wireflow 13" width="700">
</div>

<div align="center">
<img src="images/wireflow14.png" alt="Wireflow 14" width="700">
</div>

<div align="center">
<img src="images/wireflow15.png" alt="Wireflow 15" width="700">
  <p><i><b>Fuente</b>: Elaboración propia.</i></p>
</div>

Link de los Mobile Applications Wireflow Diagrams: https://www.figma.com/design/ge1sEWNd24ywwpYcSb3bRX/GETHICS-%E2%80%94-Mobile-UX-UI?node-id=1-3&t=ef2OCrXj7Nzp0ImN-1

### 3.1.4.3. Mobile Applications Mock-ups

A continuación se presentan los mock-ups de la aplicación móvil de Gethics, diseñados para el uso en campo por ganaderos y veterinarios. Las pantallas mantienen la identidad visual de la marca (vino, verde menta y beige) y una barra de navegación inferior con las secciones Inicio, Inventario, Tareas y Perfil.

**Figura 1.** Pantalla de inicio de sesión: el usuario ingresa su correo y contraseña, y tiene accesos a "¿Olvidaste tu contraseña?" y al registro.

<img src="images/mock1.png" alt="Mock-up de inicio de sesión" width="200">

**Figura 2.** Pantalla de creación de cuenta: formulario con nombre completo, nombre del fundo o granja, correo electrónico y contraseña (mínimo 8 caracteres).

<img src="images/mock2.png" alt="Mock-up de crear cuenta" width="200">

**Figura 3.** Pantalla de inicio (dashboard): resumen de la salud general de la finca, indicadores del hato (total de ganado, sanos, enfermos y en gestación) y lista de alertas recientes.

<img src="images/mock3.png" alt="Mock-up de pantalla de inicio" width="200">

**Figura 4.** Inventario de ganado: lista de animales con su arete, raza, peso y estado de salud (sano o enfermo), con búsqueda por arete o raza, filtros y botón para registrar un nuevo animal.

<img src="images/mock4.png" alt="Mock-up de inventario de ganado" width="200">

**Figura 5.** Registro de nueva res: formulario con número de arete, raza, fecha de nacimiento, peso inicial y foto del animal.

<img src="images/mock6.png" alt="Mock-up de registrar nueva res" width="200">

**Figura 6.** Detalle del animal, pestaña "Información": datos generales del animal (raza, edad, género, nacimiento, peso, ubicación y dieta).

<img src="images/mock10.png" alt="Mock-up de detalle del animal - Información" width="200">

**Figura 7.** Detalle del animal, pestaña "Salud": signos vitales en tiempo real (frecuencia cardíaca, temperatura y respiración) con gráfico de 24 horas, historial de chequeos recientes y botón para registrar un tratamiento.

<img src="images/mock5.png" alt="Mock-up de detalle del animal - Salud" width="200">

**Figura 8.** Detalle del animal, pestaña "Vacunas": historial de vacunación y desparasitación, con la próxima aplicación programada y el estado de cada registro.

<img src="images/mock9.png" alt="Mock-up de detalle del animal - Vacunas" width="200">

**Figura 9.** Calendario de salud: selector de fecha, progreso diario y lista de tareas sanitarias programadas (chequeos, vacunas y tratamientos), con marca de tarea completada y etiqueta de urgencia.

<img src="images/mock7.png" alt="Mock-up de calendario de salud" width="200">

**Figura 10.** Perfil de usuario: datos del usuario y su rol, opciones de configuración (editar perfil, gestionar personal, exportar reportes de salud y soporte) y botón para cerrar sesión.

<img src="images/mock8.png" alt="Mock-up de perfil" width="200">

#### 3.1.4.4. Mobile Applications User Flow Diagrams
#### UF-01: Registro e Inicio de Sesión de Usuario

* **Imagen referencial:**

  ![UF-01: Registro e Inicio de Sesión de Usuario](images/UF-01.png)

* **Descripción y Flujo:**
  * **Inicio / Bienvenida:** El usuario abre la aplicación móvil y visualiza la pantalla de bienvenida con las opciones para iniciar sesión o registrarse.
  * **Acción (Login/Registro):** 
    * Si elige **Iniciar Sesión**, ingresa su correo electrónico y contraseña.
    * Si elige **Registrarse**, completa el formulario con sus datos personales, correo, contraseña y rol (ganadero o veterinario).
  * **Validación de Credenciales / Datos:** El sistema verifica la autenticidad de la cuenta o valida que los campos del registro cumplan con el formato requerido.
  * **Decisión (Éxito / Error):**
    * *Si los datos son incorrectos o incompletos:* El sistema muestra un mensaje de error notificando la falla para reintentar.
    * *Si los datos son correctos:* Se concede el acceso al sistema.
  * **Fin / Destino:** Redirección exitosa a la pantalla principal (**Inicio / Dashboard**).

---

#### UF-02: Registro de un Nuevo Animal en el Inventario

* **Imagen referencial:**

  ![UF-02: Registro de un Nuevo Animal en el Inventario](images/UF-02.png)

* **Descripción y Flujo:**
  * **Punto de Inicio:** El usuario navega al módulo de **Inventario** desde la barra de navegación principal.
  * **Acción de Entrada:** Selecciona la opción **"Registrar Nueva Res"**.
  * **Ingreso de Datos:** Se despliega el formulario en el que ingresa el número de arete (*Tag ID*), raza, fecha de nacimiento/edad, peso y estado sanitario inicial.
  * **Validación:** El sistema comprueba que el código de arete no esté duplicado y que los campos obligatorios hayan sido completados.
  * **Decisión (Confirmación):**
    * *Si falta información o el Tag está repetido:* Muestra una alerta indicando el campo específico a corregir.
    * *Si la información es válida:* Presiona **"Guardar Registro"**.
  * **Fin / Destino:** El nuevo animal queda almacenado y se muestra de forma inmediata en la lista del **Inventario de Ganado**.

---

#### UF-03: Consulta y Registro de Tratamiento Sanitario

* **Imagen referencial:**

  ![UF-03: Consulta y Registro de Tratamiento Sanitario](images/UF-03.png)

* **Descripción y Flujo:**
  * **Búsqueda / Selección:** Desde el módulo de **Inventario**, el usuario busca al animal mediante su código de arete o filtro por raza y selecciona su ficha.
  * **Visualización de Ficha:** Ingresa a la **Ficha Individual del Animal** y selecciona la pestaña de **Salud** o **Tratamientos**.
  * **Acción Principal:** Presiona el botón **"Registrar Tratamiento"**.
  * **Completar Formulario:** Ingresa el tipo de evento sanitario o diagnóstico, medicamento aplicado, dosis, fecha de aplicación y observaciones adicionales.
  * **Procesamiento:** El sistema guarda el registro en el historial clínico y actualiza el estado sanitario del animal.
  * **Fin / Destino:** El nuevo tratamiento queda registrado cronológicamente dentro de la pestaña de **Salud** de la res.

#### 3.1.4.5. Mobile Applications Prototyping

<img src="images/prototype.png" alt="Mock-up de perfil">

 Link del prototipo: https://www.figma.com/proto/6s1sDsX9Z6apr5q1APEUk8/Untitled?node-id=59-3&p=f&t=69FUs3pA82ELGxLM-1&scaling=min-zoom&content-scaling=fixed&page-id=59%3A2&starting-point-node-id=59%3A3&show-proto-sidebar=1
