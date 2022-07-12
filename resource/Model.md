# Modelos en Django

Los modelos se encuentran en el corazón de cualquier ORM. Un modelo es una representación de los datos con los que trabajará la aplicación. Puede tratarse de una persona, un producto, una categoría o cualquier otra forma de datos que necesite la aplicación.

## Creación de un modelo
En Django, un modelo es cualquier clase que hereda una colección de funcionalidades de django.models.Model. La colección incluye métodos que permiten consultar la base de datos, crear nuevas entradas y guardar actualizaciones. También puede definir campos, establecer metadatos y establecer relaciones entre los modelos.

Si quiere crear dos modelos, Product y Category, deberá agregar dos clases:
```python
  from django.db import models
  class Product(models.Model):
      # details would go here
      pass

  class Category(models.Model):
      # details would go here
      pass
```

## Agregar métodos
Antes de explicar cómo configurar los datos para el modelo, es importante resaltar el hecho de que un modelo es una clase de Python. Como resultado, puede agregar métodos e invalidar los que proporciona Django.models.Model o los que son inherentes a todos los objetos de Python.

Un método concreto que cabe resaltar es __str__. Este método se usa para mostrar un objeto si no se especifica ningún campo. Si Product tiene un campo name (que veremos en un momento), puede devolverlo como la representación de cadena predeterminada para Product mediante la invalidación de __str__.

```python
  class Product(models.Model):
    name = models.TextField()
    
    def __str__(self):
        return self.name
```
## Adición de campos
Los campos definen la estructura de datos de un modelo. Los campos pueden incluir el nombre de un elemento, una fecha de creación, un precio o cualquier otro dato que el modelo necesite almacenar.

Los diferentes datos tienen diferentes tipos de datos, reglas de validación y otras formas de metadatos. El ORM de Django contiene un amplio conjunto de opciones para configurar los campos de los modelos según sus especificaciones. El ORM es extensible, por lo que puede crear sus propias reglas según sea necesario.

# Definición del tipo de campo
La parte principal de los metadatos de todos los campos es el tipo de datos que almacenará, como una cadena o un número. Los tipos de campo se asignan a un tipo de base de datos y un tipo de control de formularios HTML (como un cuadro de texto o una casilla). Django usa varios tipos de campo, incluidos los siguientes:

- CharField: una línea de texto única.
- TextField: varias líneas de texto.
- BooleanField: una opción booleana true/false.
- DateField: una fecha.
- TimeField: una hora.
- DateTimeField: fecha y hora.
- URLField: una dirección URL.
- IntegerField: un número entero.
- DecimalField: un número decimal de precisión fija.

Documentacion de tipos de campos [tipos](https://docs.djangoproject.com/en/3.1/ref/models/fields/#field-types)
Para agregar campos a nuestras clase Product y Category, podríamos usar el código siguiente:
```python
from django.db import models
class Product(models.Model):
    name = models.TextField()
    price = models.DecimalField()
    creation_date = models.DateField()

class Category(models.Model):
    name = models.TextField()
```
# Opciones de campo
Puede usar las opciones de campo para agregar metadatos para permitir valores NULL o en blanco, o para marcar un campo como único. También puede establecer opciones de validación y proporcionar mensajes personalizados para los errores de validación.

Al igual que con los tipos de campo, las opciones de campo se asignan a la configuración adecuada en la base de datos. Las reglas se aplicarán en los formularios que Django genere automáticamente.

Las opciones de campo se pasan a la función del propio campo. Distintos campos pueden admitir distintas opciones. Algunas de las opciones más comunes son las siguientes:

- null
  - Opción booleana para permitir valores NULL.
  - El valor predeterminado es False.
- blank
  - Opción booleana para permitir valores en blanco.
  - El valor predeterminado es False.
- default
  - Permite la configuración de un valor predeterminado si no se proporciona un valor para el campo.
  - Si quiere establecer el valor predeterminado en una base de datos null, establezca default en None.
- unique
  - Este campo debe contener un valor único.
  - El valor predeterminado es False.
- min_length y max_length
  - Se usa con tipos de cadena para identificar la longitud mínima y máxima de la cadena.
  - El valor predeterminado es None.
- min_value y max_value
  - Se usa con tipos numéricos para identificar los valores mínimo y máximo.
- auto_now y auto_now_add.
  - Se usa con tipos de fecha y hora para indicar si se debe usar la hora actual.
  - auto_nowsiempre establecerá el campo en la hora actual al guardar, lo que resulta útil para los campos last_update.
  - auto_now_add establecerá el campo en la hora actual en el momento de la creación, lo que resulta útil para los campos creation_date.

  Para agregar opciones a nuestros modelos, se puede usar un código parecido al siguiente:

```python
from django.db import models
class Product(models.Model):
    name = models.TextField(max_length=50, min_length=3, unique=True)
    price = models.DecimalField(min_value=0.99, max_value=1000)
    creation_date = models.DateField(auto_now_add=True)

class Category(models.Model):
    name = models.TextField(max_length=50, min_length=3, unique=True)

```

# Claves y relaciones
Una práctica estándar en las bases de datos relacionales es tener una clave principal para cada fila de una tabla, normalmente un entero incrementado automáticamente. El ORM de Django agregará esta clave automáticamente a todos los modelos que cree mediante la adición de un campo denominado id.

Si quiere invalidar este comportamiento, puede establecer el campo que quiere que sea la clave principal. Sin embargo, debe basarse en el campo id de Django en la mayoría de las situaciones.

Las bases de datos relacionales también tienen relaciones entre las tablas. Un producto tiene una categoría, un empleado tiene un administrador y un automóvil tiene un fabricante. El ORM de Django admite todas las relaciones que podría querer crear entre los modelos.

La relación más común es "de uno a varios", técnicamente conocida como relación de clave externa. En una relación de clave externa, varios elementos comparten un solo atributo. Por ejemplo, se agrupan varios productos en una única categoría. Para modelar esta relación, se usa el campo ForeignKey.

Para crear la relación, agregue el campo ForeignKey al objeto secundario. Si los productos se agrupan en categorías, agregue la propiedad category a la clase Product y establezca el tipo en ForeignKey.

Django agrega automáticamente una propiedad al elemento primario para proporcionar acceso a todos los elementos secundarios denominados <child>_set, donde <child> es el nombre del objeto secundario. En nuestro ejemplo, se agregará product_set automáticamente a Category para proporcionar acceso a todos los productos de la categoría.

ForeignKey tiene un parámetro obligatorio, on_delete. Este parámetro indica a Django qué debe hacer si se elimina el elemento primario. Es decir, si eliminamos una categoría, ¿qué debe ocurrir con los productos de esa categoría?

Las dos opciones más comunes son:

**CASCADE**, que eliminará todos los productos si una categoría se elimina en nuestro ejemplo.
**PROTECT**, que devolverá un error si intentamos eliminar una categoría que contiene productos.

Para actualizar nuestro modelo para crear la relación, podemos usar el código siguiente:

```python
from django.db import models
class Product(models.Model):
    name = models.TextField()
    price = models.DecimalField()
    creation_date = models.DateField()
    category = models.ForeignKey(
        'Category', #The name of the model
        on_delete=models.PROTECT
    )

class Category(models.Model):
    name = models.TextField()
    # product_set will be automatically createdfrom django.db import models
class Product(models.Model):
    name = models.TextField()
    price = models.DecimalField()
    creation_date = models.DateField()
    category = models.ForeignKey(
        'Category', #The name of the model
        on_delete=models.PROTECT
    )

class Category(models.Model):
    name = models.TextField()
    # product_set will be automatically created
```

El ORM de Django va más allá de permitirle interactuar con los datos. También puede usarlo para crear y actualizar la base de datos mediante un proceso conocido como migraciones.

# Migraciones
Una migración es una colección de actualizaciones que se realiza en el esquema de una base de datos. Un esquema de base de datos es la definición de la propia base de datos, incluidas todas las tablas y columnas y las relaciones entre esas tablas.

Cuando creamos nuestros modelos y definimos los campos, también definimos las tablas, columnas y relaciones entre esas tablas. Al crear los modelos, hemos creado la definición de esquema.

Las migraciones se usan para crear y actualizar la base de datos a medida que cambian los modelos. Como probablemente sabe, el software cambia constantemente. La forma en que se definen los modelos hoy podría ser diferente de cómo se definen mañana. Las migraciones nos ahorran el proceso de actualizar la base de datos nosotros mismos. Así pues, podemos realizar cambios en los modelos y usar Django para realizar los cambios necesarios en la base de datos.

# Realización de una migración
Para crear una migración, use el comando makemigrations de manage.py. El comando makemigrations usa la lista actual de migraciones para obtener un punto de partida y, después, usa el estado actual de los modelos para determinar la diferencia (los cambios que se deben realizar). Por último, genera el código necesario para actualizar la base de datos. Después de ejecutar makemigrations, muestra el nombre de la migración.
```python
python manage.py makemigrations
```

# Visualización del SQL para la migración
Todas las operaciones que se producen dentro de una base de datos relacional requieren el Lenguaje de consulta estructurado (SQL). Las migraciones de Django generan el SQL adecuado cuando se ejecutan. Aunque puede usar las herramientas de migración para actualizar la base de datos directamente, algunos entornos pueden tener administradores de bases de datos que administren el proceso automáticamente.

Para compilar las instrucciones SQL adecuadas, puede usar sqlmigrate.

```python
python manage.py sqlmigrate <app_label> <migration_name>
```
# Visualización de la lista de migraciones
Si quiere ver todas las migraciones, puede usar showmigrations.
```python
python manage.py showmigrations
```
# Realización de una migración
El comando migrate ejecuta una migración específica o todas las migraciones en la base de datos configurada en settings.py en la raíz de la carpeta del proyecto.

Si abre settings.py, verá una sección DATABASES en la parte inferior. En esta sección se incluye una opción default, que en un nuevo proyecto está configurada para usar SQLite. Puede configurar diferentes cadenas de conexión de base de datos en esta sección según sea necesario.
```python
python manage.py migrate <app_label> <migration_name>
```