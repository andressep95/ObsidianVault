## 🎯 Objetivos del Laboratorio

- Comprender los componentes fundamentales de AWS IAM
- Implementar usuarios, grupos y roles con Terraform
- Configurar políticas de acceso granulares
- Aplicar el principio de menor privilegio
- Implementar federación de identidades básica
- Gestionar credenciales de forma segura

---

## 🏗️ Arquitectura

```
┌─────────────────────────────────────────────────────────────┐
│                    AWS IAM Architecture                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   Users     │    │   Groups    │    │    Roles    │     │
│  │             │    │             │    │             │     │
│  │ • dev-user  │────│ • developers│    │ • ec2-s3    │     │
│  │ • admin-user│    │ • admins    │    │ • lambda-   │     │
│  │ • audit-user│    │ • auditors  │    │   execution │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         │                   │                   │          │
│         └───────────────────┼───────────────────┘          │
│                             │                              │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                   Policies                              │ │
│  │  • S3ReadOnlyAccess    • EC2FullAccess                  │ │
│  │  • DynamoDBReadWrite   • CloudWatchReadOnly             │ │
│  │  • CustomDeveloperPolicy                                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 AWS Resources                           │ │
│  │  S3 → EC2 → DynamoDB → Lambda → CloudWatch             │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

---

## 📁 Estructura de Archivos

```
labs/phase-1-fundamentals/lab-02-iam-fundamentals/
├── 📄 main.tf                 # Configuración principal
├── 📄 variables.tf            # Variables de entrada
├── 📄 terraform.tfvars        # Valores específicos del lab
├── 📄 outputs.tf              # Información de salida
├── 📄 versions.tf             # Versiones de providers
├── 📄 data.tf                 # Data sources
├── 📄 locals.tf               # Variables locales
├── 📄 iam-users.tf            # Definición de usuarios IAM
├── 📄 iam-groups.tf           # Definición de grupos IAM
├── 📄 iam-roles.tf            # Definición de roles IAM
├── 📄 iam-policies.tf         # Políticas personalizadas
├── 📄 iam-policy-attachments.tf # Asociaciones de políticas
└── 📄 README.md               # Documentación del laboratorio
```

### lab-02-iam-fundamentals

- [[main.tf]] - Configuración principal y providers
- [[versions.tf]] - Versiones de Terraform y providers
- [[variables.tf]] - Variables de entrada
- [[terraform.tfvars]] - Valores de variables
- [[locals.tf]] - Variables locales y tags
- [[data.tf]] - Data sources para políticas AWS
- [[outputs.tf]] - Outputs del laboratorio
- [[iam-users.tf]] - Usuarios IAM
- [[iam-groups.tf]] - Grupos IAM
- [[iam-roles.tf]] - Roles IAM
- [[iam-policies.tf]] - Políticas personalizadas
- [[iam-policy-attachments.tf]] - Asociaciones de políticas

---

## 📋 Prerrequisitos

- [x] AWS CLI configurado (`aws configure`)
- [x] Terraform >= 1.0 instalado
- [x] Credenciales AWS válidas con permisos IAM
- [x] Permisos para crear usuarios, grupos, roles y políticas IAM
- [x] Acceso a AWS Management Console (opcional, para verificación)

---

## 🚀 Ejecución del Laboratorio

### 1. Configuración Inicial

```bash
# Clonar y navegar al laboratorio
cd labs/phase-1-fundamentals/lab-02-iam-fundamentals/

# Verificar configuración AWS y permisos
aws sts get-caller-identity
aws iam get-account-summary

# Inicializar Terraform
terraform init
```

### 2. Planificación

```bash
# Ver el plan de ejecución
terraform plan

# Revisar creación de recursos IAM
terraform plan -var="environment=dev" -var="company_name=mycompany"

# Validar configuración
terraform validate
```

### 3. Aplicación

```bash
# Aplicar configuración
terraform apply

# Confirmar con 'yes' cuando se solicite
```

### 4. Exploración de Resultados

```bash
# Ver información de usuarios creados
terraform output iam_users_info

# Ver información de grupos
terraform output iam_groups_info

# Ver información de roles
terraform output iam_roles_info

# Ver resumen completo del laboratorio
terraform output lab_summary

# Probar acceso con usuario específico
aws sts get-caller-identity --profile dev-user
```

### 5. Verificación Manual (Opcional)

```bash
# Listar usuarios IAM
aws iam list-users

# Verificar políticas de un usuario
aws iam list-attached-user-policies --user-name dev-user-mycompany

# Listar roles IAM
aws iam list-roles --query 'Roles[?contains(RoleName, `mycompany`)]'
```

### 6. Limpieza

```bash
# Destruir recursos para evitar costos
terraform destroy

# Confirmar con 'yes'
```

---

## 📊 Conceptos Clave Aprendidos

### 🔐 **Componentes IAM Fundamentales**

- **Usuarios**: Identidades permanentes para personas o aplicaciones
- **Grupos**: Colecciones de usuarios con permisos similares
- **Roles**: Identidades temporales que pueden ser asumidas
- **Políticas**: Documentos JSON que definen permisos

### 🛡️ **Tipos de Políticas**

- **Políticas Administradas por AWS**: Predefinidas por AWS
- **Políticas Administradas por Cliente**: Creadas y gestionadas por el usuario
- **Políticas Inline**: Asociadas directamente a un usuario, grupo o rol

### 🎯 **Principios de Seguridad**

- **Principio de Menor Privilegio**: Otorgar solo permisos mínimos necesarios
- **Separación de Responsabilidades**: Diferentes roles para diferentes funciones
- **Rotación de Credenciales**: Cambio periódico de claves de acceso

### 🔄 **Terraform IAM Resources**

- `aws_iam_user`: Creación de usuarios IAM
- `aws_iam_group`: Creación de grupos IAM
- `aws_iam_role`: Creación de roles IAM
- `aws_iam_policy`: Creación de políticas personalizadas
- `aws_iam_policy_attachment`: Asociación de políticas

---

## 🎯 Preguntas de Preparación para el Examen

### 1. **¿Cuál es la diferencia entre un usuario IAM y un rol IAM?**

- **Usuario**: Identidad permanente con credenciales de larga duración
- **Rol**: Identidad temporal que se asume con credenciales temporales

### 2. **¿Qué sucede cuando hay conflicto entre una política que permite y otra que niega?**

- La denegación explícita siempre tiene prioridad (Explicit Deny)
- Principio: "Deny overrides Allow"

### 3. **¿Cuál es la ventaja de usar roles IAM en lugar de usuarios para aplicaciones?**

- No requieren credenciales hardcodeadas
- Credenciales temporales y rotación automática
- Mejor seguridad y cumplimiento de mejores prácticas

### 4. **¿Cómo implementa AWS el principio de menor privilegio?**

- Denegación por defecto (Implicit Deny)
- Permisos granulares a nivel de acción y recurso
- Posibilidad de usar condiciones en políticas

### 5. **¿Qué es el boundary de permisos en IAM?**

- Límite máximo de permisos que puede tener una identidad
- No otorga permisos, solo los limita
- Útil para delegación segura de administración

---

## 💡 Casos de Uso Implementados

### 👨‍💻 **Desarrolladores**

- Acceso completo a servicios de desarrollo (S3, Lambda, DynamoDB)
- Acceso de solo lectura a CloudWatch para monitoreo
- Sin acceso a facturación o configuración de cuenta

### 🔧 **Administradores**

- Acceso completo a todos los servicios AWS
- Capacidad de gestionar usuarios y políticas IAM
- Acceso a facturación y configuración de cuenta

### 📊 **Auditores**

- Acceso de solo lectura a logs y configuraciones
- Acceso a CloudTrail para auditoría
- Acceso a informes de cumplimiento

### 🤖 **Aplicaciones (Roles)**

- Rol para instancias EC2 con acceso a S3
- Rol para funciones Lambda con acceso a DynamoDB
- Rol para servicios de monitoreo con acceso a CloudWatch

---

## 💰 Estimación de Costos

- **Usuarios IAM**: Gratis
- **Grupos IAM**: Gratis
- **Roles IAM**: Gratis
- **Políticas IAM**: Gratis
- **Claves de Acceso**: Gratis
- **Total Estimado**: $0.00

> **Nota**: IAM es un servicio gratuito de AWS. Solo se cobran los recursos que estos usuarios/roles accedan.

---

## 🔗 Enlaces Útiles

- [AWS IAM Documentation](https://docs.aws.amazon.com/iam/)
- [AWS IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Terraform AWS IAM Resources](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user)
- [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html)
- [AWS IAM Security Audit](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_getting-report.html)

---

## 🏆 Mejores Prácticas Implementadas

### 🔐 **Seguridad**

- Uso de tags consistentes para identificación
- Implementación de políticas granulares
- Separación de responsabilidades por grupos
- Documentación de permisos en código

### 🛠️ **Terraform**

- Uso de variables para reutilización
- Separación de recursos en archivos lógicos
- Outputs informativos para verificación
- Versionado de providers

### 📋 **Operaciones**

- Naming conventions consistentes
- Descripción clara de políticas y roles
- Estructura modular para mantenimiento
- Documentación completa

---

## ⚠️ Importante:

- Siempre ejecuta `terraform destroy` al finalizar para limpiar recursos
- Nunca hardcodees credenciales en el código
- Revisa periódicamente los permisos otorgados
- Mantén un inventario de usuarios y roles activos