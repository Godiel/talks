PARTE 1: VISTA BASICA

crear proyecto y aplicacion:

django-admin.py startproject noticias
python manage.py startapp sitio

editar settings:

path base de datos y cliente
agregar aplicacion

editar models:

class Noticia(models.Model):
    titulo = models.CharField(max_length=50)
    texto = models.CharField(max_length=200)
    fecha = models.DateTimeField()
    archivada = models.BooleanField()

crear directorio de templates
crear template /noticias/sitio/templates/inicio.html:

<h1>Noticias.com</h1>
<p>bienvenido!</p>

editar views:

from django.shortcuts import render_to_response

def inicio(request):
    return render_to_response('inicio.html', {})

editar urls:

    (r'^inicio/$', 'sitio.views.inicio'),

levantar servidor y probar:

python manage.py runserver
http://localhost:8000/inicio





PARTE 2: MODELOS

editar views:

from sitio.models import Noticia
from datetime import datetime

    nueva = Noticia()
    nueva.titulo = 'entro alguien!'
    nueva.texto = 'acaba de entrar alguien al sitio'
    nueva.fecha = datetime.now()
    nueva.save()

sincronizar base de datos:

python manage.py syncdb

levantar sitio y probar muchas veces:

python manage.py runserver
http://localhost:8000/inicio

modificar template inicio:

{% for noticia in lista_noticias %}
    <h3>{{ noticia.fecha }} {{ noticia.titulo }}</h3>
    <p>{{ noticia.texto }}</p>
{% endfor %}

modificar views:

    noticias = Noticia.objects.all()
   
    return render_to_response('inicio.html', {'lista_noticias': noticias})

levantar servidor y probar:

python manage.py runserver
http://localhost:8000/inicio





PARTE 3: Admin

modificar settings:

    'django.contrib.admin',

modificar urls:

descomentar las lineas del admin

crear admin.py:

from sitio.models import Noticia
from django.contrib import admin

admin.site.register(Noticia)

sincronizar la base de datos:

python manage.py syncdb

levantar sitio y probar:

python manage.py runserver
http://localhost:8000/admin
mostrar

customizar el admin.py:

class AdminNoticia(admin.ModelAdmin):
    list_display = ('id', 'titulo', 'fecha',)
    list_filter = ('archivada', 'fecha')
    search_fields = ('texto', )
    date_hierarchy = 'fecha'

admin.site.register(Noticia, AdminNoticia)

python manage.py runserver
http://localhost:8000/admin
mostrar




PARTE 4: error

hacer un error, levantar el server y ver que pasa
