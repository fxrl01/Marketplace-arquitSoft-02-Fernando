# Escenarios de atributos de calidad del Marketplace

## EQ-01. Rendimiento: consulta de productos

| Elemento | Descripción |
|---|---|
| Atributo | Rendimiento |
| Fuente | Cliente |
| Estímulo | Busca productos o consulta su detalle |
| Condición | Operación normal con datos representativos |
| Respuesta | Mostrar resultados sin errores inesperados |
| Medida | Propuesta: 95 % de respuestas ≤ 2 s, menos de 1 % de errores y 200 usuarios simultáneos |
| Verificación | Prueba de rendimiento |

## EQ-02. Disponibilidad: continuidad del servicio

| Elemento | Descripción |
|---|---|
| Atributo | Disponibilidad |
| Fuente | Cliente |
| Estímulo | Realiza operaciones durante una campaña o falla de componente |
| Condición | Sistema publicado y monitoreado |
| Respuesta | Mantener disponibles las operaciones posibles y controlar errores |
| Medida | Propuesta: disponibilidad mensual de 99,5 % |
| Verificación | Revisar registros de monitoreo |

## EQ-03. Escalabilidad: aumento de usuarios

| Elemento | Descripción |
|---|---|
| Atributo | Escalabilidad |
| Fuente | Incremento de clientes |
| Estímulo | Aumentan los usuarios simultáneos |
| Condición | Prueba de carga controlada |
| Respuesta | Soportar el aumento sin superar límites acordados |
| Medida | Propuesta: 200 usuarios, 95 % de respuestas < 3 s y menos de 1 % de errores |
| Verificación | Incrementar progresivamente la carga |

## EQ-04. Seguridad: operaciones protegidas

| Elemento | Descripción |
|---|---|
| Atributo | Seguridad |
| Fuente | Usuario sin autorización |
| Estímulo | Intenta acceder a una función protegida |
| Condición | Pruebas sobre funciones protegidas |
| Respuesta | Rechazar la operación sin exponer datos |
| Medida | Rechazar 100 % de intentos no autorizados evaluados |
| Verificación | Pruebas de autorización |

## EQ-05. Mantenibilidad: cambios controlados

| Elemento | Descripción |
|---|---|
| Atributo | Mantenibilidad |
| Fuente | Equipo de desarrollo |
| Estímulo | Modificación de una regla o proveedor externo |
| Condición | Sistema modular con pruebas |
| Respuesta | Concentrar el cambio en el módulo responsable |
| Medida | Pruebas del módulo y regresión aprobadas |
| Verificación | Revisar código, pruebas y dependencias |