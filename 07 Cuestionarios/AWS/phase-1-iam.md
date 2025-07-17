### Conceptos Clave de AWS IAM y STS para Arquitectos de Soluciones

#### Fundamentos de IAM

1. **¿Qué es AWS Identity and Access Management (IAM)?**: Un servicio web que le permite controlar de forma segura el acceso a los recursos de AWS y a su cuenta. No tiene costo usar IAM.

2. **Beneficios de Usar IAM**: Permite **conceder acceso compartido** a su cuenta de AWS, asignar **permisos granulares** para controlar acciones en recursos específicos, y ofrece funciones de seguridad como **MFA** e **identidad federada**, además de integrarse con **AWS CloudTrail** para auditoría y cumplimiento.

3. **Cómo Funciona IAM (Flujo de Solicitud)**: IAM autentica un *principal* (identidad) usando sus credenciales. Luego, evalúa el contexto de la solicitud (incluyendo acciones, recursos, principal y datos del entorno) con las políticas de permisos para autorizar el acceso.

4. **Consistencia Eventual de IAM**: IAM es un servicio de consistencia eventual, lo que significa que los cambios (como crear o actualizar usuarios, grupos, roles o políticas) pueden tardar algún tiempo en replicarse globalmente. Se recomienda no incluir cambios de IAM en rutas críticas de código de alta disponibilidad.

  

#### Identidades y Credenciales

5. **Principales (Principals)**: Una entidad en AWS (usuario raíz, usuario de IAM, rol de IAM) que puede realizar una solicitud para una acción u operación sobre un recurso. Incluyen usuarios humanos, cargas de trabajo y principales federados.

6. **Usuario Raíz de la Cuenta de AWS (Root User)**: La identidad de inicio de sesión inicial con **acceso completo** a todos los servicios y recursos de AWS en la cuenta. Se recomienda usarlo solo para tareas que lo requieran y protegerlo con **MFA** y no crear claves de acceso para él.

7. **Usuarios de IAM (IAM Users)**: Representan personas o aplicaciones. Tienen **credenciales de larga duración** (claves de acceso, contraseñas de consola, claves SSH, certificados de servidor). **Mejor práctica**: Se recomienda usar **identidades federadas** o **roles de IAM** para usuarios humanos en lugar de usuarios de IAM con credenciales de larga duración.

8. **Grupos de Usuarios de IAM (IAM User Groups)**: Colecciones de usuarios de IAM a los que se pueden adjuntar políticas para administrar permisos de manera más sencilla. No pueden anidarse ni contener otros grupos.

9. **Roles de IAM (IAM Roles)**: Una identidad de IAM con permisos específicos que, a diferencia de los usuarios, no está asociada de forma única a una persona, sino que **está diseñada para ser asumida temporalmente**. Son fundamentales para otorgar **credenciales temporales**.

10. **Credenciales Temporales de Seguridad**: Proporcionadas por AWS STS, son la mejor práctica para acceder a AWS en la mayoría de los escenarios. Son de corta duración y no requieren distribución de credenciales de larga duración.

11. **Comparación de Credenciales STS**: AWS STS ofrece operaciones API como **AssumeRole**, **GetFederationToken** y **GetSessionToken** para obtener credenciales temporales, cada una con características y casos de uso específicos.

  

#### Políticas y Permisos

12. **Políticas (Policies)**: Documentos JSON en AWS que, al adjuntarse a una identidad o recurso, definen sus permisos. Determinan si una solicitud es permitida o denegada.

13. **Elementos de una Política JSON**:

* **Version**: La versión del lenguaje de la política (se recomienda '2012-10-17').

* **Statement**: Un contenedor para la información de un permiso.

* **Sid (Opcional)**: Un ID de declaración para diferenciar entre declaraciones.

* **Effect**: `Allow` o `Deny` para indicar si la política permite o deniega el acceso.

* **Principal (en políticas basadas en recursos)**: La cuenta, usuario, rol o principal federado al que se le permite o deniega el acceso.

* **Action**: Una lista de acciones permitidas o denegadas.

* **Resource**: Una lista de recursos a los que se aplican las acciones.

* **Condition (Opcional)**: Especifica circunstancias bajo las cuales la política otorga permiso (ej., `aws:MultiFactorAuthPresent`).

14. **Tipos de Políticas**:

* **Políticas Gestionadas por AWS (AWS Managed Policies)**: Creadas y administradas por AWS, tienen su propio ARN y son reutilizables.

* **Políticas Gestionadas por el Cliente (Customer Managed Policies)**: Creadas y administradas por el usuario, también tienen su propio ARN y son reutilizables.

* **Políticas en Línea (Inline Policies)**: Incrustadas directamente en una identidad de IAM, no reutilizables.

15. **Mínimo Privilegio (Least Privilege)**: Una mejor práctica de seguridad que consiste en conceder solo los permisos requeridos para realizar una tarea y ninguna otra permiso adicional.

16. **Límites de Permisos (Permissions Boundaries)**: Una característica avanzada que establece los **permisos máximos** que una política basada en identidad puede otorgar a una entidad de IAM. Las acciones deben ser permitidas tanto por la política basada en identidad como por el límite de permisos.

17. **Políticas Basadas en Recursos (Resource-based Policies)**: Se adjuntan directamente a un recurso (ej., buckets de S3, temas de SNS, colas de SQS) y especifican quién puede acceder a ese recurso y qué acciones pueden realizar.

18. **Listas de Control de Acceso (ACLs)**: Políticas de servicio que controlan qué principales de otra cuenta pueden acceder a un recurso. Son similares a las políticas basadas en recursos pero no usan formato JSON.

  

#### Seguridad y Mejores Prácticas

19. **Requerir MFA**: Se recomienda encarecidamente habilitar MFA para el usuario raíz y los usuarios de IAM para una seguridad adicional.

20. **Proteger las Credenciales del Usuario Raíz**: El usuario raíz tiene acceso ilimitado; sus credenciales deben protegerse al máximo, no compartirse y usar MFA.

21. **No Crear Claves de Acceso para el Usuario Raíz**: Se desaconseja la creación de claves de acceso para el usuario raíz debido a su naturaleza de larga duración y el riesgo de seguridad que representan.

22. **Usar Credenciales Temporales para Usuarios Humanos y Cargas de Trabajo**: Es una mejor práctica requerir que los usuarios humanos accedan a AWS mediante federación con un proveedor de identidad para usar credenciales temporales, y que las cargas de trabajo usen roles de IAM para obtener credenciales temporales.

23. **Actualizar Claves de Acceso cuando sea Necesario**: Para casos de uso que requieran credenciales de larga duración (usuarios de IAM con acceso programático), se recomienda actualizar las claves de acceso regularmente.

24. **Revisar y Eliminar Periódicamente Recursos No Utilizados**: Auditar y eliminar regularmente usuarios, roles, permisos, políticas y credenciales que ya no se utilizan es una mejor práctica de seguridad.

25. **Uso de Condiciones en Políticas de IAM**: Utilizar el elemento `Condition` en las políticas de IAM para restringir aún más el acceso, por ejemplo, basándose en la dirección IP de origen (`aws:SourceIp`) o la presencia de MFA (`aws:MultiFactorAuthPresent`).

26. **IAM Access Analyzer**: Un servicio que ayuda a identificar recursos compartidos externamente, acceso interno a recursos críticos, acceso no utilizado, y a validar políticas según las mejores prácticas y estándares de seguridad de AWS.

27. **Generación de Políticas con IAM Access Analyzer**: Una funcionalidad que utiliza la información del historial de acceso de CloudTrail para generar plantillas de políticas con el mínimo privilegio requerido, lo que facilita la creación de políticas ajustadas.

28. **Perímetro de Datos (Data Perimeters)**: Un conjunto de controles de acceso preventivos que ayudan a asegurar que las identidades solo puedan acceder a recursos confiables y desde redes esperadas. Implican el uso de **Políticas de Control de Servicios (SCPs)** y **Políticas de Endpoint de VPC** con claves de condición globales.

29. **Problema del "Confused Deputy"**: Un riesgo de seguridad en el que una entidad menos privilegiada puede usar los permisos de una entidad más privilegiada para realizar acciones. Se mitiga mediante claves de condición como `sts:ExternalId`, `aws:SourceArn`, `aws:SourceAccount`, `aws:SourceOrgID` en las políticas de confianza de los roles.

30. **Source Identity**: Un atributo opcional que se puede establecer al asumir un rol para rastrear la identidad original del solicitante durante una sesión de rol, lo que mejora la auditabilidad y el control de acceso granular.

  

#### Federación e Integraciones

31. **Federación de Identidades (Identity Federation)**: Permite que usuarios externos (administrados fuera de AWS) accedan a recursos de AWS sin necesidad de crearles usuarios de IAM, utilizando sus credenciales existentes de un IdP.

32. **AWS IAM Identity Center**: El servicio recomendado para la gestión centralizada de acceso de **usuarios humanos** a múltiples cuentas de AWS y aplicaciones de negocio, que proporciona SSO protegido por MFA y credenciales temporales.

33. **Federación SAML 2.0 (Security Assertion Markup Language)**: Permite la federación de identidades utilizando un estándar abierto que muchos proveedores de identidad utilizan para el inicio de sesión único (SSO) en la Consola de AWS o para llamar a operaciones de API.

34. **Federación OpenID Connect (OIDC)**: Permite la federación de identidades utilizando proveedores OIDC compatibles (ej., Google, Facebook, Login with Amazon) para aplicaciones móviles y web, obteniendo credenciales temporales.

35. **Amazon Cognito Identity Pools**: Recomendado para desarrolladores que desean autenticar y autorizar usuarios en sus aplicaciones móviles y web, proporcionando credenciales de IAM para acceso a recursos protegidos.

36. **External ID en AssumeRole**: Un valor opcional que debe ser utilizado cuando se delega acceso a cuentas de terceros (que no se controlan directamente) para protegerse contra el problema del "confused deputy".

37. **Tags de Sesión (Session Tags)**: Atributos personalizados que se pueden pasar a AWS STS al asumir un rol o federar un usuario. Persisten durante la sesión y pueden usarse para control de acceso basado en atributos (ABAC).

  

#### Atributos y Controles de Acceso Avanzados

38. **Control de Acceso Basado en Atributos (ABAC)**: Una estrategia de autorización que define permisos basados en atributos (tags) en lugar de listar explícitamente recursos o acciones. Permite una mayor escalabilidad y flexibilidad en la gestión de permisos.

39. **Comparación ABAC vs. RBAC Tradicional**: ABAC es más flexible y escalable que el modelo tradicional de control de acceso basado en roles (RBAC) porque permite el crecimiento de equipos y recursos con menos cambios en las políticas de AWS.

40. **Claves de Condición de Tags**: Las políticas de ABAC utilizan claves de condición de tags (ej., `aws:ResourceTag/tag-key`, `aws:PrincipalTag/tag-key`, `aws:RequestTag/tag-key`) para conceder permisos basados en la coincidencia de tags entre el principal y el recurso.

41. **Claves de Condición Globales de AWS**: Atributos de contexto que AWS genera sobre la solicitud, el principal o el recurso, y que se pueden usar en el elemento `Condition` de una política (ej. `aws:CurrentTime`, `aws:SourceIp`, `aws:MultiFactorAuthPresent`, `aws:PrincipalOrgID`, `aws:ResourceOrgID`).

42. **`aws:SourceIdentity` en Políticas**: Permite denegar el acceso a una sesión de rol específica asociada con una identidad de origen. Puede usarse en políticas basadas en identidad o en recursos.

43. **`aws:userId` en Políticas**: Permite denegar el acceso a sesiones temporales de credenciales asociadas con un usuario o rol de IAM específico o con un usuario federado de AWS STS.

44. **Pasar Roles a Servicios (iam:PassRole)**: Una acción de IAM específica que es necesaria para permitir que un usuario o servicio pase un rol a otro servicio de AWS para que ese servicio pueda asumir el rol en su nombre.

  

#### Gestión y Operaciones

45. **Reportes de Credenciales (Credential Reports)**: Permiten generar y descargar un informe que lista todos los usuarios de IAM en su cuenta y el estado de sus credenciales (contraseñas, claves de acceso, dispositivos MFA), útil para auditoría y cumplimiento.

46. **Información de Último Acceso (Last Accessed Information)**: IAM puede proporcionar información sobre cuándo se accedió por última vez a un servicio, acción o recurso, lo que ayuda a refinar los permisos al principio del mínimo privilegio.

47. **Gestión de Certificados de Servidor en IAM**: Aunque se recomienda AWS Certificate Manager (ACM) para la mayoría de las regiones, IAM puede gestionar certificados SSL/TLS en regiones no compatibles con ACM.

48. **Credenciales Específicas del Servicio**: Mecanismos de autenticación personalizados para servicios específicos de AWS, como claves API para Amazon Bedrock o credenciales Git para CodeCommit, diseñados para un uso específico.

49. **Quotas de IAM y AWS STS**: Existen límites en el número de recursos de IAM (usuarios, grupos, roles, políticas, etc.) y en el tamaño de las políticas o tags de sesión.

50. **Puntos de Conexión Regionales de AWS STS**: Se recomienda usar los puntos de conexión regionales de AWS STS en lugar del global para reducir la latencia, aumentar la redundancia y mejorar el rendimiento de las llamadas a la API.


Esta lista proporciona una base sólida de los principios y funcionalidades de IAM y STS que son esenciales para un arquitecto de soluciones en AWS.

---

# AWS Solutions Architect - IAM Exam Questions
## 50 Preguntas de Certificación AWS Solutions Architect - IAM  

### Nivel Básico (Preguntas 1-15)
  

**1. ¿Qué es AWS Identity and Access Management (IAM)?**

- [ ] A) Un servicio de base de datos

- [x] B) Un servicio de gestión de identidades y acceso

- [ ] C) Un servicio de almacenamiento

- [ ] D) Un servicio de redes

  

**2. ¿Cuál es el principio de menor privilegio en IAM?**

- [ ] A) Dar todos los permisos a todos los usuarios

- [x] B) Dar solo los permisos mínimos necesarios para realizar una tarea

- [ ] C) No dar permisos a ningún usuario

- [ ] D) Dar permisos solo a administradores

  

**3. ¿Qué elemento de IAM representa a una persona o aplicación?**

- [ ] A) Policy

- [ ] B) Role

- [x] C) User

- [ ] D) Group

  

**4. ¿Cuál es el formato estándar para las políticas de IAM?**

- [ ] A) XML

- [ ] B) YAML

- [x] C) JSON

- [ ] D) HTML

  

**5. ¿Qué significa el efecto "Deny" en una política de IAM?**

- [ ] A) Permite acceso condicional

- [ ] B) Permite acceso completo

- [x] C) Deniega explícitamente el acceso

- [ ] D) No tiene efecto

  

**6. ¿Cuál es la diferencia principal entre un User y un Role en IAM?**

- [ ] A) No hay diferencia

- [x] B) Un User es permanente, un Role es temporal

- [ ] C) Un User es temporal, un Role es permanente

- [ ] D) Ambos son idénticos

  

**7. ¿Qué es un Group en IAM?**

- [ ] A) Una colección de policies

- [x] B) Una colección de users

- [ ] C) Una colección de roles

- [ ] D) Una colección de recursos

  

**8. ¿Cuál es el usuario raíz (root) en una cuenta AWS?**

- [ ] A) Un usuario normal

- [x] B) El primer usuario creado con acceso completo

- [ ] C) Un usuario sin permisos

- [ ] D) Un usuario temporal

  

**9. ¿Qué es una Access Key en IAM?**

- [ ] A) Una contraseña

- [ ] B) Un certificado

- [x] C) Un par de claves para acceso programático

- [ ] D) Un token temporal

  

**10. ¿Cuál es la práctica recomendada para el usuario root?**

- [ ] A) Usarlo para tareas diarias

- [ ] B) Compartir sus credenciales

- [x] C) Configurar MFA y usarlo solo para tareas administrativas críticas

- [ ] D) Eliminar la cuenta

  

**11. ¿Qué es MFA (Multi-Factor Authentication)?**

- [ ] A) Múltiples contraseñas

- [x] B) Autenticación de dos o más factores

- [ ] C) Múltiples usuarios

- [ ] D) Múltiples cuentas

  

**12. ¿Cuál es el límite predeterminado de usuarios IAM por cuenta?**

- [ ] A) 100

- [ ] B) 1000

- [x] C) 5000

- [ ] D) 10000

  

**13. ¿Qué tipo de política se adjunta directamente a un usuario?**

- [ ] A) Resource-based policy

- [x] B) Identity-based policy

- [ ] C) Trust policy

- [ ] D) Bucket policy

  

**14. ¿Cuál es el ARN (Amazon Resource Name) típico para un usuario IAM?**

- [x] A) arn:aws:iam::account-id:user/username

- [ ] B) arn:aws:s3:::bucket-name

- [ ] C) arn:aws:ec2:region:account-id:instance/instance-id

- [ ] D) arn:aws:lambda:region:account-id:function:function-name

  

**15. ¿Qué sucede cuando un usuario nuevo es creado en IAM?**

- [ ] A) Obtiene permisos de administrador

- [ ] B) Obtiene permisos de solo lectura

- [x] C) No tiene permisos por defecto

- [ ] D) Obtiene permisos básicos

  

### Nivel Intermedio (Preguntas 16-35)


**16. Una empresa necesita que sus desarrolladores accedan a recursos específicos de S3. ¿Cuál es la mejor práctica?**

- [ ] A) Crear usuarios individuales con políticas adjuntas

- [x] B) Crear un grupo de desarrolladores con políticas adjuntas

- [ ] C) Usar el usuario root

- [ ] D) Crear roles para cada recurso

  

**17. ¿Cuál es la diferencia entre inline policies y managed policies?**

- [ ] A) No hay diferencia

- [ ] B) Inline policies son reutilizables, managed policies no

- [x] C) Managed policies son reutilizables, inline policies están integradas en un principal

- [ ] D) Ambas son idénticas

  

**18. Una aplicación EC2 necesita acceder a DynamoDB. ¿Cuál es la mejor práctica?**

- [ ] A) Hardcodear Access Keys en la aplicación

- [ ] B) Crear un usuario IAM y usar sus credenciales

- [x] C) Usar un IAM Role asociado a la instancia EC2

- [ ] D) Usar el usuario root

  

**19. ¿Qué es AssumeRole en IAM?**

- [ ] A) Crear un nuevo rol

- [ ] B) Eliminar un rol

- [x] C) Tomar temporalmente los permisos de un rol

- [ ] D) Modificar un rol

  

**20. ¿Cuál es el propósito de una Trust Policy?**

- [ ] A) Definir qué acciones puede realizar un rol

- [x] B) Definir quién puede asumir un rol

- [ ] C) Definir recursos accesibles

- [ ] D) Definir horarios de acceso

  

**21. Una empresa quiere permitir acceso temporal a consultores externos. ¿Qué mecanismo es más apropiado?**

- [ ] A) Crear usuarios permanentes

- [x] B) Usar roles con AssumeRole

- [ ] C) Compartir credenciales de usuario root

- [ ] D) Usar Access Keys permanentes

  

**22. ¿Qué es AWS STS (Security Token Service)?**

- [ ] A) Un servicio de almacenamiento

- [x] B) Un servicio que emite credenciales temporales

- [ ] C) Un servicio de base de datos

- [ ] D) Un servicio de redes

  

**23. ¿Cuál es la duración máxima predeterminada para credenciales temporales de STS?**

- [ ] A) 15 minutos

- [x] B) 1 hora

- [ ] C) 12 horas

- [ ] D) 24 horas

  

**24. ¿Qué condición IAM verificaría la dirección IP del solicitante?**

- [x] A) aws:SourceIp

- [ ] B) aws:UserAgent

- [ ] C) aws:RequestedRegion

- [ ] D) aws:CurrentTime

  

**25. Una empresa quiere restringir el acceso a recursos solo durante horarios laborales. ¿Qué condición usaría?**

- [ ] A) aws:SourceIp

- [ ] B) aws:CurrentTime

- [x] C) aws:RequestedRegion

- [ ] D) aws:UserAgent

  

**26. ¿Qué es AWS Organizations y cómo se relaciona con IAM?**

- [ ] A) Un servicio de base de datos

- [x] B) Un servicio para gestionar múltiples cuentas AWS y aplicar políticas centralizadas

- [ ] C) Un servicio de almacenamiento

- [ ] D) Un servicio de redes

  

**27. ¿Qué es una Service Control Policy (SCP)?**

- [x] A) Una política que define permisos para servicios

- [ ] B) Una política que define límites máximos de permisos en Organizations

- [ ] C) Una política que define acceso a recursos

- [ ] D) Una política que define horarios de acceso

  

**28. ¿Cuál es la diferencia entre Authorization y Authentication?**

- [ ] A) Son lo mismo

- [x] B) Authentication verifica identidad, Authorization verifica permisos

- [ ] C) Authorization verifica identidad, Authentication verifica permisos

- [ ] D) No hay diferencia práctica

  

**29. ¿Qué es Cross-Account Access?**

- [ ] A) Acceso dentro de la misma cuenta

- [x] B) Acceso entre diferentes cuentas AWS

- [ ] C) Acceso a recursos públicos

- [ ] D) Acceso temporal

  

**30. ¿Cuál es el propósito del External ID en cross-account access?**

- [x] A) Identificar la cuenta de origen

- [ ] B) Adicionar una capa de seguridad para prevenir confused deputy attacks

- [ ] C) Definir permisos

- [ ] D) Establecer duración de acceso

  

**31. ¿Qué es AWS IAM Access Analyzer?**

- [ ] A) Una herramienta para analizar costos

- [x] B) Una herramienta para analizar políticas y accesos externos

- [ ] C) Una herramienta para analizar performance

- [ ] D) Una herramienta para analizar redes

  

**32. ¿Cuál es la diferencia entre Allow y Deny en la evaluación de políticas?**

- [ ] A) Allow siempre gana

- [x] B) Deny siempre gana

- [ ] C) No hay diferencia

- [ ] D) Depende del orden

  

**33. ¿Qué es AWS CloudTrail en relación con IAM?**

- [ ] A) Un servicio de backup

- [x] B) Un servicio que registra llamadas a APIs de AWS

- [ ] C) Un servicio de almacenamiento

- [ ] D) Un servicio de redes

  

**34. ¿Qué información captura CloudTrail sobre eventos de IAM?**

- [ ] A) Solo errores

- [ ] B) Solo accesos exitosos

- [x] C) Todas las llamadas a APIs, incluyendo quién, qué, cuándo y desde dónde

- [ ] D) Solo cambios en políticas

  

**35. ¿Cuál es la práctica recomendada para rotar Access Keys?**

- [ ] A) Nunca rotarlas

- [ ] B) Rotarlas cada 5 años

- [x] C) Rotarlas regularmente (90 días recomendados)

- [ ] D) Rotarlas solo cuando hay incidentes

  

### Nivel Avanzado (Preguntas 36-50)
  

**36. Una empresa multinacional necesita diferentes niveles de acceso según la región. ¿Qué estrategia de IAM implementaría?**

- [ ] A) Crear usuarios por región

- [ ] B) Usar condiciones de política basadas en aws:RequestedRegion

- [ ] C) Crear cuentas separadas por región

- [ ] D) Usar grupos por región

  

**37. ¿Cómo implementaría un sistema de aprobación para acceso temporal a recursos sensibles?**

- [ ] A) Crear usuarios permanentes

- [ ] B) Usar roles con AssumeRole y un sistema de workflow externo

- [ ] C) Compartir credenciales

- [ ] D) Usar Access Keys rotativas

  

**38. ¿Qué es AWS IAM Identity Center (anteriormente AWS SSO)?**

- [ ] A) Un servicio de base de datos

- [ ] B) Un servicio de single sign-on para múltiples cuentas AWS

- [ ] C) Un servicio de almacenamiento

- [ ] D) Un servicio de redes

  

**39. ¿Cuál es la diferencia entre Permission Sets y Policies en IAM Identity Center?**

- [ ] A) Son idénticos

- [ ] B) Permission Sets son templates de políticas para múltiples cuentas

- [ ] C) Policies son templates de Permission Sets

- [ ] D) No hay diferencia práctica

  

**40. Una aplicación Lambda necesita acceder a múltiples servicios AWS. ¿Cuál es la mejor práctica?**

- [ ] A) Hardcodear credenciales en el código

- [ ] B) Crear un rol de ejecución con las políticas mínimas necesarias

- [ ] C) Usar credenciales del usuario root

- [ ] D) Crear múltiples usuarios

  

**41. ¿Cómo implementaría acceso Just-In-Time (JIT) usando IAM?**

- [ ] A) Crear usuarios permanentes

- [ ] B) Usar roles con AssumeRole, STS y automatización

- [ ] C) Compartir credenciales temporalmente

- [ ] D) Usar Access Keys con expiración

  

**42. ¿Qué es AWS IAM Roles Anywhere?**

- [ ] A) Un servicio para crear roles en cualquier región

- [ ] B) Un servicio que permite usar roles IAM desde fuera de AWS

- [ ] C) Un servicio de backup

- [ ] D) Un servicio de redes

  

**43. ¿Cuál es la práctica recomendada para aplicaciones containerizadas que necesitan acceso a AWS?**

- [ ] A) Usar credenciales hardcodeadas

- [ ] B) Usar IAM Roles for Service Accounts (IRSA) en EKS

- [ ] C) Compartir Access Keys

- [ ] D) Usar credenciales del usuario root

  

**44. ¿Qué es AWS IAM Policy Simulator?**

- [ ] A) Una herramienta para simular cargas de trabajo

- [ ] B) Una herramienta para probar políticas IAM antes de implementarlas

- [ ] C) Una herramienta para simular ataques

- [ ] D) Una herramienta para simular costos

  

**45. ¿Cómo implementaría segregación de entornos (dev, staging, prod) usando IAM?**

- [ ] A) Usar la misma cuenta para todos los entornos

- [ ] B) Usar cuentas separadas con cross-account roles

- [ ] C) Usar solo diferentes usuarios

- [ ] D) Usar solo diferentes grupos

  

**46. ¿Qué es AWS Config en relación con IAM?**

- [ ] A) Un servicio de backup

- [ ] B) Un servicio que monitorea configuraciones y compliance de recursos AWS

- [ ] C) Un servicio de almacenamiento

- [ ] D) Un servicio de redes

  

**47. ¿Cuál es la diferencia entre AWS Managed Policies y Customer Managed Policies?**

- [ ] A) No hay diferencia

- [ ] B) AWS Managed son creadas por AWS, Customer Managed por el cliente

- [ ] C) Customer Managed son creadas por AWS

- [ ] D) AWS Managed son más seguras

  

**48. ¿Cómo implementaría un sistema de Break Glass para acceso de emergencia?**

- [ ] A) Crear usuarios permanentes con máximos privilegios

- [ ] B) Usar roles especiales con monitoreo y notificaciones automáticas

- [ ] C) Compartir credenciales del usuario root

- [ ] D) Usar Access Keys permanentes

  

**49. ¿Qué consideraciones de seguridad aplicaría para una aplicación que procesa datos sensibles?**

- [ ] A) Usar credenciales hardcodeadas

- [ ] B) Implementar principio de menor privilegio, rotación de credenciales, y monitoreo

- [ ] C) Dar permisos de administrador

- [ ] D) Usar solo el usuario root

  

**50. ¿Cómo auditaría y monitorizaría el uso de IAM en una organización grande?**

- [ ] A) Revisar manualmente una vez al año

- [ ] B) Usar combinación de CloudTrail, Config, Access Analyzer, y herramientas de automatización

- [ ] C) Confiar en los usuarios

- [ ] D) No es necesario auditar

  

---

## Notas para Estudio
### Conceptos Clave para Recordar:

1. **Principio de Menor Privilegio**: Siempre dar solo los permisos mínimos necesarios

2. **Roles vs Users**: Roles para servicios AWS, Users para personas

3. **Políticas**: JSON que define permisos

4. **Cross-Account Access**: Usar roles con AssumeRole

5. **Credenciales Temporales**: Más seguras que credenciales permanentes

6. **MFA**: Obligatorio para acceso privilegiado

7. **Auditoría**: CloudTrail, Config, Access Analyzer son fundamentales

  

### Servicios Relacionados:

- **AWS STS**: Security Token Service

- **AWS Organizations**: Gestión de múltiples cuentas

- **AWS IAM Identity Center**: Single Sign-On

- **AWS CloudTrail**: Auditoría de APIs

- **AWS Config**: Compliance y configuración

- **AWS Access Analyzer**: Análisis de accesos externos

  

### Patrones Comunes:

- **EC2 + IAM Role**: Para aplicaciones en EC2

- **Lambda + Execution Role**: Para funciones Lambda

- **Cross-Account Access**: Para colaboración entre cuentas

- **Federated Access**: Para identidades externas

- **Just-In-Time Access**: Para acceso temporal controlado

  

---

  

## Instrucciones de Uso

### Para Marcar Respuestas:

1. Marca tu respuesta cambiando `[ ]` por `[x]`

2. Ejemplo: `- [x] B) Un servicio de gestión de identidades y acceso`

  

### Para Convertir a Fichas Bibliográficas:

1. Cada pregunta puede convertirse en una ficha individual

2. Anverso: La pregunta y opciones

3. Reverso: La respuesta correcta con explicación

4. Usa las notas de estudio como referencia adicional

  

### Sistema de Evaluación:

- **Nivel Básico (1-15)**: Fundamentos - 80%+ para aprobar

- **Nivel Intermedio (16-35)**: Aplicación práctica - 70%+ para aprobar

- **Nivel Avanzado (36-50)**: Escenarios complejos - 60%+ para aprobar