# Necesidad del negocio

## Contexto

Se requiere una plataforma Marketplace especializada en productos para
mascotas, donde diferentes vendedores puedan ofrecer sus productos y los
clientes puedan buscarlos, agregarlos a un carrito y realizar compras.

El sistema debe permitir la participación de clientes, vendedores y
administradores, además de integrarse con servicios externos necesarios
para completar el proceso de compra.

## Problema

La comercialización de productos para mascotas requiere centralizar en una
misma plataforma la publicación de productos, gestión del catálogo, carrito,
pedidos, pagos y seguimiento de las operaciones.

Una solución con responsabilidades fuertemente acopladas dificultaría la
evolución del sistema conforme aumenten los usuarios, funcionalidades e
integraciones externas.

## Necesidad

Construir un Marketplace que permita gestionar el proceso de compra de
productos para mascotas y que pueda evolucionar de manera mantenible,
segura y escalable.

## Objetivo general

Diseñar la arquitectura de un Marketplace de productos para mascotas que
permita gestionar usuarios, catálogo, carrito, pedidos y pagos, manteniendo
una adecuada separación de responsabilidades e integración con servicios
externos.

## Actores principales

- Cliente.
- Seller o vendedor.
- Administrador.

## Sistemas externos

- Pasarela de pago.
- Servicio de envío.

## Resultado esperado

Disponer de una solución estructurada que soporte las principales operaciones
del Marketplace y permita incorporar cambios futuros reduciendo el impacto
sobre el resto del sistema.