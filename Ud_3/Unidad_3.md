
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

Para que el precio del software sea de 1.9 el precio de coste indico un descuento del -90%.

imagen 23

Para aplicar las tarifas deberemos hacerlo al crear un pedido de ventas.

Se puede crear una Tarifa general y añadir reglas que aplicaran distintos calculos segun los criterios que indiquemos como la categoria de producto. Asi podra incluir distintas formas de calcular el precio si en un mismo pedido tenemos productos de distintas categorias.

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

Ahora el pedido aparece en estado Para facturar y en Inventario -> Movimientos de existencias aparecen los productos situados en la Tienda.

imagen 28

3. Generar factura

En el pedido pinchamos en Facturas de p... (esquina superior derecha del formulario del pedido) y en Crear.
Aparece el nombre del proveedor seleccionado y los datos del pedido. Elegir la fecha de la facura y Validar.

imagen dia 29

4. Realizar pago
Pinchar en la opcion de Registrar pago (esquina superrior izquierda en el desde la propia factura)
imagen

En el dialogo que aparece elegir la opcion de pago elegido y validar

imagen

Debe aparecer como Pagado.

# REALIZAR VENTA A CLIENTE

1. Realizar venta

En Ventas -> Clientes elegimos el cliente que desea realizar la compra. 
imagen

Pinchamos en Ventas (esquina superior derecha de la ficha del cliente) y aparecera el listado de todas las ventas realizadas a ese cliente. Seleccionamos la opcion Crear.

imagen

Seleccionar los productos y la cantidad.Debe aparecer toda la informacion de los mismos en el formulario automaticamente.
Seleccionamos la tarifa que se le aplica.
En la pestaña Otra informacion podemos elegir desde que ubicación se le envian los productos. Asegurarse de que es la correcta y comprobar si es necesario si hay existencias suficientes.

Guardamos y pinchamos en Confirmar venta si todo es correcto.
imagen

Si queremos realizar varios pedidos repetimos el proceso.

2. Comprobar stock

En Inventario -> Informes -> Movimientos de existencias podemos comprobar todas las operaciones realizadas sobre el stock: movimientos de una ubicacion a otra, compras, ventas... Aparece la informacion de los productos, su ubicacion inicial y final y su estado.

3. Generar factura

En Ventas -> Presupuestos seleccionamos los pedidos de los que vamos a generar la factura y pinchamos en el desplegable Accion -> Orden de facturacion.

Elegimos Crear y ver facturas y Validar

imagen

4. Registrar pago

Desde Contabilidad -> Ventas -> Factura de cliente elegimos la factura y nos aparece el formulario de la misma.

Pinchar en Registrar pago

imagen

Elegir la forma de pago y Validar

Debe aparecer como pagada.

# MÓDULO TPV

1. Instalación

Activar el modo desarrollador en Configuración (esquina inferior derecha)
Buscamos en Aplicaciones el modulo Punto de Venta e instalamos.

2. Configuración
Comprobamos los productos que estarán disponibles para su venta en Punto de Venta -> Pedidos -> Productos

imagen

Eliminamos los que no sean necesarios seleccionando el producto y pinchando en Accion -> Suprimir.

imagen

En Punto de venta -> Configuración -> Configuración elegimos las opciones que consideremos oportunas para el funcionamiento del modulo y seleccionamos Aplicar.

imagen

3. Realización de ventas

En Punto de venta -> Tablero aparecen las sesiones disponibles. Si no tenemos ninguna elegir Nueva sesión.

imagen

Aparece el terminal de venta 

imagen

Pinchamos en los productos que se van a vender y elegimos el cliente

imagen

Pinchamos en Pagos, seleccionamos el metodo de pago, si es Efectivo introducimos tambien la cantidad introducida y pinchamos en Validar.

imagen

Genera la venta y muestra el ticket

imagen

4. Realización de devoluciones

Hay que salir del modo terminal de venta pinchando en Cerrar y Confirmar (en la esquina superior derecha).
En Punto de venta -> Pedidos -> Pedidos seleccionamos el pedido del que se quiere realizar la devolución.

imagen

Elegir la opcion Devolver productos

imagen

Al volver a Pedidos aparece otro pedido igual pero con el importe negativo por ser una devolución. 

Pinchar en el y confirmar la devolucion del dinero eligiendo Pagos -> Realizar pago

imagen

5. Comprobacion de stock

En Movimientos de existencias comprobamos que se realizó la venta correctamente pasando los productos del almacen a la ubicación del cliente, y que al realizar la devolución el producto volvió del cliente al almacen.

imagen

# MÓDULO CRM

1. Instalación

En modo desarrollador buscar el modulo CRM en Aplicaciones e instalar.
En Ventas aprecen funcionalidades nuevas ademas de otras pestañas como Calendario o Rastreador de enlaces

imagen

2. Crear oportunidades de venta

Pinchamos en Ventas directas -> Nuevo -> Oportunidad

imagen

Pinchamos en presupuesto y aparece un formulario.
En el presuopuesto le vamos a aplicar un 10% de descuento, para ello creamos una tarifa sobre la Tarifa general (pinchamos en el desplegable Tarifa -> Crear tarifa) y se la aplicamos.

imagen

Añadir los productos al presupuesto y guardar.

3. Enviar presupuesto por correo electrónico

En el presupuesto pinchar en Enviar por correo electrónico.

imagen

imagen

Pulsamos en Enviar

4. Planificar llamada a cliente

En Ventas -> Flujo de Ventas aparecen las Oportunidades creadas, en este caso el presupuesto enviado.

imagen

Pinchamos en la oportunidad, en un circulo de color muy pequeño que aparece junto al simbolo de la camara. Rellenar el dialogo que aparece con la informacion de la actividad a realizar y pinchar Planificar actividad.

imagen

5. Ganar oportunidad de venta

En Ventas -> Flujo de ventas pinchamos en la oportunidad y en la opción Marcar como ganada
imagen

# CREAR SITIO WEB

1. Instalar Constructor de sitio web

Con el modo desarrollador activado vamos a Aplicaciones e instalamos Constructor del sitio web.

2. Elegir tipo de plantilla
  
imagen 1 3/12

Aparece estas dos opciones al instalar la aplicación. Elijo Plain Bootstrap y pincho en el boton Instalar que tiene en la esquina inferior derecha.

imagen 2

3. Personalizar la pagina

Solo es necesario seguir las marcas que aparecen del tutorial e ir realizando las acciones que nos indican.
En primer lugar pulsamos en Editar y empezamos a modificar los elementos:

imagen 3

4. Incorporar localización con Google Maps

En Administración del sitio web -> Configuración -> Dominio -> Google Maps seguir el enlace para crear la clave API

imagen 

Crear una key de la API de Google

imagen anterior

Introducirla en Odoo



# INSTALAR TIENDA ONLINE

Encuentro problemas en la instalacion de la tienda asique tengo que volver a una instantanea anterior, justo despues de la creación de los productos, los clientes y los proveedores.

imagen dia 4

1. Instalar la aplicaión

En modo desarrollador ir a Aplicaciones e instalar Tienda del sitio web. Si no se ha instalado la aplicación del sitio web esta se instalará automaticamente.

2. Editar la tienda y el sitio web

Elegir el tema entre los dos que te proponen. Aparece la página de inicio y solo hay que seguir el tutorial empezando por opción Editar. Es como con configurar el sitio web, solo que esta vez añaden la pestaña tienda.

imagen























