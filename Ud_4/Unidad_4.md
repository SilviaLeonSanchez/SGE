
![Logo Odoo][odoo]

# Indice<a name="indice"/>

* [Crear nueva empresa](#id1)
* [Modificar modelo de datos](#id2)
* [Modificar vista](#id3)
* [Crear vista heredada](#id4)

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


## Modificar modelo de datos<a name="id2"/>

1. Acceder a los modelos de datos de la base de datos:

  `Configuración > Técnico > Estructura de la base de datos > Modelos`

![Captura de pantalla 1][img1]

2. Seleccionar el objeto que queremos modificar:

![Captura de pantalla 2][img2]

3. Añadir los campos necesarios:

Pulsar 'Editar' y al final de la lista 'Añadir elemento'.

![Captura de pantalla 3][img3]

Pulsar 'Guardar' en el formulario y 'Guardar' en la lista de objetos. Aparecerá al final de la lista (si hay más de una página comprobar la última).

Para los objetos que creemos nosotros nombrarlos con x_nombreobjeto.

![Captura de pantalla 4][img4]

[**Indice**](#indice)


## Modificar vista<a name="id3"/>

Estando en la vista que queremos modificar pulsar el botón con forma de escarabajo que hay en la barra superior ('Herramientas del desarollador').

![Captura de pantalla 5][img5]

En este caso pulsamos la opción 'Editar formVer'.

`Esta opcion variará sugún el tipo de vista que queramos editar`

![Captura de pantalla 6][img6]

Si en el campo heredar hay otra vista tener cuidado porque a lo mejor queremos modificar esa.
Para ello pulsar el botón que aparece junto al nombre y nos lleva a la vista padre (es la vista padre si no hereda de ninguna otra).

![Captura de pantalla 7][img7]


## Crear vista heredada<a name="id4"/>

1. Obtener información de la vista padre

    Vamos a la vista de la cual queremos que herede la nueva vista que vamos a crear.

![Captura de pantalla 11][img11]

`Herramientas del desarollador > Editar FormVer`

![Captura de pantalla 12][img12]


2. Definir la nueva vista:

    `Editar > Vistas Heredadas > Añadir un elemento`

![Captura de pantalla 8][img8]

3. Modificar la acción de ventana para que nos lleve a la vista que hemos creado.

  `Configuración > Técnico > Acciones > Acciones de ventana`

Elegir la acción a la que se llama para abrir esa vista y pulsar en ella.

![Captura de pantalla 9][img9]

Pulsar el botón 'Editar'.

![Captura de pantalla 10][img10]

`Opciones generales > Vistas > Ref. vista`

Rellenar con el nombre de la vista que hemos creado.

Puede aparecer vacío si inicialmente la acción de ventana dirige hacia una vista por defecto.

## Crear modelo de datos



## Crear nueva vista

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

## Crear acción de ventana

`Configuración > Técnoico > Acciones > Acciones de ventana'

Crear la acción que abrirá la Vistas.

Como nombre de la acción elegir el nombre que aparecerá en el menú.

## Crear elemento de menú

Son jerárquicos, elegir donde irá colocado

Indicar la acción que ejecutará (la que creamos anteriormente)

~ Al buscar busca automaticamente por el campo Name


## Permisos

`Configuración > Usuarios > Grupos`

Se ven los permisos que se pueden asignar, los roles que hay para cada aplicación y que usuarios los tienen.

Son CRUD y se aplican sobre cada objeto. Se utiliza la herencia, de forma que un rol que tenga x permisos, si heredamos tendrá siempre esos x permisos y los adicionales.

'Configuración > Usuarios > Usuarios'

Se asignan de forma jerárquica

En Aplicación (en la ventana del usuario) aparecen las aplicaciones y el rol que tiene el usuario en cada una.

Abajo aparecen las opciones donde elegir el rol o roles que queremos asignarle para cada aplicación.

## Crear un grupo de permisos

'Configuración > Usuarios > Grupos'

Dar todos los permisos de acceso al objeto y la plantilla del mismo, indicar la aplicación sobre la que se aplica el rol.

'Configuración > Usuarios > Usuarios'

Meter al usuario en el grupo de permisos que acabamos de crear.

Para comprobar que el nuevo usuario tiene permisos podemos abrir sesión con el en otro navegador y así no tenemos que cerrar nuestra sesiónl.








[Capturas/Captura_1.jpg](#img1)
