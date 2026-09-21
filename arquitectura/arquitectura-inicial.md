# Arquitectura inicial del sistema

## Arquitectura en tres capas

El Marketplace de productos para mascotas se organiza inicialmente mediante una arquitectura de tres capas, separando las responsabilidades de presentación, lógica de negocio y acceso a datos.

### 1. Capa de Presentación

Esta capa permite la interacción de los usuarios con el sistema.

- Aplicación Web
- API REST

### 2. Capa de Lógica de Negocio

Esta capa contiene las principales funcionalidades y reglas del Marketplace.

- Usuarios
- Sellers
- Catálogo
- Carrito
- Pedidos

### 3. Capa de Datos

Esta capa se encarga del almacenamiento y consulta de la información del sistema.

- Base de datos
## Diagrama de arquitectura

```mermaid
flowchart TD

    subgraph ACTORES["ACTORES"]
        Cliente["Cliente"]
        Seller["Seller"]
        Admin["Administrador"]
    end

    subgraph PRESENTACION["PRESENTACIÓN"]
        Web["Aplicación Web"]
        API["API REST"]
    end

    subgraph NEGOCIO["LÓGICA DE NEGOCIO"]
        Usuarios["Usuarios"]
        Sellers["Sellers"]
        Catalogo["Catálogo"]
        Carrito["Carrito"]
        Pedidos["Pedidos"]
    end

    subgraph DATOS["DATOS"]
        BD["Base de datos"]
    end

    subgraph EXTERNOS["SISTEMAS EXTERNOS"]
        Pago["Pasarela de pago"]
        ERP["ERP"]
        Envio["Servicio de envío"]
    end

    ACTORES --> Web
    Web --> API
    API --> NEGOCIO
    NEGOCIO --> BD

    Pedidos --> Pago
    Pedidos --> Envio
    BD --> ERP
```