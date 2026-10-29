# Arquitectura Inicial y Evolución hacia Startup Escalable

> **Proyecto:** Marketplace & Plataforma de Intercambio / Subastas en Tiempo Real  
> **Capa:** Arquitectura de Software · Evolución de Diseño  
> **Estándar:** Software Design Description (SDD) · Versión 2.0  
> **Enfoque:** Clean Architecture + Event-Driven + Cloud Native (AWS Free Tier)

---

## 1. Arquitectura Inicial (Línea Base de 3 Capas)

En la concepción original del laboratorio, el sistema fue concebido bajo el modelo clásico monolítico de tres capas lineales:

- **Presentación:** Aplicación web cliente consumiendo endpoints HTTP síncronos mediante una API REST tradicional.
- **Lógica de negocio:** Monolito centralizado que encapsulaba usuarios, vendedores (*sellers*), catálogo de bienes y transacciones de pedidos/pujas.
- **Datos:** Una única base de datos relacional compartida (**PostgreSQL**) que soportaba tanto los registros permanentes como las consultas de alta frecuencia.

```mermaid
flowchart TD
    subgraph PRESENTACION["1. Capa de Presentación"]
        Web["Aplicación Web (SPA Monolítica) → API REST HTTP"]
    end

    subgraph NEGOCIO["2. Capa de Lógica de Negocio"]
        Modulos["Módulos Acoplados: Usuarios | Catálogo | Transacciones | Pedidos"]
    end

    subgraph DATOS["3. Capa de Datos (Monolítica)"]
        BD["Base de Datos Única (PostgreSQL)"]
    end

    subgraph EXTERNOS["Sistemas Externos"]
        Pago["Pasarela de Pago Tradicional"]
    end

    PRESENTACION -->|"HTTP REST síncrono"| NEGOCIO
    NEGOCIO -->|"Lecturas y escrituras directas"| DATOS
    NEGOCIO -->|"Llamadas bloqueantes"| EXTERNOS

    style PRESENTACION fill:#FFF3E0,stroke:#E65100,color:#000
    style NEGOCIO fill:#E8F5E9,stroke:#2E7D32,color:#000
    style DATOS fill:#F3E5F5,stroke:#6A1B9A,color:#000
    style EXTERNOS fill:#FFF8E1,stroke:#F9A825,color:#000
```

---

## 2. Diagnóstico Arquitectónico: ¿Por qué la arquitectura inicial no era viable para una Startup?

Tras la evaluación del diseño inicial, se identificaron fallas estructurales críticas que hacían al sistema inviable para operar como una startup real moderna:

| Dimensión | Limitación del Diseño Inicial | Impacto en Producción / Startup | Solución Arquitectónica Adoptada |
|---|---|---|---|
| **Persistencia Acoplada** | Una sola BD relacional (PostgreSQL) atendía tanto el historial contable como la consulta recurrente de precios en caliente. | La contención de disco y bloqueos de fila colapsan la base de datos ante ráfagas concurrentes de peticiones simultáneas. | **Desacoplamiento de Persistencia:** Separación estricta entre **PostgreSQL** (ACID relacional duradero) y **Redis** (In-Memory locks y lecturas en $< 1$ ms). |
| **Consumo de Memoria en la Nube** | Runtime de Node.js consumiendo entre 150 MB y 250 MB de memoria RAM por cada servicio o worker. | **Inviable en AWS Free Tier:** Las instancias gratuitas (`t2.micro` / `t3.micro`) cuentan con únicamente 1 GB de RAM. Múltiples procesos Node.js causan colapso por *OOM (Out Of Memory)*. | **Migración a Go (Golang):** El binario estático compilado consume únicamente **~20 MB de RAM**, permitiendo ejecutar el backend completo junto a Redis en una instancia gratuita. |
| **Latencia de Comunicación** | Peticiones HTTP síncronas tradicionales (*request/response*) o *polling*. | Latencias $> 1.5$ segundos inaceptables para experiencias en vivo y riesgo de condiciones de carrera (*race conditions*). | **WebSockets bidireccionales concurrentes** en Go (`gorilla/websocket`) con Goroutines y Canales para difusión en $< 25$ ms. |
| **Experiencia de Usuario (UI/UX)** | SPA genérica sin renderizado en servidor ni optimización para motores de búsqueda. | Bajo posicionamiento SEO en el catálogo público y experiencia poco profesional. | **Next.js 15 (React 19 / App Router):** SSR para indexación en buscadores y diseño cinematográfico exclusivo. |
| **Seguridad y Fraude** | Validación de reglas manuales sin detección inteligente de anomalías. | Exposición a fraudes transaccionales y compradores sin liquidez. | **Agente de IA (Google Gemini)** con patrón **Circuit Breaker** en memoria para evaluar riesgo sin bloquear el camino crítico. |

---

## 3. Arquitectura Evolucionada y Escalable (Startup-Ready en AWS)

La nueva arquitectura transforma el sistema en una solución desacoplada, reactiva y preparada para alta concurrencia:

```mermaid
flowchart TD
    %% =========================
    %% ACTORES
    %% =========================
    subgraph ACTORES["USUARIOS & CLIENTES VIP"]
        Comprador["👤 Cliente / Postor VIP"]
        Operador["👤 Administrador / Martillero"]
    end

    %% =========================
    %% RED & PRESENTACIÓN
    %% =========================
    subgraph PRESENTACION["PRESENTACIÓN & CDN (AWS Edge)"]
        CDN["AWS CloudFront / Reverse Proxy"]
        NextApp["🌐 Frontend Web Next.js 15 (React 19)<br>• Catálogo Indexable con SSR (SEO)<br>• Sala de Intercambio Cinematográfica<br>• Cliente WebSocket Bidireccional"]
    end

    %% =========================
    %% BACKEND EN GO (CLEAN ARCHITECTURE)
    %% =========================
    subgraph BACKEND["CORE ENGINE EN GO (Clean Architecture & Goroutines)"]
        Gateway["⚡ Gateway & WebSocket Hub (Go)<br><i>(Goroutines concurrentes + Canales)</i>"]
        CoreService["🔨 Core Transaction Engine (Go)<br><i>(Clean Architecture: Dominio + Aplicación)</i>"]
        CircuitBreaker["🛡️ Circuit Breaker & Risk Adapter (Go)"]
    end

    %% =========================
    %% PERSISTENCIA DESACOPLADA
    %% =========================
    subgraph DATOS["ALMACENAMIENTO DESACOPLADO (AWS Free Tier)"]
        Redis["🧠 Redis 7.2 In-Memory<br>• Locks Atómicos Distribuidos (SETNX)<br>• Caché de precio/estado en caliente (< 1ms)<br>• Canales Pub/Sub reactivos"]
        Postgres["🗄️ PostgreSQL 16 (AWS RDS Free Tier)<br>• Persistencia relacional ACID<br>• Usuarios, balances y catálogo<br>• Trazabilidad inmutable de auditoría"]
    end

    %% =========================
    %% INTEGRACIONES EXTERNAS
    %% =========================
    subgraph EXTERNOS["SERVICIOS EXTERNOS & IA"]
        Gemini["🤖 Google Gemini AI<br><i>(Análisis de riesgo y fraude)</i>"]
        Pago["💳 Pasarela de Pagos & Custodia (Niubiz/Stripe)"]
    end

    %% FLUJOS
    ACTORES --> PRESENTACION
    CDN --> NextApp
    NextApp -.->|"WSS Tiempo Real (< 25ms)"| Gateway
    NextApp -->|"HTTP REST /api/v1"| Gateway
    Gateway --> CoreService
    CoreService -->|"Locks atómicos atómicos y caché caliente"| Redis
    CoreService -->|"Persistencia duradera asíncrona"| Postgres
    CoreService -->|"Evaluación preventiva"| CircuitBreaker
    CircuitBreaker -->|"Score de riesgo"| Gemini
    CoreService -->|"Retención y liquidación"| Pago
    Redis -.->|"Broadcast Pub/Sub"| Gateway

    %% ESTILOS
    style ACTORES fill:#DBEAFE,stroke:#1D4ED8,color:#000
    style PRESENTACION fill:#1E293B,stroke:#0F172A,color:#FFF
    style BACKEND fill:#00ADD8,stroke:#007D9C,color:#000
    style DATOS fill:#F3E5F5,stroke:#6A1B9A,color:#000
    style EXTERNOS fill:#6366F1,stroke:#4338CA,color:#FFF
```

---

## 4. Responsabilidades por Componente en el Nuevo Diseño

| Componente | Tecnología | Responsabilidad Principal | Consumo de Recursos en AWS Free Tier |
|---|---|---|---|
| **Capa Web** | Next.js 15, React 19, Tailwind CSS | Renderizado dinámico del catálogo con SSR, gestión de estado reactivo y conexión WebSocket en vivo. | ~120 MB RAM (o Serverless en AWS Amplify/Vercel) |
| **API Gateway & WebSocket Hub** | Go (Golang 1.23+), Gorilla/Coder | Mantiene miles de conexiones simultáneas mediante Goroutines (~2 KB de stack cada una), eliminando cuellos de botella de red. | **~15 MB – 25 MB RAM** |
| **Motor de Negocio (Core)** | Go, Clean Architecture | Aplica las reglas invariantes de dominio (anti-sniping, incrementos por tramo, validación de saldos y adjudicación). | **~20 MB – 30 MB RAM** |
| **Caché & Concurrencia** | Redis 7.2 | Control de concurrencia mediante locks distribuidos atómicos (`SETNX`) y lectura ultrarrápida del estado líder sin estresar la base de datos. | ~30 MB – 50 MB RAM |
| **Base de Datos Principal** | PostgreSQL 16 (AWS RDS Free Tier) | Almacén transaccional definitivo con garantías ACID completas para usuarios, bienes, pagos y auditoría. | Instancia gratuita db.t3.micro (20 GB) |
| **Agente de Confianza / IA** | Google Gemini API + Go Circuit Breaker | Análisis preventivo de patrones de riesgo en transacciones con degradación elegante a reglas locales en memoria si la API externa tarda $> 150$ ms. | Stateless |

---

## 5. Viabilidad en AWS Free Tier

El rediseño permite desplegar la plataforma completa dentro de los límites estrictos de la capa gratuita de AWS:
1. **Memoria Total del Backend:** $< 60$ MB de RAM, garantizando que el sistema operativo y Redis convivan holgadamente en una instancia `t2.micro` o `t3.micro` (1 GB de RAM) sin riesgo de cuelgues por swap o *Out Of Memory*.
2. **Cómputo y Red:** El paso de peticiones bloqueantes a Go con Goroutines permite atender miles de conexiones con una sola CPU virtual (1 vCPU).
3. **Persistencia Desacoplada:** El uso de AWS RDS PostgreSQL en la capa gratuita separa la carga de disco del servidor de cómputo, logrando alta resiliencia.
