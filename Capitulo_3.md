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


#### 3.1.2.3. SEO Tags and Meta Tags


#### 3.1.2.4. Searching Systems


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
