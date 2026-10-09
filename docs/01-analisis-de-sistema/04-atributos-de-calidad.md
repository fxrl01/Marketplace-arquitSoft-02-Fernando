# 04. Atributos de calidad

Escenario considerado: durante una campaña comercial, el marketplace podría recibir una gran cantidad de usuarios consultando productos y realizando compras simultáneamente.

## Atributos identificados

| ID | Atributo de calidad | Escenario de calidad | Métrica objetivo |
|:---|:---|:---|:---|
| AC01 | **Rendimiento** | Las consultas de productos y operaciones del carrito deben responder rápidamente incluso cuando exista una alta cantidad de usuarios concurrentes. | Tiempo de respuesta < 2 segundos |
| AC02 | **Disponibilidad** | El sistema debe permanecer disponible durante la campaña comercial y permitir que los usuarios realicen sus operaciones. | Disponibilidad ≥ 99.5% |
| AC03 | **Escalabilidad** | El sistema debe poder soportar un incremento de usuarios y solicitudes sin afectar significativamente su funcionamiento. | Soporte de hasta 1000 usuarios concurrentes |
| AC04 | **Seguridad** | Los datos de los usuarios, cuentas y operaciones de compra deben estar protegidos frente a accesos no autorizados. | Autenticación JWT + HTTPS obligatorio |
| AC05 | **Mantenibilidad** | El sistema debe estar organizado de manera que permita realizar cambios y correcciones sin afectar innecesariamente otras funcionalidades. | Arquitectura modular en capas |
| AC06 | **Usabilidad** | El sistema debe ser fácil de usar para clientes y sellers, permitiendo completar las operaciones principales con pocos pasos. | Flujo de compra en ≤ 5 pasos |

## Relación con la arquitectura

| Atributo | ¿Cómo influye en la arquitectura? |
|:---|:---|
| **Rendimiento** | Requiere optimización de consultas, posible uso de caché y paginación en la API REST. |
| **Disponibilidad** | Puede requerir redundancia en la base de datos y monitoreo del sistema. |
| **Escalabilidad** | Influye en la decisión de separar módulos y la posibilidad de escalar horizontalmente. |
| **Seguridad** | Requiere capa de autenticación/autorización transversal a todos los módulos. |
| **Mantenibilidad** | Justifica la separación en capas y la modularización del backend. |
| **Usabilidad** | Influye en el diseño de la capa de presentación y la API REST. |
