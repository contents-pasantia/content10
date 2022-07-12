# Creación de la carpeta del proyecto
Antes de descargar Django, cree un entorno virtual para aislarlo de otras aplicaciones. Si no se crea un entorno virtual y el marco se instala globalmente, podría producirse un conflicto con otras aplicaciones de Python, lo que provocaría un error.

Empiece por crear una carpeta para incluir el proyecto nuevo. También conservará la carpeta para el entorno virtual.

1. Abra un comando o una ventana de terminal.

2. Cree un directorio llamado hello_django y vaya a ese directorio.

~~~
  # Windows
  md hello_django
  cd hello_django

  #macOS or Linux
  mkdir hello_django
  cd hello_django
~~~

3. Use el comando siguiente para abrir la carpeta en Editor de codigo.
 
~~~
  code .
~~~

# Creación y activación del entorno virtual
Usaremos el terminal integrado en Visual Studio Code para evitar el cambio de ventanas mientras ejecutamos los comandos necesarios a fin de crear los recursos que necesitamos. Comenzaremos por la creación de un entorno virtual y su activación.

1. En Visual Studio Code seleccione Terminal>Nuevo terminal.

2. En la ventana de terminal de la parte inferior de Visual Studio  Code, ejecute los comandos siguientes para crear y activar su entorno virtual.

~~~
  # Windows
  python -m venv venv
  .\\venv\\Scripts\\Activate

  # macOS or Linux
  python3 -m venv venv
  source ./venv/bin/activate
~~~

El nombre del entorno virtual estará entre paréntesis, seguido de la ruta en la que se encuentra actualmente. Este símbolo del sistema es donde comenzará a instalar el marco de Django.

# Instalación de Django
La forma más común de administrar paquetes de Python es mediante el uso de un archivo de requisitos o requirements.txt. En el archivo requirements.txt se muestra una lista de los paquetes que utiliza la aplicación. Vamos a crear el archivo requirements.txt, a agregar Django y, después, a instalar la biblioteca.

1. En Visual Studio Code, cree un archivo denominado requirements.txt dentro de la carpeta hello_django.

2. Agregue el texto siguiente a requirements.txt.

~~~
  Django
~~~

3. Dentro de la ventana de terminal, ejecute el comando siguiente para instalar Django y cualquier otro paquete que figure en requirements.txt.

~~~
pip install -r requirements.txt
~~~

Con este comando, el marco de Django comenzará a descargarse. Una vez finalizada la descarga, podemos empezar a desarrollar la aplicación.

# Creación de un proyecto con django-admin

Tal como se ha resaltado anteriormente, un proyecto de Django es el contenedor para todo el proyecto y cualquier aplicación que vayamos a crear. Vamos a crear nuestro proyecto.

Ejecute el comando siguiente dentro de la ventana del terminal en Visual Studio Code:

~~~
  django-admin startproject helloproject .
~~~

" El punto final del comando es importante. Indica a django-admin que use la carpeta actual. Si deja fuera este punto final, se creará un subdirectorio adicional. "

Después de ejecutar el comando anterior, el proyecto nuevo debe estar ahora en el directorio elegido. En esta instancia, verá una carpeta nueva denominada helloproject.

# Exploración de la estructura del proyecto
Ahora que se ha creado el proyecto de Django, echemos un vistazo a la estructura para ver lo que se ha incluido en él.

~~~
manage.py
helloproject/
    __init__.py
    settings.py
    urls.py
    asgi.py
    wsgi.py
~~~

- La utilidad de la línea de comandos manage.py se crea en cada proyecto de Django. Tiene la misma función que django-admin. En el ejemplo siguiente se muestra cómo se podría usar si estuviera en la carpeta del proyecto y quisiera ver los subcomandos disponibles.

~~~
python manage.py help
~~~

- **helloproject** se considera como el paquete de Python para el proyecto.

- **init.py** es un archivo vacío que funciona para indicar a Python que este directorio se debe considerar como un paquete.

- **settings.py** incluye todos los valores o configuraciones.

- **urls.py** incluye las direcciones URL del proyecto.

- **asgi.py y wsgi.py** sirven como punto de entrada para los servidores web en función del tipo de servidor implementado.

# Ejecución del proyecto
Ahora que Django está instalado, se ha creado un proyecto y hemos examinado su estructura, es el momento de asegurarse de que nuestro proyecto funciona correctamente.

1. Dentro de la ventana del terminal en Visual Studio Code, escriba el código siguiente para iniciar el servidor.

```bash
python manage.py runserver
```
El proyecto realiza comprobaciones del sistema e inicia el servidor de desarrollo. Copie y pegue la dirección URL del servidor de desarrollo, que debe ser http://localhost:8000, en el explorador que prefiera. Debería ver una página Congratulations (Enhorabuena) en Django con una imagen de un cohete despegando.

2. Detenga el servidor temporalmente, ya que será necesario volver a configurar nuestro proyecto. Dentro de la ventana del terminal, seleccione Ctrl+C.

# Creación de la aplicación Hola mundo

Hemos descubierto los aspectos básicos sobre el marco de Django y examinado la estructura de carpetas de nuestro proyecto. Ahora es el momento de crear nuestra primera aplicación. Esta aplicación ¡Hola mundo! permitirá comprender cómo se crean las aplicaciones y cómo funcionan al unísono con el proyecto de Django.

Desde la ventana del terminal, ejecute el comando siguiente para crear la aplicación.

~~~
python manage.py startapp hello_world
~~~

Con este comando, Django crea las carpetas y los archivos necesarios, y la estructura siguiente ahora debería estar visible.

~~~
hello_world/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
~~~

# Registro de la aplicación en el proyecto
Dado que las aplicaciones y los proyectos son independientes en Django, debe registrar la aplicación en el proyecto. Para ello, se actualiza la variable INSTALLED_APPS dentro de settings.py en el proyecto y se agrega una referencia a la clase config para la aplicación. La clase config se encuentra en apps.py y tiene el mismo nombre que el proyecto. En nuestro ejemplo, la clase se llamará HelloWorldConfig.

1. Dentro de helloproject, abra settings.py.

2. Busque la lista INSTALLED_APPS, que debe estar en la línea 33.

3. Agregue lo siguiente al final de la lista, entre corchetes ([ ]):

```python
  'hello_world.apps.HelloWorldConfig',
```
4. La lista INSTALLED_APPS actualizada debería ser similar a la siguiente imagen:
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'hello_world.apps.HelloWorldConfig',
]
```
5. Guarde todos los archivos; para ello, seleccione Archivo>Guardar todo.

Enhorabuena. Ahora ha creado su primer proyecto y aplicación de Django. Lo siguiente es crear una ruta de acceso y una vista para agregar algunas funcionalidades.

# Descripción de las rutas y las vistas.

Las vistas y rutas (o rutas) son fundamentales para cualquier marco web. Se usan para determinar qué información se debe mostrar al usuario y cómo accederá a ella. En Django también se usan estos conceptos.

Rutas de acceso
Todas las aplicaciones permiten a los usuarios ejecutar métodos o funciones diferentes mediante determinados mecanismos. Esta acción podría pulsar un botón de una aplicación móvil o ejecutar un comando desde la línea de comandos.

Para realizar solicitudes de usuario en una aplicación web, haga lo siguiente:

- Navegar a distintas direcciones URL.
- Escribir en ella.
- Seleccionar un vínculo.
- Pulsar un botón.
- Una ruta indica a Django si el usuario realiza una solicitud para que una dirección URL, o ruta, determinada sepa qué función se va a ejecutar.

Una dirección URL como https://adventure-works.com/about podría ejecutar una función denominada about. La dirección URL https://adventure-works.com/login podría ejecutar una función denominada authenticate.

Las rutas en Django se registran mediante la configuración de urlpatterns. Estos patrones identifican qué debe buscar Django en la dirección URL que el usuario solicita y determinan la función que debe controlar la solicitud. Estos patrones se recopilan en un módulo que Django denomina URLconf.

# Vistas
Las vistas determinan qué información se debe devolver al usuario. Las vistas son funciones o clases que ejecutan código en respuesta a la solicitud del usuario. Devuelven HTML u otros tipos de respuestas, como un error 404.

# Creación de rutas y vistas

Una vez creada la estructura de la aplicación, podemos empezar a seguir los pasos para agregar nuestro propio código personalizado. Crearemos una vista y, después, registraremos una ruta dentro de un elemento URLconf.

# Crear la vista
1. Dentro de Visual Studio Code, abra views.py, que estará dentro de hello_world.

2. Reemplace el código que hay dentro de views.py por el siguiente:

```python
from django.shortcuts import render
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world!")
```
La función auxiliar HttpResponse permite devolver texto u otros tipos primitivos al autor de la llamada.

# Creación de la ruta
Una vez creada la vista, el paso siguiente consiste en asignarla a la dirección URL o ruta adecuada.

1. Dentro de Visual Studio Code, cree un archivo en hello_world denominado urls.py.

2. Agregue el código siguiente al archivo urls.py nuevo.

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

La parte más importante de este código es la tupla urlpatterns. Esta tupla es donde las vistas y las direcciones URL están conectadas o asignadas. Tal como se puede ver, hemos importado nuestro archivo views.py para poder usarlo en la línea urlpatterns.

# Registro de nuestro elemento URLconf con el proyecto
Nuestro elemento URLconf recientemente creado está dentro de nuestra aplicación hello_world. Dado que el proyecto controla todas las solicitudes de los usuarios, es necesario registrar nuestro elemento URLconf en el archivo principal urls.py, que está dentro de helloproject.

1. Abra urls.py dentro de helloproject.

2. Anote al principio los comentarios del documento. Estos comentarios explican cómo se pueden registrar módulos de URLconf nuevos.

3. Reemplace la línea que lee from django.urls import path con la instrucción import siguiente para agregar include y path.

```python
  from django.urls import include, path
```
El uso de include nos permite importar módulos de URLconf, y path se usa para identificar la raíz de URLconf.

4. Dentro de la lista, debajo de la línea que lee urlpatterns = [, agregue el código siguiente:

```python
path('', include('hello_world.urls')),
```
Este código registra nuestro elemento URLconf.

El código que se encuentra debajo del comentario del documento ahora debe tener el aspecto siguiente:
```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('', include('hello_world.urls')),
    path('admin/', admin.site.urls),
]
```

Ejecución de la primera aplicación
La estructura se ha completado, se han agregado vistas y se han asignado las direcciones URL. Ahora es el momento de ejecutar la aplicación.

Dentro de la ventana del terminal en Visual Studio Code, ejecute el comando siguiente para iniciar de nuevo el servidor.
```python
  python manage.py runserver
```
Abra la dirección URL en su explorador favorito:

http://localhost:8000/

Debería ver ¡Hola mundo! en la ventana del explorador. ¡Enhorabuena! Ha creado su primera aplicación de Django