# Capítulo IV: Product Implementation & Validation

## 4. Product Implementation & Validation

Este capítulo documenta la implementación y validación de Gethics Mobile a lo largo de los Sprints de desarrollo. Se parte del Software Configuration Management del equipo: las herramientas de colaboración, el esquema de control de versiones con GitFlow, las convenciones de código y la configuración de despliegue que mantienen consistentes los tres productos de la solución: Landing Page, Web Services (backend) y la aplicación móvil. Sobre esa base, el capítulo reúne las evidencias de avance por Sprint (implementación, pruebas y despliegue de cada producto) junto con los resultados de las validaciones realizadas con los segmentos de usuario definidos en el Capítulo I, que permiten verificar que la solución responde a las necesidades identificadas para ganaderos, veterinarios y técnicos agropecuarios.

## 4.1. Software Configuration Management

Esta sección documenta las decisiones y convenciones que el equipo JamSell adopta para mantener la consistencia del proyecto Gethics Mobile durante todo su ciclo de vida: qué herramientas se usan para colaborar, cómo se organiza el versionado del código fuente, qué convenciones de estilo se siguen al programar y cómo se configura el despliegue de cada producto.

### 4.1.1. Software Development Environment Configuration

A continuación se especifica cada producto de software utilizado por el equipo para colaborar en el ciclo de vida de Gethics Mobile, agrupado por tipo de actividad. Para cada uno se indica su propósito dentro del proyecto y su ruta de referencia (herramientas SaaS) o de descarga (herramientas instaladas en el computador de cada miembro del equipo).

| Tipo de actividad | Producto | Propósito en el proyecto | Ruta de referencia / descarga |
|---|---|---|---|
| Project Management | Trello | Tablero Kanban del equipo (To Do / In Progress / Done) para organizar y dar seguimiento a las tareas de cada Sprint. | https://trello.com |
| Requirements Management | Trello | Mismo tablero del equipo, utilizado también para registrar y priorizar el backlog de historias de usuario del producto. | https://trello.com |
| Product UX/UI Design | Figma | Diseño de los wireframes y mock-ups de las pantallas de la aplicación móvil y del Landing Page, y definición del Design System (Style Guidelines: color, tipografía, iconografía) del equipo. | https://www.figma.com |
| Software Development | Android Studio | IDE utilizado por el equipo tanto para el desarrollo de la aplicación móvil (Flutter/Dart) como del backend (Spring Boot/Java). | https://developer.android.com/studio |
| Software Development | Flutter SDK | Framework utilizado para construir la aplicación móvil multiplataforma de Gethics. | https://flutter.dev |
| Software Development | PostgreSQL | Motor de base de datos relacional del backend, donde se persiste la información del hato, los usuarios y los eventos sanitarios. | https://www.postgresql.org |
| Software Development | GitHub | Control de versiones y colaboración sobre el código fuente de los tres productos del equipo (Landing Page, Web Services y Mobile App). | https://github.com |
| Software Testing | Postman | Pruebas manuales y colecciones de pruebas sobre los endpoints del backend (Web Services), antes de integrarlos con la aplicación móvil. | https://www.postman.com |
| Software Deployment | Vercel | Despliegue del Landing Page como sitio estático. | https://vercel.com |
| Software Deployment | Render | Despliegue del backend (Web Services) y de la base de datos PostgreSQL gestionada. | https://render.com |
| Software Documentation | GitHub | Repositorio del informe del proyecto, redactado en Markdown y versionado junto con el resto de productos del equipo. | https://github.com |

Como se observa, el equipo prioriza herramientas de modelo SaaS (Trello, Figma, GitHub, Postman, Vercel, Render) para facilitar la colaboración remota entre los miembros del equipo, reservando las instalaciones locales (Android Studio, Flutter SDK, PostgreSQL) a los productos que efectivamente requieren ejecutarse en el computador de cada desarrollador.

### 4.1.2. Source Code Management

Para la gestión y seguimiento de modificaciones del código fuente de **Gethics**, el equipo utiliza **GitHub** como plataforma de alojamiento de repositorios y **Git** como sistema de control de versiones.

La solución se encuentra distribuida en repositorios independientes de acuerdo con los principales productos de software desarrollados por el equipo: Landing Page, aplicación móvil, Web Services y documentación del proyecto.

### Repositories

| Product | Repository |
|---|---|
| Project Report | https://github.com/UPc-1ACC0238-2620-4939-JamSell/upc-pre-202620-1acc0238-4939-jamsell-report |
| Landing Page | https://github.com/UPc-1ACC0238-2620-4939-JamSell/gethics-landing-page.git |
| Mobile Application | https://github.com/UPc-1ACC0238-2620-4939-JamSell/gethics-mobile-app.git |
| Web Services / Backend | https://github.com/UPc-1ACC0238-2620-4939-JamSell/gethics-backend.git |

El repositorio correspondiente a **Web Services / Backend** contendrá tanto el código fuente de los servicios como los archivos relacionados con las pruebas unitarias y las pruebas de integración o aceptación desarrolladas durante la implementación.

A continuación, se presenta la organización actual de los repositorios del equipo en GitHub.

![Gethics GitHub Repositories](images/gethics-github-repositories.png)

### GitFlow

Para organizar el desarrollo colaborativo del proyecto se aplicará **GitFlow** como modelo de ramificación.

El flujo de trabajo considera las siguientes ramas principales:

- `main`: contendrá las versiones estables y preparadas para entrega o despliegue.
- `develop`: funcionará como rama de integración para los cambios desarrollados durante cada Sprint.

Actualmente, el repositorio del Project Report cuenta con las ramas `main` y `develop`, utilizando `develop` como rama de integración para los avances del informe.

A partir de estas ramas principales se utilizarán ramas temporales de acuerdo con el tipo de modificación realizada.

#### Feature Branches

Cada nueva funcionalidad será desarrollada en una rama independiente creada a partir de `develop`.

La convención establecida será:

```text
feature/<user-story>-<short-description>
```

### 4.1.3. Source Code Style Guide & Conventions


### 4.1.4. Software Deployment Configuration


---

## 4.2. Landing Page & Mobile Application Implementation

### 4.2.1. Sprint n

#### 4.2.1.1. Sprint Planning n


#### 4.2.1.2. Aspect Leaders and Collaborators


#### 4.2.1.3. Sprint Backlog n


#### 4.2.1.4. Development Evidence for Sprint Review


#### 4.2.1.5. Testing Suite Evidence for Sprint Review


#### 4.2.1.6. Execution Evidence for Sprint Review


#### 4.2.1.7. Services Documentation Evidence for Sprint Review


#### 4.2.1.8. Software Deployment Evidence for Sprint Review


#### 4.2.1.9. Team Collaboration Insights during Sprint


---

## 4.3. Validation Interviews

### 4.3.1. Diseño de Entrevistas


### 4.3.2. Registro de Entrevistas


### 4.3.3. Evaluaciones según heurísticas


---

# Conclusiones

## Conclusiones y recomendaciones


---

# Video App Validation


# Video About the Product


# Video About the Team


---

# Glosario


# Bibliografía


# Anexos
