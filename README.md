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

## Comandos de docker
~~~sh
docker run [imagen] #Corre una imagen de dockerhub
docker-compose -f local.yml build # contrulle nuestro contenedor teniendo en cuenta las especificaciones que le hemos dado en el archivo local.yml descargando todo lo que sea necesario
docker-compose -f local.yml up #levanta nuestro contenedor utilizando el archivo local.yml
docker-compose -f local.yml ps #muestra los servicios que corren dentro de nuestro contenedor
docker-compose -f local.yml down #baja la instancia que habiamos creado con este archi .yml
export COMPOSE-FILE=local.yml #crea una variable de entorno para no tener que andar escribiendo el nombre del archivo todo el tiempo.
docker container
docer images
docker volume 
docker network 
ls rm prune -a -q
~~~

### Comandos de administración
~~~sh
docker-compose run --rm django COMMAND #Ejecuta un comando de django en el contenedor que tenemos encendido
docker-compose run --rm django \
	python manage.py createsuperuser #por ejemplo
~~~

### Habilitar el debuger
~~~sh
docker-compose up
docker-compose ps
docker rm -f <ID>
docker-compose run --rm --service-ports django 
~~~

## cookiecutter
Es una herramienta que me permite generar plantillas de proyectos de django para reducir aun más las tareas repetitivas y poderme concetrar en el código a maypr profundidad.  
[Aquí](https://cookiecutter-django.readthedocs.io/en/latest/) podrás encontrar un enlace a la página y empezar a echarle un ojo.

## Herencia de Modelos en Django
Para crear modelos que contengan información general y despues heredarlos en nuestro modelos reales será necesario crear un modelo con la información que requerimos y en la clase META le decimos que es abstracto.  
~~~py
from django.db import models

class CommonInfo(models.Model):
	name = models.CharField(max_length=255)
	age = models.PositiveIntegerField()

	class Meta:
		abstract = True

class Student(CommonInfo):
	home_group = models.CharField(max_length=5)
~~~

## Proxy models
Los modelos proxy me ayudan a agregar funcionalidad extra a las tablas ya existentes sin crear una tabla nueva.  
~~~py
from django.db import models

class User(models.Model):
	name = models.CharField(max_length=255)
	age = models.PositiveIntegerField()


class Profile(User):
	is_hunter = models.BooleanField(default=False)

	class Meta:
		proxy = True
~~~

## Creando un User personalizado
Django nos permite heredar de un modelo llamado AbstractUser, que como su nombre lo indica es un modelo abstracto que no va a generar un cambio en la base de datos pero nos va a servir como un molde para personalizar nuestro usuario y hacer cosas como agregarle los campos que deseemos, generar el log in con el correo en vez del username, agregarle roles, etc!  
~~~py
from django.db import models
from django. contrib.auth.models import AbstractUser
from django.core.validators import RegexValidator

class User(models.Model, AbstractUser):
	email = models.EmailField(
		'email address',
		unique=True,
		error_message={
			'unique'='Email already exist'
		}
	)

	#creamos un validador para que el numero de telefono ingresado 
	#cumpla con las caracteristicas especificadas
	phone_regex = RegexValidator(
		regex=r'\+?1?\d{9-15}$',
		message="el numero telefonico debe estar ingresado en el formato +12345689"
	)
	phone_number = models.CharField(validators=[phone_regex], max_length=17, blank=True)

	USERNAME_FIELD = "email"
	REQUIRE_FIELDS = ['username','first_name','last_name']

	is_client = models.BooleanField(
		'client status',
		default=True,
		help_text = (
			'Ayuda a distinguir los usuarios y mejorar las busquedas',
			'Los clientes son el principal tipo de usuarios'
		)
	)

	is_verified = models.BooleanField(
		'verified email status',
		default=False,
		help_text =('se pone verdader cuando el usuario ha verificado su email')
	)

	def __str__(self):
		return self.username

	def get_short_name(self):
		return self.username
~~~

Y en el settings.py hay que indicar que vamos a utilizar un modelo custom para el usuario.  
~~~py
#wsgi
AUTH_USER_MODEL='users.user'
#apps
~~~

### Modelo de perfiles
Ahora debemos hacer un modelo para el perfil pero se puede poner muy extenso y para ello vamos a crear un modulo (un folder) que va a contener nuestros archivos de usuarios y perfiles 

### modelo de circulos
Para poder empezar a construir nuestra API debemos tener la forma en la cual va a interactuar nuestro front con el back

#### Ejecutar una consola interactiva con super poderes
~~~sh
docker-compose -f local.yml run --rm django python manage.py shell_plus
~~~

Función para cargar archivos desde un csv  
~~~py
import csv

defimport_csv(filename): 
    with open(filename) as csvarchivo:
        entrada=csv.DictReader(csvarchivo)
        for reg in entrada:
            if int(reg['members_limit'])!=0:
                Circle.objects.create( 
                name=reg['name'], 
                slug_name=reg['slug_name'], 
                is_public=reg['is_public'], 
                verifed=reg['verifed'], 
                is_limited=1, 
                members_limit=reg['members_limit']) 
                print(reg['name']) 
            else:
                Circle.objects.create( 
                name=reg['name'], 
                slug_name=reg['slug_name'], 
                is_public=reg['is_public'], 
                verifed=reg['verifed'],  
                members_limit=reg['members_limit']) 
                print(reg['name'])
~~~

## Django REST Framework
Para dar respuestas en formato json podemos hacerlo utilizando el Django normalito, de toda la vida, y damos respuestas con la clase JsonResponse.

para instalar django REST framework lo hacemos utilizando el manejador de paquetes de python  
~~~sh
pip install djangorestframework
~~~






## Referencias
* [Documentación de Django](https://docs.djangoproject.com/es/2.2/) 
* [Github de Django](https://github.com/django/django) Ideal para poder examinar cada una de las clases y visualizar los metodos que contienen
* [Django REST framework](https://www.django-rest-framework.org/)
* [github DRF](https://www.github.com/encode/django-rest-framework)