# Capítulo II: Requirements Development and Software Solution Design

## 2.1. Competidores

### 2.1.1. Análisis competitivo


### 2.1.2. Estrategias y tácticas frente a competidores


---

## 2.2. Entrevistas

### 2.2.1. Diseño de entrevistas


### 2.2.2. Registro de entrevistas


### 2.2.3. Análisis de entrevistas


---

## 2.3. Needfinding

### 2.3.1. User Personas


### 2.3.2. User Task Matrix


### 2.3.3. User Journey Mapping


### 2.3.4. Empathy Mapping


### 2.3.5. Big Picture EventStorming


### 2.3.6. Ubiquitous Language


---

## 2.4. Requirements Specification

### 2.4.1. User Stories


### 2.4.2. Impact Mapping


### 2.4.3. Product Backlog


---

## 2.5. Strategic-Level Domain-Driven Design

### 2.5.1. EventStorming

#### 2.5.1.1. Candidate Context Discovery


#### 2.5.1.2. Domain Message Flows Modeling


#### 2.5.1.3. Bounded Context Canvases


### 2.5.2. Context Mapping


### 2.5.3. Software Architecture

#### 2.5.3.1. Software Architecture Context Level Diagrams


#### 2.5.3.2. Software Architecture Container Level Diagrams


#### 2.5.3.3. Software Architecture Deployment Diagrams


---

## 2.6. Tactical-Level Domain-Driven Design

En esta sección se presenta la perspectiva táctica de Domain-Driven Design aplicada a Gethics. A partir de los bounded contexts identificados durante el diseño estratégico, se define la estructura interna de cada uno de ellos, considerando sus responsabilidades, elementos de dominio y las capas que conforman la solución.

Cada bounded context mantiene sus propias reglas de negocio y responsabilidades, permitiendo separar las diferentes capacidades de Gethics y reducir el acoplamiento entre los módulos de la aplicación.

Para el diseño táctico de Gethics se consideran los siguientes bounded contexts:

| N.° | Bounded Context | Responsabilidad principal |
|---|---|---|
| 1 | Livestock Management | Gestionar las fincas y el registro individual de los animales del ganado. |
| 2 | Animal Health Management | Gestionar historiales médicos, visitas veterinarias, vacunas, tratamientos y eventos sanitarios. |
| 3 | Financial Management | Gestionar los ingresos y egresos relacionados con la actividad ganadera. |
| 4 | Monitoring and Analytics | Gestionar dispositivos IoT, mediciones, reportes, estadísticas y alertas. |
| 5 | Identity and Access Management | Gestionar usuarios, roles y relaciones entre ganaderos y veterinarios. |
| 6 | Subscription Management | Gestionar los planes y suscripciones disponibles para los usuarios de Gethics. |

A continuación, se desarrolla la perspectiva táctica correspondiente a cada bounded context.

### 2.6.1. Bounded Context: Livestock Management

El bounded context **Livestock Management** se encarga de gestionar la información principal relacionada con las fincas y los animales registrados en Gethics. Su objetivo es permitir que los ganaderos mantengan organizada la información de su ganado desde la aplicación móvil, reemplazando progresivamente el uso de registros manuales.

Dentro de este bounded context se consideran funcionalidades como el registro de fincas, registro individual de animales, consulta de información, búsqueda, filtrado, actualización de datos y control del estado de cada animal.

Livestock Management se mantiene separado de otros bounded contexts como **Animal Health Management**, debido a que su responsabilidad se concentra en la identificación y administración general del ganado, mientras que los historiales médicos, tratamientos, vacunas y demás información sanitaria son gestionados por el dominio de salud animal.

#### Diccionario de clases

Las principales clases identificadas para el bounded context Livestock Management son las siguientes:

| Clase | Tipo | Propósito | Atributos principales | Métodos principales | Relaciones |
|---|---|---|---|---|---|
| `Farm` | Aggregate Root / Entity | Representa una finca registrada dentro de Gethics y permite organizar los animales pertenecientes a un ganadero. | `id`, `ownerId`, `name`, `location`, `status` | `updateInformation()`, `activate()`, `deactivate()` | Una finca puede estar relacionada con múltiples animales. |
| `Animal` | Aggregate Root / Entity | Representa a cada animal registrado dentro de una finca. | `id`, `farmId`, `tag`, `name`, `breed`, `birthDate`, `sex`, `status` | `updateInformation()`, `changeStatus()`, `remove()` | Cada animal pertenece a una finca. |
| `AnimalTag` | Value Object | Representa el código o identificador utilizado para reconocer a un animal dentro de una finca. | `value` | `validate()` | Es utilizado por `Animal`. |
| `Breed` | Value Object | Representa la raza registrada para un animal. | `name` | `validate()` | Es utilizado por `Animal`. |
| `AnimalSex` | Enumeration | Define los posibles valores para el sexo de un animal. | `MALE`, `FEMALE` | No aplica | Es utilizado por `Animal`. |
| `AnimalStatus` | Enumeration | Define el estado actual del registro de un animal. | `ACTIVE`, `SOLD`, `DECEASED`, `INACTIVE` | No aplica | Es utilizado por `Animal`. |
| `FarmRepository` | Repository Interface | Define las operaciones necesarias para almacenar y recuperar fincas. | No aplica | `save()`, `findById()`, `findByOwnerId()` | Trabaja con `Farm`. |
| `AnimalRepository` | Repository Interface | Define las operaciones necesarias para almacenar y recuperar animales. | No aplica | `save()`, `findById()`, `findByFarmId()`, `existsByTag()` | Trabaja con `Animal`. |
| `AnimalRegistrationService` | Domain Service | Aplica las reglas necesarias antes de registrar un animal dentro de una finca. | No aplica | `validateRegistration()` | Utiliza información de `Animal`, `Farm` y `AnimalRepository`. |

---

#### 2.6.1.1. Domain Layer

El **Domain Layer** contiene las clases que representan el núcleo de negocio de Livestock Management. En esta capa se encuentran las entidades, Aggregate Roots, Value Objects, enumeraciones, Domain Services y las interfaces de Repository necesarias para manejar las reglas relacionadas con las fincas y los animales.

`Farm` representa una finca perteneciente a un ganadero y funciona como un Aggregate Root independiente. Mantiene información como el nombre, ubicación, propietario y estado de la finca.

`Animal` representa a un animal registrado dentro de Gethics y también funciona como Aggregate Root. Cada animal posee una identidad propia y mantiene información general como su identificador, raza, fecha de nacimiento, sexo y estado.

Los conceptos `AnimalTag` y `Breed` son representados como Value Objects debido a que no poseen una identidad propia y su importancia está determinada por el valor que contienen.

Las enumeraciones `AnimalSex` y `AnimalStatus` permiten restringir los posibles estados de estos atributos y mantener consistencia dentro del modelo.

`AnimalRegistrationService` contiene las reglas de dominio necesarias para validar el registro de un animal. Por ejemplo, puede verificar que un animal tenga información válida y que no exista otro registro con el mismo identificador dentro de una finca.

Finalmente, `FarmRepository` y `AnimalRepository` son interfaces que definen las operaciones de persistencia requeridas por el dominio sin establecer todavía qué tecnología de almacenamiento será utilizada.

---

#### 2.6.1.2. Interface Layer

El **Interface Layer** contiene los componentes responsables de recibir las solicitudes realizadas desde las aplicaciones móviles y comunicar dichas solicitudes con los casos de uso definidos en el Application Layer.

Para Livestock Management se consideran principalmente los siguientes Controllers:

| Clase | Tipo | Propósito | Operaciones principales |
|---|---|---|---|
| `FarmController` | Controller | Recibe las solicitudes relacionadas con la gestión de las fincas del usuario. | `createFarm()`, `getFarm()`, `getFarms()`, `updateFarm()` |
| `AnimalController` | Controller | Recibe las solicitudes relacionadas con el registro y gestión de animales. | `createAnimal()`, `getAnimal()`, `getAnimals()`, `updateAnimal()`, `deleteAnimal()` |

`FarmController` permite exponer las operaciones requeridas para registrar, consultar y actualizar las fincas asociadas a un ganadero.

`AnimalController` permite registrar nuevos animales, consultar la información de un animal, recuperar el listado correspondiente a una finca, actualizar sus datos y eliminar o desactivar registros.

Los Controllers no contienen directamente las reglas de negocio. Su responsabilidad consiste en recibir la información enviada por el cliente, enviarla al caso de uso correspondiente y retornar el resultado obtenido.

---

#### 2.6.1.3. Application Layer

El **Application Layer** coordina los casos de uso disponibles dentro de Livestock Management. Esta capa conecta las solicitudes recibidas desde Interface Layer con las reglas existentes en Domain Layer.

Para mantener separadas las operaciones que modifican información de aquellas que solamente realizan consultas, se consideran Commands y Queries.

| Clase | Tipo | Propósito |
|---|---|---|
| `CreateFarmCommandHandler` | Command Handler | Coordina el registro de una nueva finca. |
| `UpdateFarmCommandHandler` | Command Handler | Coordina la actualización de los datos de una finca. |
| `CreateAnimalCommandHandler` | Command Handler | Coordina el registro de un nuevo animal. |
| `UpdateAnimalCommandHandler` | Command Handler | Coordina la modificación de la información de un animal. |
| `DeleteAnimalCommandHandler` | Command Handler | Coordina la eliminación o desactivación de un animal. |
| `GetFarmByIdQueryHandler` | Query Handler | Obtiene la información correspondiente a una finca. |
| `GetFarmsByOwnerQueryHandler` | Query Handler | Obtiene las fincas pertenecientes a un ganadero. |
| `GetAnimalByIdQueryHandler` | Query Handler | Obtiene la información de un animal específico. |
| `GetAnimalsByFarmQueryHandler` | Query Handler | Obtiene los animales registrados dentro de una finca. |
| `AnimalRegisteredEventHandler` | Event Handler | Gestiona las acciones posteriores al registro exitoso de un animal. |

Por ejemplo, cuando el usuario registra un nuevo animal desde la aplicación móvil, la solicitud es recibida por `AnimalController`, el cual invoca a `CreateAnimalCommandHandler`. El handler utiliza las reglas definidas en el Domain Layer y posteriormente solicita al `AnimalRepository` almacenar la información.

De esta manera, las reglas del dominio permanecen separadas de los procesos de coordinación de la aplicación.

---

#### 2.6.1.4. Infrastructure Layer

El **Infrastructure Layer** contiene las implementaciones encargadas de acceder a recursos técnicos y servicios externos necesarios para Livestock Management.

Aquí se ubican las implementaciones concretas de las interfaces Repository definidas en Domain Layer, así como los mecanismos utilizados para comunicarse con la base de datos o almacenamiento correspondiente.

| Clase | Tipo | Propósito |
|---|---|---|
| `FarmRepositoryImpl` | Repository Implementation | Implementa las operaciones definidas por `FarmRepository` para almacenar y recuperar fincas. |
| `AnimalRepositoryImpl` | Repository Implementation | Implementa las operaciones definidas por `AnimalRepository` para almacenar y recuperar animales. |
| `LivestockDataSource` | Data Source | Gestiona la comunicación con la fuente de datos utilizada por Livestock Management. |
| `LocalLivestockDataSource` | Local Data Source | Permite almacenar localmente en el dispositivo la información necesaria para determinadas funcionalidades móviles. |
| `LivestockApiClient` | API Client | Permite que la aplicación móvil se comunique con los servicios REST relacionados con la gestión del ganado. |

`FarmRepositoryImpl` y `AnimalRepositoryImpl` implementan las interfaces definidas en el dominio, permitiendo que este último permanezca independiente de la tecnología utilizada para persistir la información.

Asimismo, `LocalLivestockDataSource` permite contemplar el almacenamiento local requerido por la aplicación móvil, mientras que `LivestockApiClient` gestiona la comunicación con los servicios REST de Gethics.

---

### 2.6.1.5. Bounded Context Software Architecture Component Level Diagrams

En esta sección se presenta el Component Diagram correspondiente al bounded context **Livestock Management**, siguiendo el enfoque del modelo C4 y la arquitectura basada en Domain-Driven Design.

El objetivo del diagrama es representar la estructura interna del bounded context, mostrando los principales componentes que participan en la gestión del ganado, sus responsabilidades y la comunicación existente entre las diferentes capas definidas previamente: Interface Layer, Application Layer, Domain Layer e Infrastructure Layer.

Dentro de **Livestock Management**, la aplicación móvil permite a los usuarios gestionar la información principal de los animales registrados en una finca, incluyendo operaciones como el registro, actualización, consulta e identificación mediante códigos QR.

El flujo principal inicia cuando el usuario interactúa con la aplicación móvil. Las solicitudes realizadas son recibidas por los componentes pertenecientes a la capa de interfaz, los cuales delegan la ejecución hacia los servicios correspondientes de la capa de aplicación. Posteriormente, esta capa coordina los casos de uso utilizando las reglas definidas en el dominio, donde se encuentran los agregados principales como **Animal** y **Farm**. Finalmente, la capa de infraestructura proporciona los mecanismos necesarios para la persistencia y comunicación con servicios externos.

**Livestock Management Software Architecture Component Level Diagram**

![Livestock Management Software Architecture Component Level Diagram](images/BoundedContextSoftwareArchitecture.png)


El diagrama representa los siguientes componentes principales:

| Componente | Responsabilidad |
|---|---|
| Animal Controller | Recibe las solicitudes relacionadas con la gestión de animales desde la aplicación móvil. |
| Farm Controller | Gestiona las operaciones relacionadas con la administración de fincas. |
| Animal Application Services | Coordina los casos de uso relacionados con el registro, actualización y consulta de animales. |
| Farm Application Services | Coordina las operaciones relacionadas con la gestión de fincas. |
| Animal Aggregate | Representa la entidad principal del dominio y contiene las reglas relacionadas con el ciclo de vida del animal. |
| Farm Aggregate | Representa la unidad productiva donde se organizan los animales registrados. |
| Animal Repository Interface | Define las operaciones necesarias para almacenar y recuperar información relacionada con animales. |
| Farm Repository Interface | Define las operaciones necesarias para almacenar y recuperar información relacionada con fincas. |
| Animal Repository Implementation | Implementa el acceso a los datos correspondientes al agregado Animal. |
| Farm Repository Implementation | Implementa el acceso a los datos correspondientes al agregado Farm. |
| Local Data Source | Permite almacenar información localmente para soportar escenarios con conectividad limitada. |
| API Client | Permite la comunicación con servicios externos mediante solicitudes REST. |


El flujo principal de comunicación dentro del bounded context sigue los siguientes pasos:

1. El usuario interactúa con la aplicación móvil para registrar, actualizar o consultar información relacionada con un animal o una finca.
2. La solicitud es recibida por los componentes de la Interface Layer, como los controladores correspondientes.
3. La capa de aplicación procesa la solicitud mediante los casos de uso definidos utilizando Commands y Queries.
4. La capa de dominio valida las reglas de negocio asociadas a los agregados principales del contexto.
5. Los repositorios definidos en el dominio son implementados por la capa de infraestructura para acceder a los mecanismos de persistencia.
6. La información procesada es retornada nuevamente hacia la aplicación móvil.

---

### 2.6.1.6. Bounded Context Software Architecture Code Level Diagrams

En esta sección se presentan los diagramas correspondientes al nivel de código del bounded context **Livestock Management**, siguiendo la propuesta de diseño basada en Domain-Driven Design.

Estos diagramas permiten representar la estructura interna del contexto a nivel de implementación, mostrando las principales clases, relaciones y componentes que forman parte de la capa de dominio.

El diseño mantiene la separación de responsabilidades definida previamente, donde la lógica de negocio permanece encapsulada dentro del dominio, mientras que las capas externas se encargan de la comunicación con interfaces de usuario, aplicación e infraestructura.

---

### 2.6.1.6.1. Bounded Context Domain Layer Class Diagrams

En esta sección se presenta el diagrama de clases UML correspondiente a la capa de dominio del bounded context **Livestock Management**.

El diagrama representa las principales entidades, objetos de valor y contratos definidos dentro del dominio para gestionar la información relacionada con animales y fincas.

La entidad **Animal** representa el agregado principal del contexto, debido a que concentra la información necesaria para identificar y administrar cada animal registrado dentro del sistema. Asimismo, la entidad **Farm** representa la finca donde se organizan los animales pertenecientes al usuario.

Además, se incluyen los objetos de valor utilizados para representar identificadores únicos y códigos QR, así como las interfaces de repositorio encargadas de definir las operaciones necesarias para acceder a la información del dominio sin depender de una implementación tecnológica específica.

**Livestock Management Domain Layer Class Diagram**

![Livestock Management Domain Layer Class Diagram](images/BoundedContextSoftwareArchitectureCodeLevel.png)

El diseño del dominio permite mantener las reglas de negocio independientes de los mecanismos de persistencia, facilitando la evolución del sistema y manteniendo los principios establecidos por Domain-Driven Design.

Las principales relaciones representadas en el diagrama son:

- **Farm** mantiene una relación de composición con múltiples objetos **Animal**, debido a que una finca puede contener varios animales registrados.
- **Animal** utiliza objetos de valor como **AnimalId** y **QRCode** para garantizar una identificación única dentro del sistema.
- **AnimalRepository** y **FarmRepository** definen los contratos necesarios para almacenar y recuperar información de las entidades principales.
- La separación entre entidades, objetos de valor y repositorios permite mantener una arquitectura desacoplada y preparada para cambios futuros.


Esta separación permite mantener la lógica de negocio independiente de los mecanismos tecnológicos utilizados para almacenar información o comunicarse con servicios externos, siguiendo los principios establecidos por Domain-Driven Design y facilitando la evolución futura del sistema.

---

##### 2.6.1.6.2. Bounded Context Database Design Diagram

En esta sección se presenta el diseño de base de datos correspondiente al bounded context **Livestock Management**.

El modelo de persistencia representa la información necesaria para gestionar las fincas y los animales registrados dentro de Gethics. Este diseño mantiene la separación de responsabilidades definida en el modelo de dominio, permitiendo almacenar únicamente la información perteneciente a este bounded context.

La estructura principal está conformada por las entidades **Farm** y **Animal**, donde una finca puede contener múltiples animales registrados, mientras que cada animal pertenece únicamente a una finca determinada.

Asimismo, se considera la identificación mediante código QR como parte de la información principal del animal, debido a que esta característica permite facilitar la identificación rápida del ganado, una de las responsabilidades principales definidas para este bounded context.

**Livestock Management Database Design Diagram**

![Livestock Management Database Design Diagram](images/BoundedContextDatabaseDesign.png)


El diseño propuesto contiene las siguientes entidades:

| Entidad | Descripción |
|---|---|
| Farm | Representa la información principal de una finca registrada dentro de Gethics. |
| Animal | Representa cada animal perteneciente a una finca y contiene la información necesaria para su identificación y gestión. |


### Entidad Farm

| Campo | Tipo | Restricción | Descripción |
|---|---|---|---|
| id | UUID | Primary Key | Identificador único de la finca. |
| owner_id | UUID | Foreign Key | Identificador del usuario propietario de la finca. |
| name | VARCHAR | NOT NULL | Nombre asignado a la finca. |
| location | VARCHAR | NOT NULL | Ubicación registrada de la finca. |
| status | VARCHAR | NOT NULL | Estado actual de la finca. |
| created_at | DATETIME | NOT NULL | Fecha de creación del registro. |


### Entidad Animal

| Campo | Tipo | Restricción | Descripción |
|---|---|---|---|
| id | UUID | Primary Key | Identificador único del animal. |
| farm_id | UUID | Foreign Key | Identificador de la finca a la que pertenece. |
| qr_code | VARCHAR | UNIQUE, NOT NULL | Código QR utilizado para identificar al animal. |
| name | VARCHAR | NULL | Nombre asignado al animal. |
| breed | VARCHAR | NOT NULL | Raza del animal registrado. |
| birth_date | DATE | NOT NULL | Fecha de nacimiento del animal. |
| sex | VARCHAR | NOT NULL | Sexo del animal. |
| status | VARCHAR | NOT NULL | Estado actual del animal. |
| created_at | DATETIME | NOT NULL | Fecha de creación del registro. |


### Relaciones principales

La relación principal del modelo es:

- Una entidad **Farm** puede tener múltiples entidades **Animal** asociadas.
- Cada entidad **Animal** pertenece únicamente a una entidad **Farm**.

La multiplicidad de la relación se representa como:
Farm 1 -------- 0..* Animal

Esta relación permite organizar el ganado dentro de una estructura jerárquica donde cada animal se encuentra asociado a la finca correspondiente.

Además, se establece una restricción de unicidad para el atributo `qr_code`, evitando que dos animales diferentes posean el mismo código de identificación dentro del sistema.

El diseño de base de datos mantiene la consistencia con el modelo de dominio previamente definido, donde **Animal** representa el agregado principal encargado de mantener la información individual del ganado, mientras que **Farm** representa el contexto organizativo donde estos registros son almacenados.

---

## 2.6.2. Bounded Context: Sanitary Tracking

El bounded context **Sanitary Tracking** se encarga de gestionar el seguimiento de los eventos sanitarios asociados a los animales registrados dentro de Gethics.

Su objetivo es permitir que los ganaderos puedan organizar y monitorear actividades preventivas relacionadas con la salud del ganado, como vacunaciones, desparasitaciones y controles programados, evitando depender únicamente de registros manuales.

Este bounded context mantiene la responsabilidad de administrar la planificación y seguimiento de eventos sanitarios, mientras que la información relacionada con diagnósticos médicos y tratamientos específicos realizados por veterinarios pertenece al bounded context **Veterinary Care**.

Sanitary Tracking utiliza la identificación del animal proporcionada por **Livestock Management**, permitiendo asociar cada evento sanitario con el animal correspondiente sin modificar directamente la información interna de dicho contexto.

---

### Diccionario de clases

Las principales clases identificadas para el bounded context **Sanitary Tracking** son las siguientes:

| Clase | Tipo | Propósito | Atributos principales | Métodos principales | Relaciones |
|---|---|---|---|---|---|
| `SanitaryEvent` | Aggregate Root / Entity | Representa una actividad sanitaria programada o realizada sobre un animal. | `id`, `animalId`, `type`, `scheduledDate`, `status`, `description` | `schedule()`, `complete()`, `cancel()` | Se relaciona con un animal mediante `animalId`. |
| `SanitaryCalendar` | Entity | Representa la planificación de eventos sanitarios de una finca o animal. | `id`, `ownerId`, `createdAt` | `addEvent()`, `removeEvent()`, `getUpcomingEvents()` | Contiene múltiples eventos sanitarios. |
| `Reminder` | Entity | Representa una notificación preventiva asociada a un evento sanitario próximo. | `id`, `eventId`, `date`, `status` | `send()`, `markAsSent()` | Se relaciona con un evento sanitario. |
| `SanitaryType` | Enumeration | Define el tipo de actividad sanitaria registrada. | `VACCINATION`, `DEWORMING`, `CHECKUP`, `OTHER` | No aplica | Es utilizado por `SanitaryEvent`. |
| `SanitaryStatus` | Enumeration | Define el estado actual del evento sanitario. | `PENDING`, `COMPLETED`, `CANCELLED` | No aplica | Es utilizado por `SanitaryEvent`. |
| `ScheduleDate` | Value Object | Representa una fecha válida para programar un evento sanitario. | `date` | `validate()` | Es utilizado por `SanitaryEvent`. |
| `SanitaryEventRepository` | Repository Interface | Define las operaciones necesarias para almacenar y consultar eventos sanitarios. | No aplica | `save()`, `findByAnimalId()`, `findUpcoming()` | Trabaja con `SanitaryEvent`. |
| `ReminderRepository` | Repository Interface | Define las operaciones necesarias para gestionar recordatorios. | No aplica | `save()`, `findPending()` | Trabaja con `Reminder`. |
| `SanitaryScheduleService` | Domain Service | Contiene reglas relacionadas con la programación sanitaria. | No aplica | `validateSchedule()`, `createReminder()` | Utiliza eventos sanitarios. |

---

## 2.6.2.1. Domain Layer

El **Domain Layer** contiene las reglas principales relacionadas con el seguimiento sanitario preventivo del ganado.

El agregado principal del contexto es `SanitaryEvent`, encargado de representar cada actividad sanitaria asociada a un animal. Este agregado permite controlar el ciclo de vida del evento desde su programación hasta su finalización o cancelación.

`SanitaryCalendar` representa la organización de los eventos sanitarios programados, permitiendo consultar actividades próximas y mantener un seguimiento ordenado.

Los Value Objects permiten representar conceptos que requieren validación propia. Por ejemplo, `ScheduleDate` permite controlar que las fechas utilizadas para programar eventos sean válidas dentro del dominio.

Las enumeraciones `SanitaryType` y `SanitaryStatus` permiten restringir los valores aceptados para los tipos y estados de los eventos sanitarios.

Finalmente, las interfaces `SanitaryEventRepository` y `ReminderRepository` definen las operaciones necesarias para acceder a la información persistida sin depender de una tecnología específica.

---

## 2.6.2.2. Interface Layer

El **Interface Layer** contiene los componentes encargados de recibir las solicitudes provenientes de la aplicación móvil relacionadas con el seguimiento sanitario.

Esta capa permite que los usuarios puedan consultar eventos próximos, registrar actividades sanitarias y visualizar recordatorios asociados al ganado.

| Clase | Tipo | Propósito | Operaciones principales |
|---|---|---|---|
| `SanitaryEventController` | Controller | Gestiona las operaciones relacionadas con eventos sanitarios. | `createEvent()`, `getEvents()`, `updateEvent()`, `completeEvent()` |
| `SanitaryCalendarController` | Controller | Gestiona la consulta del calendario sanitario. | `getCalendar()`, `getUpcomingEvents()` |
| `ReminderController` | Controller | Gestiona los recordatorios generados por eventos sanitarios. | `getReminders()`, `markAsRead()` |

Los Controllers reciben las solicitudes del usuario y delegan la ejecución hacia los casos de uso correspondientes definidos en la capa de aplicación.

---

## 2.6.2.3. Application Layer

El **Application Layer** coordina los casos de uso relacionados con la planificación y seguimiento de eventos sanitarios.

Esta capa no contiene reglas de negocio propias, sino que coordina la interacción entre los Controllers, los agregados del dominio y los repositorios correspondientes.

| Clase | Tipo | Propósito |
|---|---|---|
| `CreateSanitaryEventCommandHandler` | Command Handler | Coordina la creación de un nuevo evento sanitario. |
| `UpdateSanitaryEventCommandHandler` | Command Handler | Coordina la actualización de información de un evento sanitario. |
| `CompleteSanitaryEventCommandHandler` | Command Handler | Coordina el cambio de estado de un evento sanitario completado. |
| `CancelSanitaryEventCommandHandler` | Command Handler | Coordina la cancelación de una actividad sanitaria. |
| `GetSanitaryCalendarQueryHandler` | Query Handler | Obtiene el calendario sanitario asociado al usuario. |
| `GetUpcomingEventsQueryHandler` | Query Handler | Obtiene próximos eventos sanitarios pendientes. |
| `GenerateReminderEventHandler` | Event Handler | Genera recordatorios asociados a eventos próximos. |

Por ejemplo, cuando un usuario programa una vacunación desde la aplicación móvil, la solicitud llega al Controller correspondiente, el Application Handler coordina la operación y finalmente el dominio valida que el evento pueda ser registrado correctamente.

---

## 2.6.2.4. Infrastructure Layer

El **Infrastructure Layer** contiene las implementaciones técnicas necesarias para almacenar información y comunicarse con servicios externos utilizados por Sanitary Tracking.

Esta capa implementa las interfaces definidas por el dominio y permite que los componentes internos permanezcan independientes de la tecnología utilizada.

| Clase | Tipo | Propósito |
|---|---|---|
| `SanitaryEventRepositoryImpl` | Repository Implementation | Implementa las operaciones de persistencia de eventos sanitarios. |
| `ReminderRepositoryImpl` | Repository Implementation | Implementa las operaciones de persistencia de recordatorios. |
| `SanitaryDataSource` | Data Source | Gestiona el acceso a la fuente de datos sanitaria. |
| `LocalSanitaryDataSource` | Local Data Source | Permite almacenar información sanitaria localmente en el dispositivo móvil. |
| `SanitaryApiClient` | API Client | Permite la comunicación con servicios REST relacionados con eventos sanitarios. |
| `NotificationService` | External Service Adapter | Permite enviar recordatorios y notificaciones al usuario. |

La separación entre capas permite que la lógica relacionada con eventos sanitarios pueda evolucionar sin depender directamente de la base de datos, servicios de notificación o mecanismos específicos de comunicación.

---

### 2.6.2.5. Bounded Context Software Architecture Component Level Diagrams

En esta sección se presenta el Component Level Diagram correspondiente al bounded context **Sanitary Tracking**, siguiendo el enfoque del modelo C4 y manteniendo consistencia con las decisiones establecidas previamente en el Strategic-Level Domain-Driven Design de Gethics Mobile.

El objetivo del diagrama es representar la organización interna de los componentes responsables del seguimiento sanitario de los animales, así como las interacciones entre las capas de Interface, Application, Domain e Infrastructure.

Sanitary Tracking tiene como responsabilidad principal registrar y dar seguimiento a los eventos sanitarios asociados a los animales, incluyendo vacunas, tratamientos y enfermedades. Asimismo, permite programar actividades sanitarias, mantener actualizado el historial clínico y generar recordatorios o alertas cuando corresponda.

Este bounded context recibe la identificación y datos generales del animal desde **Livestock Management**, manteniendo separados ambos modelos. Asimismo, Sanitary Tracking es propietario del historial clínico, por lo que las actualizaciones realizadas desde **Veterinary Care** deben efectuarse mediante las operaciones expuestas por este contexto y no mediante acceso directo a sus datos.

Finalmente, la información sanitaria generada puede ser utilizada por **Analytics & Alerts** para el análisis de tendencias, mientras que el envío de recordatorios y alertas se delega al **Servicio de Notificaciones Push** definido como sistema externo.

**Sanitary Tracking Software Architecture Component Level Diagram**

![Sanitary Tracking Software Architecture Component Level Diagram](images/SanitaryTracking.png)

El diagrama presenta los componentes principales que participan en el bounded context:

| Componente | Responsabilidad |
|---|---|
| `Sanitary Event Controller` | Recibe las solicitudes relacionadas con el registro, consulta, actualización y finalización de eventos sanitarios. |
| `Sanitary Calendar Controller` | Gestiona las solicitudes relacionadas con la consulta y planificación del calendario sanitario. |
| `Reminder Controller` | Gestiona las solicitudes relacionadas con los recordatorios sanitarios. |
| `Sanitary Event Application Service` | Coordina los casos de uso relacionados con el registro y actualización de eventos sanitarios. |
| `Calendar Application Service` | Coordina los casos de uso relacionados con la programación y consulta del calendario sanitario. |
| `Reminder Application Service` | Coordina la generación y administración de recordatorios relacionados con los eventos sanitarios. |
| `Sanitary Event Aggregate` | Representa el agregado principal del contexto y controla el ciclo de vida de los eventos sanitarios. |
| `Sanitary Calendar` | Organiza los eventos sanitarios programados y permite consultar las actividades próximas. |
| `Reminder` | Representa un recordatorio asociado a un evento sanitario próximo. |
| `Sanitary Schedule Service` | Contiene las reglas de dominio necesarias para validar la programación de actividades sanitarias y la generación de recordatorios. |
| `Sanitary Event Repository Interface` | Define las operaciones requeridas por el dominio para almacenar y recuperar eventos sanitarios. |
| `Reminder Repository Interface` | Define las operaciones requeridas para almacenar y consultar recordatorios. |
| `Sanitary Event Repository Implementation` | Implementa las operaciones de persistencia definidas por el dominio para los eventos sanitarios. |
| `Reminder Repository Implementation` | Implementa las operaciones de persistencia correspondientes a los recordatorios. |
| `Local Sanitary Data Source` | Permite mantener temporalmente información sanitaria en el dispositivo móvil para soportar el registro sin conexión. |
| `Sanitary API Client` | Permite la comunicación entre la aplicación móvil y los servicios RESTful asociados al bounded context. |
| `Notification Service` | Adaptador encargado de solicitar el envío de recordatorios y alertas mediante el servicio externo de notificaciones push. |

El flujo principal de comunicación dentro de Sanitary Tracking se desarrolla de la siguiente manera:

1. El usuario interactúa con Gethics Mobile para registrar, consultar o actualizar información sanitaria de un animal.
2. Los Controllers de la Interface Layer reciben la solicitud y delegan su procesamiento hacia los servicios correspondientes del Application Layer.
3. Los Application Services coordinan el caso de uso y utilizan los elementos del Domain Layer para aplicar las reglas de negocio.
4. `SanitaryEvent` controla el ciclo de vida del evento sanitario, mientras que `SanitaryScheduleService` valida las reglas relacionadas con su programación.
5. Las interfaces de Repository definidas en el dominio permiten solicitar la persistencia de la información sin depender de una tecnología concreta.
6. Los Repository Implementations y Data Sources de la Infrastructure Layer realizan el almacenamiento y recuperación de la información.
7. Cuando un evento sanitario requiere generar un recordatorio o alerta, la infraestructura solicita el envío correspondiente al Servicio de Notificaciones Push.

Además de este flujo interno, Sanitary Tracking mantiene las siguientes relaciones con otros bounded contexts y sistemas:

- **Livestock Management → Sanitary Tracking:** proporciona los datos necesarios para identificar al animal relacionado con el evento sanitario.
- **Veterinary Care → Sanitary Tracking:** solicita la actualización del historial clínico mediante las operaciones expuestas por Sanitary Tracking.
- **Sanitary Tracking → Analytics & Alerts:** expone la información del historial clínico actualizado para apoyar el análisis de tendencias.
- **Sanitary Tracking → Servicio de Notificaciones Push:** solicita el envío de recordatorios y alertas sanitarias hacia los usuarios.

Esta organización permite mantener a **Sanitary Tracking** como propietario de la información sanitaria y del historial clínico, evitando que otros bounded contexts modifiquen directamente sus datos. Al mismo tiempo, la separación por capas reduce el acoplamiento entre las reglas de negocio y los mecanismos técnicos de persistencia, sincronización y notificación.

---

### 2.6.2.6. Bounded Context Software Architecture Code Level Diagrams

En esta sección se presentan los diagramas de nivel de código correspondientes al bounded context **Sanitary Tracking**. Estos diagramas permiten detallar la implementación de los componentes definidos previamente, manteniendo consistencia con las decisiones tomadas durante el Strategic-Level Domain-Driven Design.

Para este bounded context se consideran el **Domain Layer Class Diagram**, encargado de representar las clases y relaciones que conforman el dominio sanitario, y el **Database Design Diagram**, encargado de representar los objetos necesarios para persistir su información.

---

#### 2.6.2.6.1. Bounded Context Domain Layer Class Diagrams

En esta sección se presenta el Class Diagram UML correspondiente al Domain Layer del bounded context **Sanitary Tracking**.

El modelo representa las clases responsables de gestionar el historial clínico y los eventos sanitarios asociados a los animales de Gethics. De acuerdo con las decisiones tomadas en el diseño estratégico, **Sanitary Tracking es el propietario del agregado ClinicalHistory**, garantizando que la información sanitaria sea modificada únicamente mediante las operaciones controladas por este bounded context.

`ClinicalHistory` funciona como Aggregate Root y mantiene los eventos sanitarios correspondientes a un animal. Cada `SanitaryEvent` representa una vacuna, tratamiento, enfermedad, control u otra actividad sanitaria registrada.

Asimismo, `SanitaryCalendar` permite organizar los eventos programados, mientras que `Reminder` representa los recordatorios asociados a actividades próximas. `SanitaryScheduleService` concentra las reglas de dominio necesarias para validar la programación de eventos y generar recordatorios.

Las interfaces de Repository permiten definir las operaciones necesarias para recuperar y persistir la información del dominio sin acoplarla directamente a una tecnología de almacenamiento.

**Sanitary Tracking Domain Layer Class Diagram**

![Sanitary Tracking Domain Layer Class Diagram](images/SanitaryTrackingDomainLayerClassDiagram.png)

Las principales relaciones representadas en el diagrama son:

- Un `ClinicalHistory` pertenece a un único animal identificado mediante `animalId`.
- Un `ClinicalHistory` puede contener cero o múltiples `SanitaryEvent`.
- Cada `SanitaryEvent` pertenece a un único `ClinicalHistory`.
- Un `SanitaryEvent` utiliza `SanitaryEventType`, `SanitaryEventStatus` y `Severity` para mantener valores controlados dentro del dominio.
- Un `SanitaryEvent` puede generar cero o múltiples `Reminder`.
- `SanitaryCalendar` organiza los eventos sanitarios programados.
- `SanitaryScheduleService` aplica reglas relacionadas con la programación de eventos y generación de recordatorios.
- `ClinicalHistoryRepository` define las operaciones de persistencia correspondientes al Aggregate Root.
- `ReminderRepository` define las operaciones necesarias para recuperar y persistir recordatorios.

Esta estructura permite mantener centralizada la información sanitaria dentro de Sanitary Tracking y evita que otros bounded contexts modifiquen directamente el historial clínico. De esta forma, las interacciones provenientes de **Veterinary Care** deben realizarse mediante las operaciones expuestas por Sanitary Tracking, manteniendo el límite de consistencia definido para el contexto.

---

#### 2.6.2.6.2. Bounded Context Database Design Diagram

En esta sección se presenta el Database Design Diagram correspondiente al bounded context **Sanitary Tracking**. El modelo representa las estructuras de persistencia necesarias para almacenar el historial clínico de los animales, los eventos sanitarios registrados y los recordatorios asociados a dichos eventos.

De acuerdo con las decisiones establecidas durante el Strategic-Level Domain-Driven Design, **Sanitary Tracking es el propietario de la información relacionada con el historial clínico**. Por ello, las estructuras de persistencia correspondientes al historial y sus eventos pertenecen exclusivamente a este bounded context.

La identificación del animal se mantiene mediante el atributo `animal_id`, el cual representa una referencia al animal administrado por **Livestock Management**. Esta referencia no se implementa como una Foreign Key hacia una tabla externa, debido a que ambos elementos pertenecen a bounded contexts diferentes. De esta manera se mantiene la independencia y el desacoplamiento entre sus respectivos modelos de persistencia.

**Sanitary Tracking Database Design Diagram**

![Sanitary Tracking Database Design Diagram](images/SanitaryTrackingDatabaseDesign.png)

El diseño de base de datos está conformado por las siguientes entidades:

### Clinical Histories

La tabla `CLINICAL_HISTORIES` representa el historial clínico asociado a cada animal. Cada animal mantiene un único historial dentro del bounded context Sanitary Tracking.

| Campo | Tipo | Restricción | Descripción |
|---|---|---|---|
| `id` | UUID | Primary Key, NOT NULL | Identificador único del historial clínico. |
| `animal_id` | UUID | UNIQUE, NOT NULL | Identificador externo del animal administrado por Livestock Management. |
| `created_at` | DATETIME | NOT NULL | Fecha y hora de creación del historial clínico. |
| `updated_at` | DATETIME | NOT NULL | Fecha y hora de la última actualización del historial. |

El atributo `animal_id` se define como una Alternate Key dentro del modelo para garantizar que un mismo animal no posea más de un historial clínico dentro de Sanitary Tracking.

### Sanitary Events

La tabla `SANITARY_EVENTS` almacena los diferentes eventos sanitarios registrados dentro del historial clínico de un animal. Estos eventos pueden representar vacunaciones, tratamientos, enfermedades, controles médicos u otras actividades relacionadas con la salud del ganado.

| Campo | Tipo | Restricción | Descripción |
|---|---|---|---|
| `id` | UUID | Primary Key, NOT NULL | Identificador único del evento sanitario. |
| `clinical_history_id` | UUID | Foreign Key, NOT NULL | Identificador del historial clínico al que pertenece el evento. |
| `type` | VARCHAR | NOT NULL | Tipo de evento sanitario registrado. |
| `scheduled_date` | DATE | NULL | Fecha programada para la realización del evento, cuando corresponda. |
| `occurred_at` | DATETIME | NULL | Fecha y hora en la que el evento ocurrió o fue realizado. |
| `severity` | VARCHAR | NOT NULL | Nivel de severidad asociado al evento sanitario. |
| `status` | VARCHAR | NOT NULL | Estado actual del evento sanitario. |
| `description` | TEXT | NULL | Información adicional relacionada con el evento. |
| `created_at` | DATETIME | NOT NULL | Fecha y hora de creación del registro. |

El atributo `clinical_history_id` funciona como Foreign Key hacia `CLINICAL_HISTORIES.id`, estableciendo la relación entre cada evento sanitario y su respectivo historial clínico.

### Reminders

La tabla `REMINDERS` almacena los recordatorios generados a partir de eventos sanitarios programados. Estos recordatorios permiten informar al usuario sobre actividades próximas, como vacunaciones, tratamientos o controles sanitarios.

| Campo | Tipo | Restricción | Descripción |
|---|---|---|---|
| `id` | UUID | Primary Key, NOT NULL | Identificador único del recordatorio. |
| `sanitary_event_id` | UUID | Foreign Key, NOT NULL | Identificador del evento sanitario asociado. |
| `scheduled_for` | DATETIME | NOT NULL | Fecha y hora programada para generar el recordatorio. |
| `status` | VARCHAR | NOT NULL | Estado actual del recordatorio. |
| `created_at` | DATETIME | NOT NULL | Fecha y hora de creación del registro. |

El atributo `sanitary_event_id` funciona como Foreign Key hacia `SANITARY_EVENTS.id`, permitiendo relacionar cada recordatorio con el evento sanitario que lo originó.

### Relaciones del modelo

El modelo establece las siguientes relaciones principales:

- Un `CLINICAL_HISTORY` puede contener cero o múltiples `SANITARY_EVENTS`.
- Cada `SANITARY_EVENT` pertenece obligatoriamente a un único `CLINICAL_HISTORY`.
- Un `SANITARY_EVENT` puede generar cero o múltiples `REMINDERS`.
- Cada `REMINDER` pertenece obligatoriamente a un único `SANITARY_EVENT`.
- Cada `CLINICAL_HISTORY` corresponde a un único animal identificado mediante `animal_id`.

Las cardinalidades principales pueden representarse de la siguiente manera:

```text
CLINICAL_HISTORIES  1 ───────── 0..* SANITARY_EVENTS

SANITARY_EVENTS     1 ───────── 0..* REMINDERS
```

---

## 2.6.3. Bounded Context: Veterinary Care

El bounded context **Veterinary Care** se encarga de gestionar la relación profesional entre veterinarios y ganaderos dentro de Gethics, permitiendo administrar asignaciones, consultar los pacientes asociados a cada cliente y realizar el seguimiento clínico de los animales atendidos.

Este bounded context tiene como concepto principal la **Veterinary Assignment**, que representa la relación existente entre un veterinario y un cliente. A partir de dicha asignación, el profesional puede consultar los animales pertenecientes al ganadero y registrar información relacionada con su seguimiento clínico.

Los datos maestros de los animales no son administrados directamente por Veterinary Care, sino que se consultan desde **Livestock Management**, que mantiene la propiedad de dicha información.

De manera similar, Veterinary Care no es propietario del historial clínico. Cuando un veterinario registra información que debe formar parte del historial sanitario de un paciente, la actualización se realiza mediante las operaciones expuestas por **Sanitary Tracking**, evitando el acceso directo a las estructuras internas de dicho bounded context.

Veterinary Care también contempla la recepción de información proveniente de sensores o dispositivos IoT. Debido a que estos dispositivos pueden manejar protocolos y estructuras de datos propias, su integración se realiza mediante una Anti-Corruption Layer que transforma las lecturas externas en conceptos comprensibles por el dominio.

### Class Dictionary

Las principales clases identificadas para el bounded context **Veterinary Care** son las siguientes:

| Clase | Tipo | Propósito | Atributos principales | Métodos principales | Relaciones |
|---|---|---|---|---|---|
| `VeterinaryAssignment` | Aggregate Root | Representa la asignación entre un veterinario y un cliente ganadero. | `id`, `veterinarianId`, `clientId`, `assignedAt`, `status` | `assign()`, `activate()`, `deactivate()` | Relaciona un veterinario con un cliente. |
| `ClinicalFollowUp` | Entity | Representa el seguimiento profesional realizado sobre un paciente. | `id`, `assignmentId`, `patientId`, `notes`, `status`, `updatedAt` | `update()`, `registerObservation()`, `registerAnomaly()` | Pertenece a una asignación y referencia a un paciente. |
| `VeterinaryAssignmentId` | Value Object | Representa el identificador de una asignación veterinaria. | `value` | `validate()` | Identifica a `VeterinaryAssignment`. |
| `VeterinaryAssignmentStatus` | Enumeration | Representa el estado actual de una asignación. | `ACTIVE`, `INACTIVE` | No aplica | Utilizado por `VeterinaryAssignment`. |
| `FollowUpStatus` | Enumeration | Representa el estado del seguimiento clínico. | `NORMAL`, `OBSERVATION`, `ALERT` | No aplica | Utilizado por `ClinicalFollowUp`. |
| `VeterinaryAssignmentRepository` | Repository Interface | Define las operaciones necesarias para persistir y consultar asignaciones veterinarias. | No aplica | `save()`, `findById()`, `findByVeterinarianId()` | Trabaja con `VeterinaryAssignment`. |
| `ClinicalFollowUpRepository` | Repository Interface | Define las operaciones necesarias para almacenar y consultar seguimientos clínicos. | No aplica | `save()`, `findByPatientId()` | Trabaja con `ClinicalFollowUp`. |
| `ClinicalMonitoringService` | Domain Service | Evalúa información clínica y determina si un paciente requiere seguimiento o alerta. | No aplica | `evaluateReading()`, `detectAnomaly()` | Trabaja con `ClinicalFollowUp`. |

---

### 2.6.3.1. Domain Layer

El **Domain Layer** contiene las reglas de negocio relacionadas con la asignación de veterinarios a clientes y el seguimiento profesional de los pacientes atendidos.

El agregado principal del bounded context es `VeterinaryAssignment`, encargado de representar la relación entre un veterinario y un cliente. Una misma persona con rol Veterinarian puede mantener múltiples asignaciones activas, permitiéndole consultar los diferentes ganaderos bajo su atención profesional.

Cada asignación mantiene las referencias necesarias hacia el veterinario y el cliente mediante sus respectivos identificadores. Veterinary Care no mantiene una copia del modelo completo de usuario, debido a que la información de identidad y roles es proporcionada por **Identity & Access**.

La clase `ClinicalFollowUp` representa el seguimiento clínico que el veterinario realiza sobre un paciente. El paciente se identifica mediante `patientId`, correspondiente al identificador del animal administrado por **Livestock Management**. De esta manera, Veterinary Care utiliza al animal como una referencia externa sin apropiarse de su información maestra.

`ClinicalMonitoringService` concentra las reglas necesarias para evaluar observaciones clínicas y las lecturas recibidas desde dispositivos IoT. Cuando una lectura indica una anomalía, el dominio puede actualizar el estado del seguimiento clínico para reflejar que el paciente requiere observación o atención.

El historial clínico completo no forma parte del modelo interno de Veterinary Care. Cuando una observación o atención debe incorporarse al historial sanitario del animal, el bounded context solicita dicha actualización a **Sanitary Tracking**, que mantiene la propiedad del agregado correspondiente.

Las interfaces `VeterinaryAssignmentRepository` y `ClinicalFollowUpRepository` permiten que el Domain Layer defina sus necesidades de persistencia sin depender directamente de una tecnología de almacenamiento específica.

---

### 2.6.3.2. Interface Layer

El **Interface Layer** contiene los componentes responsables de recibir las solicitudes relacionadas con las operaciones del módulo veterinario.

Esta capa permite gestionar las asignaciones veterinarias, consultar los clientes atendidos por un profesional, acceder a los pacientes asociados y registrar actualizaciones relacionadas con su seguimiento clínico.

| Clase | Tipo | Propósito | Operaciones principales |
|---|---|---|---|
| `VeterinaryAssignmentController` | Controller | Gestiona las operaciones relacionadas con asignaciones entre veterinarios y clientes. | `createAssignment()`, `getAssignments()`, `deactivateAssignment()` |
| `VeterinaryClientController` | Controller | Permite consultar los clientes asignados a un veterinario. | `getAssignedClients()`, `getClient()` |
| `VeterinaryPatientController` | Controller | Permite consultar los pacientes pertenecientes a los clientes asignados. | `getPatients()`, `getPatientById()` |
| `ClinicalFollowUpController` | Controller | Gestiona las operaciones relacionadas con el seguimiento clínico de los pacientes. | `getFollowUp()`, `updateFollowUp()`, `registerObservation()` |

Los Controllers reciben las solicitudes provenientes de la aplicación y delegan la ejecución de cada operación hacia los casos de uso definidos en el Application Layer.

La información detallada de los pacientes no se obtiene directamente desde una estructura propia de Veterinary Care. Las solicitudes correspondientes son coordinadas con **Livestock Management**, respetando los límites establecidos entre ambos bounded contexts.

---

### 2.6.3.3. Application Layer

El **Application Layer** coordina los casos de uso relacionados con la atención veterinaria y la interacción con los bounded contexts y servicios externos necesarios.

Esta capa organiza el flujo de ejecución entre los Controllers, los elementos del dominio y las interfaces necesarias para acceder a información administrada por otros contextos.

| Clase | Tipo | Propósito |
|---|---|---|
| `AssignVeterinarianToClientCommandHandler` | Command Handler | Coordina la creación de una nueva asignación entre un veterinario y un cliente. |
| `DeactivateVeterinaryAssignmentCommandHandler` | Command Handler | Coordina la desactivación de una asignación veterinaria. |
| `GetAssignedClientsQueryHandler` | Query Handler | Obtiene los clientes asignados a un veterinario. |
| `GetPatientQueryHandler` | Query Handler | Obtiene la información de un paciente mediante Livestock Management. |
| `GetClientPatientsQueryHandler` | Query Handler | Obtiene los pacientes pertenecientes a un cliente asignado. |
| `UpdateClinicalFollowUpCommandHandler` | Command Handler | Coordina la actualización manual del seguimiento clínico de un paciente. |
| `ProcessIoTReadingCommandHandler` | Command Handler | Procesa una lectura proveniente de un dispositivo IoT y coordina la actualización del seguimiento clínico cuando corresponde. |
| `UpdateClinicalHistoryCommandHandler` | Command Handler | Coordina el envío de una actualización hacia Sanitary Tracking cuando la información debe incorporarse al historial clínico. |

Cuando un veterinario consulta un paciente, el Application Layer verifica la asignación correspondiente y coordina la obtención de la información del animal desde **Livestock Management**.

Cuando el profesional registra una nueva observación, `UpdateClinicalFollowUpCommandHandler` coordina la modificación del seguimiento clínico interno. Si dicha información debe formar parte del historial clínico del animal, se utiliza la integración correspondiente con **Sanitary Tracking**.

De manera similar, cuando se recibe información proveniente de un dispositivo IoT, `ProcessIoTReadingCommandHandler` coordina su procesamiento. Una vez que la lectura ha sido transformada al lenguaje del dominio, `ClinicalMonitoringService` puede evaluar si existe una anomalía y actualizar el seguimiento del paciente.

---

### 2.6.3.4. Infrastructure Layer

El **Infrastructure Layer** contiene las implementaciones técnicas necesarias para persistir la información de Veterinary Care y comunicarse con otros bounded contexts o servicios externos.

Esta capa mantiene aisladas las dependencias técnicas para evitar que los elementos del dominio dependan directamente de APIs, protocolos de comunicación, bases de datos o dispositivos físicos.

| Clase | Tipo | Propósito |
|---|---|---|
| `VeterinaryAssignmentRepositoryImpl` | Repository Implementation | Implementa las operaciones de persistencia de las asignaciones veterinarias. |
| `ClinicalFollowUpRepositoryImpl` | Repository Implementation | Implementa las operaciones de persistencia del seguimiento clínico. |
| `VeterinaryDataSource` | Data Source | Gestiona el acceso a los datos propios del bounded context Veterinary Care. |
| `LivestockManagementClient` | External Context Client | Permite consultar la información de los animales administrados por Livestock Management. |
| `SanitaryTrackingClient` | External Context Client | Permite solicitar actualizaciones del historial clínico administrado por Sanitary Tracking. |
| `IoTDeviceAdapter` | Anti-Corruption Layer Adapter | Transforma las lecturas provenientes de sensores o dispositivos IoT al modelo utilizado por Veterinary Care. |
| `IoTReadingMapper` | Mapper | Traduce las estructuras de datos externas provenientes de dispositivos IoT a conceptos utilizados por el dominio. |

La integración con los sensores o dispositivos IoT se realiza mediante una **Anti-Corruption Layer**. De esta forma, los formatos, protocolos o estructuras propias de cada dispositivo permanecen aislados de los elementos internos del bounded context.

El `IoTDeviceAdapter` recibe la información externa y utiliza `IoTReadingMapper` para convertirla en un formato comprensible para Veterinary Care. Posteriormente, la lectura puede ser evaluada por los servicios del dominio para determinar si existe alguna anomalía que requiera modificar el seguimiento clínico.

Por otro lado, `LivestockManagementClient` permite consultar los datos de los pacientes sin replicar el modelo de Animal dentro de Veterinary Care, mientras que `SanitaryTrackingClient` permite solicitar la actualización controlada del historial clínico sin realizar escrituras directas sobre los datos de Sanitary Tracking.

Esta separación permite que Veterinary Care mantenga su propio modelo centrado en la relación veterinario-cliente-paciente y en el seguimiento profesional, mientras que las responsabilidades correspondientes a los animales y al historial clínico permanecen dentro de sus respectivos bounded contexts.

---


