# Requisitos funcionales

Los requisitos funcionales indican las acciones que debe realizar el marketplace para atender las historias de usuario.

| ID | Requisito funcional |
|---|---|
| RF01 | El sistema debe permitir buscar productos por nombre y categoría. |
| RF02 | El sistema debe mostrar la información, el precio y la disponibilidad de cada producto. |
| RF03 | El sistema debe permitir a cada seller registrar y actualizar sus propios productos. |
| RF04 | El sistema debe permitir agregar productos al carrito, cambiar sus cantidades y eliminarlos. |
| RF05 | El sistema debe generar un pedido a partir del carrito y registrar la dirección de entrega. |
| RF06 | El sistema debe permitir al cliente consultar sus pedidos y el estado de cada uno. |
| RF07 | El sistema debe permitir al administrador registrar, actualizar y desactivar sellers. |
| RF08 | El sistema debe mostrar el detalle de un pedido a los usuarios autorizados. |
| RF09 | El sistema debe enviar la solicitud de pago a una pasarela externa y registrar su resultado. |
| RF10 | El sistema debe permitir al seller consultar los pedidos correspondientes a sus productos. |

## Relación entre historias y requisitos

| Historia de usuario | Requisitos relacionados |
|---|---|
| HU01: Buscar y consultar productos | RF01, RF02 |
| HU02: Gestionar productos | RF03 |
| HU03: Gestionar carrito | RF04 |
| HU04: Realizar un pedido | RF05, RF08 |
| HU05: Gestionar sellers | RF07 |
| HU06: Consultar pedidos | RF06, RF08 |
| HU07: Pagar un pedido | RF09 |
| HU08: Consultar ventas como seller | RF08, RF10 |