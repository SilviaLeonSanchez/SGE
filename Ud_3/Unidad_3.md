
# CREAR NUEVA BASE DE DATOS NUEVA

Al conectar a Odoo a través del servicio web  nos ofrece conectarnos a las bases de datos de que disponemos, y tambien crear nuevas:

imagen 1

# MODIFICAR LA COMPAÑIA POR DEFECTO

Configuracion -> Compañias -> Editar

Incluimos los datos necesarios.

imagen 5

# INSTALAR LOS MODULOS NECESARIOS PARA LA PRACTICA

l10n_es

imagen 2

l10n_es_partner

imagen 3

l10n_es_toponyms

imagen 4

# ESTABLECER EL PLAN CONTABLE PARA UNA PYME ESPAÑOLA

Contabilidad -> Configuracion -> Plan Contable -> Plantilla

Elegimos PGCE PYMEs 2008

Se rellenan los datos automaticamente con la informacion que tenemos de los modulos instalados.

Pinchamos en Aplicar.

imagen 6 

# INSTALAR LOS MODULOS NECESARIOS

Ventas
imagen 7

Gestion de inventario
imagen 8

Gestion de compras 
imagen 9


# CREAR ALMACENES

En Inventario -> Configuracion -> Ubicación y almacén -> Nivel de uso de almacenes y ubicaciones marcar la opcion:
Gestiona varios Almacenes, con varias ubicaciones cada uno

imagen 29

Aparece la opción Gestión de almacenes:

Modifico el almacen que aparece por defecto y creo los Almacenes extra que necesite.

imagen 30

Creo las ubicaciones necesarias dentro de los almacenes indicando en ubicacion padre el almacen al que pertenece. En este caso no es necesario dado que solo necesitamos una ubicacion por almacen que por defecto es existencias.

Una vez  creadas aparecen listadas en Ubicaciones:

imagen 31

imagen 21??

# CREAR PROVEEDORES

Compras -> Proveedores -> Crear 

imagen 10

Se rellenan sus datos, sin olvidar el NIF que va en la pestaña de Contabilidad, incluyendo delante el prefijo ES para que el sistema lo acepte.

No olvidar marcar la casilla de Compañia en vez de Individual si son empresas.

* Si ya teniamos creadas las compañias  basta con elegirla en el despelegable que aparece debajo del nombre.

imagen 11

Si hemos marcado en la pestaña Ventas y Compras del formulario la casilla indicando que son proveedores deberian aparecer en la pagina principal de proveedores:

imagen 12

# CREAR CLIENTES DE LA EMPRESA

Ventas -> Clientes -> Crear

imagen 13

Se rellenan los datos exactamente igual que para los proveedores, solo que esta vez marcaremos la casilla de cliente en vez de proveedor y la casilla Individual si son personas.

imagen 14

Comprobamos que aparecen en la pagina de Clientes:

imagen 15

# CREAR CATEGORIAS DE PRODUCTOS

Inventario -> Categoria de productos -> Crear

imagen 16

Creamos las categorias jerarquicamente: 

1. 'Software' que herede de 'Todos'

2. Despues 'Sistemas operativos' que herede de 'Software'

imagen 17

Repetimos la operacion con la categoria 'Hardware' que tendra varios niveles de subcategorías: 

1. Crear categoria 'Hardware' que herede de 'Todos'

2. Crear categorias hijas 'Portatiles' y 'Componentes' que hereden de 'Hardware'

3. Crear 'DiscosSSD' y 'Graficas' que hereden de 'Componentes'

Deberia quedar asi:

imagen 18


# CREAR PRODUCTOS

Inventario -> Productos -> Crear

imagen 19

Categoria se indica en Categoria interna.

Coste se indica en Coste.

En Factura tenemos que indicar los impuestos de compra y de venta para que aparezca de forma automatica.

En Precio de venta no pongo nada porque despues se utilizara una Tarifa para que lo calcule automaticamente en la factura.

El proveedor lo indico en la pestaña Inventario, añadiendo uno nuevo y eligiendo uno de los proveedores ya existentes, incluyendo el nombre del producto y el precio.

Incluyo la descripcion en la pestaña Notas.

Para indicar la cantidad que hay en stock pinchar en el boton Actualizar cantidad de stock fisico (arriba a la izquierda) y elegir la ubicacion.
Incluir las actualizaciones necesarias para incluir las existencias de cada ubicacion.

imagen 20

Al terminar se deberian encontrar todos en la pagina principal de productos

imagen 22


# CREAR TARIFA DE VENTA

En Ventas -> Configuracion -> Precio -> Precio de Venta marcamos:

Precios avanzados basados en fórmulas (descuentos, márgenes, redondeo)
y aparece la opcion Tarifas.

Para crear una nueva:
imagen 32

Ventas -> Tarifas -> Crear

imagen 22?

Se añaden los elementos sobre los que se va a aplicar la tarifa, en este caso sobre una determinada categoria.

Para indicar un precio sobre el precio de coste se indica la opcion formula, donde marcamos sobre precio de coste, y en descuento ponemos un descuento negativo para que resulte en el aumento de precio que queremos conseguir.
Se puede conseguir el mismo resultado en la opcion porcentaje.

Para que el precio del software sea de 1.9 el precio de coste indico un descuento del -90%.

imagen 23

Para aplicar las tarifas deberemos hacerlo al crear un pedido de ventas.

# REALIZAR PEDIDO A PROVEEDOR

Compras -> Pedidos de compra -> Crear 

1. Realizar pedido:

Elegir el proveedor y la fecha
Añadir los productos, eligiendo del desplegable, deberia aparecer la informacion del producto al elegirlo.
El IVA deberia aparecer automaticamente si se ha indicado en la creacion del producto.
Indicar las unidades de cada producto.

imagen 24?

Se ha creado la solicitud de presupuesto. Ahora pinchamos en confirmar pedido.

imagen 25

2. Recibir el pedido

Pincho en recibir productos

imagen 26

Modificar el documento indicando en cada producto la misma cantidad en Hecho que la que aparece en Para ejecutar y modificando la ubicacion de recepcion. Pinchando despues en validar

imagen 35

---------------------

Ahora el pedido aparece en estado Para facturar y en Inventario -> Movimientos de existencias aparecen los productos situados en la Tienda.

imagen 28

























