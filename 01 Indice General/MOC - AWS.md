---
tags: [moc, aws, cloud, infraestructura]
aliases: [Amazon Web Services, AWS Index]
---
# ☁️ Plan de Estudios - AWS Solutions Architect Associate (SAA-C03)

> **🎯 Objetivo:** Obtener la certificación AWS Certified Solutions Architect - Associate en 3-4 meses **📅 Creado:** 27/06/2025 **🔄 Última actualización:** {{date}}

## 📋 Prerrequisitos Completados

- [x] Experiencia en programación (Java/Spring Boot) ✅
- [x] Conocimientos básicos de redes e infraestructura
- [x] Cuenta AWS Free Tier creada
- [x] Entorno de estudio configurado

## [Mapa de Certificaciones de AWS (PDF)](https://d1.awsstatic.com/es_ES/training-and-certification/docs/AWS_certification_paths.pdf)

## 🗺️ Mapa de Ruta General

```mermaid
graph TD
    A[Fundamentos AWS] --> B[Compute & Storage]
    B --> C[Databases & Networking]
    C --> D[Security & Monitoring]
    D --> E[Architectures & Patterns]
    E --> F[Exam Preparation]
    F --> G[🏆 Certification]
```

---

## 📚 Fase 1: Fundamentos AWS (Semanas 1-2)

**⏱️ Tiempo sugerido:** 1-2 horas/día

### 🎯 Conceptos Clave a Dominar

- [x] [[AWS Global Infrastructure]]
- [x] [[AWS Well-Architected Framework]]
- [x] [[AWS Shared Responsibility Model]]
- [ ] [[AWS Management Console]]
- [ ] [[AWS Pricing Models]]

### ⚙️ Servicios Core

- [ ] [[AWS IAM & AWS CLI - Identity and Access Management]]
- [ ] [[Amazon EC2 - Elastic Compute Cloud]]
- [ ] [[Amazon S3 - Simple Storage Service]]
- [ ] [[Amazon VPC - Virtual Private Cloud]]

### 📖 Recursos de Estudio

**Curso Principal** (elegir uno):

- [ ] [Ultimate AWS Certified Solutions Architect Associate](https://www.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/?couponCode=LETSLEARNNOW)
- [ ] AWS Certified Solutions Architect Associate (A Cloud Guru)
- [ ] AWS Training oficial

**Documentación:**

- [ ] [AWS Documentation - Getting Started](https://docs.aws.amazon.com/index.html)

### 🧪 Laboratorios Prácticos - Semana 1

- [ ] [[Lab 01 - Crear primera instancia EC2]]
- [ ] [[Lab 02 - Configurar bucket S3 básico]]
- [ ] [[Lab 03 - Gestión básica de usuarios IAM]]

### 🧪 Laboratorios Prácticos - Semana 2

- [ ] [[Lab 04 - Configurar VPC básica con subnets]]
- [ ] [[Lab 05 - Políticas de seguridad S3]]
- [ ] [[Lab 06 - Security Groups y NACLs]]

**✅ Checkpoint Semana 2:**

- [ ] Puedo explicar la infraestructura global de AWS
- [ ] Entiendo el modelo de responsabilidad compartida
- [ ] Puedo crear y gestionar recursos básicos
- [ ] Comprendo conceptos de facturación

---

## 🏗️ Fase 2: Compute y Storage (Semanas 3-4)

**⏱️ Tiempo sugerido:** 1.5-2 horas/día

### ⚙️ Servicios de Compute

- [ ] [[Amazon EC2 Advanced - Auto Scaling y Load Balancers]]
- [ ] [[AWS Lambda - Serverless Computing]]
- [ ] [[Amazon ECS - Elastic Container Service]]
- [ ] [[AWS Elastic Beanstalk - Platform as a Service]]
- [ ] [[AWS Fargate - Serverless Containers]]

### 💾 Servicios de Storage

- [ ] [[Amazon EBS - Elastic Block Store]]
- [ ] [[Amazon EFS - Elastic File System]]
- [ ] [[AWS Storage Gateway]]
- [ ] [[Amazon S3 Advanced Features]]

### 🧪 Laboratorios Prácticos - Semana 3

- [ ] [[Lab 07 - Desplegar Spring Boot en Elastic Beanstalk]]
- [ ] [[Lab 08 - Configurar Auto Scaling Group]]
- [ ] [[Lab 09 - Crear función Lambda básica]]

### 🧪 Laboratorios Prácticos - Semana 4

- [ ] [[Lab 10 - Application Load Balancer]]
- [ ] [[Lab 11 - Contenedores con ECS]]
- [ ] [[Lab 12 - Integración Lambda con API Gateway]]

### 🔗 Conexión con Java/Spring Boot

- [ ] [[Deploying Java Apps on AWS]]
- [ ] [[Spring Boot + AWS Lambda]]
- [ ] [[Containerización con ECS]]
- [ ] [[Spring Boot + Elastic Beanstalk Best Practices]]

**✅ Checkpoint Semana 4:**

- [ ] Puedo diseñar soluciones de compute escalables
- [ ] Entiendo cuándo usar cada servicio de storage
- [ ] Puedo desplegar aplicaciones Java en AWS
- [ ] Comprendo conceptos de containerización

---

## 🗄️ Fase 3: Databases y Networking (Semanas 5-6)

**⏱️ Tiempo sugerido:** 1.5-2 horas/día

### 🗃️ Servicios de Base de Datos

- [ ] [[Amazon RDS - Relational Database Service]]
- [ ] [[Amazon DynamoDB - NoSQL Database]]
- [ ] [[Amazon ElastiCache - In-memory Caching]]
- [ ] [[Amazon Redshift - Data Warehouse]]
- [ ] [[Amazon Aurora - MySQL/PostgreSQL Compatible]]

### 🌐 Networking Avanzado

- [ ] [[VPC Advanced - NAT Gateways y VPC Endpoints]]
- [ ] [[Amazon Route 53 - DNS Service]]
- [ ] [[AWS CloudFront - CDN]]
- [ ] [[AWS Direct Connect]]
- [ ] [[VPC Peering y Transit Gateway]]

### 🧪 Laboratorios Prácticos - Semana 5

- [ ] [[Lab 13 - Conectar Java App con RDS PostgreSQL]]
- [ ] [[Lab 14 - Configurar ElastiCache para Spring Boot]]
- [ ] [[Lab 15 - DynamoDB con aplicación Java]]

### 🧪 Laboratorios Prácticas - Semana 6

- [ ] [[Lab 16 - Arquitectura Multi-AZ]]
- [ ] [[Lab 17 - CloudFront para contenido estático]]
- [ ] [[Lab 18 - Route 53 con health checks]]

**✅ Checkpoint Semana 6:**

- [ ] Puedo diseñar soluciones de base de datos apropiadas
- [ ] Entiendo networking avanzado en AWS
- [ ] Puedo implementar alta disponibilidad
- [ ] Comprendo optimización de performance

---

## 🔒 Fase 4: Security y Monitoring (Semanas 7-8)

**⏱️ Tiempo sugerido:** 1-2 horas/día

### 🛡️ Servicios de Seguridad

- [ ] [[AWS IAM Advanced - Roles, Policies, Federation]]
- [ ] [[AWS KMS - Key Management Service]]
- [ ] [[AWS Secrets Manager]]
- [ ] [[AWS WAF - Web Application Firewall]]
- [ ] [[Amazon Inspector]]
- [ ] [[AWS GuardDuty]]

### 📊 Monitoring y Logging

- [ ] [[Amazon CloudWatch - Monitoring y Logs]]
- [ ] [[AWS CloudTrail - API Logging]]
- [ ] [[AWS Config - Configuration Management]]
- [ ] [[AWS Systems Manager]]
- [ ] [[AWS X-Ray - Distributed Tracing]]

### 🧪 Laboratorios Prácticos - Semana 7

- [ ] [[Lab 19 - Monitoreo avanzado aplicación Java]]
- [ ] [[Lab 20 - Logging centralizado con CloudWatch]]
- [ ] [[Lab 21 - Gestión de secretos con Secrets Manager]]

### 🧪 Laboratorios Prácticos - Semana 8

- [ ] [[Lab 22 - Configurar alertas CloudWatch]]
- [ ] [[Lab 23 - WAF para proteger aplicación web]]
- [ ] [[Lab 24 - Compliance con AWS Config]]

**✅ Checkpoint Semana 8:**

- [ ] Puedo implementar seguridad en profundidad
- [ ] Entiendo compliance y governance
- [ ] Puedo configurar monitoreo completo
- [ ] Comprendo incident response

---

## ☁️ Fase 5: Arquitecturas y Patrones (Semanas 9-10)

**⏱️ Tiempo sugerido:** 2 horas/día

### 🏗️ Patrones Arquitectónicos

- [ ] [[3-Tier Web Architecture]]
- [ ] [[Microservices on AWS]]
- [ ] [[Event-Driven Architecture]]
- [ ] [[Disaster Recovery Patterns]]
- [ ] [[Serverless Architectures]]

### 🔗 Servicios de Integración

- [ ] [[Amazon SQS - Simple Queue Service]]
- [ ] [[Amazon SNS - Simple Notification Service]]
- [ ] [[AWS API Gateway]]
- [ ] [[AWS Step Functions]]
- [ ] [[Amazon EventBridge]]

### 💼 Casos de Uso para Backend Developer

- [ ] [[Migrating Monolith to AWS]]
- [ ] [[Implementing CI-CD with AWS]]
- [ ] [[Scaling Java Applications]]
- [ ] [[Cost Optimization Strategies]]

### 🧪 Proyectos Prácticos

- [ ] [[Proyecto 01 - Migrar aplicación monolítica]]
- [ ] [[Proyecto 02 - Implementar arquitectura de microservicios]]
- [ ] [[Proyecto 03 - Sistema de procesamiento de eventos]]

**✅ Checkpoint Semana 10:**

- [ ] Puedo diseñar arquitecturas complejas
- [ ] Entiendo trade-offs arquitectónicos
- [ ] Puedo calcular costos aproximados
- [ ] Comprendo patrones de disaster recovery

---

## 📝 Fase 6: Preparación Final (Semanas 11-12)

**⏱️ Tiempo sugerido:** 2-3 horas/día

### 📋 Exámenes de Práctica

- [ ] AWS Practice Exams (oficiales)
- [ ] Udemy Practice Tests (Stephane Maarek)
- [ ] Whizlabs Practice Tests
- [ ] Tutorials Dojo Practice Tests

### 📚 Repaso Final

- [ ] [[AWS Services Cheat Sheet]]
- [ ] [[Common Exam Scenarios]]
- [ ] [[Cost Calculation Examples]]
- [ ] [[Security Best Practices Summary]]
- [ ] [[Troubleshooting Common Issues]]

### 🎯 Resultados Simulacros

- [ ] Simulacro 1: ___% (Objetivo: >70%)
- [ ] Simulacro 2: ___% (Objetivo: >75%)
- [ ] Simulacro 3: ___% (Objetivo: >80%)
- [ ] Simulacro 4: ___% (Objetivo: >85%)

### ✅ Checklist Final Pre-Examen

- [ ] Domino los 5 pilares del Well-Architected Framework
- [ ] Puedo diseñar arquitecturas multi-tier
- [ ] Entiendo pricing y cost optimization
- [ ] Conozco límites y quotas de servicios principales
- [ ] Puedo resolver casos de troubleshooting
- [ ] Promedio >80% en exámenes de práctica
- [ ] Repasé scenarios de disaster recovery
- [ ] Tengo clara la diferencia entre servicios similares

---

## 📅 Cronograma Detallado

|Semana|Fase|Tiempo/día|Enfoque Principal|Deliverable|
|---|---|---|---|---|
|1-2|Fundamentos|1-2h|Teoría + Labs básicos|Labs 1-6 completados|
|3-4|Compute/Storage|1.5-2h|Labs prácticos|Aplicación Java desplegada|
|5-6|BD/Networking|1.5-2h|Integración con Java|Arquitectura multi-tier|
|7-8|Seguridad/Monitoreo|1-2h|Casos reales|Monitoreo completo|
|9-10|Arquitecturas|2h|Diseño de soluciones|Proyecto end-to-end|
|11-12|Preparación final|2-3h|Exámenes práctica|>85% en simulacros|

---

## 🛠️ Herramientas y Recursos

### 📚 Plataformas de Estudio

- [ ] AWS Free Tier account configurada
- [ ] Udemy/A Cloud Guru subscription activa
- [ ] AWS Documentation bookmarked
- [ ] AWS Whitepapers descargados

### 🧪 Labs y Práctica

- [ ] AWS Hands-on Labs
- [ ] Qwiklabs access
- [ ] Cloud Academy Labs
- [ ] Proyectos personales en GitHub

### 👥 Comunidad

- [ ] AWS Community Builders
- [ ] Reddit r/AWSCertifications joined
- [ ] Discord/Slack AWS groups
- [ ] LinkedIn AWS groups seguidos

---

## 🎯 Roadmap Post-Certificación

### 📈 Próximos Pasos

- [ ] [[AWS Developer Associate Preparation]]
- [ ] [[Kubernetes CKA Preparation]]
- [ ] [[Advanced AWS Architectures]]
- [ ] [[Infrastructure as Code]] (Terraform/CloudFormation)

### 💼 Aplicación Práctica

- [ ] Migrar proyecto personal a AWS
- [ ] Implementar CI/CD pipeline completo
- [ ] Documentar arquitecturas en Obsidian
- [ ] Compartir conocimiento (blog/GitHub)
- [ ] Contribuir a proyectos open source

---

## 📊 Tracking de Progreso

### 📈 Métricas Semanales

```
Semana 1: ___% completado
Semana 2: ___% completado
Semana 3: ___% completado
Semana 4: ___% completado
Semana 5: ___% completado
Semana 6: ___% completado
Semana 7: ___% completado
Semana 8: ___% completado
Semana 9: ___% completado
Semana 10: ___% completado
Semana 11: ___% completado
Semana 12: ___% completado
```

### 🎯 Objetivos Clave

- [ ] **Mes 1:** Fundamentos sólidos + primeros labs
- [ ] **Mes 2:** Servicios avanzados + integración Java
- [ ] **Mes 3:** Arquitecturas complejas + casos de uso reales
- [ ] **Meta Final:** 🏆 Certificación AWS SAA-C03

---

## 📚 Enlaces Útiles

- [AWS Certification Roadmap](https://aws.amazon.com/certification/)
- [AWS Well-Architected Tool](https://aws.amazon.com/well-architected-tool/)
- [AWS Architecture Center](https://aws.amazon.com/architecture/)
- [AWS Free Tier](https://aws.amazon.com/free/)
- [AWS Training and Certification](https://aws.amazon.com/training/)

---

> **💡 Nota:** Este plan está optimizado para desarrolladores backend con experiencia en Java/Spring Boot. Ajusta los tiempos según tu disponibilidad y ritmo de aprendizaje.

**🔄 Próxima revisión:** {{date+7d}} **📝 Estado actual:** En planificación