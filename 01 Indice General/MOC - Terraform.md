---
tags:
  - moc
  - terraform
  - indice
aliases:
  - Terraform
  - Software Development
  - Dev MOC
---
# 🏗️ Estructura de Terraform para Certificación AWS SAA-C03

```
aws-saa-terraform-labs/
├── 📁 environments/                    # Configuraciones por ambiente
│   ├── dev/
│   │   ├── terraform.tfvars
│   │   ├── backend.tf
│   │   └── main.tf
│   ├── staging/
│   └── prod/
│
├── 📁 modules/                         # Módulos reutilizables
│   ├── networking/                     # VPC, Subnets, Security Groups
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   ├── versions.tf
│   │   └── README.md
│   │
│   ├── compute/                        # EC2, Auto Scaling, Load Balancers
│   │   ├── ec2/
│   │   ├── auto-scaling/
│   │   ├── load-balancer/
│   │   └── lambda/
│   │
│   ├── storage/                        # S3, EBS, EFS
│   │   ├── s3/
│   │   ├── ebs/
│   │   └── efs/
│   │
│   ├── database/                       # RDS, DynamoDB, ElastiCache
│   │   ├── rds/
│   │   ├── dynamodb/
│   │   └── elasticache/
│   │
│   ├── security/                       # IAM, KMS, Secrets Manager
│   │   ├── iam/
│   │   ├── kms/
│   │   └── secrets-manager/
│   │
│   └── monitoring/                     # CloudWatch, CloudTrail
│       ├── cloudwatch/
│       └── cloudtrail/
│
├── 📁 labs/                           # Laboratorios específicos del plan
│   ├── phase-1-fundamentals/
│   │   ├── lab-01-first-ec2/
│   │   │   ├── main.tf
│   │   │   ├── variables.tf
│   │   │   ├── terraform.tfvars
│   │   │   ├── README.md
│   │   │   └── architecture.drawio
│   │   │
│   │   ├── lab-02-s3-basic/
│   │   ├── lab-03-iam-management/
│   │   ├── lab-04-vpc-subnets/
│   │   ├── lab-05-s3-security/
│   │   └── lab-06-security-groups/
│   │
│   ├── phase-2-compute-storage/
│   │   ├── lab-07-elastic-beanstalk/
│   │   ├── lab-08-auto-scaling/
│   │   ├── lab-09-lambda-basic/
│   │   ├── lab-10-application-lb/
│   │   ├── lab-11-ecs-containers/
│   │   └── lab-12-lambda-api-gateway/
│   │
│   ├── phase-3-databases-networking/
│   │   ├── lab-13-rds-java-app/
│   │   ├── lab-14-elasticache-spring/
│   │   ├── lab-15-dynamodb-java/
│   │   ├── lab-16-multi-az-architecture/
│   │   ├── lab-17-cloudfront-static/
│   │   └── lab-18-route53-health-checks/
│   │
│   ├── phase-4-security-monitoring/
│   │   ├── lab-19-java-monitoring/
│   │   ├── lab-20-centralized-logging/
│   │   ├── lab-21-secrets-management/
│   │   ├── lab-22-cloudwatch-alerts/
│   │   ├── lab-23-waf-protection/
│   │   └── lab-24-compliance-config/
│   │
│   └── phase-5-architectures/
│       ├── project-01-monolith-migration/
│       ├── project-02-microservices/
│       └── project-03-event-processing/
│
├── 📁 shared/                         # Recursos compartidos
│   ├── data-sources/                  # AMIs, AZs, etc.
│   ├── locals/                        # Variables locales comunes
│   └── remote-state/                  # Configuración de remote state
│
├── 📁 scripts/                        # Scripts de automatización
│   ├── setup.sh                      # Configuración inicial
│   ├── deploy.sh                     # Deploy automatizado
│   ├── destroy.sh                    # Cleanup de recursos
│   └── validate.sh                   # Validación de sintaxis
│
├── 📁 docs/                          # Documentación
│   ├── architecture/                 # Diagramas de arquitectura
│   │   ├── phase-1/
│   │   ├── phase-2/
│   │   ├── phase-3/
│   │   ├── phase-4/
│   │   └── phase-5/
│   │
│   ├── best-practices/               # Mejores prácticas
│   │   ├── terraform-standards.md
│   │   ├── aws-naming-conventions.md
│   │   ├── security-guidelines.md
│   │   └── cost-optimization.md
│   │
│   ├── exam-notes/                   # Notas para el examen
│   │   ├── services-comparison.md
│   │   ├── architectural-patterns.md
│   │   ├── pricing-models.md
│   │   └── troubleshooting-guide.md
│   │
│   └── lab-guides/                   # Guías de laboratorio
│       ├── prerequisites.md
│       ├── common-issues.md
│       └── cleanup-procedures.md
│
├── 📁 examples/                      # Ejemplos de referencia
│   ├── well-architected-patterns/
│   ├── disaster-recovery/
│   ├── cost-optimization/
│   └── security-patterns/
│
├── 📄 .gitignore                     # Archivos a ignorar en Git
├── 📄 .pre-commit-config.yaml        # Hooks de pre-commit
├── 📄 README.md                      # Documentación principal
├── 📄 CHANGELOG.md                   # Registro de cambios
└── 📄 terraform.tf                   # Configuración global de providers
```

## 📋 Descripción de Responsabilidades

### 🌍 **environments/**

- **Propósito**: Configuraciones específicas por ambiente (dev/staging/prod)
- **Responsabilidad**: Gestionar variables de entorno, backends remotos, y configuraciones específicas
- **Archivo clave**: `terraform.tfvars` con valores específicos del ambiente

### 🧩 **modules/**

- **Propósito**: Módulos reutilizables para diferentes servicios AWS
- **Responsabilidad**: Encapsular lógica de recursos, promover reutilización
- **Estructura estándar**: `main.tf`, `variables.tf`, `outputs.tf`, `versions.tf`, `README.md`

### 🧪 **labs/**

- **Propósito**: Implementaciones específicas de cada laboratorio del plan de estudios
- **Responsabilidad**: Código práctico para cada fase de preparación
- **Incluye**: Diagramas de arquitectura, documentación específica, variables de prueba

### 🤝 **shared/**

- **Propósito**: Recursos y configuraciones compartidas entre laboratorios
- **Responsabilidad**: Data sources comunes, variables globales, configuración de remote state

### 🔧 **scripts/**

- **Propósito**: Automatización de tareas comunes
- **Responsabilidad**: Setup, deployment, validación, y cleanup automatizado

### 📚 **docs/**

- **Propósito**: Documentación técnica y de preparación para el examen
- **Responsabilidad**: Arquitecturas, mejores prácticas, notas de estudio, guías

### 💡 **examples/**

- **Propósito**: Patrones de referencia y casos de uso avanzados
- **Responsabilidad**: Implementaciones de Well-Architected Framework, DR, optimización

## 🛠️ Archivos de Configuración Estándar

### **Estructura de Módulo Tipo**

```
module-name/
├── main.tf          # Recursos principales
├── variables.tf     # Variables de entrada
├── outputs.tf       # Outputs del módulo
├── versions.tf      # Versiones de providers
├── README.md        # Documentación del módulo
└── examples/        # Ejemplos de uso
```

### **Estructura de Laboratorio Tipo**

```
lab-XX-name/
├── main.tf              # Configuración principal
├── variables.tf         # Variables específicas
├── terraform.tfvars     # Valores por defecto
├── outputs.tf           # Outputs importantes
├── README.md            # Instrucciones del lab
├── architecture.drawio  # Diagrama de arquitectura
└── tests/              # Tests de validación
```

## 🎯 Convenciones de Nomenclatura

### **Recursos AWS**

- **Prefijo**: `saa-cert-{environment}-{service}`
- **Ejemplo**: `saa-cert-dev-web-server`, `saa-cert-prod-database`

### **Variables**

- **Snake_case**: `instance_type`, `subnet_cidr_blocks`
- **Descriptivas**: `web_server_instance_type` vs `type`

### **Tags Estándar**

```hcl
tags = {
  Project     = "AWS-SAA-Certification"
  Environment = var.environment
  Phase       = "Phase-1-Fundamentals"
  Lab         = "Lab-01-First-EC2"
  Owner       = "YourName"
  CreatedBy   = "Terraform"
}
```

## 🚀 Flujo de Trabajo Recomendado

1. **Preparación**: `scripts/setup.sh`
2. **Desarrollo**: Trabajar en `labs/phase-X/lab-XX/`
3. **Validación**: `scripts/validate.sh`
4. **Deploy**: `scripts/deploy.sh lab-01`
5. **Documentación**: Actualizar `docs/` con aprendizajes
6. **Cleanup**: `scripts/destroy.sh lab-01`

## 📖 Referencias de Arquitectura

### **Fase 1 - Fundamentos**

- VPC básica con subnets públicas/privadas
- EC2 con Security Groups
- S3 con políticas IAM

### **Fase 2 - Compute/Storage**

- Auto Scaling Groups con ALB
- Lambda con API Gateway
- ECS con Fargate

### **Fase 3 - Databases/Networking**

- RDS Multi-AZ con read replicas
- CloudFront con S3 origin
- Route 53 con health checks

### **Fase 4 - Security/Monitoring**

- WAF con CloudFront
- CloudWatch dashboards
- Config rules para compliance

### **Fase 5 - Arquitecturas**

- Patrones de microservicios
- Event-driven architecture
- Disaster recovery patterns

---

**💡 Nota**: Esta estructura está optimizada para el aprendizaje progresivo según tu plan de estudios SAA-C03, permitiendo reutilización de módulos y escalabilidad para futuros proyectos.