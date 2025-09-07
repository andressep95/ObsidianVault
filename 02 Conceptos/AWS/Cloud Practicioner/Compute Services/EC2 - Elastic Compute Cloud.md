## ¿Qué es?

**Amazon Elastic Compute Cloud (EC2)** es un servicio web que proporciona capacidad de computación redimensionable en la nube de AWS. Permite lanzar servidores virtuales bajo demanda, escalando automáticamente hacia arriba o hacia abajo según las necesidades de la aplicación, eliminando la necesidad de invertir en hardware por adelantado.

![AWS EC2](../../../../attachments/Compute%20Services/EC2/img-ec2.jpeg)

**Diagrama:**

```
[Usuario] → [AWS Management Console/CLI/API] → [EC2 Service]
                                                    ↓
[VPC] → [Availability Zone] → [EC2 Instance] ← [Security Group]
   ↓         ↓                      ↓              ↓
[Subnet] [EBS Volume]        [Instance Store] [Key Pair]
   ↓         ↓                      ↓
[Route Table] [Snapshot]    [AMI Template]
```

## Escenarios de uso

- **Hosting de aplicaciones web** - Servidores web, bases de datos, APIs
- **Procesamiento por lotes** - Jobs de análisis de datos, rendering, cálculos científicos
- **Entornos de desarrollo y pruebas** - Ambientes temporales para equipos de desarrollo
- **Backup y recuperación ante desastres** - Réplicas de sistemas críticos en diferentes regiones
- **Big Data y Analytics** - Clusters de procesamiento para Hadoop, Spark, etc.
- **Gaming servers** - Servidores dedicados para juegos online
- **Machine Learning** - Entrenamiento e inferencia de modelos de ML
- **Microservicios** - Contenedores y aplicaciones distribuidas

## Buenas prácticas

- **Usar instancias del tamaño apropiado** - Monitorear métricas y ajustar según necesidad real
- **Implementar Auto Scaling** - Configurar escalado automático basado en métricas de CloudWatch
- **Distribuir en múltiples AZ** - Colocar instancias en diferentes zonas de disponibilidad para alta disponibilidad
- **Seguridad por capas** - Combinar Security Groups, NACLs, WAF y herramientas de monitoreo
- **Gestión de claves adecuada** - Usar AWS Systems Manager Parameter Store o Secrets Manager
- **Backups regulares** - Implementar snapshots automáticos de volúmenes EBS
- **Monitoreo proactivo** - Configurar alarmas en CloudWatch para métricas críticas
- **Etiquetado consistente** - Aplicar tags para organización, facturación y gobierno

## Aspectos a configurar

- **Instance Type** - Seleccionar familia y tamaño según requisitos de CPU, memoria, red y almacenamiento
- **AMI (Amazon Machine Image)** - Elegir imagen base del sistema operativo y software preinstalado
- **Key Pairs** - Configurar autenticación SSH para acceso seguro a instancias Linux
- **Security Groups** - Definir reglas de firewall para tráfico de entrada y salida
- **Network settings** - VPC, subnet, IP pública/privada, Enhanced Networking
- **Storage configuration** - Tipos de volúmenes EBS, tamaños, cifrado, IOPS
- **User Data** - Scripts de inicialización automática al lanzar la instancia
- **IAM Roles** - Permisos para que la instancia acceda a otros servicios AWS

## Versiones/Variantes del servicio

| Familia/Tipo                         | Caso de uso              | Características                                                  |
| ------------------------------------ | ------------------------ | ---------------------------------------------------------------- |
| **General Purpose (M, T)**           | Aplicaciones balanceadas | Balance de compute, memoria y red. T\* con performance burstable |
| **Compute Optimized (C)**            | CPU intensivo            | Alto rendimiento de procesador para HPC, gaming, ML inference    |
| **Memory Optimized (R, X, z1d)**     | En memoria               | Grandes datasets en RAM, bases de datos en memoria, analytics    |
| **Storage Optimized (I, D, H1)**     | I/O intensivo            | Alto IOPS secuencial, distributed file systems, data warehousing |
| **Accelerated Computing (P, G, F1)** | GPU/FPGA                 | Machine learning, HPC científico, rendering, genomics            |
| **High-Performance Computing (HPC)** | HPC específico           | Workloads de supercomputación con mejor precio-rendimiento       |

## Modelo de precios y facturación

- **Método de cobro:** Por segundo de uso (mínimo 60 segundos), basado en tipo de instancia
- **Opciones de pricing:**
  - **On-Demand:** Pago por uso sin compromisos
  - **Reserved Instances:** Descuentos hasta 72% con compromiso de 1-3 años
  - **Spot Instances:** Hasta 90% descuento usando capacidad no utilizada
  - **Savings Plans:** Descuentos hasta 72% con compromiso de gasto por hora
  - **Dedicated Hosts:** Hardware físico dedicado para compliance
- **Costos típicos:** Desde $0.0058/hora (t4g.nano) hasta $24.48/hora (p4d.24xlarge)
- **Free Tier:** 750 horas/mes de t2.micro o t3.micro por 12 meses

## Integración con otros servicios AWS

- **Servicios comunes:**
  - **EBS** - Almacenamiento persistente de bloques
  - **ELB** - Balanceadores de carga para distribución de tráfico
  - **Auto Scaling** - Escalado automático de grupos de instancias
  - **CloudWatch** - Monitoreo de métricas y logs
  - **Systems Manager** - Administración y patching automatizado
  - **VPC** - Redes virtuales privadas y aislamiento
- **Patrones arquitecturales:**
  - Web tier con ELB + Auto Scaling Group + RDS
  - Microservicios con ECS/EKS + ALB + Service Discovery
  - Big Data con EMR + S3 + Redshift
- **Dependencias:** VPC (obligatorio), Security Groups, Key Pairs para acceso SSH

## Límites y cuotas

- **Límites por defecto:**
  - 20 instancias On-Demand por región (familias estándar)
  - 5 instancias On-Demand para familias especializadas (P, X, etc.)
  - 100 Security Groups por VPC
  - 50 Key Pairs por región
- **Límites aumentables:** Todos los límites de instancias mediante Service Quotas
- **Consideraciones de escalabilidad:**
  - Placement Groups para baja latencia entre instancias
  - Enhanced Networking para alto rendimiento de red
  - Instance Store para I/O de muy baja latencia (efímero)

## Seguridad y compliance

- **Modelo de responsabilidad:**
  - **AWS:** Seguridad física, hipervisor, infraestructura de red
  - **Cliente:** SO, aplicaciones, datos, configuración de red, IAM
- **Opciones de cifrado:**
  - EBS encryption at rest y in-transit
  - Instance Store encryption (donde esté disponible)
  - Network encryption con VPN/TLS
- **Certificaciones:** SOC, PCI DSS, HIPAA, FedRAMP, ISO 27001
- **Control de acceso:**
  - IAM roles y policies para API calls
  - Security Groups para network access
  - Key Pairs para SSH authentication
  - AWS SSM Session Manager para acceso sin SSH

## Monitoreo y troubleshooting

- **CloudWatch metrics:**
  - CPU Utilization, Network In/Out, Disk Read/Write
  - Status Check Failed, Credit Balance (instancias T\*)
  - Custom metrics vía CloudWatch Agent
- **Logs generados:**
  - System logs, Application logs, VPC Flow Logs
  - CloudTrail para API calls de gestión
- **CloudTrail events:**
  - RunInstances, TerminateInstances, StartInstances, StopInstances
  - ModifyInstanceAttribute, CreateTags
- **Herramientas de diagnóstico:**
  - EC2 Instance Connect para troubleshooting
  - Systems Manager Session Manager
  - EC2 Serial Console para boot issues
  - Instance metadata service (IMDS)

## Disponibilidad y durabilidad

- **SLA:** 99.99% de disponibilidad mensual por región
- **Durabilidad:** N/A (no aplica para compute, pero EBS tiene 99.999%)
- **Opciones de redundancia:**
  - **Multi-AZ:** Distribución en múltiples zonas de disponibilidad
  - **Multi-Region:** Para disaster recovery y compliance
  - **Placement Groups:** Cluster, Partition, Spread para diferentes estrategias
- **Backup/Restore:**
  - EBS Snapshots para backup de datos
  - AMI creation para backup completo del sistema
  - AWS Backup para políticas centralizadas
  - Cross-region snapshot copy para DR

## Casos de uso: Correcto vs Incorrecto

### ✅ Cuándo SÍ usar EC2:

- **Aplicaciones que requieren control total del OS** - Configuraciones específicas, software personalizado
- **Workloads con patrones de uso variables** - Aplicaciones que necesitan escalar dinámicamente
- **Migración lift-and-shift** - Mover aplicaciones existentes a la nube sin rediseño
- **Desarrollo y testing** - Entornos temporales que se pueden crear/destruir rápidamente
- **Aplicaciones legacy** - Sistemas que no pueden ser containerizados o serverless
- **High Performance Computing** - Simulaciones científicas, rendering, análisis intensivos

### ❌ Cuándo NO usar EC2:

- **Funciones simples y event-driven** → **Alternativa:** AWS Lambda para serverless computing
- **Aplicaciones web estáticas** → **Alternativa:** S3 + CloudFront para hosting estático
- **Workloads containerizados sin gestión de infraestructura** → **Alternativa:** AWS Fargate o ECS/EKS
- **Bases de datos relacionales estándar** → **Alternativa:** Amazon RDS para gestión automatizada
- **Procesamiento de datos sin servidor permanente** → **Alternativa:** AWS Batch para jobs por lotes
- **APIs simples sin estado** → **Alternativa:** API Gateway + Lambda para arquitecturas serverless
- **Almacenamiento de archivos compartido** → **Alternativa:** Amazon EFS o FSx para file systems gestionados
