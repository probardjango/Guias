# Deployment con Heroku & Django

Cómo llevar tu proyecto a producción en Heroku.com.


1. Crear un proyecto de Django.
	El resultado de crear uno nuevo sería parecido a esto:
	```
	src/
	src/manage.py
	src/myproject/
	src/myproject/settings.py

	```
2. Instalar [Heroku toolbelt](https://toolbelt.heroku.com/) para tu sistema operativo.

3. Reubicar `settings.py` en un módulo nuevo para settings.
	- Renombrar `settings.py` a `old_settings.py`; pero NO LO BORREMOS.
	- Crear un módulo nuevo de python (una carpeta) llamado `settings` en el directorio principal del proyecto (root configuration)
	- Añadir 3 archivos nuevos a la carpeta nueva de `settings` y nombrarlos de la siguiente manera:
		- `__init__.py`
		- `local.py`
		- `production.py`
	- Ahora nuestro proyecto debería parecerse a esto:

		```
		src/
		src/manage.py
		src/myproject/
		src/myproject/old_settings.py
		src/myproject/settings/__init__.py
		src/myproject/settings/local.py
		src/myproject/settings/production.py
		```

4. Añadir más contenido:

	Al archivo `__init__.py` escribimos:
	```
	try:	
		from .local import *
	except:
		pass

	from .production import *
	```

	Al archivo `local.py`:
	Copiar/pegar todos los datos de `old_settings.py`

	Al archivo `production.py`:
	Copiar/pegar todos los datos de `old_settings.py`


5. Iniciar un repo nuevo de Git & añadir el archivo `.gitingore` siguiendo los pasos abajo:

	En la raíz de nuestro proyecto hacemos lo siguiente:
	- En línea de comandos, iniciar git con el comando: `git init`
	- Crear el archivo `.gitignore` asegurándonos que sea `.gitignore` tal cual (posiblemente hará falta utilizar algún editor de texto para crear esto). Dejamos este archivo dónde vive el archivo `manage.py`. Al archivo `.gitignore` escribimos lo siguiente:

	```
	#.gitignore
	yourproject/settings/local.py
	```


6. Añadir lo siguiente al archvio `requirements.txt` (o si es necesario, crear el archivo `requirements.txt`):
	```
	dj-database-url==0.4.0
	Django==1.9.7
	gunicorn==19.4.5
	psycopg2==2.6.1
	whitenoise==2.0.6
	```
	Siempre verificando que las versiones de arriba son las correctas.

7. Crear `Procfile`:
	Crear un archivo nuevo con el nombre `Procfile` SIN ninguna extensión (ni `.py`, ni `.txt` ni nada!). Guardarlo dónde vive el archivo `manage.py` y esribir lo siguiente:
	```
	web: gunicorn <tuproyecto>.wsgi 
	```
	***usando el nombre de tu proyecto por supuesto donde arriba ^^ pone <tuproyecto>

8. En el archivo `production.py` cambiar lo siguiente: 

	```
	import dj_database_url

	DEBUG = FALSE
	
	DATABASES = {
		'default': dj_database_url.config()
	}

	SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')
	```
	*dejar `local.py` sin tocar, es para hacer local testing*

9. Añadir/actualizar el proyecto en git:
	```
	$ git status -u #local.py should not be in the results here
	$ git add --all
	$ git commit -m "Preparar para producción"
	```

10. Crear proyecto de Heroku & base de datos

	```
	$ heroku create <yourprojectname>
	$ heroku addons:create heroku-postgresql:hobby-dev #para añadir la base de datos
	$ heroku config:set DISABLE_COLLECTSTATIC=1 #para no tener que configurar los archivos estáticos ahora
	```
	**¡OJO!** Elegir un nombre para el proyecto (dónde pone) `<yourprojectname>` es opcional. Si lo omitimos, Heroku generará un nombre para nuestro proyecto automáticamente (nuestro proyecto en Heroku).

11. Deploy Heroku con este comando:
	```
	git push heroku master
	```

12. Has hecho cambios en tu proyecto? Sería lo más normal así que nos aseguramos de hacer lo siguiente:
**Si vamos a hacer local testing, es necesario garantizar que todos los cambios a settings están aplicados tanto en el archvio para local como en el de producción. Esto es importante para deployment. Hazlo.**


	1. Actualizar requirements.txt si es necesario
	2. Actualizar production.py si es necesario (sin suponer nada, siempre lo comparamos con nuestro local.py)
	3. Commit todos los cambios:
	
		```
		git add --all
		git commit -m "Actualizar x"
		```
	4. Enviar (push) a Heroku:
		```
		git push heroku master
		```




#### Comandos comunes Heroku

`$ heroku restart`: Por si en cualquier momento tenemos que reiniciar nuestra app.

`$ heroku run bash`: Ejecuta el bash de Linux en Heroku para nuestra app

`$ heroku run python manage.py shell`: Ejecuta el shell de Python en Heroku

`$ heroku run python manage.py`: Nos permite ejecutar cualquier comando CLI de Django como `heroku run python manage.py migrate`

`$ heroku logs`: Recupera el historial (logs) de nuestra app; genial por si vemos `Application Errors` en deployment o mientras accediendo a nuestra web.

`$ heroku open`: Abrirá tu proyecto/web.

`$ heroku ps:scale web=X worker=Y`:
	- reemplazar la `X` con el número de web dynos necesarios; cuanto más alto ese número, mayor coste y mejor rendimiento 
	- reemplazar `Y` con el número de trabajdores necesarios; cuanto más alto ese número, mayor coste y mejor rendimiento 
	- Más sobre scaling [aquí](https://devcenter.heroku.com/articles/scaling).

	
Suscríbete a nuestro [Canal de YouTube](https://www.youtube.com/channel/UCLQUXOwRimwewRObZx1v2VA) y únete a nuestra comunidad dónde encontrarás muchos [MÁS CURSOS de DJANGO](http://probardjango.com).


Saludos!


#### Organizado por Team ProbarDjango & CodingForEntrepreneurs