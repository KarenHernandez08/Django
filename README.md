# Crea un blog con Django.
___

Desacargar e instalar python [python](https://www.python.org/downloads/)

Crear un entorno de desarrollo virtual en python, una vez dentro de la carpeta del proyecto, ejecutar los siguientes comandos:

```
pip install  virtualenv 

python -m venv my_venv 

```

* **pip install  virtualenv** podemos disponer de diferentes versiones de paquetes dentro de nuetsro proyecto

* **python -m venv my_venv** crea un entorno de desarrollo independiente, esto generara un directorio dentro de mi proyecto con nombre my_env

Para activar el entorno virtual colocar en la terminal ```my_venv\Scripts\activate```, y para desactivarlo solo con la palabra ```deactivate```.

Instalar django mediante pip, podemos especificar la versión que queremos ```pip install Django==4.1.7``` quedara instalado en nuestro entorno virtual.

___

# Crear el primer proyecto.

En la terminal dentro de nuestro proyecto, colocaremos el siguiente comando ```django-admin startproject mysite```, {mysite} es el nombre de mi proyecto.

Se creara la carpeta con diferentes archivos.

![](https://github.com/KarenHernandez08/Django/blob/main/imagenes/mysite.JPG)

* ```manage.py``` es un script que permite interactuar con el proyecto y no es necesario editarlo o modificarlo.
* ```mysite``` es el directorio del proyecto el cual contiene:
    * ```__init__.py```  es un fichero vacio que indica que es un modulo de python.
    * ```settings.py``` es donde se encuentra toda la configuración de nuestro proyecto.
    * ```urls.py``` es donde va a contener todas las urls.
    * ```wsgi.py``` es la configuración para que nuestro proyecto lo podamos desplegar (Web Server Gateway Interface).

El comando ```python manage.py migrate``` genera las migraciones de base de datos aplicada por Django, en la terminal antes de colocar el comando, posicionarnos en la carpeta de nuestro proyecto con ```cd``` en seguida el nombre de la carpeta.


Con Django podemos correr el servidor con este comando ```python manage.py runserver```, nos va a dar las siguientes líneas en la terminal.

```
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
March 17, 2023 - 13:26:59
Django version 4.1.7, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.
```

Vamos a acceder a la url que aparece en el reglon de Starting development server at, después de pegarla en nuestro navegador, veremos algo como la siguiente imagen.

![](https://github.com/KarenHernandez08/Django/blob/main/imagenes/servidor_django.JPG)



La configuración del proyecto que se encuentra en el fichero ```settings.py``` se puede observar más a fondo en el siguiente [link](https://docs.djangoproject.com/en/2.0/ref/settings/)

___

## Crear una aplicación. 

Para crear la aplicación, ejecutar en nuestra terminal el siguiente comando ```python manage.py startapp blog``` {blog} es el nombre de nuestra aplicación.

Dentro de nuestra carpeta del proyecto esta nuestra aplicación blog, se crearon archivos de ``` migrations```  va a contener las migraciones de nuestra aplicación, ``` admin```  que es donde se registran los modelos, ``` apps```  es la configuración principal de la aplicación blog, ``` models```  contiene los modelos de datos de la aplicación, ``` test```  donde se incluyen los test de la aplicación y ``` views```  contiene la lógica de la aplicación.

![](https://github.com/KarenHernandez08/Django/blob/main/imagenes/blog.JPG)

___

# Activar la aplicación.

Nos dirigimos al ```settings.py``` y anotaremos el nombre de nuestra aplicación en la lista de INSTALLED_APPS. 
```python
'blog.apps.BlogConfig',
```

Creamos nuestras migraciones con el comando ```python manage.py makemigrations blog```  {blog} es el nombre de la aplicación.

La salida de la terminal sera algo así 
```
Migrations for 'blog':                               Hub\Django\mysite>
  blog\migrations\0001_initial.py
    - Create model Post
```

___

# Para revisar las migraciones.

Utilizar el sigueinte comando para revisar la salida SQL de la migración anterior ```python manage.py sqlmigrate blog 0001```

___

# Crear un superusuario.

En la terminal colocaremos el siguiente comando ``` python manage.py createsuperuser```, en seguida de darle enter en la consola nos va a pedir un Username, un correo con el que podemos entrar al servidor y la contraseña.

Cuando levantemos de nuevo el servidor, le agregaremos admin/ a la url que nos dara, es donde colocaremos el correo y la contraseña, misma que pusimos en nuesstra terminal

Aquí es donde pondremos el username y la contraseña.

![](https://github.com/KarenHernandez08/Django/blob/main/imagenes/admin.JPG)

Cuando entremos, se vera algo así, es el panel inicial.

![](https://github.com/KarenHernandez08/Django/blob/main/imagenes/login.JPG)

___

# Añadir modelos al sitio de administración.

En nuestro proyecto tenemos un archivo dentro de nuestra aplicación que se llama ```admin.py```  y vamos a estar agregando nuestros modelos, en este caso solo se a creado Post, se vera de la siguiente manera.

```python
from django.contrib import admin
from.models import Post
admin.site.register(Post)
```


Después de agregarlo, vamos a corer nuestro servidor, cuando entremos al admin, ya veremos que está el nuevo modelo Post

## Personalizar la vista de modelos

Quedara de la siguiente manera 

```python
from django.contrib import admin
from.models import Post
# Register your models here.
admin.site.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ('title', 'slug', 'author', 'publish', 'status')
    list_filter = ('status', 'created', 'publish', 'author')
search_fields =('title', 'body')
prepoluted_fields = {'slug': ('title',)}
raw_id_fields = ('author')
date_hierarchy = 'publish'
ordering = ('status', 'publish')
```

___

# Cuándo se evalúan los Querysets

Estos se evaluán en las siguientes situaciones:

* La primera vez que se itera sobre ellos.
* Cuando accedemos a un elementos, las posiciones
+ Cuando se hacen operaciones booleanas, or, and o if.

___

# Crear gestores de modelos

El gestor permitirá recuperar los articulos, definiendo gestores personalizados.

```python
class PublishedManager(models.Manager):
    def get_queryset(self):
        return super (PublishedManager,
                      self).get_queryset()\
                           .filter(status='published')
```

___
# Elaborar vistas 
Una vista de Django recibe una solicitud web y la devuelve como una respuesta web, se crean las aplicaciones de vistas creando las plantillas html, como respuesta HTTP.

en nuestro archivo ```views.py``` vamos a colocar el siguiente código.

```python
from django.shortcuts import render, get_object_or_404
from .models import Post

def post_list(request):
    posts = Post.published.all()
    return render(request,
                  'blog/post/list.html',
                  {'posts':posts})

def post_detail(request, year, month,day, post):
    post = get_object_or_404(Post, slug=post,
                             status= 'published',
                             publish_year=year,
                             publish_month = month,
                             publish_day=day)
    return render (request, 
                   'blog/post/list.html',
                  {'post':post})
```
___

# Añadir url
permiten relacionar url con vistas.

vamos a crear una nueva carpeta cin nombre urls.py dentro de nuestra aplicación y colocaremos el siguiente código.

```python
from django.urls import path
from . import views

app_name='blog'

urlpatterns= [
    path('', views.post_list, name='post_list'),
    path('<int:year>/<int:month>/<int:day>/<slug:post>/',
         views.post_detail,
         name= 'post_detail'),
]
```

Después colocaremos nuetra url de nuestra aplicación en el proyecto 

```python
path('blog/', include('blog.urls',namespace='blog')),
```