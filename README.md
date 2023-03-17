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


