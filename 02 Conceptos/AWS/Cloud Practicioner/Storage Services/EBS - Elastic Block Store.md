## ¿Qué es?

**Amazon Elastic Block Store (EBS)** es un servicio de almacenamiento de bloques de alto rendimiento y escalable diseñado para usarse con Amazon EC2. Proporciona volúmenes de almacenamiento persistente que se comportan como discos duros físicos y se pueden conectar a instancias EC2, ofreciendo durabilidad, disponibilidad y consistencia para cargas de trabajo críticas.

![AWS EC2](../../../../attachments/Storage%20Services/EBS/img-ebs.png)

**Diagrama:**

```
[EC2 Instance] ←→ [EBS Volume] → [Availability Zone A]
      ↓               ↓              ↓
[EBS-Optimized] → [Volume Type] → [Automatic Replication]
      ↓               ↓              ↓
[IOPS/Throughput] [Encryption] → [EBS Snapshots] → [S3 Storage]
                                        ↓              ↓
                              [Cross-Region Copy] → [Lifecycle Mgmt]
```

## Escenarios de uso

- **Sistemas de archivos y bases de datos** - Almacenamiento primario para sistemas operativos, aplicaciones y databases
- **File systems distribuidos** - Almacenamiento para Hadoop, sistemas de archivos en cluster
- **Backup y archivado** - Snapshots para backup, disaster recovery y archivado de datos
- **Boot volumes** - Volúmenes de arranque para instancias EC2 con persistencia
- **Data warehousing** - Almacenamiento para grandes volúmenes de datos analytics
- **Desarrollo y testing** - Entornos temporales con datos persistentes
- **Enterprise applications** - SAP, Oracle, Microsoft SQL Server con requerimientos específicos de IOPS
- **Contenido multimedia** - Almacenamiento para procesamiento de video, imágenes y audio

## Buenas prácticas

- **Usar volúmenes gp3 por defecto** - Mejor relación precio-rendimiento que gp2 para nuevos workloads
- **Implementar encriptación automática** - Habilitar encriptación por defecto en la cuenta
- **Optimizar tipos de instancia EBS** - Usar instancias EBS-optimized para máximo rendimiento
- **Monitorear métricas CloudWatch** - Configurar alarmas para IOPS, throughput y queue depth
- **Estrategia de snapshots automatizada** - Usar Data Lifecycle Manager para backups regulares
- **Right-sizing de volúmenes** - Ajustar tamaño y rendimiento según patrones de uso reales
- **Usar placement groups** - Para aplicaciones que requieren baja latencia entre volúmenes
- **Implementar Multi-Attach cuando sea necesario** - Para clusters que requieren acceso compartido

## Aspectos a configurar

- **Volume Type** - Seleccionar tipo SSD (gp3, gp2, io1, io2) o HDD (st1, sc1) según workload
- **Volume Size** - Capacidad de almacenamiento desde 1 GB hasta 64 TB según tipo
- **IOPS provisioned** - IOPS baseline y burst para tipos gp3, io1, io2
- **Throughput** - MB/s independiente de IOPS para tipos gp3 y io2 Block Express
- **Encryption settings** - Cifrado en reposo con KMS keys (AWS managed o customer managed)
- **Snapshot schedule** - Políticas automáticas de backup y retención
- **Availability Zone** - Ubicación específica del volumen (no cross-AZ)
- **Tags and labeling** - Etiquetado para organización, facturación y governance

## Versiones/Variantes del servicio

| Tipo de Volumen                    | Caso de uso                         | Características                                                    |
| ---------------------------------- | ----------------------------------- | ------------------------------------------------------------------ |
| **gp3 (General Purpose SSD)**      | Workloads transaccionales generales | 3,000 IOPS base, hasta 16,000 IOPS, throughput independiente       |
| **gp2 (General Purpose SSD)**      | Aplicaciones con burst performance  | IOPS escalable con tamaño, burst credits, legacy                   |
| **io1 (Provisioned IOPS SSD)**     | Databases críticas, I/O intensivo   | Hasta 64,000 IOPS, consistent performance, Multi-Attach            |
| **io2 (Provisioned IOPS SSD)**     | Mission-critical, ultra-high IOPS   | Hasta 64,000 IOPS, 99.999% durability, NVMe reservations           |
| **io2 Block Express**              | Aplicaciones más demandantes        | Hasta 256,000 IOPS, 4,000 MB/s throughput, sub-millisecond latency |
| **st1 (Throughput Optimized HDD)** | Big data, data warehousing          | 500 MB/s throughput, optimizado para streaming                     |
| **sc1 (Cold HDD)**                 | Almacenamiento infrequente          | Menor costo, 250 MB/s throughput, archival                         |

## Modelo de precios y facturación

- **Método de cobro:** Por GB-mes provisioned + IOPS adicionales + throughput + snapshots + transferencia de datos
- **Opciones de pricing:**
  - **Storage:** $0.08-$0.125/GB-mes (gp3), $0.045-$0.015/GB-mes (HDD)
  - **IOPS:** $0.005/IOPS provisioned-mes (io1, io2)
  - **Throughput:** $0.04/MB/s-mes provisioned (gp3)
  - **Snapshots:** $0.05/GB-mes (standard), $0.0125/GB-mes (archive)
- **Costos típicos:** gp3 100GB = $8/mes, io2 100GB + 10,000 IOPS = $62.5/mes
- **Free Tier:** 30 GB de cualquier combinación de volúmenes EBS por 12 meses

## Integración con otros servicios AWS

- **Servicios comunes:**
  - **EC2** - Attachment directo a instancias como storage principal
  - **KMS** - Encryption keys para cifrado de volúmenes y snapshots
  - **Data Lifecycle Manager** - Automatización de snapshots y lifecycle policies
  - **CloudWatch** - Métricas de rendimiento y monitoring
  - **AWS Backup** - Backup centralizado y compliance
  - **Systems Manager** - Gestión y patching de sistemas
- **Patrones arquitecturales:**
  - High Availability: EBS + Multi-AZ deployment + automated snapshots
  - Performance: io2 Block Express + Cluster Compute instances
  - Cost-optimized: gp3 + snapshot lifecycle + S3 archive
- **Dependencias:** EC2 instance (obligatorio), mismo AZ que la instancia

## Límites y cuotas

- **Límites por defecto:**
  - 5,000 EBS volumes por región por cuenta
  - 10,000 snapshots por región por cuenta
  - 20 TiB total de storage gp2/gp3 por región
  - 300 TiB total de Provisioned IOPS storage por región
- **Límites aumentables:** Todos los límites a través de Service Quotas console
- **Consideraciones de escalabilidad:**
  - Volumen máximo: 64 TiB (io2 Block Express), 16 TiB (otros)
  - IOPS máximos: 256,000 (io2 Block Express), 64,000 (io1/io2)
  - Throughput máximo: 4,000 MB/s (io2 Block Express), 1,000 MB/s (gp3/io1)

## Seguridad y compliance

- **Modelo de responsabilidad:**
  - **AWS:** Infraestructura física, replicación automática en AZ, durabilidad del servicio
  - **Cliente:** Cifrado de datos, gestión de keys, backup strategy, access control
- **Opciones de cifrado:**
  - Encryption at rest con AES-256
  - AWS managed keys o customer managed KMS keys
  - In-transit encryption entre EC2 y EBS (automático)
- **Certificaciones:** SOC, PCI DSS, HIPAA eligible, ISO 27001, FedRAMP
- **Control de acceso:**
  - IAM policies para operaciones de EBS
  - KMS key policies para encryption access
  - Resource-based policies para cross-account sharing
  - CloudTrail logging para audit trail

## Monitoreo y troubleshooting

- **CloudWatch metrics:**
  - VolumeReadOps/VolumeWriteOps (IOPS), VolumeReadBytes/VolumeWriteBytes
  - VolumeThroughputPercentage, VolumeConsumedReadWriteOps
  - VolumeQueueLength, VolumeTotalReadTime/VolumeTotalWriteTime
  - BurstBalance (gp2 volumes), VolumeStalledIOCheck
- **Logs generados:**
  - CloudTrail para API calls (CreateVolume, AttachVolume, CreateSnapshot)
  - VPC Flow Logs si se accede desde VPC endpoints
- **CloudTrail events:**
  - AttachVolume, DetachVolume, CreateVolume, DeleteVolume
  - CreateSnapshot, DeleteSnapshot, ModifyVolume
- **Herramientas de diagnóstico:**
  - EBS Volume Insights para análisis de performance
  - CloudWatch Container Insights para métricas detalladas
  - AWS X-Ray para tracing de I/O performance
  - Instance Store performance testing tools

## Disponibilidad y durabilidad

- **SLA:** 99.999% availability (io2), 99.8%-99.9% para otros tipos
- **Durabilidad:** 99.999% durability (io2 Block Express), 99.8%-99.9% para otros
- **Opciones de redundancia:**
  - **Automatic replication:** Dentro de la misma AZ automáticamente
  - **Cross-AZ:** Snapshots pueden restaurarse en cualquier AZ
  - **Cross-Region:** Snapshots pueden copiarse entre regiones
  - **Multi-Attach:** Acceso concurrente desde múltiples instancias (io1/io2)
- **Backup/Restore:**
  - EBS Snapshots incrementales almacenados en S3
  - Point-in-time recovery con snapshots
  - Fast Snapshot Restore para restauración rápida
  - Snapshot Archive para retención a largo plazo (90+ días)

## Casos de uso: Correcto vs Incorrecto

### ✅ Cuándo SÍ usar EBS:

- **Datos persistentes críticos** - Databases, file systems que requieren durabilidad
- **Alto rendimiento IOPS** - Aplicaciones que necesitan >16,000 IOPS consistentes
- **Boot volumes persistentes** - Instancias que requieren arranque rápido y datos persistentes
- **Backup y disaster recovery** - Estrategias de backup con snapshots cross-region
- **Shared storage en clusters** - Multi-Attach para aplicaciones cluster-aware
- **Compliance y auditoría** - Datos que requieren cifrado y audit trails detallados

### ❌ Cuándo NO usar EBS:

- **Almacenamiento temporal de alta performance** → **Alternativa:** Instance Store (NVMe SSD) para caches y temp data
- **Archivos estáticos web de gran escala** → **Alternativa:** S3 + CloudFront para content delivery
- **Big data processing temporal** → **Alternativa:** S3 + EMR con instance store para Hadoop/Spark
- **Almacenamiento de logs de corta duración** → **Alternativa:** CloudWatch Logs o S3 direct streaming
- **Datos que no requieren persistencia** → **Alternativa:** Instance Store para swap files, temp processing
- **Almacenamiento cross-region por defecto** → **Alternativa:** S3 para datos que necesitan acceso multi-region
- **Streaming de datos en tiempo real** → **Alternativa:** Kinesis Data Streams para data streaming
- **Content delivery global** → **Alternativa:** S3 + CloudFront para distribución mundial
