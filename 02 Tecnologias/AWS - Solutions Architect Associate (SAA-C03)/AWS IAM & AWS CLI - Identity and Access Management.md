
> **📂 Categoría:** Core | **🏷️ Tags:** #aws #core #iam #cli
> **📅 Creado:** 04/07/2025 | **🔄 Actualizado:** 04/07/2025  
> **📈 Nivel:** Basico | **💰 Pricing Tier:** N/A

## 📋 Descripción General

**¿Qué es?**
Es un servicio global de AWS, en donde IAM significa identidad y gestion de acceso.

**¿Para qué sirve?**  
Su función es controlar quien puede acceder a que recurso y bajo que condiciones.

**Funciones Principales**
- **Autenticación:** Verifica la identidad de usuarios y servicios
	- Gestión de credenciales (usuarios, contraseñas, claves de acceso)
	- Integración con proveedores de identidad externos (SAML, OpenID Connect)
- **Autorización:** Determinar que acciones pueden tomar los usuarios autenticados
	- Politicas granulares de permisos
	- Principio de menor privilegio
- **Gestión de identidades:** Crear y administrar diferentes tipos de identidades
	- Usuarios IAM
	- Grupos IAM
	- Roles IAM
	- Politicas IAM

**¿Dónde encaja en AWS?**
Es la base sobre la cual se construye el resto del entorno en la nube. Antes de que cualquier usuario, aplicación o servicio pueda interactuar con otros servicios AWS, primero debe de autenticarse a través de IAM.

---

## ⚙️ Cómo Funciona / Arquitectura

### 🏗️ Componentes Principales 
- **Usuarios (Users):** Representan a personas o aplicaciones que interactúan con AWS. Tienen credenciales de acceso (contraseña, claves de acceso).
- **Grupos (Groups):** Colecciones de usuarios de IAM. Permite asignar permisos a múltiples usuarios a la vez, simplificando la administración.
- **Roles (Roles):** Identidades de IAM que puedes asumir para obtener permisos temporales. Ideales para servicios de AWS, acceso entre cuentas o acceso temporal para usuarios.
- **Políticas (Policies):** Documentos JSON que definen los permisos. Se adjuntan a usuarios, grupos o roles para especificar qué acciones se permiten o deniegan en qué recursos.
* **Políticas Basadas en Identidad:** Adjuntas a usuarios, grupos o roles.
* **Políticas Basadas en Recursos:** Adjuntas directamente a un recurso (ej., un bucket S3) para controlar quién puede acceder a ese recurso.
- **Proveedores de Identidad (Identity Providers - IdP):** Permite la federación de identidades, integrando IAM con sistemas de identidad corporativos (ej., Microsoft Active Directory, Okta).

---

### 🔄 Flujo de Trabajo

```mermaid
graph TD
    A[Principal - Usuario o Servicio] --> B[Intenta acceder a un recurso AWS]
    B --> C[IAM evalua la solicitud]
    C --> D[Autenticacion - Quien eres]
    D --> E[Autorizacion - Que puedes hacer]
    E --> F[Evalua politicas de permisos adjuntas]
    F --> G[Evalua politicas de confianza - si es un rol]
    G --> H[Evalua politicas de limite - si existen]
    H --> I{La solicitud esta permitida}
    I --|Si|--> J[Acceso permitido al recurso AWS]
    I --|No|--> K[Acceso denegado]

```
---

## 🎛️ Configuraciones Clave

| **Parámetro** | **Descripción**                            | **Valores**                           | **Notas**                                                    |
| ------------- | ------------------------------------------ | ------------------------------------- | ------------------------------------------------------------ |
| Usuario IAM   | Identidad para personas/aplicaciones       | Nombre de usuario, credenciales       | Puede tener claves de acceso y contraseña                    |
| Grupo IAM     | Colección de usuarios                      | Nombre del grupo                      | Simplifica la gestión de permisos para múltiples usuarios    |
| Rol IAM       | Identidad asumible con permisos temporales | Nombre del rol, política de confianza | Ideal para servicios AWS y acceso entre cuentas              |
| Política IAM  | Documento JSON de permisos                 | Allow/Deny, Action, Resource          | Define qué acciones se permiten/deniegan en qué recursos     |
| MFA           | Autenticación Multifactor                  | Activado/Desactivado                  | Capa adicional de seguridad para usuarios IAM y usuario root |

--- 

## 🎯 Casos de Uso / Cuándo Usarlo

### ✅ Ideal Para:
- **Control de Acceso Granular:** Definir permisos específicos para usuarios y servicios
- **Delegación Segura:** Permitir que otros servicios de AWS (ej., EC2, Lambda) interactúen con otros servicios (ej., S3, DynamoDB) de forma segura
- **Acceso entre Cuentas:** Conceder acceso seguro a recursos en una cuenta AWS desde otra cuenta
- **Federación de identidades:** Integrar sistemas de identidad corporativos (ej., Active Directory) con AWS
- **Auditoria de accesos:** Registrar y monitorear quién puede acceder a qué recursos y cuándo (con CloudTrail)

### ❌ No Recomendado Para:
- **Compartir Credenciales Root:** Nunca se debe de compartir las credenciales de la cuenta root de AWS
- **Permisos Excesivos:** Otorgar permisos más amplios de los necesarios (violación del principio de privilegio mínimo)
- **Credenciales Permanentes para Servicios:** Usar claves de acceso de usuarios IAM directamente en aplicaciones en lugar de roles

### 🏢 Ejemplos del Mundo Real
1. **Desarrollo de Aplicaciones:** Un rol de IAM asignado a una instancia de EC2 que permite a la aplicación leer y escribir en un bucket de S3 especifico para almacenar imágenes
2. **Administrador de Bases de Datos:** Un usuario de IAM con una política que le permite gestionar bases de datos en Amazon RDS, pero sin acceso a recursos de red o de computo
3. **Auditor Externo:** Un rol de IAM temporal que un auditor externo puede asumir para acceder a registros de CloudTrail y métricas de CloudWatch en tu cuenta, sin acceso a datos sensibles

--- 

## ⚖️ Pros y Contras

### ✅ Ventajas

- **Seguridad Mejorada:** Implementa el principio de privilegio minimo, reduciendo la superficie de ataque
- **Flexibilidad:** Permite definir permisos muy granulares y complejos
- **Gratuito:** El servicio IAM no tiene costo adicional
- **Escalabilidad:** Fácil de gestionar identidades y accesos a medida que tu infraestructura crece
- **Integración Completa:** Se integra con todos los servicios de AWS y con proveedores de identidad externos

### ❌ Desventajas

- **Complejidad Inicial:** Puede ser abrumador para principiantes debido a la granularidad de las políticas
- **Costos Opcionales:** Características avanzadas como IAM Access Analyzer tienen costos asociados
- **Gestión de Políticas:** Mantener políticas claras y actualizadas puede ser un desafío en entornos grandes
- **Riesgo de Mala Configuración:** Una configuración incorrecta puede llevar a brechas de seguridad o a denegación de servicios


---

## 💰 Modelo de Precios

### 💳 Cómo se Cobra
- **Modelo:** AWS IAM es un servicio gratuito. No se cobra por crear usuarios, grupos, roles o políticas.
- **Free Tier:** Incluido como parte de la cuenta de AWS sin costo directo.
- **Factores de Costo:**  
  Los únicos costos asociados pueden provenir del uso de características avanzadas como **AWS IAM Access Analyzer**, que se cobra por la cantidad de recursos o identidades analizadas.

---

### 📊 Estimación de Costos

| Servicio                            | Costo estimado                               |
|-------------------------------------|----------------------------------------------|
| IAM (básico)                        | $0.00 / mes                                   |
| IAM Access Analyzer (ejemplo)       |                                              |
| - Análisis de recursos              | $9.00 / recurso analizado / mes / analizador |
| - Análisis de acceso no utilizado   | $0.20 / rol o usuario analizado / mes        |
| - Verificaciones de políticas       | $0.0020 / llamada a la API                   |

---

### 💡 Tips de Optimización

- 🔧 **Tip 1:** Utiliza el principio de **privilegio mínimo** para evitar permisos excesivos, lo que también puede reducir la superficie de ataque.
- 📉 **Tip 2:** Revisa regularmente las **políticas y los roles** para eliminar permisos innecesarios o no utilizados.
- 📊 **Tip 3:** Aprovecha **IAM Access Analyzer** para identificar accesos no deseados o permisos excesivos, invirtiendo en seguridad.

---
## 🧚 Configuración Práctica

### 🚀 Setup Básico

```bash
# Crear un nuevo usuario IAM
aws iam create-user --user-name mi-usuario-de-ejemplo

# Crear un nuevo grupo IAM
aws iam create-group --group-name mi-grupo-de-desarrolladores

# Adjuntar una política gestionada a un usuario (ej. AmazonS3ReadOnlyAccess)
aws iam attach-user-policy --user-name mi-usuario-de-ejemplo --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess

# Crear un rol IAM para una instancia EC2
aws iam create-role --role-name mi-ec2-role --assume-role-policy-document file://trust-policy-ec2.json
```

**Contenido de `trust-policy-ec2.json`:**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": { "Service": "ec2.amazonaws.com" },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

---

### ⚙️ Configuración Avanzada

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::mi-bucket-de-aplicacion/*",
      "Condition": {
        "StringEquals": {
          "s3:x-amz-acl": "public-read"
        }
      }
    }
  ]
}
```

> Esta política permite leer y escribir objetos en un bucket específico, pero solo si el objeto se sube con el ACL `public-read`.

---

### 🐍 Código Python/Boto3

```python
import boto3
import json

# Cliente IAM
iam = boto3.client('iam')

# Listar usuarios IAM
response = iam.list_users()
print("Usuarios IAM:")
for user in response['Users']:
    print(f"- {user['UserName']}")

# Crear una política personalizada
policy_document = {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:ListAllMyBuckets",
            "Resource": "*"
        }
    ]
}

response = iam.create_policy(
    PolicyName='MiPoliticaDeEjemploS3List',
    PolicyDocument=json.dumps(policy_document)
)

print(f"Política creada: {response['Policy']['Arn']}")
```

---

### ☕ Integración con Java/Spring Boot

```java
import com.amazonaws.auth.STSAssumeRoleSessionCredentialsProvider;
import com.amazonaws.services.s3.AmazonS3ClientBuilder;
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.regions.Regions;

// Ejemplo de cómo asumir un rol y usar sus credenciales
public class S3AccessWithRole {
    public static void main(String[] args) {
        String roleArn = "arn:aws:iam::123456789012:role/MiAplicacionS3Role"; // Reemplaza con tu ARN de rol
        String roleSessionName = "S3AccessSession";

        STSAssumeRoleSessionCredentialsProvider credentialsProvider =
            new STSAssumeRoleSessionCredentialsProvider.Builder(roleArn, roleSessionName).build();

        AmazonS3 s3Client = AmazonS3ClientBuilder.standard()
            .withCredentials(credentialsProvider)
            .withRegion(Regions.US_EAST_1)
            .build();

        // Ahora puedes usar s3Client para interactuar con S3 con los permisos del rol
        System.out.println("Listando buckets con el rol asumido:");
        s3Client.listBuckets().forEach(bucket -> System.out.println(bucket.getName()));

        // Cierra el proveedor de credenciales cuando ya no lo necesites
        credentialsProvider.close();
    }
}
```

---

### 🔒 Seguridad y Mejores Prácticas

#### 🏡 Consideraciones de Seguridad

- **Principio del Privilegio Mínimo:** Concede solo los permisos necesarios.
- **MFA para Todos:** Habilita MFA para todos los usuarios, especialmente el root.
- **Roles sobre Usuarios:** Usa roles en lugar de claves de acceso permanentes.
- **Rotación de Credenciales:** Cambia periódicamente las claves.
- **AWS CloudTrail:** Audita todas las acciones, incluidas las de IAM.
- **IAM Access Analyzer:** Detecta accesos no deseados o excesivos.

#### ✅ Best Practices

- 📋 No uses el usuario root. Protege con MFA.
- 🔧 Usa grupos para simplificar permisos.
- 📊 Usa roles para servicios.
- 📝 Utiliza políticas gestionadas por el cliente.

#### ⚠️ Errores Comunes

- ❌ Otorgar `*` (todos los permisos).
    - ✅ Solución: Especifica acciones y recursos.
- ❌ Compartir claves de acceso.
    - ✅ Solución: Usa roles.
- ❌ No usar MFA.
    - ✅ Solución: Habilita MFA.

---

### 📊 Monitoring y Troubleshooting

#### 📈 Métricas Clave (CloudWatch)

- **IAM Credentials:** Uso de credenciales.
- **MFA Usage:** Seguimiento del uso de MFA.
- **CloudTrail Events:** Registro de llamadas a la API de IAM.

#### 🚨 Alertas Recomendadas (YAML)

```yaml
IAMRootLoginAlert:
  Metric: AWS/CloudTrail
  MetricName: ConsoleLogin
  Dimensions:
    - Name: "EventType"
      Value: "AwsConsoleSignIn"
    - Name: "UserType"
      Value: "Root"
  Threshold: 1
  ComparisonOperator: GreaterThanOrEqualToThreshold
  EvaluationPeriods: 1
  Period: 300
  Statistic: Sum
  Action: SNS notification

IAMFailedLoginAttempts:
  Metric: AWS/CloudTrail
  MetricName: ConsoleLogin
  Dimensions:
    - Name: "EventType"
      Value: "AwsConsoleSignIn"
    - Name: "LoginStatus"
      Value: "Failed"
  Threshold: 5
  ComparisonOperator: GreaterThanOrEqualToThreshold
  EvaluationPeriods: 1
  Period: 300
  Statistic: Sum
  Action: SNS notification
```

#### 🔍 Troubleshooting Common Issues

|Problema|Síntomas|Solución|
|---|---|---|
|Acceso Denegado|Errores de "Access Denied"|Revisa las políticas con el Simulador de Políticas de IAM|
|Rol no asumible|Error al intentar asumir un rol|Verifica la política de confianza del rol|
|Claves de acceso perdidas|No se puede acceder programáticamente|Genera nuevas claves y elimina las antiguas|

--- 

### 🧪 Hands-on Labs

- [[01 - Gestión de Identidades y Acceso]]

---

## 📝 Mis Notas y Experiencias