# ADR-002: Clean Architecture

## Estado
Aceptado.

## Contexto
Las reglas del negocio no deben depender directamente de frameworks,
interfaces gráficas, bases de datos ni servicios externos.

## Driver relacionado
- DA06 - Mantenibilidad.

## Decisión
Se adopta Clean Architecture como enfoque arquitectónico interno.

Se establecen las siguientes capas:

- Dominio.
- Aplicación.
- Presentación.
- Infraestructura.

## Regla de dependencias
Las dependencias del código deberán apuntar hacia las capas internas.

El Dominio no dependerá de Angular, bases de datos, APIs o servicios externos.

## Justificación
Permite separar las reglas del negocio de los detalles tecnológicos y
reducir el impacto producido por cambios en infraestructura o interfaz.

## Consecuencias positivas
- Mayor mantenibilidad.
- Mayor facilidad de pruebas.
- Menor acoplamiento tecnológico.
- Mejor separación de responsabilidades.

## Consecuencias negativas
- Mayor número de abstracciones.
- Requiere disciplina para mantener la dirección correcta de las dependencias.

## Resultado
Dominio, Aplicación, Presentación e Infraestructura con dependencias
controladas hacia el núcleo del sistema.