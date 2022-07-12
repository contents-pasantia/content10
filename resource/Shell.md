# Configuración del shell interactivo
Django incluye un shell interactivo en el que puede ejecutar código de Python en el entorno de Django.

- Vuelva al terminal en Visual Studio Code; para ello, seleccione Ver>Terminal.

- Ejecute el comando siguiente para iniciar el shell:
~~~
python manage.py shell=
~~~

Importe los modelos desde models dentro de dog_shelters:

```python
from dog_shelters.models import Shelter, Dog
```

# Creación y modificación de objetos
Dado que los modelos son clases de Python, las nuevas instancias se crean con la misma sintaxis que usaríamos para crear un objeto. Dado que heredan de Django.models.Model, heredan la funcionalidad del ORM de Django. Esa funcionalidad incluye save, que se usa para guardar el objeto en la base de datos.

1. Cree un nuevo refugio ejecutando el comando de Python siguiente en el shell:
```python
shelter = Shelter(name="Demo shelter", location="Seattle, WA")
shelter.save()
```
La parte save escribirá el objeto en la base de datos. Como lo hemos creado desde cero, ejecutará una instrucción INSERT en la base de datos.

2. Actualice la ubicación del refugio a Redmond, WA; para ello, establezca el campo location llamando a save:
```python
  shelter.location = "Redmond, WA"
  shelter.save()
```
Este comando emitirá una instrucción UPDATE para actualizar el valor en la base de datos.

3. Cree dos nuevos perros para el refugio ejecutando los comandos de Python siguientes en el Shell:
```python
  Dog(name="Sammy", description="Cute black and white dog", shelter=shelter).save()
  Dog(name="Roscoe", description="Lab mix", shelter=shelter).save()
```
Como antes, save inserta el perro. Observe cómo se establece el parámetro shelter en el objeto shelter que hemos creado antes. Django establecerá automáticamente la relación en la base de datos.

Tenga en cuenta también que no hemos configurado una variable local para cada instancia Dog. Dado que no se reutilizarán los objetos, no es necesario establecerlos en una variable.

# Recuperación de objetos
Para recuperar objetos de una base de datos, Django proporciona una propiedad objects en todas las clases Model. La propiedad objects proporciona varias funciones, como all, filter y get.

1. Recupere todos los perros del Refugio de demostración ejecutando el comando siguiente:
```python
  Shelter.dog_set.all()
```
La parte dog_set almacena la lista de todos los perros para un refugio determinado. Django devolverá un objeto QuerySet con los dos perros que hemos creado.
```bash
<QuerySet [<Dog: Sammy>, <Dog: Roscoe>]>
```
2. Recupere el segundo perro usando get tal como se muestra en el comando siguiente:
```python
Dog.objects.get(pk=1)
```
La función get devolverá solo un objeto. Puede pasar parámetros a get para proporcionar una cadena de consulta. Aquí usamos pk, que es una palabra clave especial para indicar la clave principal. El resultado devuelto será Roscoe.

```bash
<Dog: Roscoe>
```
3. Recupere todos los perros del refugio de demostración mediante filter tal como se muestra en el comando siguiente:
```python
Dog.objects.filter(shelter__name='Demo shelter')
```
Al igual que get, filter nos permite pasar una consulta en los parámetros. Observe que podemos usar dos caracteres de subrayado (__) para ir de propiedad en propiedad. Dado que queremos encontrar todos los perros del refugio denominado refugio de demostración, usamos shelter__name para acceder a la propiedad name de shelter. El resultado devuelto será todos los perros, porque solo tenemos un refugio.
```bash
<QuerySet [<Dog: Sammy>, <Dog: Roscoe>]>
```
