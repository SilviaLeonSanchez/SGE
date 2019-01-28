
![Logo Odoo][odoo]

# Indice<a name="indice"/>

* [Crear nueva empresa](#id1)
* [Crear modelo de datos](#id2)
* [Modificar modelo de datos](#id3)
* [Relaciones entre modelos de datos](#id4)
* [Crear nueva vista](#id5)
    * [Árbol](#id5a)
    * [Formulario](#id5b)
* [Crear vista heredada](#id6)
* [Modificar vista](#id7)
* [Crear acción de ventana](#id8)
* [Crear elemento de menú](#id9)
* [Permisos](#id10)
* [Crear grupo de permisos](#id11)
* [Crear un tablero](#id12)
* [Informes](#)

# Contenido

## Crear nueva empresa<a name="id1"/>

Seguir los pasos de la Unidad 3 para:
1. Crear y configurar una nueva empresa con su base de datos
2. Instalar los módulos de la internacionalización al español
3. Establecer el plan contable
4. Instalar los módulos:
  * Ventas
  * Gestión de inventario
  * Gestión de compras
  * Contabilidad y finanzas

[**Indice**](#indice)

## Crear modelo de datos<a name="id2"/>

  `Configuración > Técnico > Estructura de la base de datos > Modelos > Crear`

  ![Captura de pantalla 16][img16]

En `Descripción del modelo` escribir el nombre que sera visible, y tanto en `Modelo` como el nombre del los nuevos campos usar la nomenclatura x_nombreobjeto para indicar que es una entidad creada por nosotros.

[**Indice**](#indice)

## Modificar modelo de datos<a name="id3"/>

1. Acceder a los modelos de datos de la base de datos:

  `Configuración > Técnico > Estructura de la base de datos > Modelos`

![Captura de pantalla 1][img1]

2. Seleccionar el objeto que queremos modificar:

![Captura de pantalla 2][img2]

3. Añadir los campos necesarios:

Pulsar 'Editar' y al final de la lista 'Añadir elemento'.


![Captura de pantalla 3][img3]

Pulsar 'Guardar' en el formulario y 'Guardar' en la lista de objetos. Aparecerá al final de la lista (si hay más de una página comprobar la última).

![Captura de pantalla 4][img4]

[**Indice**](#indice)

## Relaciones entre modelos de datos<a name="id4"/>

## Crear nueva vista<a name="id5"/>

`Configuración > Técnico > Interfaz de usuario > Vistas`

Crear una nueva y como nombre poner el nombre del modelo .form o .tree (el nombre del tipo de vista). Asociar el modelo correcto y crear la vista en xml.

* Etiqueta padre el tipo de vista

```
<tree>
  <field name=""/>
</tree>
```

Si es form se dividen en grupos

```
<form>
  <group>
    <field name=""/>
  </group>
</form>
```
Si hereda de alguna otra vista indicarlo también.

[**Indice**](#indice)

## Crear vista heredada<a name="id6"/>

Se puede obtener el mismo resultado que en el apartado anterior (aunque con otras implicaciones) mediante la herencia.

1. Obtener información de la vista padre

    Vamos a la vista de la cual queremos que herede la nueva vista que vamos a crear.

`Herramientas del desarollador > Editar FormVer`

![Captura de pantalla 12][img12]

2. Definir la nueva vista:

    `Editar > Vistas Heredadas > Añadir un elemento`

![Captura de pantalla 13][img13]

Asegurarnos de que la nueva vista tiene un numero de secuencia menor que la vista de la que hereda, pues se abre por niveles de prioridad (siempre la vista de número menor).

Si refrescamos el navegador y vamos a la vista aparecerá la nueva vista.

![Captura de pantalla 14][img14]

![Captura de pantalla 15][img15]






[**Indice**](#indice)

## Modificar vista<a name="id7"/>

Estando en la vista que queremos modificar pulsar el botón con forma de escarabajo que hay en la barra superior ('Herramientas del desarollador').

![Captura de pantalla 5][img5]

En este caso pulsamos la opción 'Editar formVer'.

`Esta opcion variará sugún el tipo de vista que queramos editar`

![Captura de pantalla 6][img6]

Si en el campo heredar hay otra vista tener cuidado porque a lo mejor queremos modificar esa.
Para ello pulsar el botón que aparece junto al nombre y nos lleva a la vista padre (es la vista padre si no hereda de ninguna otra).

![Captura de pantalla 7][img7]

[**Indice**](#indice)


## Crear acción de ventana<a name="id8"/>

`Configuración > Técnoico > Acciones > Acciones de ventana`

Crear la acción que abrirá la Vistas.

Como nombre de la acción elegir el nombre que aparecerá en el menú.

[**Indice**](#indice)


## Crear elemento de menú<a name="id9"/>

Son jerárquicos, elegir donde irá colocado

Indicar la acción que ejecutará (la que creamos anteriormente)

~ Al buscar busca automaticamente por el campo Name

[**Indice**](#indice)


## Permisos<a name="id10"/>

`Configuración > Usuarios > Grupos`

Se ven los permisos que se pueden asignar, los roles que hay para cada aplicación y que usuarios los tienen.

Son CRUD y se aplican sobre cada objeto. Se utiliza la herencia, de forma que un rol que tenga x permisos, si heredamos tendrá siempre esos x permisos y los adicionales.

'Configuración > Usuarios > Usuarios'

Se asignan de forma jerárquica

En Aplicación (en la ventana del usuario) aparecen las aplicaciones y el rol que tiene el usuario en cada una.

Abajo aparecen las opciones donde elegir el rol o roles que queremos asignarle para cada aplicación.

[**Indice**](#indice)


## Crear un grupo de permisos<a name="id11"/>

'Configuración > Usuarios > Grupos'

Dar todos los permisos de acceso al objeto y la plantilla del mismo, indicar la aplicación sobre la que se aplica el rol.

'Configuración > Usuarios > Usuarios'

Meter al usuario en el grupo de permisos que acabamos de crear.

Para comprobar que el nuevo usuario tiene permisos podemos abrir sesión con el en otro navegador y así no tenemos que cerrar nuestra sesiónl.

[**Indice**](#indice)


## Crear un tablero<a name="id12"/>



[**Indice**](#indice)


[img1]: ./Capturas/Captura_1.png
[img2]: ./Capturas/Captura_2.png
[img3]: ./Capturas/Captura_3.png
[img4]: ./Capturas/Captura_4.png
[img5]: ./Capturas/Captura_5.png
[img6]: ./Capturas/Captura_6.png
[img7]: ./Capturas/Captura_7.png
[img8]: ./Capturas/Captura_8.png
[img9]: ./Capturas/Captura_9.png
[img10]: ./Capturas/Captura_10.png
[img11]: ./Capturas/Captura_11.png
[img12]: ./Capturas/Captura_12.png
[img13]: ./Capturas/Captura_13.png
[img14]: ./Capturas/Captura_14.png
[img15]: ./Capturas/Captura_15.png
[img16]: ./Capturas/Captura_16.png
