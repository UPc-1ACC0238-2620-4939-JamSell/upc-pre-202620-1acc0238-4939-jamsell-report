# Capítulo III: Solution UI/UX Design

## 3.1. Product Design

### 3.1.1. Style Guidelines

#### 3.1.1.1. General Style Guidelines

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


---

### 3.1.3. Landing Page UI Design

#### 3.1.3.1. Landing Page Wireframe


#### 3.1.3.2. Landing Page Mock-up


---

### 3.1.4. Mobile Applications UX/UI Design

#### 3.1.4.1. Mobile Applications Wireframes


#### 3.1.4.2. Mobile Applications Wireflow Diagrams


#### 3.1.4.3. Mobile Applications Mock-ups


#### 3.1.4.4. Mobile Applications User Flow Diagrams


#### 3.1.4.5. Mobile Applications Prototyping
