# Curso de Django avanzado con platzi
En este curso vamos a ver la ruta de un backend full stack developer cuyo lenguaje principal es python.

## Objetivos
* Conocer más a fondo los temas conceptuales y no técnicos del desarrollo de una aplicación
* Identificar los requerimientos de la aplicación perfectamente

## Pre-requisitos
* Python
* Django
* Docker
* Fundamentos de ingeniría de software
* Desarrollo web online 

## Proyecto  
El proyecto que se va a desarrollar va a ser una aplicación llamada Comparte Ride, es una aplicación desarrollada hace algunos años por el profesor Pablo Trinidad y nos va a mostrar como es la implementación de este proyecto en la vida real.

### Identificando los modelos   
#### Usuarios  
* *Base*
	* Email
	* Username
	* Phone number
	* First name
	* Last Name
* *Perfil*
	* User (PK)
	* Picture
	* Biography
	* Rides tomados
	* Rides ofrecidos
* *Miembro*
	* User(PK)/Profile(PK)
	* Circulo(PK)
	* Administrador del circulo(BOOL)
	* Invitaciones(Usadas/restantes)
	* Quien lo invitó
	* Rides tomados
	* Rides ofrecidos

#### Circulo  
* *Circulo*
	* Nombre
	* Slug name
	* About
	* miembros
	* Rides tomados
	* Rides ofrecidos
	* Circulo oficial
	* Circulo público
	* Limite de miembros
* *Invitación*
	* código
	* circulo
	* quien invita
	* quien la uso
	* cuando se usó

#### Rides  
* *Ride*
	* quien lo ofrecio
	* donde se ofreció
	* cuando donde
	* asientos disponibles
	* comentarios adicionales
	* calificación (promedio)
	* activo
* *Calificación*
	* ride(pk)
	* circulo(pk)
	* quien califica
	* a quien califica
	* calificacion(1-5)

### Funcionalidades
#### Usuarios  
* Signup
* Log in
* detalle de usuario
* actualización de datos
	* perfil
	* base

#### Circulos
* listar todos los circulos (incluye filtrado y busqueda)
* crear un circulo
* detalle del circulo
* actualizar datos
* listar miembros de un circulo
* unirse a un cirulo (invitacion)
* detalles de un miembro
* eliminar a un miembro
* obtener código de invitación

#### Rides
* listar rides (Filtrado y búsqueda)
* crear un ride en un circulo
* unirte a un ride
* calificar un ride
* mandar recordatorio a los usuarios para calificar 

#### Bonus
* Crear un admin-action que descargue a los usuarios con mejores calificaciones en un CSV
* crear una tarea asincrona que envíe reportes mensuales a los admins
* deployment AWS
* configuración de dominio
* setup de sertificado SSL

## Contenido
Vamos a hacer una API con Django REST framework 
* arquitectura de una aplicación
* buenas prácticas
* codebase setup
* diseño de una API REST
* Modelos avanzados
* Django REST framework
* autenticacion y permisos
* vistas avanzadas
* test-driven development
* tareas administrativas
* tareas asincronas y calendarizadas
* deployment

## Recomendaciones
* Perderle el miedo al inglés
* participar activamente en las discusiones
* leer hasta el cansancio
* practica, practica y practica
* se paciente

## The twelve-factor app
es un conjunto de principios reunido por gente que se dedica a construir Software As A Service, principalmente personas de heroku. Los objetivos de esto principios son:  
* Formas declarativas de configuracion
* contrato claro con el OS
* listas para lanzar
* minimizar la diferencia entre entornos de desarrollo
* facil de escalar

### Principios
1. Codebase
2. Dependencies
3. Configuration
4. backing services
5. Build, release, run
6. Processes
7. Port binding
8. Concurrency
9. Disposability
10. Dev/prod parity
11. Logs
12. Admin processes

## Arquitectura de una aplicación
Es el conjunto de planos sobre lo que está pasando y se definen los componentes de nuestra aplicación y la relación entre estas.  
Son las desiciones sobre estructura fundamental de la aplicación las cualtes cuesta mucho cambiar una vez que se hace la implementación.  
Como desarrolladores nuestro trabajo no termina simplemte en la aplicación, sino que existen un montón de cosas que hay que saber y para ello existe un camino a seguir para ello. Podemos encontrar en [este proyecto](https://github.com/kamranahmedse/developer-roadmap) todo lo que debemos saber para hacer un excelente trabajo.  

### Back-end
* Servidor
* Aplicación
* Base de datos

### SOA
* Autocontenida
* es una caja negra para los consumidores
* Representa una actividad del negocio muy espesífica

### Web services
es la forma en la cual son accesibles los servicios que prestamos.  
* SOAP el servicio de mensajeria de estados unido tiene apis montadas en soap y puede ser consultado [aquí](https://www.usps.com/business/web-tools-apis/)
* RESTful HTTP facebook tiene muy buena docuemtnación de esto [aqui](https://developers.facebook.com/docs/graph-api/)
* GraphQL.

## Codebase: Setting modular
Para generar una aplicación altamente portable se va a utilizar docker ya que cuenta con grandes características que lo hacen muy facil de exportar y vamos a montar 4 servicios en este que serán:  
* Django :8000
* PostgreSQL :5432
* Redis :6379
* Celery :5555

