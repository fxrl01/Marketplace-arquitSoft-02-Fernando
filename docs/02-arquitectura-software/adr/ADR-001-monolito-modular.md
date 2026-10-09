# ADR-001: Monolito Modular

## Estado
Aceptado.

## Contexto
El Marketplace contiene funcionalidades de usuarios, catálogo, carrito,
pedidos y pagos. Estas funcionalidades deben mantenerse organizadas y
con bajo acoplamiento sin introducir inicialmente la complejidad operativa
de una arquitectura distribuida.

## Drivers relacionados
- DA01 - Escalabilidad.
- DA06 - Mantenibilidad.

## Decisión
Se adopta un Monolito Modular.

El sistema será desplegado como una sola aplicación, pero estará dividido
internamente en módulos funcionales claramente delimitados:

- Usuarios.
- Catálogo.
- Carrito.
- Pedidos.
- Pagos.

## Alternativas consideradas
- Monolito tradicional.
- Microservicios.
- Monolito modular.

## Justificación
El Monolito Modular permite mantener un despliegue sencillo mientras se
establecen límites claros entre las funcionalidades del sistema.

## Consecuencias
### Positivas
- Menor complejidad de despliegue.
- Separación funcional.
- Mejor mantenibilidad.
- Posibilidad de evolución futura.

### Negativas
- La aplicación continúa siendo una única unidad de despliegue.
- El escalamiento inicial afecta al sistema completo.

## Resultado
Una aplicación desplegable organizada internamente mediante módulos.