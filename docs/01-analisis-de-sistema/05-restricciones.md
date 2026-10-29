# 05. Restricciones del Sistema

Las restricciones son condiciones fijas, decisiones tecnológicas obligatorias o limitaciones del entorno de negocio e infraestructura que limitan el espacio de diseño del arquitecto.

## Registro de Restricciones

| ID | Restricción | Descripción | Justificación Arquitectónica |
|:---|:---|:---|:---|
| **RC01** | **Aplicación Web Accesible** | El sistema debe ser accesible mediante cualquier navegador web estándar moderno (Chrome, Firefox, Safari, Edge) sin requerir instalación de plugins. | Garantiza el alcance a todo tipo de postores y clientes desde ordenadores o dispositivos móviles. |
| **RC02** | **Control de Versiones** | El código fuente y su documentación deben gestionarse exclusivamente mediante Git y alojarse en GitHub bajo un flujo de integración continua. | Asegura la trazabilidad de cambios, auditoría de código y revisiones colaborativas. |
| **RC03** | **Protocolos de Comunicación** | El frontend se comunica mediante **WebSockets (WSS)** para operaciones en tiempo real (pujas y actualizaciones en vivo) y mediante **API REST (JSON sobre HTTPS)** para operaciones transaccionales o administrativas. | Cumple con la latencia estricta $< 50$ ms requerida para eventos interactivos en vivo. |
| **RC04** | **Pasarela de Pago y Custodia** | La plataforma debe integrarse con pasarelas financieras autorizadas (Stripe, Niubiz) mediante APIs desacopladas para retención de depósitos (*escrow*) y captura de fondos. | Cumple con los estándares de seguridad bancaria y previene retenciones fraudulentas. |
| **RC05** | **Tecnología Backend** | El motor central transaccional y el gateway de WebSockets deben desarrollarse en **Go (Golang 1.23+)** siguiendo los principios de **Clean Architecture**. | Go genera binarios estáticos ultraligeros (~20 MB RAM) con soporte nativo de concurrencia (Goroutines), esencial para operar en entornos con recursos limitados. |
| **RC06** | **Persistencia Desacoplada** | El sistema debe utilizar una arquitectura de doble almacenamiento: **PostgreSQL 16** para persistencia relacional con garantías ACID y **Redis 7.2** para locks atómicos en memoria y caché de lectura rápida. | Evita cuellos de botella de I/O en disco durante ráfagas de transacciones en caliente. |
| **RC07** | **Tecnología Frontend** | La interfaz de usuario debe desarrollarse sobre **Next.js 15 (React 19)** con App Router y soporte de renderizado en servidor (SSR). | Permite indexación SEO de los bienes en catálogo y ofrece una experiencia visual de alto valor (*luxury aesthetic*). |
| **RC08** | **Infraestructura de Despliegue** | La arquitectura debe estar optimizada para operar dentro de la capa gratuita **AWS Free Tier** (instancia EC2 `t2.micro` o `t3.micro` con 1 GB de RAM, y AWS RDS PostgreSQL Free Tier). | Viabilidad económica para etapa de startup temprana con costo cero de infraestructura base. |
| **RC09** | **Inteligencia Artificial y Resiliencia** | La evaluación de riesgo y fraude debe integrarse con **Google Gemini AI**, incorporando obligatoriamente un **Circuit Breaker** en memoria para conmutar a heurísticas locales si la API externa supera los 150 ms o falla. | Protege la disponibilidad del sistema en tiempo real contra fallos o latencias de proveedores externos. |
| **RC10** | **Documentación SDD** | Toda la documentación de análisis, arquitectura y diseño de software debe mantenerse en formato Markdown estructurado según el estándar SDD dentro del repositorio. | Mantenibilidad y alineación continua entre código y especificación. |
