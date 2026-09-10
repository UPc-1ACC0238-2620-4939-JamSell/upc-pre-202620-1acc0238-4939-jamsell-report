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


