# Brief Ejecutivo-Técnico: E-commerce Retail

## A1) Arquitectura aplicada al caso
Nuestra organización es un E-commerce de Retail. El **System of Record (SoR)** es el ERP central que gestiona órdenes y clientes. Los sistemas satélites son el servicio de inventario y el servicio de despacho. Para conectar estos sistemas, utilizamos un broker de mensajes basado en **Apache Kafka** para lograr un flujo *Event-Driven* (orientado a eventos) para mayor escalabilidad y tolerancia a fallos.

### Diagrama de Arquitectura
```mermaid
graph TD
    User((Cliente)) -->|Compra| Frontend[Tienda Online]
    Frontend -->|Registra Orden| SOR[(ERP - System of Record)]
    SOR -->|Publica Evento: 'Orden Creada'| Broker{Kafka Broker}
    Broker -->|Notifica| Inv[Servicio Inventario]
    Broker -->|Notifica| Ship[Servicio Despacho]
    SOR -->|Carga de Datos| BI[Dashboard BI]

A2) Gobierno de TI (COBIT)
Roles y Responsabilidades:
Dirección: Define estrategia y presupuesto.
Gerente de TI: Responsable de disponibilidad técnica.
Oficial de Seguridad (CISO): Cumplimiento y protección.
Dueño de Proceso (Retail): Valida integridad de datos de ventas.
Decisiones Gobernadas:
Fuente de verdad del cliente (SoR).
Selección de proveedores Cloud/SaaS.
Ventanas de mantenimiento crítico.
Gestión de cambios en aplicaciones core.
Política de accesos y privilegios.
Plan de inversión tecnológica anual.
Políticas Mínimas:
Accesos: MFA obligatorio y revisión de roles trimestral.
Cambios: Todo despliegue requiere revisión de pares (Code Review).
Backups: Respaldo diario con prueba de restauración mensual.
Incidentes: Reporte formal y post-mortem obligatorio.
Proveedores: Evaluación de seguridad antes de contratar un SaaS.

A3) Riesgo y Seguridad (NIST CSF 2.0)

Para fortalecer la resiliencia del E-commerce, se ha evaluado el estado de ciberseguridad actual frente al objetivo deseado utilizando las 6 funciones del framework NIST.

Perfil de Madurez: Actual vs. Objetivo
Función	Perfil Actual (Tier 1/2)	Perfil Objetivo (Tier 3/4)
Govern	Políticas informales basadas en necesidad inmediata.	Gobernanza centralizada y alineada al negocio.
Identify	Inventario de activos manual en hojas de cálculo.	Gestión de activos automatizada y mapa de dependencias.
Protect	Uso de contraseñas simples y permisos amplios.	MFA obligatorio, microsegmentación y cifrado.
Detect	Revisión de logs solo tras un incidente.	Monitoreo 24/7 con alertas en tiempo real (SIEM).
Respond	Reacción reactiva sin guías documentadas.	Playbooks de respuesta a incidentes por categoría.
Recover	Restauración manual desde cintas o discos.	Plan de Recuperación ante Desastres (DRP) probado periódicamente.

 Controles Priorizados
  1.Autenticación Multifactor (MFA)
Justificación: Mitiga la gran mayoría de ataques de robo de credenciales.
Impacto: Alto / Viabilidad: Alta
  2.Escaneo de Vulnerabilidades Semanal
Justificación: Permite identificar fallos en el software antes de que sean explotados.
Impacto: Medio / Viabilidad: Alta
  3.Segregación de Redes (Microsegmentación)
Justificación: Evita que un ataque al frontend se propague hacia sistemas críticos como el ERP.
Impacto: Alto / Viabilidad: Media
  4.Cifrado de Datos en Reposo (AES-256)
Justificación: Protege la información de clientes ante accesos físicos o fugas de datos.
Impacto: Alto / Viabilidad: Alta
  5.Logging y Monitoreo Centralizado
Justificación: Permite detectar comportamientos anómalos en servicios y en el broker de eventos (Kafka).
Impacto: Medio / Viabilidad: Alta
  6.Programa de Concientización en Seguridad
Justificación: Reduce el riesgo humano, especialmente ante ataques de phishing.
Impacto: Alto / Viabilidad: Alta

  7.Mini Plan de Respuesta a Incidentes (NIST IR)
En caso de una brecha de seguridad o caída crítica, se seguirá el siguiente flujo de 3 pasos:
  8.Detección y Contención
Identificar el origen del incidente (por ejemplo, una IP maliciosa) y aislar inmediatamente el sistema afectado para evitar la propagación.
Erradicación
Eliminar la causa raíz del incidente: limpieza de malware, aplicación de parches de seguridad o rotación de credenciales comprometidas.
  9.Recuperación y Post-Mortem
Restaurar los servicios desde respaldos verificados y realizar un análisis de lecciones aprendidas para prevenir recurrencias.

A4) Métricas (DORA + Operación)
Deployment Frequency (DORA): Frecuencia de salidas a producción. Mide agilidad.
Change Failure Rate (DORA): % de cambios que causan fallos. Mide estabilidad.
Uptime / SLO (Operación): Disponibilidad del servicio (meta 99.9%).
MTTR (Operación): Tiempo medio de recuperación tras un incidente.
