  

## 🎯 Objetivos del Laboratorio
- Comprender la infraestructura global de AWS
- Explorar regiones y zonas de disponibilidad
- Practicar data sources en Terraform
- Implementar configuración multi-región
- Aplicar mejores prácticas de seguridad

  

## 🏗️ Arquitectura

  

```

  

┌─────────────────┐ ┌─────────────────┐

│ us-east-1 │ │ eu-west-1 │

│ (Primary) │ │ (Secondary) │

├─────────────────┤ ├─────────────────┤

│ AZs: us-east-1a │ │ AZs: eu-west-1a │

│ us-east-1b │ │ eu-west-1b │

│ us-east-1c │ │ eu-west-1c │

│ │ │ │

│ Resources: │ │ Resources: │

│ • S3 Bucket │ │ • S3 Bucket │

│ • AMI Info │ │ • AMI Info │

└─────────────────┘ └─────────────────┘

  

```

  

## 📋 Prerrequisitos

  

- [x] AWS CLI configurado (`aws configure`)

- [x] Terraform >= 1.0 instalado

- [x] Credenciales AWS válidas

- [x] Permisos para crear recursos S3

  

## 🚀 Ejecución del Laboratorio

  

### 1. Configuración Inicial

  

```bash

# Clonar y navegar al laboratorio

cd labs/phase-1-fundamentals/lab-01-regions-azs/

  

# Verificar configuración AWS

aws sts get-caller-identity

  

# Inicializar Terraform

terraform init

```

  

### 2. Planificación

  

```bash

# Ver el plan de ejecución

terraform plan

  

# Revisar que las regiones sean correctas

terraform plan -var="primary_region=us-east-1" -var="secondary_region=eu-west-1"

```

  

### 3. Aplicación

  

```bash

# Aplicar configuración

terraform apply

  

# Confirmar con 'yes' cuando se solicite

```

  

### 4. Exploración de Resultados

  

```bash

# Ver información de regiones

terraform output primary_region_info

  

# Ver comparación entre regiones

terraform output regions_comparison

  

# Ver resumen completo

terraform output lab_summary

```

  

### 5. Limpieza

  

```bash

# Destruir recursos para evitar costos

terraform destroy

  

# Confirmar con 'yes'

```

  

## 📊 Conceptos Clave Aprendidos

  

### 🌍 **Infraestructura Global AWS**

  

- **Regiones**: Ubicaciones geográficas con múltiples AZs

- **Zonas de Disponibilidad**: Centros de datos aislados

- **Edge Locations**: Puntos de presencia para CloudFront

  

### 🏗️ **Terraform Data Sources**

  

- `aws_region`: Información de regiones

- `aws_availability_zones`: Lista de AZs disponibles

- `aws_caller_identity`: Información de la cuenta

- `aws_ami`: Imágenes de máquinas virtuales

  

### 🔧 **Multi-Provider Configuration**

  

- Proveedores con alias para múltiples regiones

- Configuración de tags por defecto

- Gestión de recursos distribuidos

  

## 🎯 Preguntas de Preparación para el Examen

  

### 1. **¿Cuál es la diferencia entre una Región y una Zona de Disponibilidad?**

  

- **Región**: Área geográfica con múltiples AZs

- **AZ**: Centro de datos aislado dentro de una región

  

### 2. **¿Cuántas AZs tiene cada región típicamente?**

  

- Mínimo 3 AZs por región

- Máximo varía (algunas tienen 6+)

  

### 3. **¿Cómo afecta la elección de región a la latencia?**

  

- Proximidad geográfica reduce latencia

- Considerar ubicación de usuarios finales

  

## 💰 Estimación de Costos

  

- **S3 Buckets**: Gratis (Free Tier)

- **Data Transfer**: Mínimo (solo metadatos)

- **Total Estimado**: $0.00

  

## 🔗 Enlaces Útiles

  

- [AWS Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/)

- [AWS Regions and AZs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html)

- [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)

  

---

  

**⚠️ Importante**: Siempre ejecuta `terraform destroy` al finalizar para evitar costos innecesarios.