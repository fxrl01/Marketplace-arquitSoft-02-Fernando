# Arquitectura inicial del sistema

## Descripción

La arquitectura inicial se organiza en tres capas principales:

- **Presentación:** permite la interacción de los usuarios con el sistema mediante la aplicación web y la API REST.
- **Lógica de negocio:** contiene los principales módulos responsables de las funcionalidades del sistema: usuarios, sellers, catálogo, carrito y pedidos.
- **Datos:** permite almacenar y consultar la información mediante una base de datos.

Además, el módulo de **Pedidos** se integra con sistemas externos como la **pasarela de pago**, el **servicio de envío** y el **ERP**.

Cada capa tiene sus propias responsabilidades y se comunica con la capa inmediatamente inferior.

## Módulos por capa

| Capa | Pregunta que responde | Módulos / elementos |
|:---|:---|:---|
| Presentación | ¿Cómo interactúa el usuario? | Aplicación Web, API REST |
| Lógica de negocio | ¿Qué hace el sistema? | Usuarios, Sellers, Catálogo, Carrito, Pedidos |
| Datos | ¿Dónde se almacena la información? | Base de datos (PostgreSQL) |
| Sistemas externos | ¿Con qué se integra? | Pasarela de pago, Servicio de envío, ERP |

## Diagrama de arquitectura

```mermaid
flowchart TD
    %% =========================
    %% ACTORES
    %% =========================
    subgraph ACTORES["ACTORES"]
        Cliente["Cliente"]
        Seller["Seller"]
        Admin["Administrador"]
    end

    %% =========================
    %% PRESENTACIÓN
    %% =========================
    subgraph PRESENTACION["PRESENTACIÓN"]
        Web["Aplicación Web → API REST"]
    end

    %% =========================
    %% LÓGICA DE NEGOCIO
    %% =========================
    subgraph NEGOCIO["LÓGICA DE NEGOCIO"]
        Usuarios["Usuarios"]
        Sellers["Sellers"]
        Catalogo["Catálogo"]
        Carrito["Carrito"]
        Pedidos["Pedidos"]
    end

    %% =========================
    %% DATOS
    %% =========================
    subgraph DATOS["DATOS"]
        BD["Base de datos"]
    end

    %% =========================
    %% SISTEMAS EXTERNOS
    %% =========================
    subgraph EXTERNOS["SISTEMAS EXTERNOS"]
        Pago["Pasarela de pago"]
        ERP["ERP"]
        Envio["Servicio de envío"]
    end

    %% =========================
    %% FLUJO PRINCIPAL
    %% =========================
    ACTORES --> PRESENTACION
    PRESENTACION --> NEGOCIO
    NEGOCIO --> DATOS
    Pedidos -->|"integraciones"| EXTERNOS

    %% =========================
    %% ESTILOS
    %% =========================
    style ACTORES fill:#E3F2FD,stroke:#1565C0,stroke-width:2px,color:#000
    style PRESENTACION fill:#FFF3E0,stroke:#E65100,stroke-width:2px,color:#000
    style NEGOCIO fill:#E8F5E9,stroke:#2E7D32,stroke-width:2px,color:#000
    style DATOS fill:#F3E5F5,stroke:#6A1B9A,stroke-width:2px,color:#000
    style EXTERNOS fill:#FFF8E1,stroke:#F9A825,stroke-width:2px,color:#000
```

