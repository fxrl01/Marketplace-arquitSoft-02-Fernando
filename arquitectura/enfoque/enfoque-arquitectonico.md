# Enfoque arquitectónico: Clean Architecture

## 1. Enfoque seleccionado

Para la organización interna del Marketplace se adopta **Clean Architecture
(Arquitectura Limpia)**.

Este enfoque busca separar las responsabilidades del sistema y controlar
la dirección de sus dependencias, manteniendo las reglas del negocio
independientes de los detalles tecnológicos.

## 2. Objetivo

Separar las reglas del negocio de elementos externos como:

- Frameworks.
- Interfaz de usuario.
- Base de datos.
- APIs externas.
- Pasarela de pago.
- Servicio de envío.

De esta manera, los cambios tecnológicos pueden realizarse sin afectar
innecesariamente el núcleo del sistema.

## 3. Problema que resuelve

Sin una separación adecuada de responsabilidades, las reglas del negocio
podrían quedar fuertemente acopladas a tecnologías concretas.

Por ejemplo, un caso de uso de procesamiento de pago no debería depender
directamente de una pasarela específica.

Clean Architecture permite introducir interfaces y adaptadores para que
las capas internas trabajen mediante contratos y no mediante
implementaciones tecnológicas concretas.

## 4. Capas definidas

### 4.1 Dominio

Representa el núcleo del sistema y contiene las reglas fundamentales
del negocio.

Elementos principales:

- Producto.
- Cliente.
- Carrito.
- Pedido.

Responsabilidades:

- Representar las entidades principales del Marketplace.
- Mantener las reglas esenciales del negocio.
- Evitar dependencias hacia frameworks o infraestructura.

El Dominio no debe conocer PostgreSQL, Angular, APIs externas ni
pasarelas de pago.

---

### 4.2 Aplicación

Contiene las reglas específicas de la aplicación y coordina los casos de uso.

Ejemplos:

- Consultar catálogo.
- Agregar producto al carrito.
- Crear pedido.
- Confirmar compra.
- Procesar pago.

La capa de Aplicación utiliza las entidades del Dominio y define los
contratos necesarios para comunicarse con recursos externos.

---

### 4.3 Presentación

Gestiona la interacción entre los usuarios y el sistema.

Puede contener:

- Controllers.
- DTO.
- Mappers.
- Componentes asociados a la interfaz.
- Entrada y salida de solicitudes HTTP.

Su responsabilidad es recibir solicitudes y transformarlas en llamadas
a los casos de uso correspondientes.

---

### 4.4 Infraestructura

Contiene los detalles tecnológicos y las implementaciones concretas.

Ejemplos:

- Acceso a PostgreSQL.
- Implementaciones de repositorios.
- Adaptador de pasarela de pago.
- Adaptador del servicio de envío.
- Implementación de caché.
- Clientes HTTP.

Infraestructura puede cambiar sin modificar las reglas fundamentales
del Dominio.

## 5. Regla de dependencias

En Clean Architecture las dependencias deben apuntar hacia el interior.

```text
Presentación
     |
     v
Aplicación
     |
     v
  Dominio
     ^
     |
Infraestructura