
![Logo Odoo][odoo]

# Indice<a name="indice"/>

* [Crear nueva empresa](#id1)
* [Crear modelo de datos](#id2)
* [Modificar modelo de datos](#id3)
* [Relaciones entre modelos de datos](#id4)
* [Crear nueva vista](#id5)
* [Crear vista heredada](#id6)
* [Modificar vista](#id7)
* [Crear acción de ventana](#id8)
* [Modificar acción de ventana](#id8b)
* [Crear elemento de menú](#id9)
* [Crear un usuario](#id10)
* [Permisos](#id11)
* [Crear grupo de permisos](#id12)
* [Crear un tablero](#id13)
* [Informes](#id14)


# Contenido

Para realizar la mayoría de los cambios es necesario activar las opciones de desarrollador desde el menu de Configuración.

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

En 'Descripción del modelo' escribir el nombre que sera visible, y tanto en 'Modelo' como en el nombre del los nuevos campos usar la nomenclatura x_nombreobjeto para indicar que es una entidad creada por nosotros.

* Implementar el modelo:

El nuevo modelo necesitará tener [nuevas vistas](#id5) para visualizar e introducir los nuevos datos o [modificar las vistas existentes](#id7).

También es posible que requieran [elementos de menú](#id9) para acceder a las vistas del nuevo modelo.

Para que lo haga Odoo automaticamente solo hay que pinchar en 'Crear un menú' en la creación del modelo, pero es bastante limitado.

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

Pulsar 'Guardar' en el formulario y 'Guardar' en la lista de objetos.

![Captura de pantalla 4][img4]

Aparecerá al final de la lista (si hay más de una página comprobar la última).

[**Indice**](#indice)


## Relaciones entre modelos de datos<a name="id4"/>

Pueden ser de uno a muchos (one2many), muchos a uno (many2one) o muchos a muchos (many2many).

Primero tenemos que conocer el nombre del otro modelo con el que queremos establecer la relación.

`Configuración > Técnico > Estructura de la base de datos > Modelos`

O si no sabemos exactamente cual es podemos acceder a él editando cualquiera de las vistas que lo usen, ya que aparecerá en el campo 'Modelo'.

[Modificar el modelo](#id3) añadiendo un campo que recoja la información del otro modelo con el que queremos establecer la relación.

En 'Tipo de campo' indicar la relación que hay y en 'Relación del objeto' el nombre del otro modelo.

[Modificar las vistas](#id7) asociadas con este modelo para que reflejen el nuevo campo.

Al incluir el nuevo campo en las vistas, estas se adaptan según el tipo de relación y el modelo (ofreciendo un desplegable o lo que haga falta para recoger la nueva información).

[**Indice**](#indice)


## Crear nueva vista<a name="id5"/>

Hay varios tipos de vistas, entre otros:

* Kanban
----CAPTURA

* Árbol
----CAPTURA

* Formulario
----CAPTURA

Para ver todas las vistas disponibles:

`Configuración > Técnico > Interfaz de usuario > Vistas`

----CAPTURA

Crear una nueva y poner la extensión adecuada al nombre (.form, .tree, etc según el tipo de vista). Dejar 'Vista heredada' en blanco y en 'Ver modo heredado' elegir Vista base.

----CAPTURA

Asociar en 'Modelo' el objeto de la base de datos sobre el que actúa y crear el xml.

* Arbol:

```
<tree string="Etiqueta modelo">
    <field name="nombre_campo"/>
</tree>
```

* Formulario:

```
<form string="Etiqueta modelo">
    <group>
        <field name="nombre_campo"/>
    </group>
</form>
```
Se divide en grupos.

Para que la nueva vista sea visible desde algun lugar tendremos que asociarla a alguna [Acción de ventana](#id8).

[**Indice**](#indice)


## Crear vista heredada<a name="id6"/>

1. Obtener información de la vista padre

Vamos a la vista de la cual queremos que herede la nueva vista que vamos a crear.

`Herramientas del desarollador > Editar FormVer`

![Captura de pantalla 12][img12]


2. Definir la nueva vista:

`Editar > Vistas Heredadas > Añadir un elemento`

![Captura de pantalla 13][img13]

Nombrarla manteniendo el nombre de la vista padre y añadiendo un sufijo que defina la vista. Añadir el codigo xml, usando xpath para hacer referencia a elementos de la vista padre, que podremos usar como referencia, modificar o incluso invisivilizar.

Asegurarnos de que la nueva vista tiene un numero de secuencia menor que la vista de la que hereda, pues se abre por niveles de prioridad (siempre la vista de número menor).

No obstante, en las [Acciones de ventana](#id8b) podemos indicar que vista queremos que se muestre de forma especifica. Por eso puede que no se vea la nueva vista aunque tenga secuencia menor si hay otra vista seleccionada para esa acción.

Si refrescamos el navegador y vamos a la vista aparecerán los nuevos elementos.

![Captura de pantalla 14][img14]

[**Indice**](#indice)


## Modificar vista<a name="id7"/>

Estando en la vista que queremos modificar pulsar el botón con forma de escarabajo que hay en la barra superior:

`Herramientas del desarollador > Editar XXXXVer`

![Captura de pantalla 5][img5]

Esta opción variará según el tipo de vista que queramos editar.

![Captura de pantalla 6][img6]

Si en el campo 'Vista heredada' hay otra vista tener cuidado porque a lo mejor lo que queremos modificar se encuentra en la vista padre.

Para ello pulsar el botón que aparece junto al nombre de la vista heredada y nos lleva a su vista padre.

![Captura de pantalla 7][img7]

Hay que tener cuidado al modificar vistas que no hayan sido creadas por nosotros, o que tengan herencia por que podrían dar errores inesperados.

No obstante, se pueden ocultar elementos de la vista añadiendo el atributo invisible = "1" a la etiqueta del elemento o añadir elementos nuevos sin problemas.

Es importante también asignar las vistas durante la creación de [elementos de menú](#id9) para que al pinchar en ellos aparezcan las vistas adecuadas.

[**Indice**](#indice)


## Crear acción de ventana<a name="id8"/>

`Configuración > Técnico > Acciones > Acciones de ventana > Crear`

Servirá para enlazar las vistas que indiquemos con cada elemento de menú que utilice esta acción.

----CAPTURA

Elegir el 'Nombre' de la acción. En 'ID externo objeto' indicar el modelo sobre el que actuará y en 'Modo de vista' enumerar los tipos de vista que tenemos disponibles para esa acción ordenados por prioridad.

Podemos ahora asociar esta nueva acción a algún [elemento de menú](#id9).

[**Indice**](#indice)


## Modificar acción de Ventana<a name="id8b"/>

Podemos modificar la acción que hace que al pinchar un elemento de menú se abra una vista, para conseguir que se abra otra.

Accediendo desde el propio elemento de menú:

`Configuración > Técnico > Interfaz de usuario > Elementos menú > Acción`

----CAPTURA

En 'Modo de vista' aparecen listados los tipos de vista que hay disponibles para esta acción.
En 'Vistas' aparecen especificadas las vistas que se abrirán según el modo (tree, kanban, formulario, calendario) y la secuencia de prioridad.

Si no hay ninguna indicada se guía simplemente por el número de secuencia.

[**Indice**](#indice)


## Crear elemento de menú<a name="id9"/>

`Configuración > Técnico > Interfaz de usuario > Elementos menú`

----CAPTURA

Aparecen todos los elementos de menú de Odoo y la jerarquía de los mismos en la 'ruta' que se indica en el nombre.

Si pinchamos en cualquiera de ellos aparece la información necesaria para que funcione como el 'Menú' (nombre que será visible), de que elemento de menú hereda y que acción de ventana se ejecuta cuando pinchamos en él.

----CAPTURA

Si pinchamos en 'Crear' podemos diseñar un nuevo elemento de menú. Si queremos duplicar uno existente solo tenemos que seleccionarlo, elegir el desplegable 'Duplicar' y cambiar la ruta donde aparecerá el elemento.

Para que aparezca en la barra superior solo tenemos que indicar que no hereda de ningún otro elemento.

----CAPTURA

En caso de que el elemento no esté asignado a ningún grupo de permisos será visible para todos los usuarios. En el momento en que se asigne a un grupo desaparecerá de aquellos a los que no esté asignado.

----CAPTURA

[**Indice**](#indice)


## Crear un usuario<a name="id10"/>

`Configuración > Usuarios > Usuarios`

Aparecen los usuarios disponibles.

----CAPTURA

Para crear un nuevo usuario pinchar en Crear.

----CAPTURA

Introducir el nombre y correo electronico y seleccionar los permisos para cada aplicación seleccionando el rol adecuado.

Si no queremos que tenga acceso a alguna aplicación simplemente no se selecciona ningún rol para esa aplicación.

----CAPTURA

Pinchar en 'Cambiar contraseña' para indicar una nueva ya que por defecto no lo hace.

----CAPTURA

Por último realizar la comprobación de acceso con ese usuario entrando a Odoo desde otro navegador (para poder dejar abierta la sesión actual) con el email y contraseña del usuario.

Debería tener acceso solo a las aplicaciones indicadas, es decir, el resto de aplicaciones y opciones de menú no serán visibles para este usuario.

----CAPTURA


## Permisos<a name="id11"/>

`Configuración > Usuarios > Grupos`

Aparecen todos los grupos disponibles indicando en el nombre la estructura jerarquica que forman.

----CAPTURA

Podemos usar el buscador para comprobar que grupos hay para una aplicación concreta.

----CAPTURA

Pinchando en cada grupo aparecen en las distintas pestañas caracteristicas como 'Permisos de acceso', 'Usuarios', 'Menús' o 'Vistas', pudiendo modificarlo pinchando en 'Editar'.

----CAPTURA

Los permisos se aplican sobre cada objeto y son crear, eliminar, leer y modificar.

[**Indice**](#indice)


## Crear un grupo de permisos<a name="id12"/>

Se utiliza la herencia, de forma que un rol que tenga ciertos permisos, el grupo que herede de él siempre tendrá esos permisos y los adicionales.

`Configuración > Usuarios > Grupos > Crear`

Indicar la aplicación sobre la que se aplicará el grupo de permisos, el nombre del grupo y el grupo del que hereda.

----CAPTURA

`Permisos de acceso > Añadir un elemento`

Añadir también los permisos adicionales indicando el objeto y los permisos que tiene sobre el, dandole un nombre a la nueva regla y pinchando en 'Guardar'.

----CAPTURA

`Configuración > Usuarios > Usuarios`

Seleccionar un usuario y asignarle al nuevo grupo de permisos para comprobar que funciona.

[**Indice**](#indice)


## Crear un tablero<a name="id13"/>

Es una vista que incluye otras vistas. Se puede instalar la aplicación 'Tableros' para manejarlos.

Podemos crear distintos tableros. Después solo tenemos que ir a las vistas, y en 'Favoritos' seleccionar la opción 'Añadir a mi tablero'.

Una vez en el Tablero podemos ordenas las vistas que hemos añadido anteriormente o modificar el layout pulsando 'Cambiar diseño'.

Para elegir donde aparecerá el nuevo tablero vamos a los [elementos de menú](#id9) y buscamos por el nombre del tablero. La aplicación ha creado un elemento de menú para el mismo y podemos modificar la ruta para ubicarlo donde necesitemos.

[**Indice**](#indice)


## Informes<a name="id14"/>




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
