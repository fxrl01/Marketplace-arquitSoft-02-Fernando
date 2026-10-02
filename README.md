# Marketplace de productos para mascotas

## Integrantes
- Fernando Olivares Chuhui

## Descripción
Marketplace académico de productos para mascotas, en el cual diferentes sellers pueden ofrecer sus productos y los clientes pueden realizar compras en línea.

## Caso de estudio
GoPet como referencia funcional: https://www.gopet.pe/

## Curso
Arquitectura de Software [IS-488]

## Estructura del repositorio
- `analisis-de-sistema/` — Actores, historias de usuario, requisitos funcionales, atributos de calidad, restricciones y drivers arquitectónicos.
- `arquitectura/` — Propuesta inicial de arquitectura en capas y diagrama Mermaid.
## Guía 03 - Análisis y selección de estilos y enfoques arquitectónicos

La Guía 03 continúa el análisis realizado en la Guía 02 e incorpora
decisiones arquitectónicas, estilo arquitectónico y Clean Architecture.

### Entregables

1. [Necesidad del negocio](analisis-de-sistema/00-necesidad-del-negocio.md)
2. [Requisitos funcionales](analisis-de-sistema/03-requisitos-funcionales.md)
3. [Atributos de calidad](analisis-de-sistema/04-atributos-de-calidad.md)
4. [Drivers arquitectónicos](analisis-de-sistema/06-driver-arquitectonicos.md)
5. [Decisiones arquitectónicas](arquitectura/decisiones-arquitectonicas.md)
6. [Estilo arquitectónico](arquitectura/estilo-arquitectonico.md)
7. [Enfoque Clean Architecture](arquitectura/enfoque/enfoque-arquitectonico.md)

### Architecture Decision Records

- [ADR-001 - Monolito Modular](arquitectura/adr/ADR-001-monolito-modular.md)
- [ADR-002 - Clean Architecture](arquitectura/adr/ADR-002-clean-architecture.md)
- [ADR-003 - Estrategia de Caché](arquitectura/adr/ADR-003-estrategia-cache.md)
- [ADR-004 - Integración de Pagos](arquitectura/adr/ADR-004-integracion-pagos.md)

### Arquitectura seleccionada

El Marketplace utiliza:

- **Estilo arquitectónico:** Monolito Modular.
- **Comunicación:** Cliente-Servidor mediante API REST.
- **Enfoque interno:** Clean Architecture.