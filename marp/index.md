---
marp: true
theme: default
---
<style>
    :root {
    font-family: 'Roboto Condensed', sans-serif;
    font-weight: initial;
    background-color: #12203d;
    color: #ffff;
}

h1{
    color: #ffffff;
    
}
table{
  color: #000;
}
pre{
  color: #000;
}
</style>
# ¿Qué es Django?

Django, pronunciado "yango", es un marco gratuito y de código abierto que se lanzó por primera vez en 2005. Django recibe su nombre del famoso guitarrista de jazz, Django Reinhardt. A lo largo de los años, se han desarrollado muchos marcos de Python, pero Django se ha convertido en uno de los más populares debido a su flexibilidad y seguridad.

---

Mediante el uso de Django, se pueden desarrollar aplicaciones web complejas y controladas por bases de datos que pueden incluir lo siguiente:

- Machine Learning
- Plataformas de comercio electrónico
- Análisis de datos
- Administración de contenido

---
# Django vrs Flask

| Django	                |            Flask |
|-------------------------|------------------| 
| Marco de pila completo	| Marco web ligero |
| Ideal para aplicaciones controladas por datos |	Ideal para API y servicios existentes|
| Posiblemente más como una curva de aprendizaje |	Posiblemente menos como una curva de aprendizaje |
| Seguridad de serie |	Bibliotecas adicionales necesarias para la seguridad |
| Motor de plantillas HTML personalizado	| Motor de plantillas HTML Jinja |

---
# Introducción a la instalación

Antes de instalar Django, asegúrese en primer lugar de que la versión correcta de Python está instalada para el marco. Para comprobar la versión instalada, vaya al símbolo del sistema y escriba el comando siguiente:
~~~
# Windows
python --version 

# macOS or Linux
python3 --version
~~~

Mi primer proyecto en Django [tutorial](https://github.com/contents-pasantia/content10/blob/main/resource/CreacionProyecto.md)

---
# Conceptos básicos en Django

## Proyectos frente a aplicaciones

|   Project	     |   Aplicación   |
|----------------|---------------------|
|Solo hay un proyecto.	| Puede haber muchas aplicaciones en el proyecto único. |
| Incluye la configuración o aplicaciones necesarias para un sitio web específico. |	Es un componente del sitio web de mayor tamaño. |
| Los proyectos no se usan en otros proyectos. |	Las aplicaciones pueden usarse en varios proyectos. |

---
# Vistas

Las vistas son otro componente de las aplicaciones de Django que cumplen una función específica en la aplicación. Las vistas incluyen todo el código necesario que devolverá una respuesta específica cuando se solicite, como una plantilla o una imagen. Incluso pueden redirigirse a otra página en caso de que la solicitud no siga la lógica necesaria en la función.

---

![img](https://static.platzi.com/media/user_upload/Screenshot%20from%202021-02-21%2013-47-50-65ef7035-94a5-405d-8ccc-420f589efc42.jpg)


---
# Introducción al ORM de Django
Django se creó para aplicaciones controladas por datos, por lo que es natural que tenga un ORM integrado. El ORM de Django resultará natural para los desarrolladores de Python, ya que usa la herencia y la sintaxis de clase con la que ya está familiarizado.

Dado que Django está diseñado para ser un marco web, puede usar la estructura de los modelos que crea para generar automáticamente HTML y formularios. En la mayoría de los casos, Django puede crear dinámicamente el código HTML para permitir al usuario editar los datos sin necesidad de crear el formulario manualmente. Incluso puede administrar las llamadas de base de datos.

---

# Model en Django
 Tutorial [enalce](https://github.com/contents-pasantia/content10/blob/main/resource/Model.md)

---
# Consola interactiva
Tutorial [enalce](https://github.com/contents-pasantia/content10/blob/main/resource/Shell.md)


