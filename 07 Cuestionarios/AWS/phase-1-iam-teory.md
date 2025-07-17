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