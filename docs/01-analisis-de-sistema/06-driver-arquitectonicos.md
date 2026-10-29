# 06. Drivers arquitectónicos

Los drivers arquitectónicos son el conjunto de requisitos funcionales críticos, atributos de calidad y restricciones técnicas que moldean directamente las decisiones de diseño del sistema.

## Tabla de drivers arquitectónicos

| ID | Driver arquitectónico | Origen | ¿Por qué influye en la arquitectura? | Decisión Arquitectónica Asociada |
|:---|:---|:---|:---|:---|
| **DA01** | **Escalabilidad y Límites de Cómputo en la Nube** | AC03 - Escalabilidad / RC08 - AWS Free Tier | El sistema debe operar dentro de una instancia con recursos limitados (1 GB RAM en AWS `t2.micro` / `t3.micro`) sin colapsar por sobreconsumo de memoria. | Adopción de **Go (Golang)** para el backend central (consumo de ~20 MB RAM frente a >150 MB de Node.js). |
| **DA02** | **Rendimiento y Baja Latencia en Concurrencia** | AC01 - Rendimiento / RC03 - WebSockets | En eventos de alta concurrencia, las transacciones y consultas de precio deben responder en $< 50$ ms sin provocar condiciones de carrera. | Implementación de **WebSockets bidireccionales** en Go y control de concurrencia atómica mediante **Redis Locks (`SETNX`)**. |
| **DA03** | **Desacoplamiento de Persistencia** | AC01 - Rendimiento / AC05 - Mantenibilidad | Almacenar datos en caliente (precios dinámicos, locks atómicos) en la misma base de datos relacional genera saturación de conexiones y cuellos de botella de I/O. | Separación estricta: **Redis 7.2** para caché y locks atómicos en memoria; **PostgreSQL 16** para persistencia transaccional ACID duradera. |
| **DA04** | **Prevención de Fraude e Inteligencia Artificial** | AC04 - Seguridad / RC09 - Gemini AI | Se requiere evaluar preventivamente el riesgo crediticio y conductual del usuario sin bloquear el hilo principal ni comprometer la disponibilidad del sistema. | Integración del modelo **Google Gemini AI** protegido mediante el patrón **Circuit Breaker** en memoria (conmutación automática por timeout > 150 ms). |
| **DA05** | **Experiencia de Usuario de Alta Gama y SEO** | AC07 - Usabilidad / RC07 - Next.js | La interfaz debe ofrecer una experiencia visual exclusiva y fluida en tiempo real, junto con renderizado en servidor (SSR) para indexar bienes en buscadores. | Adopción de **Next.js 15 (React 19)** con App Router y cliente WebSocket reactivo. |
| **DA06** | **Integración de Pasarela de Pagos Externa** | RC04 - Pasarela de pago | Se requiere congelar fondos en garantía (*escrow*) y procesar liquidaciones financieras sin acoplar el código al proveedor bancario. | Aplicación del patrón **Adapter / Hexagonal Architecture** (`PaymentEscrowPort`) con implementaciones intercambiables (Stripe, Niubiz). |
| **DA07** | **Aislamiento de Reglas de Negocio (Mantenibilidad)** | AC06 - Mantenibilidad / RC10 - SDD | El motor central de transacciones debe ser completamente independiente de bases de datos, frameworks web y librerías externas para permitir pruebas unitarias en memoria. | Implementación de **Clean Architecture (Puertos y Adaptadores)** en paquetes modulares en Go (`domain`, `services`, `adapters`). |

## Diagrama de Relación: Requisitos → Drivers → Arquitectura

```mermaid
flowchart LR
    AC01["AC01 Rendimiento (< 50ms)"] --> DA02["DA02 Baja Latencia & Concurrencia"]
    AC03["AC03 Escalabilidad (1000+ users)"] --> DA01["DA01 AWS Free Tier Limits"]
    AC04["AC04 Seguridad & Fraude"] --> DA04["DA04 Agente IA + Circuit Breaker"]
    AC05["AC05 Integridad Transaccional"] --> DA03["DA03 Persistencia Desacoplada"]
    AC06["AC06 Mantenibilidad"] --> DA07["DA07 Clean Architecture en Go"]
    AC07["AC07 Usabilidad & SEO"] --> DA05["DA05 Next.js SSR & UI"]
    RC04["RC04 Pasarela de Pago"] --> DA06["DA06 Adaptador de Pagos / Escrow"]

    DA01 --> SolucionGo["Backend Go (Golang)"]
    DA02 --> SolucionWS["WebSockets + Redis Locks"]
    DA03 --> SolucionDB["Postgres ACID + Redis Cache"]
    DA04 --> SolucionIA["Gemini AI Circuit Breaker"]
    DA05 --> SolucionUI["Next.js 15 App Router"]
    DA07 --> SolucionHex["Arquitectura Hexagonal Pura"]

    style AC01 fill:#DBEAFE,stroke:#1D4ED8,color:#000
    style AC03 fill:#DBEAFE,stroke:#1D4ED8,color:#000
    style AC04 fill:#DBEAFE,stroke:#1D4ED8,color:#000
    style AC05 fill:#DBEAFE,stroke:#1D4ED8,color:#000
    style AC06 fill:#DBEAFE,stroke:#1D4ED8,color:#000
    style AC07 fill:#DBEAFE,stroke:#1D4ED8,color:#000
    style SolucionGo fill:#D1FAE5,stroke:#059669,color:#000
    style SolucionWS fill:#D1FAE5,stroke:#059669,color:#000
    style SolucionDB fill:#D1FAE5,stroke:#059669,color:#000
    style SolucionIA fill:#FEF3C7,stroke:#D97706,color:#000
    style SolucionUI fill:#D1FAE5,stroke:#059669,color:#000
    style SolucionHex fill:#D1FAE5,stroke:#059669,color:#000
```
