
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

# 🎛️ Configuraciones Clave

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
3. 