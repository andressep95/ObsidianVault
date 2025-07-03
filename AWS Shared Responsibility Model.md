

> **📂 Categoría:** Fundamentos | **🏷️ Tags:** #aws #infrastructure #regions #responsability-model  
> **📅 Creado:** 2025-07-02 | **🔄 Actualizado:** 2025-06-27  
> **📈 Nivel:** Básico | **💰 Pricing Tier:** N/A (Conceptual)

---

## Explicación

El Modelo de Responsabilidad Compartida de AWS es un marco de seguridad que define claramente la división de responsabilidades de seguridad entre AWS y los clientes. Este modelo es fundamental para entender cómo funciona la seguridad en la nube y es esencial para diseñar arquitecturas seguras.

### Componentes Principales

**Responsabilidades de AWS ("Seguridad DE la Nube")**

- Seguridad física de centros de datos y hardware
- Seguridad de infraestructura (networking, hipervisor, sistema operativo host)
- Seguridad de servicios y parcheo de servicios administrados por AWS
- Controles de red global y seguridad de edge locations

**Responsabilidades del Cliente ("Seguridad EN la Nube")**

- Gestión de Identidades y Acceso (IAM)
- Encriptación de datos en tránsito y en reposo
- Parches y actualizaciones del sistema operativo (para EC2)
- Protección de tráfico de red y configuración de firewall
- Seguridad a nivel de aplicación y vulnerabilidades de código

### Diagrama de Arquitectura

```
┌─────────────────────────────────────────────────────────┐
│                Responsabilidad del Cliente                │
│  ┌─────────────────────────────────────────────────────┐  │
│  │       Datos del Cliente y Clasificación            │  │
│  │  ┌─────────────────────────────────────────────────┐│  │
│  │  │      Plataforma, Aplicaciones, IAM             ││  │
│  │  │  ┌─────────────────────────────────────────────┐││  │
│  │  │  │   Sistema Operativo, Red y Firewall        │││  │
│  │  │  │  ┌─────────────────────────────────────────┐│││  │
│  │  │  │  │    Encriptación de Datos Cliente-Side   ││││  │
│  │  │  │  │  ┌─────────────────────────────────────┐│││  │
│  │  │  │  │  │      Encriptación Server-Side       ││││  │
│  │  │  │  │  │  ┌─────────────────────────────────┐│││  │
│  │  │  │  │  │  │   Protección de Tráfico de Red   ││││  │
│  │  │  │  │  │  └─────────────────────────────────┘│││  │
│  │  │  │  │  └─────────────────────────────────────┘││  │
│  │  │  │  └─────────────────────────────────────────┘│  │
│  │  │  └─────────────────────────────────────────────┘  │
│  │  └─────────────────────────────────────────────────┘  │
│  └─────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────┐
│                  Responsabilidad de AWS                   │
│  ┌─────────────────────────────────────────────────────┐  │
│  │           Infraestructura Global de AWS            │  │
│  │  ┌─────────────────────────────────────────────────┐│  │
│  │  │         Regiones, AZs, Edge Locations           ││  │
│  │  │  ┌─────────────────────────────────────────────┐││  │
│  │  │  │       Cómputo, Almacenamiento, Base de      │││  │
│  │  │  │              Datos, Networking              │││  │
│  │  │  │  ┌─────────────────────────────────────────┐│││  │
│  │  │  │  │        Servicios Administrados AWS      ││││  │
│  │  │  │  └─────────────────────────────────────────┘│││  │
│  │  │  └─────────────────────────────────────────────┘││  │
│  │  └─────────────────────────────────────────────────┘│  │
│  └─────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

### Responsabilidades Específicas por Servicio

|Tipo de Servicio|Responsabilidad de AWS|Responsabilidad del Cliente|
|---|---|---|
|**IaaS (EC2)**|Seguridad física, hipervisor, controles de red|Parches del SO, aplicaciones, encriptación de datos, protección de tráfico de red|
|**PaaS (RDS)**|Software de base de datos, parches del SO, hardware|Configuración de BD, IAM, encriptación, estrategia de backup|
|**SaaS (S3)**|Infraestructura, disponibilidad del servicio, durabilidad|Clasificación de datos, políticas IAM, políticas de bucket, encriptación|

## Ejemplos del Mundo Real

**Ejemplo 1: Aplicación de E-commerce**

- **AWS maneja**: Seguridad física del centro de datos, mantenimiento de hardware del servidor, protección de infraestructura de red
- **Cliente maneja**: Seguridad del código de aplicación, autenticación de usuarios, encriptación de datos de tarjetas de crédito, controles de acceso a base de datos

**Ejemplo 2: Análisis de Datos de Salud**

- **AWS maneja**: Infraestructura elegible para HIPAA, cumplimiento de hardware, certificaciones de servicios
- **Cliente maneja**: Configuración de cumplimiento HIPAA, encriptación de datos de pacientes, registro de accesos, pistas de auditoría

**Ejemplo 3: Servicios Financieros**

- **AWS maneja**: Controles de seguridad física, monitoreo de infraestructura, disponibilidad de servicios
- **Cliente maneja**: Encriptación de datos financieros, configuración de cumplimiento regulatorio, gestión de identidades, sistemas de detección de fraude

## Consejos para el Examen

1. **Recuerda la distinción "DE vs EN"**: AWS es responsable de la seguridad DE la nube (infraestructura), los clientes de la seguridad EN la nube (sus datos y aplicaciones)
    
2. **El modelo de servicio determina la responsabilidad**: Mientras más administrado sea el servicio (IaaS → PaaS → SaaS), más aumenta la responsabilidad de AWS y disminuye la del cliente
    
3. **Los datos son siempre responsabilidad del cliente**: Sin importar el servicio, los clientes siempre son responsables de la clasificación, encriptación y controles de acceso de sus datos
    

## Preguntas de Práctica

**Pregunta 1:** Una empresa está ejecutando una aplicación web en instancias Amazon EC2. Según el Modelo de Responsabilidad Compartida de AWS, ¿cuál de las siguientes tareas de seguridad es responsabilidad del cliente?

A) Seguridad física del centro de datos B) Parches y actualizaciones del hipervisor C) Parches de seguridad del sistema operativo D) Protección de la infraestructura de red

**Pregunta 2:** Una organización está usando Amazon RDS para sus necesidades de base de datos. ¿De cuál de los siguientes es responsable AWS bajo el Modelo de Responsabilidad Compartida?

A) Gestión de cuentas de usuario de la base de datos B) Parches y actualizaciones del motor de base de datos C) Gestión de claves de encriptación de la base de datos D) Programación de backups de la base de datos

**Pregunta 3:** Una empresa de salud está almacenando datos de pacientes en Amazon S3. Según el Modelo de Responsabilidad Compartida, ¿cuál de los siguientes es responsabilidad del cliente?

A) Disponibilidad y durabilidad del servicio S3 B) Seguridad física de las instalaciones de almacenamiento S3 C) Clasificación de datos y controles de acceso D) Seguridad de los endpoints de la API S3

**Pregunta 4:** ¿Cuál declaración describe mejor el Modelo de Responsabilidad Compartida de AWS?

A) AWS es responsable de todos los aspectos de seguridad de los servicios en la nube B) Los clientes son responsables de todos los aspectos de seguridad de sus aplicaciones C) Las responsabilidades de seguridad se comparten entre AWS y los clientes basándose en el modelo de servicio D) AWS y los clientes tienen responsabilidades de seguridad idénticas

**Pregunta 5:** Una empresa está migrando desde on-premises a AWS. ¿Qué responsabilidad de seguridad se trasladará del cliente a AWS?

A) Encriptación de datos en tránsito B) Gestión de identidades y acceso C) Seguridad física del centro de datos D) Gestión de vulnerabilidades de aplicaciones

---

_Nota: Proporcionaré las respuestas a estas preguntas de práctica una vez que hayas tenido oportunidad de reflexionar sobre ellas. Esto ayuda a reforzar el proceso de aprendizaje y te prepara mejor para el formato real del examen._