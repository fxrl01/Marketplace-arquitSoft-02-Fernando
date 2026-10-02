# Decisiones arquitectónicas

Las decisiones arquitectónicas se establecen a partir de los drivers
identificados durante el análisis del Marketplace.

| ID | Decisión arquitectónica | Driver relacionado | Resultado |
|---|---|---|---|
| ADR-001 | Monolito modular | DA01 - Escalabilidad, DA06 - Mantenibilidad | Organización en módulos de Usuarios, Catálogo, Carrito, Pedidos y Pagos |
| ADR-002 | Clean Architecture | DA06 - Mantenibilidad | Separación entre Dominio, Aplicación, Presentación e Infraestructura |
| ADR-003 | Estrategia de caché | DA02 - Rendimiento | Reducir consultas repetitivas y mejorar tiempos de respuesta |
| ADR-004 | Integración de pagos mediante interfaces y adaptadores | DA04 - Pago externo | Desacoplar los casos de uso de la pasarela de pago |

## Relación entre drivers y decisiones

```mermaid
flowchart LR
    DA01[DA01 Escalabilidad] --> ADR1[ADR-001 Monolito modular]
    DA02[DA02 Rendimiento] --> ADR3[ADR-003 Estrategia de caché]
    DA04[DA04 Pago externo] --> ADR4[ADR-004 Interfaces y adaptadores]
    DA06[DA06 Mantenibilidad] --> ADR1
    DA06 --> ADR2[ADR-002 Clean Architecture]