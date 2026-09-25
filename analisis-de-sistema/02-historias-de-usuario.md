# 02. Historias de usuario

Formato utilizado: **Como [actor], quiero [acción], para [beneficio].**

## Historias del Cliente

| ID | Historia de usuario | Prioridad |
|:---|:---|:---|
| HU01 | Como **cliente**, quiero buscar y consultar productos, para encontrar el producto que necesito. | Alta |
| HU03 | Como **cliente**, quiero gestionar los productos de mi carrito, para preparar los productos que deseo comprar. | Alta |
| HU04 | Como **cliente**, quiero realizar un pedido con los productos de mi carrito, para completar mi compra. | Alta |
| HU06 | Como **cliente**, quiero consultar mis pedidos y su estado, para conocer el estado de mis compras. | Media |
| HU07 | Como **cliente**, quiero realizar el pago de mi pedido de forma segura, para completar la compra con confianza. | Alta |
| HU08 | Como **cliente**, quiero recibir información de envío y seguimiento de mi pedido, para saber cuándo llegará. | Media |

## Historias del Seller

| ID | Historia de usuario | Prioridad |
|:---|:---|:---|
| HU02 | Como **seller**, quiero registrar y gestionar mis productos, para ofrecerlos a los clientes. | Alta |
| HU09 | Como **seller**, quiero consultar las ventas asociadas a mis productos, para conocer el desempeño de mi negocio. | Media |

## Historias del Administrador

| ID | Historia de usuario | Prioridad |
|:---|:---|:---|
| HU05 | Como **administrador**, quiero gestionar los sellers de la plataforma, para administrar a los vendedores registrados. | Alta |
| HU10 | Como **administrador**, quiero gestionar las categorías de productos, para mantener el catálogo organizado. | Media |
| HU11 | Como **administrador**, quiero monitorear el estado general del sistema, para asegurar su correcto funcionamiento. | Baja |

## Criterios de aceptación (ejemplos)

### HU01 — Buscar y consultar productos
- **Dado** que el cliente ingresa un término de búsqueda, **cuando** ejecuta la búsqueda, **entonces** el sistema muestra los productos que coinciden con el criterio.
- **Dado** que el cliente selecciona un producto, **cuando** accede a su detalle, **entonces** el sistema muestra nombre, descripción, precio, stock disponible e imágenes.

### HU04 — Realizar pedido
- **Dado** que el cliente tiene productos en el carrito, **cuando** confirma el pedido, **entonces** el sistema genera una orden con un identificador único.
- **Dado** que el carrito está vacío, **cuando** el cliente intenta generar un pedido, **entonces** el sistema muestra un mensaje indicando que no hay productos.

### HU07 — Realizar pago
- **Dado** que el cliente confirma el pedido, **cuando** selecciona el método de pago, **entonces** el sistema redirige a la pasarela de pago externa.
- **Dado** que el pago fue procesado exitosamente, **cuando** la pasarela responde, **entonces** el sistema actualiza el estado del pedido a "pagado".
