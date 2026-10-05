# Estilo arquitectónico del marketplace

## Estilo seleccionado

Se propone un monolito modular. Los módulos de Usuarios, Sellers, Catálogo, Carrito y Pedidos funcionan dentro de una misma aplicación, pero cada uno mantiene separadas sus responsabilidades. El backend se organiza en las capas de presentación, lógica de negocio y datos.

## Diagrama de arquitectura

```mermaid
flowchart TB
    Cliente["Cliente"] --> Web["Cliente web"]
    Seller["Seller"] --> Web
    Admin["Administrador"] --> Web

    subgraph Backend["Marketplace Backend - Node.js y Express"]
        direction TB

        Middleware["Middlewares Express: CORS, JSON, JWT, validación y errores"]

        subgraph Presentacion["1. CAPA DE PRESENTACIÓN"]
            direction LR

            subgraph ModUsuarios["Módulo Usuarios"]
                direction TB
                UR["usuarios.routes.js"] --> UC["usuarios.controller.js"]
            end

            subgraph ModSellers["Módulo Sellers"]
                direction TB
                SR["sellers.routes.js"] --> SC["sellers.controller.js"]
            end

            subgraph ModCatalogo["Módulo Catálogo"]
                direction TB
                CR["catalogo.routes.js"] --> CC["catalogo.controller.js"]
            end

            subgraph ModCarrito["Módulo Carrito"]
                direction TB
                KR["carrito.routes.js"] --> KC["carrito.controller.js"]
            end

            subgraph ModPedidos["Módulo Pedidos"]
                direction TB
                PR["pedidos.routes.js"] --> PC["pedidos.controller.js"]
            end
        end

        subgraph Negocio["2. CAPA DE LÓGICA DE NEGOCIO"]
            direction LR
            US["usuarios.service.js"]
            SS["sellers.service.js"]
            CS["catalogo.service.js"]
            KS["carrito.service.js"]
            PS["pedidos.service.js"]
        end

        subgraph Datos["3. CAPA DE DATOS"]
            direction LR
            URepo["usuarios.repository.js"]
            SRepo["sellers.repository.js"]
            CRepo["catalogo.repository.js"]
            KRepo["carrito.repository.js"]
            PRepo["pedidos.repository.js"]
            ORM["Acceso a datos compartido - Sequelize ORM"]
        end

        Middleware --> UR
        Middleware --> SR
        Middleware --> CR
        Middleware --> KR
        Middleware --> PR

        UC --> US --> URepo
        SC --> SS --> SRepo
        CC --> CS --> CRepo
        KC --> KS --> KRepo
        PC --> PS --> PRepo

        URepo --> ORM
        SRepo --> ORM
        CRepo --> ORM
        KRepo --> ORM
        PRepo --> ORM

        PS -.-> KS
        PS -.-> CS
    end

    Web -->|"HTTPS y JSON"| Middleware
    ORM -->|"SQL"| BD[("PostgreSQL")]
    PS -->|"HTTPS y REST"| Pago["Pasarela de pagos"]
    PS -->|"HTTPS y REST"| Envio["Servicio de envíos"]

    classDef actor fill:#ffffff,stroke:#6b7280,color:#111827
    classDef presentacion fill:#e8f0ff,stroke:#7996c4,color:#172b4d
    classDef negocio fill:#e5f2df,stroke:#7ea573,color:#1e3a20
    classDef datos fill:#fff1d8,stroke:#d4a75d,color:#523c17
    classDef externo fill:#eeeeee,stroke:#888888,color:#222222

    class Cliente,Seller,Admin actor
    class Web,Middleware,UR,UC,SR,SC,CR,CC,KR,KC,PR,PC presentacion
    class US,SS,CS,KS,PS negocio
    class URepo,SRepo,CRepo,KRepo,PRepo,ORM,BD datos
    class Pago,Envio externo
```

## Justificación

El monolito modular permite desplegar el backend como una sola aplicación y mantener organizadas las funciones por módulo. La capa de presentación recibe las solicitudes, la lógica de negocio aplica las reglas del marketplace y la capa de datos gestiona la persistencia. La pasarela de pagos y el servicio de envíos permanecen como sistemas externos.