# deliverNOW - App de pedidos a domicilio

**deliverNOW** es una aplicación diseñada para facilitar el pedido y entrega de productos a domicilio. Actualmente, se centra en la compra de comida de restaurantes y productos de supermercados o tiendas. La app se compone de varios servicios que se comunican entre sí, permitiendo a los usuarios realizar pedidos, gestionar pagos, asignar repartidores y consultar el estado de sus pedidos.

## Arquitectura general

La aplicación se compone de varios microservicios interconectados, que funcionan de forma independiente pero coordinada para ofrecer una experiencia de usuario fluida. Cada servicio está contenido en un contenedor Docker, y la base de datos se encuentra en un servicio separado.

Los principales servicios que componen **deliverNOW** son:

1. **Backend de pedidos** (Spring)
2. **Backend de asignación de repartidores** (Spring)
3. **Backend de pagos** (Spring)
4. **Backend de consulta de pedidos** (Spring)
5. **Frontend** (React)
6. **Base de datos** (PostgreSQL)

Cada uno de estos servicios tiene su propio repositorio en GitHub, con código y configuraciones necesarias para ejecutar la aplicación en contenedores Docker.

## Repositorios

A continuación se presentan los enlaces a los repositorios correspondientes para cada uno de los servicios:

### 1. [deliverNOW-docs (repositorio actual)](https://github.com/sbarba-indra2025/deliverNOW-docs)

Este repositorio contiene toda la **documentación** de la aplicación, incluyendo este README. Aquí puedes encontrar detalles sobre la arquitectura, los flujos de la aplicación y las instrucciones para desplegar los servicios.

### 2. [deliverNOW-front](https://github.com/sbarba-indra2025/deliverNOW-front)

Este repositorio contiene el **frontend** de la aplicación, desarrollado en React. El frontend interactúa con todos los servicios backend para permitir a los usuarios realizar pedidos, consultar el estado de sus pedidos, asignar repartidores y gestionar pagos.

### 4. [deliverNOW-repartidores](https://github.com/sbarba-indra2025/deliverNOW-repartidores)

Este servicio gestiona la **asignación de repartidores** a los pedidos. Utiliza un algoritmo que tiene en cuenta la **disponibilidad** y la **distancia** entre los repartidores y la dirección del usuario para asignar el repartidor más adecuado. También permite la asignación manual, donde el usuario puede elegir un repartidor de una lista disponible.

### 5. [deliverNOW-pagos](https://github.com/sbarba-indra2025/deliverNOW-pagos)

Este repositorio contiene el servicio encargado de la **gestión de pagos**. Permite a los usuarios pagar sus pedidos de manera segura y gestionar el estado de los pagos.

### 6. [deliverNOW-pedidos](https://github.com/sbarba-indra2025/deliverNOW-pedidos)

Este es el servicio principal para la **gestión de pedidos**. Permite a los usuarios crear nuevos pedidos, seleccionar la categoría, proveedor y productos, y enviar el pedido para que sea procesado.

### 7. [deliverNOW-consulta](https://github.com/sbarba-indra2025/deliverNOW-consulta)

Este servicio permite a los usuarios **consultar el estado de sus pedidos**. A través de este, los usuarios pueden acceder a la lista de pedidos realizados, junto con detalles importantes como el estado del pedido y el repartidor asignado.

### 8. [deliverNOW-db](https://github.com/sbarba-indra2025/deliverNOW-db)

Este repositorio contiene la configuración de la **base de datos** PostgreSQL que almacena todos los datos relacionados con los pedidos, los repartidores, y los pagos de los usuarios.

## Flujos disponibles para el usuario

La aplicación permite a los usuarios interactuar a través de diferentes flujos para realizar sus pedidos y gestionar su experiencia de compra. Los flujos principales son:

### 1. **Realizar un pedido**

* El usuario selecciona el tipo de pedido (comida, productos de supermercado, etc.).
* Elige el proveedor (restaurante, supermercado, tienda).
* Selecciona los productos que desea comprar y realiza el pedido.

### 2. **Asignación de repartidor**

* Una vez realizado el pedido, el sistema asigna un repartidor de manera **automática** según su **disponibilidad** y su **distancia** respecto a la ubicación del usuario.
* El usuario también puede optar por la **asignación manual**, eligiendo de una lista de repartidores disponibles.

### 3. **Pago del pedido**

* Una vez que el pedido ha sido asignado a un repartidor, el usuario puede proceder al pago a través del servicio de gestión de pagos. Este flujo permite realizar el pago de manera segura.

### 4. **Consulta de pedidos**

* El usuario puede acceder a un historial de sus **pedidos anteriores** y consultar el estado actual de sus pedidos activos (en preparación, entregado, etc.), así como la información del repartidor asignado.

## Licencia

Este proyecto está licenciado bajo la [Licencia MIT](LICENSE).

---

## Instrucciones de despliegue

Para desplegar la aplicación, tienes dos opciones:

1. **Desplegar todos los servicios de forma conjunta** utilizando Docker Compose.
2. **Desplegar los servicios individualmente** utilizando los `Dockerfile` en cada repositorio.

### Despliegue conjunto con Docker Compose

Si se quiere levantar todos los servicios al mismo tiempo, se puede usar el archivo `docker-compose.yml` que se encuentra en este repositorio. Este archivo está configurado para crear y ejecutar los contenedores necesarios para todos los servicios (backend, frontend y base de datos) en un solo comando.

#### Pasos para desplegar con Docker Compose:

1. Clonar este repositorio:

   ```bash
   git clone https://github.com/sbarba-indra2025/deliverNOW-docs.git
   cd deliverNOW-docs
   ```

2. Es necesario tener instalados **Docker** y **Docker Compose** siguiendo las [instrucciones oficiales de Docker](https://docs.docker.com/get-docker/) para instalarlos.

3. En la raíz de este repositorio, se encuentra el archivo `docker-compose.yml`. Este archivo ya está configurado para levantar todos los servicios, incluidos los backends de pedidos, asignación de repartidores, pagos, consulta de pedidos, el frontend, y la base de datos.

4. Para ejecutar todos los servicios:

   ```bash
   docker-compose up --build
   ```

   Este comando hará lo siguiente:

   * Construirá las imágenes de los servicios usando los `Dockerfile` correspondientes (en cada subdirectorio de servicio).
   * Levantará todos los contenedores necesarios.
   * Expondrá los puertos de los servicios según lo especificado (por ejemplo, el frontend estará disponible en `http://localhost:3000`).

5. Una vez que todos los contenedores estén levantados, se puede acceder a la aplicación a través del navegador en la URL:

   ```
   Frontend: http://localhost:3000
   ```

   También se puede interactuar con los servicios backend, que estarán expuestos en los siguientes puertos:

   * Backend de creación de pedidos: `http://localhost:8081`
   * Backend de asignación de repartidores: `http://localhost:8082`
   * Backend de pagos: `http://localhost:8083`
   * Backend de consulta de pedidos: `http://localhost:8084`
   * Base de datos (PostgreSQL): `localhost:5432` (utiliza las credenciales `admin/admin` para conectarte)

### Despliegue de los servicios de forma independiente

Cada servicio puede ser ejecutado de forma independiente utilizando los `Dockerfile` correspondientes que se encuentran en los repositorios de cada servicio.

#### Pasos para ejecutar un servicio individualmente:

1. **Clonar el repositorio correspondiente**. Por ejemplo, para ejecutar el servicio de "backend de creación de pedidos", clonar el siguiente repositorio:

   ```bash
   git clone https://github.com/sbarba-indra2025/deliverNOW-pedidos.git
   cd deliverNOW-pedidos
   ```

2. **Construir la imagen Docker**. Desde el directorio del repositorio:

   ```bash
   docker build -t <nombre_imagen> .
   ```

   Por ejemplo:

   ```bash
   docker build -t deliverNOW-backend-pedidos .
   ```

3. **Ejecutar el contenedor**. Una vez que la imagen esté construida, se puede ejecutar el contenedor ejecutando:

   ```bash
   docker run -p <puerto_local>:8080 <nombre_imagen>
   ```

   Donde `<puerto_local>` es el puerto en el que se va exponer el servicio en la máquina local. Por ejemplo:

   ```bash
   docker run -p 8081:8080 deliverNOW-backend-pedidos
   ```

#### Puntos a tener en cuenta durante la ejecución individual:

* **Conexiones entre servicios**: Cuando se ejecutan servicios de forma independiente, es necesario configurar manualmente las conexiones entre los contenedores, indicando las direcciones IP de los contenedores o las redes de Docker.

* **Base de datos**: En el `docker-compose.yml`, la base de datos está ya configurada con todas las estructuras de datos y credenciales de usuario necesarios. Si se ejecutan los servicios individualmente, hay que asegurarse de tener las credenciales y los datos correctos (usuario: `admin`, contraseña: `admin`, base de datos: `delivernowdb`).
