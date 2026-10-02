# ADR-003: Estrategia de Caché

## Estado
Aceptado.

## Contexto
El Marketplace tendrá información consultada frecuentemente y puede recibir
alta concurrencia durante campañas comerciales.

## Driver relacionado
- DA02 - Rendimiento.

## Decisión
Incorporar una estrategia de caché para información de consulta frecuente.

## Justificación
Reducir consultas repetitivas a la fuente de datos y disminuir los tiempos
de respuesta.

## Consecuencias positivas
- Reducción de carga sobre la base de datos.
- Mejores tiempos de respuesta.
- Mejor comportamiento ante alta concurrencia.

## Consecuencias negativas
- Se debe controlar la invalidación del caché.
- Puede existir información temporalmente desactualizada.

## Resultado
Uso de caché para las operaciones de consulta que lo requieran.