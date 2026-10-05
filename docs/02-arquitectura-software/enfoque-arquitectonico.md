# Enfoque arquitectónico: Clean Architecture

## Enfoque seleccionado

| Elemento | Descripción aplicada al marketplace |
|---|---|
| Patrón o enfoque | Clean Architecture (Arquitectura Limpia). |
| Objetivo | Separar responsabilidades y dirigir las dependencias hacia el dominio. |
| Problema que resuelve | Evita que las reglas de negocio dependan directamente de Angular, la API REST o los servicios externos. |
| Capas | Presentación, Aplicación, Dominio e Infraestructura. |
| Beneficios | Facilita las pruebas, el mantenimiento y el cambio de implementaciones técnicas. |

## Diagrama del enfoque

```mermaid
flowchart LR
    Usuario["Usuario<br>Cliente"]

    subgraph Web["Marketplace Web - Angular 18 y TypeScript"]
        direction LR

        subgraph Presentacion["PRESENTACIÓN"]
            direction TB
            CatalogoComponent["CatalogoComponent"]
            EstadoCarrito["EstadoCarrito"]
            CarritoComponent["CarritoComponent"]
            AppComponent["AppComponent"]
        end

        subgraph Aplicacion["APLICACIÓN - CASOS DE USO"]
            direction TB
            Consultar["ConsultarCatalogoCasoUso"]
            Agregar["AgregarAlCarritoCasoUso"]
            Registrar["RegistrarCompraCasoUso"]
        end

        subgraph Dominio["DOMINIO - ENTIDADES Y CONTRATOS"]
            direction TB
            Producto["Producto"]
            Carrito["Carrito"]
            Pedido["Pedido"]
            Precios["Reglas de precios"]

            RepoProductos["RepositorioProductos"]
            RepoPedidos["RepositorioPedidos"]
            ProcesadorPagos["ProcesadorPagos"]
            Notificador["NotificadorCliente"]
        end

        subgraph Infraestructura["INFRAESTRUCTURA - ADAPTADORES"]
            direction TB
            ProductosHTTP["RepositorioProductosHttp"]
            PedidosMemoria["RepositorioPedidosMemoria"]
            PagosSimulados["ProcesadorPagosSimulado"]
            NotificadorConsola["NotificadorConsola"]
            Tokens["tokens.ts"]
        end

        Config["app.config.ts - composición e inyección"]
    end

    API["Marketplace API REST<br>Backend externo"]

    Usuario -->|"usa"| AppComponent
    AppComponent --> CatalogoComponent
    AppComponent --> CarritoComponent

    CatalogoComponent -->|"invoca"| Consultar
    CarritoComponent -->|"invoca"| Agregar
    CarritoComponent -->|"invoca"| Registrar

    Consultar -.-> Producto
    Consultar -.-> RepoProductos
    Agregar -.-> Carrito
    Registrar -.-> Pedido
    Registrar -.-> Precios
    Registrar -.-> RepoPedidos
    Registrar -.-> ProcesadorPagos
    Registrar -.-> Notificador

    EstadoCarrito -.-> Carrito

    ProductosHTTP -.->|"implementa"| RepoProductos
    PedidosMemoria -.->|"implementa"| RepoPedidos
    PagosSimulados -.->|"implementa"| ProcesadorPagos
    NotificadorConsola -.->|"implementa"| Notificador

    Config -.-> Tokens
    Config -.-> ProductosHTTP
    Config -.-> PedidosMemoria
    Config -.-> PagosSimulados
    Config -.-> NotificadorConsola

    ProductosHTTP -->|"HTTP / JSON"| API

    classDef persona fill:#ffffff,stroke:#777777,color:#222222
    classDef presentacion fill:#e4efff,stroke:#789bc7,color:#17365d
    classDef aplicacion fill:#e7f3df,stroke:#85a96f,color:#294523
    classDef dominio fill:#fff2d4,stroke:#d5aa53,color:#4c3914
    classDef infraestructura fill:#f0e6f5,stroke:#a27bb2,color:#40254d
    classDef externo fill:#eeeeee,stroke:#888888,color:#222222

    class Usuario persona
    class CatalogoComponent,EstadoCarrito,CarritoComponent,AppComponent presentacion
    class Consultar,Agregar,Registrar aplicacion
    class Producto,Carrito,Pedido,Precios,RepoProductos,RepoPedidos,ProcesadorPagos,Notificador dominio
    class ProductosHTTP,PedidosMemoria,PagosSimulados,NotificadorConsola,Tokens,Config infraestructura
    class API externo
```

## Regla de dependencia

Las dependencias del código apuntan hacia el interior: presentación e infraestructura pueden depender de aplicación y dominio, pero el dominio no depende de Angular, HTTP ni implementaciones concretas. Los casos de uso trabajan con contratos; los adaptadores de infraestructura implementan esos contratos.

`app.config.ts` selecciona e inyecta los adaptadores concretos. Por ello, cambiar un adaptador no exige modificar las entidades y reglas del dominio.