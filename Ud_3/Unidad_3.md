![Logo Odoo][odoo]

# Indice<a name="indice"/>

* [Crear nueva base de datos](#id1)
* [Modificar la compañia por defecto](#id2)
* [Instalar los módulos de la internacionalización al español](#id3)
* [Establecer el plan contable para una PYME española](#id4)
* [Instalar los modulos necesarios para la práctica](#id5)
  * [Ventas](#id5a)
  * [Gestión de inventario](#id5b)
  * [Gestión de compras](#id5c)
* [Crear almacenes](#id6)
* [Crear proveedores](#id7)
* [Crear clientes](#id8)
* [Crear categorías de productos](#id9)
* [Crear productos](#id10)
* [Crear tarifa de venta](#id11)
* [Realizar pedido a proveedor](#id12)
  1. [Realizar pedido](#id12a)
  2. [Recibir pedido](#id12b)
  3. [Generar factura](#id12c)
  4. [Realizar pago](#id12d)
* [Realizar venta a cliente](#id13)
  1. [Realizar venta](#id13a)
  2. [Comprobar stock](#id13b)
  3. [Generar factura](#id13c)
  4. [Registrar pago](#id13d)
* [Módulo TPV](#id14)
  1. [Instalación](#id14a)
  2. [Configuración](#id14b)
  3. [Realización de ventas](#id14c)
  4. [Realización de devoluciones](#id14d)
  5. [Comprobacion de stock](#id14e)
* [Módulo CRM](#id15)
  1. [Instalación](#id15a)
  2. [Crear oportunidades de venta](#id15b)
  3. [Enviar presupuesto por correo electrónico](#id15c)
  4. [Planificar llamada a cliente](#id15d)
  5. [Ganar oportunidad de venta](#id15e)



# Contenido

## Crear nueva base de datos<a name="id1"/>

Al conectar a Odoo a través del servicio web  nos ofrece conectarnos a las bases de datos de que disponemos, y tambien crear nuevas:

![Captura de pantalla 1][img1]

[**Indice**](#indice)

## Modificar la compañia por defecto<a name="id2"/>

`Configuracion > Compañias > Editar`

Incluimos los datos necesarios.

![Captura de pantalla 2][img2]

[**Indice**](#indice)

## Instalar los módulos de la internacionalización al español<a name="id3"/>

* l10n_es

![Captura de pantalla 3][img3]

* l10n_es_partner

![Captura de pantalla 4][img4]

* l10n_es_toponyms

![Captura de pantalla 5][img5]

[**Indice**](#indice)

## Establecer el plan contable para una PYME española<a name="id4"/>

> Contabilidad > Configuracion > Plan Contable > Plantilla

Elegimos PGCE PYMEs 2008

Se rellenan los datos automaticamente con la informacion que tenemos de los modulos instalados.

Pinchamos en Aplicar.

![Captura de pantalla 6][img6]

[**Indice**](#indice)

## Instalar los modulos necesarios para la práctica<a name="id5"/>

#### Ventas<a name="id5a"/>

![Captura de pantalla 7][img7]

#### Gestion de inventario<a name="id5b"/>

![Captura de pantalla 8][img8]

#### Gestion de compras<a name="id5c"/>

![Captura de pantalla 9][img9]

[**Indice**](#indice)

## Crear almacenes<a name="id6"/>

> Inventario > Configuracion > Ubicación y almacén > Nivel de uso de almacenes y ubicaciones

Marcar la opción **Gestiona varios Almacenes, con varias ubicaciones cada uno**.

![Captura de pantalla 10][img10]

Aparece la opción Gestión de almacenes.
Modifico el almacen que aparece por defecto y creo los Almacenes extra que necesite.

![Captura de pantalla 11][img11]

Creo las ubicaciones necesarias dentro de los almacenes indicando en ubicacion padre el almacen al que pertenece.

![Captura de pantalla 12][img12]

En este caso no es necesario dado que solo necesitamos una ubicacion por almacen que por defecto es existencias.
Una vez creadas aparecen listadas en Ubicaciones:

![Captura de pantalla 13][img13]

[**Indice**](#indice)

## Crear proveedores<a name="id7"/>

> Compras > Proveedores > Crear

![Captura de pantalla 14][img14]

Se rellenan sus datos, sin olvidar el NIF que va en la pestaña de Contabilidad, incluyendo delante el prefijo ES para que el sistema lo acepte.

No olvidar marcar la casilla de Compañia en vez de Individual en caso de que sea una empresa.

En caso de que ya tuvieramos creada la compañia bastaría con elegirla en el despelegable que aparece debajo del nombre.

![Captura de pantalla 15][img15]

Si en la pestaña Ventas y Compras del formulario hemos marcado la casilla indicando que son proveedores deberian aparecer en la pagina principal de proveedores:

![Captura de pantalla 16][img16]

[**Indice**](#indice)

## Crear clientes<a name="id8"/>

> Ventas > Clientes > Crear

![Captura de pantalla 17][img17]

Se rellenan los datos exactamente igual que para los proveedores, solo que esta vez marcaremos la casilla de cliente en vez de proveedor y la casilla Individual si son personas.

![Captura de pantalla 18][img18]

Comprobamos que aparecen en la pagina de Clientes:

![Captura de pantalla 19][img19]

[**Indice**](#indice)

## Crear categorías de productos<a name="id9"/>

> Inventario > Categoria de productos > Crear

![Captura de pantalla 20][img20]

Creamos las categorias jerarquicamente:

1. 'Software' que herede de 'Todos'

2. Despues 'Sistemas operativos' que herede de 'Software'

![Captura de pantalla 21][img21]

Repetimos la operacion con la categoria 'Hardware' que tendra varios niveles de subcategorías:

1. Crear categoria 'Hardware' que herede de 'Todos'

2. Crear categorias hijas 'Portatiles' y 'Componentes' que hereden de 'Hardware'

3. Crear 'DiscosSSD' y 'Graficas' que hereden de 'Componentes'

Deberia quedar asi:

![Captura de pantalla 22][img22]

[**Indice**](#indice)

## Crear productos<a name="id10"/>

> Inventario > Productos > Crear

![Captura de pantalla 23][img23]

Rellenar los datos con la información del producto.

Indicar el **coste del producto** en *Coste*.

En *Factura* tenemos que indicar los **impuestos de compra y de venta** para que aparezca de forma automática.

En *Precio de venta* no pongo nada porque despues se utilizara una Tarifa para que lo calcule automáticamente en la factura.

El **proveedor** lo indico en la pestaña *Inventario*, añadiendo uno nuevo y eligiendo uno de los proveedores ya existentes, incluyendo el nombre del producto y el precio.

Incluyo la **descripcion** en la pestaña *Notas*.

Para indicar la **cantidad** que hay en stock pinchar en el boton *Actualizar cantidad de stock fisico* (arriba a la izquierda) y elegir la ubicacion.
Añadir las actualizaciones necesarias para incluir las existencias de cada ubicacion.

![Captura de pantalla 24][img24]

Al terminar se deberian encontrar todos en la pagina principal de productos

![Captura de pantalla 25][img25]

[**Indice**](#indice)

## Crear tarifa de venta<a name="id11"/>

> Ventas > Configuracion > Precio > Precio de Venta

Marcar la opción **Precios avanzados basados en fórmulas (descuentos, márgenes, redondeo)**.

![Captura de pantalla 25b][img25b]

Aparece la opcion *Tarifas*.

Para crear una nueva:

![Captura de pantalla 26][img26]

> Ventas > Tarifas > Crear  

Se añaden los elementos sobre los que se va a aplicar la tarifa, en este caso sobre una determinada categoria.

Para establecer un precio calculado sobre el precio de coste se indica la opcion *Fórmula*, donde marcamos *Sobre precio de coste*, y en *Descuento* ponemos un descuento negativo para que resulte en el aumento de precio que queremos conseguir.

Para que el precio del software sea de 1.9 el precio de coste indico un descuento del -90%.

Se puede visualizar la lista completa de tarifas:

![Captura de pantalla 27][img27]

Para aplicar las tarifas deberemos hacerlo al crear un pedido de ventas.

Se puede crear una Tarifa general y añadir reglas que calcularán el precio con distintas fórmulas según la categoria de producto. Asi, si en un mismo pedido tenemos productos de distintas categorías, aplicando la Tarifa general realizará los cálculos correctamente para todos los productos de forma independiente.

[**Indice**](#indice)

## Realizar pedido a proveedor<a name="id12"/>

> Compras > Pedidos de compra > Crear

#### 1. Realizar pedido<a name="id12a"/>

* Elegir el proveedor y la fecha.
* Añadir los productos, eligiendo del desplegable (deberia aparecer la informacion del producto al elegirlo).
* El IVA deberia aparecer automaticamente si se ha indicado en la creación del producto.
* Indicar las unidades de cada producto.

![Captura de pantalla 28][img28]

Se ha creado la solicitud de presupuesto. Ahora pinchamos en *Confirmar pedido*.

![Captura de pantalla 29][img29]

[**Indice**](#indice)

#### 2. Recibir pedido<a name="id12b"/>

Elijo el pedido y pincho en *Recibir productos*.

![Captura de pantalla 30][img30]

Modificar el documento indicando en cada producto la misma **cantidad** en *Hecho* que la que aparece en *Para ejecutar* y modificando la **ubicacion** de recepcion. Pinchando despues en *Validar*.

![Captura de pantalla 31][img31]

Ahora el pedido aparece en estado *Para facturar*.

Se pueden consultar todos los Movimientos en:

> Inventario > Movimientos de existencias

[**Indice**](#indice)


#### 3. Generar factura<a name="id12c"/>

En el pedido pinchamos en *Facturas de p...* (esquina superior derecha del formulario del pedido) y en *Crear*.

Aparece el nombre del proveedor seleccionado y los datos del pedido. Elegir la fecha de la factura y pinchar en *Validar*.

![Captura de pantalla 32][img32]  

[**Indice**](#indice)

#### 4. Realizar pago<a name="id12d"/>

Pinchar en la opcion *Registrar pago* (esquina superior izquierda en la propia factura).

![Captura de pantalla 33][img33]   

En el diálogo que aparece indicar la opcion de pago elegido y *Validar*.

![Captura de pantalla 34][img34]   

Debe aparecer como **Pagado**.

[**Indice**](#indice)

## Realizar venta a cliente<a name="id13"/>

#### 1. Realizar venta<a name="id13a"/>

Elegimos el cliente que desea realizar la compra en

> Ventas > Clientes

![Captura de pantalla 35][img35]  

Pinchamos en *Ventas* (esquina superior derecha de la ficha del cliente) y aparecera el listado de todas las ventas realizadas a ese cliente.

Seleccionamos la opcion *Crear*.

![Captura de pantalla 36][img36]  

* Seleccionar los **productos** y la **cantidad**. Debe aparecer toda la información de los mismos en el formulario automáticamente.
* Seleccionar la **tarifa** que se le aplica.
* Elegir desde que ubicación se le envían los productos en la pestaña *Otra informacion*. Asegurarse de que es la correcta y comprobar si hay existencias suficientes.

Guardamos y pinchamos en *Confirmar venta* si todo es correcto.

![Captura de pantalla 37][img37]

Si queremos realizar varios pedidos repetimos el proceso.

[**Indice**](#indice)

#### 2. Comprobar stock<a name="id13b"/>

Para comprobar todas las operaciones realizadas sobre el stock:

> Inventario > Informes > Movimientos de existencias

Movimientos de una ubicacion a otra, compras, ventas... Aparece la informacion de los productos, ubicacion inicial, ubicacion final y su estado.

[**Indice**](#indice)

#### 3. Generar factura<a name="id13c"/>

> Ventas > Presupuestos

Seleccionamos los pedidos de los que vamos a generar la factura y pinchamos en el desplegable:

> Accion > Orden de facturacion

Elegimos *Crear y ver facturas* y *Validar*.

![Captura de pantalla 38][img38]

[**Indice**](#indice)

#### 4. Registrar pago<a name="id13d"/>

> Contabilidad > Ventas > Factura de cliente

Elegir la factura y al pinchar en ella aparece el formulario de la misma.

Pinchar en *Registrar pago*.

![Captura de pantalla 39][img39]  

Elegir la forma de pago y *Validar*.

Debe aparecer como **pagada**.

[**Indice**](#indice)

## Módulo TPV<a name="id14"/>

#### 1. Instalación<a name="id14a"/>

En *Configuración* activar el **modo desarrollador** (esquina inferior derecha)

Buscar en *Aplicaciones* el módulo *Punto de Venta* e instalar.

#### 2. Configuración<a name="id14b"/>

Comprobamos los productos que estarán disponibles para su venta en:

> Punto de Venta > Pedidos > Productos

![Captura de pantalla 40][img40]

Eliminamos los que no sean necesarios seleccionando el producto y pinchando en

> Accion > Suprimir

![Captura de pantalla 41][img41]

> Punto de venta > Configuración > Configuración

Elegir las opciones que se consideren oportunas para el funcionamiento del módulo y seleccionar *Aplicar*.

![Captura de pantalla 42][img42]

[**Indice**](#indice)

#### 3. Realización de ventas<a name="id14c"/>

Las sesiones disponibles aparecen en:

> Punto de venta > Tablero

Si no tenemos ninguna elegir *Nueva sesión*.

![Captura de pantalla 43][img43]  

Aparece el terminal de venta.

![Captura de pantalla 44][img44]

Pinchar en los **productos** que se van a vender y elegir el **cliente**.

![Captura de pantalla 45][img45]

Pinchar en *Pagos*, seleccionar el **metodo de pago**, si es *Efectivo* introducir también la cantidad introducida y pinchar en *Validar*.

![Captura de pantalla 46][img46]

Genera la venta y muestra el ticket.

![Captura de pantalla 47][img47]

[**Indice**](#indice)

#### 4. Realización de devoluciones<a name="id14d"/>

Salir del modo terminal de venta pinchando en *Cerrar* y *Confirmar* (en la esquina superior derecha).

> Punto de venta > Pedidos > Pedidos

Seleccionar el pedido del que se quiere realizar la devolución:

![Captura de pantalla 48][img48]

Elegir la opcion *Devolver productos*.

![Captura de pantalla 49][img49]

Al volver a *Pedidos* aparece otro pedido igual pero con el importe negativo por ser una devolución.

Pinchar en él y confirmar la devolución del dinero eligiendo:

> Pagos > Realizar pago

![Captura de pantalla 50][img50]

[**Indice**](#indice)

#### 5. Comprobacion de stock<a name="id14e"/>

En *Movimientos de existencias* comprobamos que se realizó la venta correctamente pasando los productos del almacén a la ubicación del cliente, y que al realizar la devolución el producto volvió del cliente al almacén.

![Captura de pantalla 51][img51]

[**Indice**](#indice)

## Módulo CRM<a name="id15"/>

#### 1. Instalación<a name="id15a"/>

Con el **modo desarrollador** activado buscar el modulo CRM en *Aplicaciones* e instalar.

En *Ventas* aparecen funcionalidades nuevas además de otras pestañas como *Calendario* o *Rastreador de enlaces*.

![Captura de pantalla 52][img52]

[**Indice**](#indice)

#### 2. Crear oportunidades de venta<a name="id15b"/>

> Ventas directas > Nuevo > Oportunidad

![Captura de pantalla 53][img53]

Aparece el formulario de la Oportunidad.

![Captura de pantalla 54][img54]

Pinchamos en *Presupuesto* y aparece un formulario para rellenar.

Le vamos a aplicar un 10% de descuento, para ello creamos una tarifa sobre la Tarifa general.

> Tarifa > Crear tarifa

Pinchamos en el desplegable y se la aplicamos. Después en *Guardar y cerrar*.

![Captura de pantalla 55][img55]

Añadir los productos al presupuesto y guardar.

[**Indice**](#indice)

#### 3. Enviar presupuesto por correo electrónico<a name="id15c"/>

![Captura de pantalla 56][img56]

En el presupuesto pinchar en *Enviar por correo electrónico*.

![Captura de pantalla 57][img57]

Introducimos los datos necesarios pulsamos en *Enviar*.

![Captura de pantalla 58][img58]

[**Indice**](#indice)

#### 4. Planificar llamada a cliente<a name="id15d"/>

Para consultar las Oportunidades creadas, en este caso el presupuesto enviado:

> Ventas > Flujo de Ventas

![Captura de pantalla 59][img59]

Pinchar en la oportunidad, en un circulo de color, muy pequeño, que aparece junto al simbolo de la camara.

Rellenar el diálogo que aparece con la información de la actividad a realizar y pinchar en *Planificar actividad*.

![Captura de pantalla 60][img60]

[**Indice**](#indice)

#### 5. Ganar oportunidad de venta<a name="id15e"/>

> Ventas > Flujo de ventas

Pinchar en la oportunidad, en la opción *Marcar como ganada*.

![Captura de pantalla 61][img61]

[**Indice**](#indice)

## Crear sitio web<a name="id16"/>

Con el **modo desarrollador** activado ir a *Aplicaciones* e instalar *Constructor del sitio web*.

Aparecen dos plantillas para elegir al instalar la aplicación:

![Captura de pantalla 62][img62]

Elijo Plain Bootstrap y pincho en el boton *Instalar* que tiene en la esquina inferior derecha.

![Captura de pantalla 63][img63]

[**Indice**](#indice)

Para personalizar la pagina solo es necesario seguir las marcas que aparecen del tutorial e ir realizando las acciones que nos indican.

En primer lugar pulsamos en Editar y empezamos a modificar los elementos:

![Captura de pantalla 64][img64]

[**Indice**](#indice)

## Instalar tienda online<a name="id17"/>

Encuentro problemas en la instalacion de la tienda asique tengo que volver a una instantanea anterior, justo despues de la creación de los productos, los clientes y los proveedores.

![Captura de pantalla 65][img65]

#### 1. Instalar la aplicación

En **modo desarrollador** ir a *Aplicaciones* e instalar *Tienda del sitio web*. Si no se ha instalado la aplicación *Sitio web* esta se instalará automaticamente.

[**Indice**](#indice)

#### 2. Editar la tienda y el sitio web

Elegir el tema entre los dos que te proponen. Aparece la página de inicio y solo hay que seguir el tutorial empezando por opción Editar. Es como con configurar el sitio web, solo que esta vez añaden la pestaña *Tienda*.

![Captura de pantalla 66][img66]

En la tienda aparecen automáticamente los productos que hubiera ya creados.

![Captura de pantalla 67][img67]

Personalizar el sitio web arrastrando los componentes de la paleta que aparece a la izquierda y modificando textos e imagenes.

![Captura de pantalla 68][img68]  

[**Indice**](#indice)

#### 3. Cambiar la configuración de la tienda y el sitio web

> Administración del sitio web > Configuración

![Captura de pantalla 69][img69]

Entre otras cosas podemos editar la configuración de envios de email de confirmación de pedido.

[**Indice**](#indice)

#### 4. Incorporar localización con Google Maps

> Administración del sitio web > Configuración > Dominio > Google Maps

Seguir el enlace para crear la clave API

![Captura de pantalla 70][img70]

Crear una key de la API de Google.

![Captura de pantalla 71][img71]

Introducirla en Odoo.

Si vamos al **sitio web**, en la pestaña *Contáctenos* aparece un mapa con la dirección que ha sacado de la información de la empresa.

![Captura de pantalla 72][img72]

[**Indice**](#indice)

#### 5. Formas de pago

Añadir la tarifa que se va a aplicar a los productos de la tienda.
Administración del sitio web -> Catálogo -> Tarifas -> Crear

imagen

Añadir metodos de pago.
Administración del sitio web -> Configuración -> Tienda del sitio web -> Metodos de pago

imagen

Compruebo que Transferencia bancaria este instalado y si es necesario cambio la configuración.

imagen

[**Indice**](#indice)

#### 6. Realizar compra a traves de la tienda online

Al haber añadido las tarifas se deben visualizar correctamente los precios de los productos.

imagen

Realizamos la primera compra para comprobar que todo funciona correctamente. Pincho en Añadir a la cesta.

imagen

Elegir Continuar a caja y en la Cesta elegir la opción Procesar compra para pasar al ingreso de los datos y el pago de la misma.

imagen

Después de confirmar la dirección de envío y facturación llegamos a la elección del método de pago. En este caso solo tenemos Transferencia bancaria.

imagen

Al confirmar, el pedido aparece pendiente de pago.

imagen

Vamos a Administracion del sitio web -> Pedidos -> Órdenes sin pagar donde se ha creado un registro con el nuevo pedido.

imagen

Si pinchamos en ella podemos Confirmar venta y Facturar.

imagen

Validar la factura y Registrar el pago.

imagen

Ahora en facturas ya aparece la orden como pagada.

[**Indice**](#indice)

#### 7. Enviar email de confiramción de compra

En Administración del sitio web -> Pedidos podemos pinchar en el pedido y enviar por correo electrónico.
Elegir la plantilla que hemos creado anterioemente en la configuración y Enviar.

imagen

[**Indice**](#indice)

## ANÁLISIS DE BASE DE DATOS ODOO

Para comprobar la estructura de la base de datos creada por Odoo tenemos varias opciones de conexión (desde el propio servidor, conectar por ssh al servidor y conectar por psql...).
En este caso voy a establecer una conexión remota directamente con la base de datos.
Para ello hay que modificar la configuración de postgres para permitir las conexiones remotas.

1. Acceder a los archivos de configuración de postgres en el servidor

Conectar con root:

`$ ssh root@192.168.3.58`

`$ nano /etc/postgresql/9.5/main/postgresql.conf`

imagen

Descomentamos la linea listen_addresses y ponemos un asterisco
para que permita conectar a cualquier IP.

imagen

`$ /etc/postgresql/9.5/main/pg_hba.conf`

* Cambiar 9.5 por la version de postgres que se tenga instalada.

En IPv4 local connections poner all en todas las opciones y guardar.

imagen

[**Indice**](#indice)

2. Instalar cliente de base de datos postgresql

En la máquina desde la que quieres acceder debes instalar el cliente postgres.

`$ sudo apt-get install postgresql-client`

[**Indice**](#indice)

3. Instalación cliente de base de DATOS

Instalar pgAdmin3, que se puede encontrar facilmente en la aplicación de software.

[**Indice**](#indice)

4. Conectar remotamente a la base de datos

Crear una nueva conexión a base de datos e introducir la información de la misma.

imagen

[**Indice**](#indice)

5. Acceder a la información de la base de DATOS

Elegir la base de datos deseada en el panel izquierdo y navegar a través de las pestañas desplegables que aparecen para ver la información.

imagen

En este caso la base de datos informatica_sotrondio cuenta con 341 tablas en total, que al pinchar en Tables aparecen listadas en la pestaña Properties del panel derecho.

Podemos acceder a toda la información de la empresa desde aquí, como por ejemplo la información de login de la empresa.

imagen

Para buscar cualquier objeto de la base de datos accedemos desde la pestaña Edit -> Search objects.

Si queremos acceder a la información de las tablas solo tenemos que pinchar el botón derecho soble el nombre de la tabla y elegir View data.

imagen

[**Indice**](#indice)






[odoo]: ./capturas/odoo_logo.png
[img1]: ./capturas/img1.png
[img2]: ./capturas/img2.png
[img3]: ./capturas/img3.png
[img4]: ./capturas/img4.png
[img5]: ./capturas/img5.png
[img6]: ./capturas/img6.png
[img7]: ./capturas/img7.png
[img8]: ./capturas/img8.png
[img9]: ./capturas/img9.png
[img10]: ./capturas/img10.png
[img11]: ./capturas/img11.png
[img12]: ./capturas/img12.png
[img13]: ./capturas/img13.png
[img14]: ./capturas/img14.png
[img15]: ./capturas/img15.png
[img16]: ./capturas/img16.png
[img17]: ./capturas/img17.png
[img18]: ./capturas/img18.png
[img19]: ./capturas/img19.png
[img20]: ./capturas/img20.png
[img21]: ./capturas/img21.png
[img22]: ./capturas/img22.png
[img23]: ./capturas/img23.png
[img24]: ./capturas/img24.png
[img25]: ./capturas/img25.png
[img25b]: ./capturas/img25b.png
[img26]: ./capturas/img26.png
[img27]: ./capturas/img27.png
[img28]: ./capturas/img28.png
[img29]: ./capturas/img29.png
[img30]: ./capturas/img30.png
[img31]: ./capturas/img31.png
[img32]: ./capturas/img32.png
[img33]: ./capturas/img33.png
[img34]: ./capturas/img34.png
[img35]: ./capturas/img35.png
[img36]: ./capturas/img36.png
[img37]: ./capturas/img37.png
[img38]: ./capturas/img38.png
[img39]: ./capturas/img39.png
[img40]: ./capturas/img40.png
[img41]: ./capturas/img41.png
[img42]: ./capturas/img42.png
[img43]: ./capturas/img43.png
[img44]: ./capturas/img44.png
[img45]: ./capturas/img45.png
[img46]: ./capturas/img46.png
[img47]: ./capturas/img47.png
[img48]: ./capturas/img48.png
[img49]: ./capturas/img49.png
[img50]: ./capturas/img50.png
[img51]: ./capturas/img51.png
[img52]: ./capturas/img52.png
[img53]: ./capturas/img53.png
[img54]: ./capturas/img54.png
[img55]: ./capturas/img55.png
[img56]: ./capturas/img56.png
[img57]: ./capturas/img57.png
[img58]: ./capturas/img58.png
[img59]: ./capturas/img59.png
[img60]: ./capturas/img60.png
[img61]: ./capturas/img61.png
[img62]: ./capturas/img62.png
[img63]: ./capturas/img63.png
[img64]: ./capturas/img64.png
[img65]: ./capturas/img65.png
[img66]: ./capturas/img66.png
[img67]: ./capturas/img67_.png
[img68]: ./capturas/img68_.png
[img69]: ./capturas/img69.png
[img70]: ./capturas/img70.png
[img71]: ./capturas/img71.png
[img72]: ./capturas/img72.png
[img73]: ./capturas/img73.png
[img74]: ./capturas/img74.png
[img75]: ./capturas/img75.png
[img76]: ./capturas/img76.png
[img77]: ./capturas/img77.png
[img78]: ./capturas/img78.png
[img79]: ./capturas/img79.png
[img80]: ./capturas/img80.png
[img81]: ./capturas/img81.png
[img82]: ./capturas/img82.png
[img83]: ./capturas/img83.png
[img84]: ./capturas/img84.png
[img85]: ./capturas/img85.png
[img86]: ./capturas/img86.png
[img87]: ./capturas/img87.png
[img88]: ./capturas/img88.png
[img89]: ./capturas/img89.png
[img90]: ./capturas/img90.png
[img91]: ./capturas/img91.png
[img92]: ./capturas/img92.png
[img93]: ./capturas/img93.png
[img94]: ./capturas/img94.png
