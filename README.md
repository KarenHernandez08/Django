# Crea un blog con Django 
___

Desacargar e instalar python [python](https://www.python.org/downloads/)

Crear un entorno de desarrollo virtual en python, una vez dentro de la carpeta del proyecto, ejecutar los siguientes comandos

```
pip install  virtualenv 

python -m venv my_venv 

```

* **pip install  virtualenv** podemos disponer de diferentes versiones de paquetes dentro de nuetsro proyecto

* **python -m venv my_venv** crea un entorno de desarrollo independiente, esto generara un directorio dentro de mi proyecto con nombre my_env

Para activar el entorno virtual colocar en la terminal ```my_venv\Scripts\activate```, y para desactivarlo solo con la palabra ```deactivate```

Instalar django mediante pip, podemos especificar la versión que queremos ```pip install Django==4.1.7``` quedara instalado en nuestro entorno virtual

___

# Crear el primer proyecto.

En la terminal dentro de nuestro proyecto, colocaremos el siguiente comando ```django-admin startproject mysite```, {mysite} es el nombre de mi proyecto.

Se creara la carpeta con diferentes archivos.
