
![Logo Odoo][odoo]

# Indice<a name="indice"/>

* [Crear nueva empresa](#id1)
* [Modelos de datos](#id2)
    * [Crear modelo de datos](#id2)
    * [Modificar modelo de datos](#id3)
    * [Relaciones entre modelos de datos](#id4)
* [Vistas](#id5)
    * [Crear nueva vista](#id5)
    * [Crear vista heredada](#id6)
    * [Modificar vista](#id7)
* [Acciones de ventana](#id8)
    * [Crear acción de ventana](#id8)
    * [Modificar acción de ventana](#id8b)
* [Elementos de menú](#id9)
* [Usuarios](#id10)
* [Permisos](#id11)
    * [Información](#id11)
    * [Grupo de permisos](#id12)
* [Tableros](#id13)
* [Informes](#id14)
    * [Información](#id14)
    * [Crear informe](#id15)


# Contenido

Para realizar la mayoría de los cambios es necesario activar las opciones de desarollador desde el menu de Configuración.

## Crear nueva empresa<a name="id1"/>

Seguir los pasos de la [Unidad 3][ud3] para:
1. Crear y configurar una nueva empresa con su base de datos
2. Instalar los módulos de la internacionalización al español
3. Establecer el plan contable
4. Instalar los módulos:
      * Ventas
      * Gestión de inventario
      * Gestión de compras
      * Contabilidad y finanzas

[**Indice**](#indice)


## Modelos de datos

### Crear modelo de datos<a name="id2"/>

`Configuración > Técnico > Estructura de la base de datos > Modelos > Crear`

En 'Descripción del modelo' escribir el nombre que sera visible, y tanto en 'Modelo' como en el nombre del los nuevos campos usar la nomenclatura x_nombreobjeto para indicar que es una entidad creada por nosotros.

![Captura de pantalla 12][img12]

El nuevo modelo necesitará tener [nuevas vistas](#id5) para visualizar e introducir los nuevos datos o [modificar las vistas existentes](#id7).

También es posible que requieran [elementos de menú](#id9) para acceder a las vistas del nuevo modelo.

Para que lo haga Odoo automaticamente solo hay que pinchar en 'Crear un menú' en la creación del modelo, pero es bastante limitado.

[**Indice**](#indice)

### Modificar modelo de datos<a name="id3"/>

1. Acceder a los modelos de datos de la base de datos:

`Configuración > Técnico > Estructura de la base de datos > Modelos`

![Captura de pantalla 1][img1]

2. Seleccionar el objeto que queremos modificar:

![Captura de pantalla 2][img2]

3. Añadir o modificar los campos necesarios:

Pulsar 'Editar' y al final de la lista 'Añadir elemento'.

![Captura de pantalla 3][img3]

Pulsar 'Guardar' en el formulario y 'Guardar' en la lista de objetos.

Aparecerá al final de la lista (si hay más de una página comprobar la última).

![Captura de pantalla 4][img4]

En el caso del modelo de datos Producto hay que modificar tanto product.product como product.template.

[**Indice**](#indice)


### Relaciones entre modelos de datos<a name="id4"/>

Pueden ser de uno a muchos (one2many), muchos a uno (many2one) o muchos a muchos (many2many).

Primero tenemos que conocer el nombre del otro modelo con el que queremos establecer la relación.

`Configuración > Técnico > Estructura de la base de datos > Modelos`

O si no sabemos exactamente cual es podemos acceder a él editando cualquiera de las vistas que lo usen, ya que aparecerá en el campo 'Modelo'.

[Modificar el modelo](#id3) añadiendo un campo que recoja la información del otro modelo con el que queremos establecer la relación.

En 'Tipo de campo' indicar la relación que hay y en 'Relación del objeto' el nombre del otro modelo.

![Captura de pantalla 11][img11]

En el modelo espacio incluyo un campo cliente para indicar que muchos espacios pueden pertenecer al mismo cliente.

[Modificar las vistas](#id7) asociadas con este modelo para que reflejen el nuevo campo.

Al incluir el nuevo campo en las vistas, estas se adaptan según el tipo de relación y el modelo (ofreciendo un desplegable o lo que haga falta para recoger la nueva información).

![Captura de pantalla 24][img24]

[**Indice**](#indice)


## Vistas

### Crear nueva vista<a name="id5"/>

Hay varios tipos de vistas, entre otros:

* Kanban

    ![Captura de pantalla 23][img23]

* Árbol

    ![Captura de pantalla 15][img15]

* Formulario

    ![Captura de pantalla 16][img16]

Para ver todas las vistas disponibles:

`Configuración > Técnico > Interfaz de usuario > Vistas`

 ![Captura de pantalla 13][img13]

Crear una nueva y poner la extensión adecuada al nombre (.form, .tree, etc según el tipo de vista). Dejar 'Vista heredada' en blanco y en 'Ver modo heredado' elegir Vista base.

Asociar en 'Modelo' el objeto de la base de datos sobre el que actúa y crear el xml.

* Kanban:

 ![Captura de pantalla 17][img17]

* Árbol:

 ![Captura de pantalla 39][img39]

* Formulario:

 ![Captura de pantalla 18][img18]

Para que la nueva vista sea visible desde algún lugar tendremos que asociarla a alguna [acción de ventana](#id8) que sea llamada desde algún [elemento de menú](#id9).

[**Indice**](#indice)


### Crear vista heredada<a name="id6"/>

1. Obtener información de la vista padre:

    Vamos a la vista de la cual queremos que herede la nueva vista que vamos a crear.

    `Herramientas del desarollador > Editar FormVer`

    ![Captura de pantalla 8][img8]

2. Definir la nueva vista desde la vista padre:

    `Editar > Vistas Heredadas > Añadir un elemento`

    Nombrarla manteniendo el nombre de la vista padre y añadiendo un sufijo que defina la vista. Añadir el codigo xml, usando xpath para hacer referencia a elementos de la vista padre, que podremos usar como referencia, modificar o incluso invisivilizar.

    ![Captura de pantalla 9][img9]

    Asegurarnos de que la nueva vista tiene un numero de secuencia menor que la vista de la que hereda, pues se abre por niveles de prioridad (siempre la vista de número menor).

    No obstante, en las [acciones de ventana](#id8b) podemos indicar que vista queremos que se muestre de forma especifica. Por eso puede que no se vea la nueva vista aunque tenga secuencia menor si hay otra vista seleccionada para esa acción.

    Si refrescamos el navegador y vamos a la vista aparecerán los nuevos elementos.

    ![Captura de pantalla 10][img10]

[**Indice**](#indice)


### Modificar vista<a name="id7"/>

Estando en la vista que queremos modificar pulsar el botón con forma de escarabajo que hay en la barra superior:

`Herramientas del desarollador > Editar TreeVer`

![Captura de pantalla 5][img5]

Esta opción variará según el tipo de vista que queramos editar.

Si en el campo 'Vista heredada' hay otra vista tener cuidado porque a lo mejor lo que queremos modificar se encuentra en la vista padre.

Para ello pulsar el botón que aparece junto al nombre de la vista heredada y nos lleva a su vista padre.

![Captura de pantalla 6][img6]   

Hay que tener cuidado al modificar vistas que no hayan sido creadas por nosotros, o que tengan herencia por que podrían dar errores inesperados.

No obstante, se pueden ocultar elementos de la vista añadiendo el atributo invisible = "1" a la etiqueta del elemento o añadir elementos nuevos sin problemas.

Para comprobar los cambios recargar el navegador.

![Captura de pantalla 7][img7]

Es importante también asignar las vistas durante la creación de [elementos de menú](#id9) para que al pinchar en ellos aparezcan las vistas adecuadas.

[**Indice**](#indice)


## Acciones de Ventana

### Crear acción de ventana<a name="id8"/>

`Configuración > Técnico > Acciones > Acciones de ventana > Crear`

Servirá para enlazar las vistas que indiquemos con cada elemento de menú que utilice esta acción.

Elegir el 'Nombre' de la acción. En 'ID externo objeto' indicar el modelo sobre el que actuará y en 'Modo de vista' enumerar los tipos de vista que tenemos disponibles para esa acción ordenados por prioridad.

![Captura de pantalla 20][img20]

Podemos ahora asociar esta nueva acción a algún [elemento de menú](#id9).

[**Indice**](#indice)


### Modificar acción de Ventana<a name="id8b"/>

Podemos modificar la acción que hace que al pinchar un elemento de menú se abra una vista, para conseguir que se abra otra accediendo desde el propio elemento de menú:

`Configuración > Técnico > Interfaz de usuario > Elementos menú > Acción`

En 'Vistas' aparecen especificadas las vistas que se abrirán según el modo (tree, kanban, formulario, calendario) y la secuencia de prioridad.
Las vistas incluidas en esta sección harán que se muestren los iconos para cambiar entre los tipos de vista en la esquina superior derecha.

[**Indice**](#indice)


## Elementos de menú<a name="id9"/>

`Configuración > Técnico > Interfaz de usuario > Elementos menú`

Aparecen todos los elementos de menú de Odoo y la jerarquía de los mismos en la 'ruta' que se indica en el nombre.

 ![Captura de pantalla 19][img19]

Si pinchamos en cualquiera de ellos aparece la información necesaria para que funcione como el 'Menú' (nombre que será visible), de que elemento de menú hereda y que acción de ventana se ejecuta cuando pinchamos en él.

Si pinchamos en 'Crear' podemos diseñar un nuevo elemento de menú.

 Si queremos duplicar uno existente solo tenemos que seleccionarlo, elegir el desplegable 'Duplicar' y cambiar la ruta donde aparecerá el elemento.

  ![Captura de pantalla 21][img21]

Para que aparezca en la barra superior solo tenemos que indicar que no hereda de ningún otro elemento, si queremos que sea un categoria simplemente no se le asocia ninguna acción.

  ![Captura de pantalla 22][img22]

Para que el elemento de menú Alquilar esté dentro de Espacios solo hay que hacer que herede de él y asociarle la acción de ventana adecuada.

En caso de que el elemento no esté asignado a ningún grupo de permisos será visible para todos los usuarios. En el momento en que se asigne a un grupo desaparecerá de aquellos a los que no esté asignado.

[**Indice**](#indice)


## Usuarios<a name="id10"/>

`Configuración > Usuarios > Usuarios`

Aparecen los usuarios disponibles.

  ![Captura de pantalla 25][img25]

Para crear un nuevo usuario pinchar en Crear.

Introducir el nombre y correo electronico y seleccionar los permisos para cada aplicación seleccionando el rol adecuado.

Si no queremos que tenga acceso a alguna aplicación simplemente no se selecciona ningún rol para esa aplicación, no obtante, recordar que si no se le da ningún permiso no podrá acceder a Odoo.

  ![Captura de pantalla 26][img26]

Pinchar en 'Cambiar contraseña' para indicar una nueva ya que por defecto no lo hace.

  ![Captura de pantalla 27][img27]

Por último realizar la comprobación de acceso con ese usuario entrando a Odoo desde otro navegador (para poder dejar abierta la sesión actual) con el email y contraseña del usuario.

Debería tener acceso solo a las aplicaciones indicadas, es decir, el resto de aplicaciones y opciones de menú no serán visibles para este usuario.

[**Indice**](#indice)


## Permisos

### Información<a name="id11"/>

`Configuración > Usuarios > Grupos`

Aparecen todos los grupos disponibles indicando en el nombre la estructura jerarquica que forman.

  ![Captura de pantalla 28][img28]

Pinchando en cada grupo aparecen en las distintas pestañas caracteristicas como 'Permisos de acceso', 'Usuarios', 'Menús' o 'Vistas', pudiendo modificarlo pinchando en 'Editar'.

Los permisos que se aplican sobre cada objeto y son crear, eliminar, leer y modificar.

[**Indice**](#indice)


### Grupo de permisos<a name="id12"/>

Se utiliza la herencia, de forma que si un grupo tiene ciertos permisos, el grupo que herede de él siempre tendrá esos permisos y los adicionales que se le añadan.

* Crear grupo de permisos Empleado

  `Configuración > Usuarios > Grupos > Crear`

  Indicar la aplicación (si procede), el nombre del grupo y el grupo del que hereda. Se pueden añadir también los usuarios que van a disfrutar de los privilegios de acceso que otorga el grupo.

    ![Captura de pantalla 37][img37]

  En la pestaña 'Hereda' podemos incluir permisos ya agrupados para facilitar la tarea. En este caso dotamos al Grupo Usuario del perfil de acceso más limitado, utilizando los grupos Usuario que ya creó Odoo para las aplicaciones instaladas de Ventas, Compras e Inventario.

    ![Captura de pantalla 38][img38]

    `Permisos de acceso > Añadir un elemento`

  Para añadir o modificar permisos sobre un objeto y los permisos que tiene sobre el, dándole un nombre a la nueva regla y pinchando en 'Guardar'.

  Para comprobar los cambios abrimos otro navegador y vemos como el usuario Empleado recien añadido al Grupo Empleado tiene acceso a la información que acabamos de indicar.

    ![Captura de pantalla 40][img40]

* Crear grupo de permisos Gerente

  Podríamos hacer que el grupo Gerente heredase de el grupo Empleado, pero realmente los permisos ya los tiene al heredar del grupo Responsable en las aplicaciones de Ventas, Compras e Inventario. Todos los usuarios de este grupo por herencia pertenecerán también a los grupos de los que herede este.

    ![Captura de pantalla 41][img41]

  Para que además tenga acceso al Tablero Gerente y a la sección Espacios le incluimos los elementos de menú asociados.

    ![Captura de pantalla 42][img42]

  No obstante, esto no será suficiente para que tenga acceso a los Espacios ya que tanto las vistas como los elementos de menú trabajan sobre el modelo Espacio. Por lo tanto debemos darle permiso de acceso al modelo explicitamente.

    ![Captura de pantalla 43][img43]

  Hay que tener cuidado porque si en algún momento añadimos a un usuario a un grupo este adquiere los permisos del grupo, pero si lo sacamos de él, Odoo no le quita los permisos asociados.

  Al comprobar el usuario gerente que forma parte del grupo Gerente vemos que tiene el control de todo el ERP incluyendo el Tablero y los Espacios pero que no tiene acceso a la configuración.

    ![Captura de pantalla 44][img44]

* Crear grupo de permisos Administrador

  Por último creamos el grupo más completo de todos, que tendrá acceso a lo mismo que el grupo Gerente, a la configuración (a traves del grupo Administrador original) y le incluiremos tambien la configuración técnica, a la que no tenía acceso ningún grupo ni usuario hasta ahora.

    ![Captura de pantalla 45][img45]  

  Vemos que el usuario Administrador que esta dentro del grupo Administrador tiene acceso a toda la configuración del ERP.

    ![Captura de pantalla 46][img46]

[**Indice**](#indice)


## Tableros<a name="id13"/>

Es una vista que incluye otras vistas. Se puede instalar la aplicación 'Tableros' para manejarlos.

  ![Captura de pantalla 29][img29]

Estando en la vista que queremos añadir al tablero pulsamos la lupa de la barra de busqueda. Esto despliega unas opciones extra donde nos permite incluir esa vista en el tablero desplegando 'Favoritos' y seleccionando la opción 'Añadir a mi tablero'.

  ![Captura de pantalla 34][img34]

Una vez en el Tablero podemos ordenas las vistas que hemos añadido anteriormente o modificar el layout pulsando 'Cambiar diseño'.

  ![Captura de pantalla 35][img35]

Para elegir donde aparecerá el nuevo tablero vamos a los [elementos de menú](#id9) y buscamos por el nombre del tablero. La aplicación ha creado un elemento de menú para el mismo y podemos modificar la ruta para ubicarlo donde necesitemos.

Por defecto, si al crearlo no indicamos que usuario o grupo tendrá acceso al tablero este será visible para todos. Podemos limitar el acceso dando permisos a algún grupo.

En ese caso desaparecerá para los demás a no ser que se lo haya añadido explicitamente o hereden el permiso.

[**Indice**](#indice)


## Informes

### Información<a name="id14"/>

Se usan para mostrar información (normalmente en pdf).

Desde la vista donde se encuentra la información que queremos recoger normalmente tenemos la opción 'Imprimir' en un desplegable, donde nos deja producir directamente nuestro informe eligiendo entre las opciones que tengamos.

Ver informes disponibles:

`Configuración > Técnico > Informes > Informes`

En 'Nombre de la plantilla' aparece el nombre del documento xml que define el informe (puede estar formado por subinformes, con varios xml) y en 'Modelo' el nombre del modelo del que va a recoger la información.

Para ver el codigo pinchamos en 'Vistas QWeb' y se mostrara la lista con el informe y subinformes si los hubiera.

El lenguaje que utiliza es <a href="https://www.odoo.com/documentation/10.0/reference/qweb.html">QWeb</a> y los elementos que aparecerán en el informe se generaran dinamicamente según lo que se programe en la plantilla del informe y la información que encuentre cuando este sea generado.

[**Indice**](#indice)


### Crear informe<a name="id15"/>

1. Crear el informe:

    `Configuración > Técnico > Informes > Informes > Crear`

    Rellenamos los datos básicos del informe. El nombre y el tipo que prefiramos, el 'Modelo' es del que va a sacar la información y en 'Nombre de la plantilla' indicar la vista que vamos a crear después (llamarla nombre_modelo.informe o algo similar).

      ![Captura de pantalla 30][img30]

    Vamos a 'Vistas Qweb' para crear la nueva vista.

    Lo que pusimos en 'Nombre de la plantilla' tiene que coincidir con el 'Nombre de la vista', y tenemos que indicar que es de tipo QWeb además del modelo de datos.

      ![Captura de pantalla 31][img31]

2. Enlazar el informe:

    Para que el informe funcione necesitamos enlazarlo bien, para lo que vamos a crear un identificador (abrir en una pestaña del navegador dejando la vista del informe abierta en otra).

    `Configuración > Técnico > Secuencias e identificadores > Identificadores externos > Crear`

    Si el nombre de la plantilla es nombre_modelo.informe, en el campo 'Modulo' debo poner nombre_modelo y en 'Identificador externo' informe.

      ![Captura de pantalla 32][img32]

    En 'Nombre del modelo' necesitamos una parte de la url que aparece en la pestaña del navegador que tiene abierta la vista del informe. Concretamente el valor de model (ir.ui.view).

    Necesitamos también el id de la vista para 'ID de registro', que sera el valor de id que aparece en la url.

3. Comprobar el enlace:

    Desde la vista de la plantilla, si hemos guardado los cambios y recargado el navegador, debe aparecer en 'ID externo' la referencia nombre_modelo.informe gracias al enlace creado.

      ![Captura de pantalla 33][img33]

4. Añadir plantilla al menú:

    Una vez terminado, desde la plantilla del informe pulsamos la opción 'Añadir al menú imprimir' para que cuando estemos en las vistas del modelo encontremos la opción de generar nuestro nuevo informe en el desplegable 'Imprimir'.

5. Desarollar el informe:

    Para realizar las pruebas podemos indicar que es de tipo HTML y así evitar generar un pdf cada vez.

    Cuando necesitemos acceder al modelo de datos del informe podemos hacerlo haciendo referencia al objeto 'docs'. Es una colección generada automáticamente con todos los objetos disponibles para sacar en el informe (una coleccion de clientes, de productos, de facturas, etc).

    * Informe de embarcaciones:

   ![Captura de pantalla 47][img47]  

   Para generarlo vamos al formulario del producto y seleccionamos el tipo de informe en el desplegable 'Imprimir'.

   ![Captura de pantalla 48][img48]  

   En este caso se muestra la información de la embarcación elegida.

   ![Captura de pantalla 49][img49]  

    * Informe de espacios:

   ![Captura de pantalla 50][img50]  

   Realizamos la comprobacion con un espacio ocupado.

   ![Captura de pantalla 51][img51]  

   Y también con un espacio vacío.

   Aunque muestran la información necesaria, los informes son bastante espartanos. Lo ideal sería invertir algo más de tiempo para que la plantilla fuese mas agradable a la vista usando las herramientas que nos proporcionan los lenguajes HTML y QWeb.

[**Indice**](#indice)


[img1]: ./Capturas/img1.png
[img2]: ./Capturas/img2.png
[img3]: ./Capturas/img3.png
[img4]: ./Capturas/img4.png
[img5]: ./Capturas/img5.png
[img6]: ./Capturas/img6.png
[img7]: ./Capturas/img7.png
[img8]: ./Capturas/img8.png
[img9]: ./Capturas/img9.png
[img10]: ./Capturas/img10.png
[img11]: ./Capturas/img11.png
[img12]: ./Capturas/img12.png
[img13]: ./Capturas/img13.png
[img14]: ./Capturas/img14.png
[img15]: ./Capturas/img15.png
[img16]: ./Capturas/img16.png
[img17]: ./Capturas/img17.png
[img18]: ./Capturas/img18.png
[img19]: ./Capturas/img19.png
[img20]: ./Capturas/img20.png
[img21]: ./Capturas/img21.png
[img22]: ./Capturas/img22.png
[img23]: ./Capturas/img23.png
[img24]: ./Capturas/img24.png
[img25]: ./Capturas/img25.png
[img26]: ./Capturas/img26.png
[img27]: ./Capturas/img27.png
[img28]: ./Capturas/img28.png
[img29]: ./Capturas/img29.png
[img30]: ./Capturas/img30.png
[img31]: ./Capturas/img31.png
[img32]: ./Capturas/img32.png
[img33]: ./Capturas/img33.png
[img34]: ./Capturas/img34.png
[img35]: ./Capturas/img35.png
[img36]: ./Capturas/img36.png
[img37]: ./Capturas/img37.png
[img38]: ./Capturas/img38.png
[img39]: ./Capturas/img39.png
[img40]: ./Capturas/img40.png
[img41]: ./Capturas/img41.png
[img42]: ./Capturas/img42.png
[img43]: ./Capturas/img43.png
[img44]: ./Capturas/img44.png
[img45]: ./Capturas/img45.png
[img46]: ./Capturas/img46.png
[img47]: ./Capturas/img47.png
[img48]: ./Capturas/img48.png
[img49]: ./Capturas/img49.png
[img50]: ./Capturas/img50.png
[img51]: ./Capturas/img51.png
[img52]: ./Capturas/img52.png
[ud3]: ../Ud_3/Unidad_3.md
[odoo]: ../Ud_3/capturas/odoo_logo.png
