# Decisiones Arquitectónicas

| ADR | Título | Driver(s) | Decisión | Justificación | Resultado |
|---|---|---|---|---|---|
| ADR-001 | Monolito Modular | DA01 - Escalabilidad, DA06 - Mantenibilidad | Organizar el sistema como monolito modular: módulos independientes dentro de una misma aplicación desplegable | Mantiene la solución sencilla al inicio y separa claramente las responsabilidades | Módulos: Catálogo, Carrito, Pedidos, Pagos, Usuarios |
| ADR-002 | Clean Architecture | DA06 - Mantenibilidad | Aplicar Clean Architecture para organizar las responsabilidades internas | Las reglas de negocio deben estar separadas de frameworks, bases de datos y servicios externos | Capas: Dominio, Aplicación, Infraestructura, Presentación |
| ADR-003 | Estrategia de caché | DA02 - Rendimiento | Usar caché para información consultada con frecuencia | Reducir consultas repetitivas a la fuente de datos y mejorar tiempos de respuesta | Caché para datos de consulta frecuente |
| ADR-004 | Integración de pagos mediante interfaces y adaptadores | DA04 - Integración con pagos | Integrar la pasarela de pago mediante interfaces y adaptadores | Los casos de uso no deben depender directamente del proveedor externo de pagos | Contrato de pagos + adaptador que se comunica con la pasarela externa |
