# Arquitectura inicial del marketplace

## Arquitectura en tres capas

| Capa | Responsabilidad | Elementos |
|---|---|---|
| Presentación | Permitir la interacción de los usuarios con el sistema. | Aplicación web y API REST. |
| Lógica de negocio | Ejecutar las funciones y reglas del marketplace. | Usuarios, Sellers, Catálogo, Carrito y Pedidos. |
| Datos | Almacenar y consultar la información del sistema. | Base de datos. |

### Relación entre las capas

1. El cliente, el seller y el administrador utilizan la aplicación web.
2. La aplicación web se comunica con la API REST.
3. La API REST solicita operaciones a los módulos de lógica de negocio.
4. Los módulos de negocio consultan o actualizan la base de datos.
