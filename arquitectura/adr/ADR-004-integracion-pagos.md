# ADR-004: Integración de pagos mediante interfaces y adaptadores

## Estado
Aceptado.

## Contexto
El Marketplace debe integrarse con una pasarela de pago externa sin
acoplar las reglas del negocio a un proveedor específico.

## Driver relacionado
- DA04 - Integración con pagos.

## Decisión
La aplicación definirá un contrato o interfaz de pago.

La infraestructura implementará dicho contrato mediante un adaptador que
se comunicará con la pasarela externa.

## Flujo

Caso de uso → Interfaz de pago → Adaptador → Pasarela externa

## Justificación
Permite desacoplar los casos de uso del proveedor tecnológico utilizado
para procesar pagos.

## Consecuencias positivas
- Posibilidad de cambiar de proveedor.
- Mayor facilidad de pruebas.
- Menor dependencia tecnológica.

## Consecuencias negativas
- Requiere interfaces y adaptadores adicionales.

## Resultado
Los casos de uso dependen de contratos internos y no directamente de
la pasarela externa.