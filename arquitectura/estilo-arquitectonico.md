# Estilo arquitectónico

## Estilo seleccionado

Para el Marketplace se adopta un estilo de **Monolito Modular**,
complementado por una arquitectura Cliente-Servidor mediante API REST.

El backend se despliega como una única aplicación, pero sus funcionalidades
se organizan internamente mediante módulos con responsabilidades definidas.

## Componentes principales

- Cliente Web.
- API REST.
- Módulo de Usuarios.
- Módulo de Catálogo.
- Módulo de Carrito.
- Módulo de Pedidos.
- Módulo de Pagos.
- Persistencia.
- Pasarela de pago externa.
- Servicio externo de envío.

## Organización general

```mermaid
flowchart TB

    Cliente[Cliente]
    Seller[Seller]
    Admin[Administrador]

    Web[Frontend / Cliente Web]

    subgraph Marketplace["Marketplace - Monolito Modular"]
        API[API REST]

        Usuarios[Módulo Usuarios]
        Catalogo[Módulo Catálogo]
        Carrito[Módulo Carrito]
        Pedidos[Módulo Pedidos]
        Pagos[Módulo Pagos]

        DB[(PostgreSQL)]
        Cache[(Caché)]
    end

    PagoExt[Pasarela de pago]
    EnvioExt[Servicio de envío]

    Cliente --> Web
    Seller --> Web
    Admin --> Web

    Web -->|HTTP / REST| API

    API --> Usuarios
    API --> Catalogo
    API --> Carrito
    API --> Pedidos
    API --> Pagos

    Usuarios --> DB
    Catalogo --> DB
    Carrito --> DB
    Pedidos --> DB
    Pagos --> DB

    Catalogo --> Cache

    Pagos --> PagoExt
    Pedidos --> EnvioExt