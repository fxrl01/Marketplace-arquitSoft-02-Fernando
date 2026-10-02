# 06. Drivers arquitectónicos

| ID | Driver arquitectónico | Origen | ¿Por qué influye en la arquitectura? |
|:---|:---|:---|:---|
| DA01 | El sistema debe soportar un incremento importante de usuarios durante campañas comerciales. | AC03 - Escalabilidad | Influye en la estrategia de escalamiento y despliegue. |
| DA02 | El sistema debe mantener tiempos de respuesta adecuados durante una alta concurrencia. | AC01 - Rendimiento | Influye en la comunicación, procesamiento, almacenamiento y uso de caché. |
| DA03 | El sistema debe proteger los datos de usuarios y operaciones de compra. | AC04 - Seguridad | Influye en autenticación, autorización y protección de datos. |
| DA04 | El sistema debe integrarse con una pasarela de pago externa mediante una API. | RC04 - Pasarela de pago | Requiere desacoplar los casos de uso del proveedor externo mediante interfaces y adaptadores. |
| DA05 | El sistema debe utilizar una API REST para la comunicación entre frontend y backend. | RC03 - API REST | Condiciona la comunicación entre la interfaz y el backend. |
| DA06 | El sistema debe permitir modificar y evolucionar funcionalidades sin afectar innecesariamente otros módulos. | AC05 - Mantenibilidad | Influye en la separación de responsabilidades, modularidad y control de dependencias internas. |