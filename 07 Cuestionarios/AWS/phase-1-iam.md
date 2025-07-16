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

- [ ] C) 5000

- [ ] D) 10000

  

**13. ¿Qué tipo de política se adjunta directamente a un usuario?**

- [ ] A) Resource-based policy

- [ ] B) Identity-based policy

- [ ] C) Trust policy

- [ ] D) Bucket policy

  

**14. ¿Cuál es el ARN (Amazon Resource Name) típico para un usuario IAM?**

- [ ] A) arn:aws:iam::account-id:user/username

- [ ] B) arn:aws:s3:::bucket-name

- [ ] C) arn:aws:ec2:region:account-id:instance/instance-id

- [ ] D) arn:aws:lambda:region:account-id:function:function-name

  

**15. ¿Qué sucede cuando un usuario nuevo es creado en IAM?**

- [ ] A) Obtiene permisos de administrador

- [ ] B) Obtiene permisos de solo lectura

- [ ] C) No tiene permisos por defecto

- [ ] D) Obtiene permisos básicos

  

### Nivel Intermedio (Preguntas 16-35)


**16. Una empresa necesita que sus desarrolladores accedan a recursos específicos de S3. ¿Cuál es la mejor práctica?**

- [ ] A) Crear usuarios individuales con políticas adjuntas

- [ ] B) Crear un grupo de desarrolladores con políticas adjuntas

- [ ] C) Usar el usuario root

- [ ] D) Crear roles para cada recurso

  

**17. ¿Cuál es la diferencia entre inline policies y managed policies?**

- [ ] A) No hay diferencia

- [ ] B) Inline policies son reutilizables, managed policies no

- [ ] C) Managed policies son reutilizables, inline policies están integradas en un principal

- [ ] D) Ambas son idénticas

  

**18. Una aplicación EC2 necesita acceder a DynamoDB. ¿Cuál es la mejor práctica?**

- [ ] A) Hardcodear Access Keys en la aplicación

- [ ] B) Crear un usuario IAM y usar sus credenciales

- [ ] C) Usar un IAM Role asociado a la instancia EC2

- [ ] D) Usar el usuario root

  

**19. ¿Qué es AssumeRole en IAM?**

- [ ] A) Crear un nuevo rol

- [ ] B) Eliminar un rol

- [ ] C) Tomar temporalmente los permisos de un rol

- [ ] D) Modificar un rol

  

**20. ¿Cuál es el propósito de una Trust Policy?**

- [ ] A) Definir qué acciones puede realizar un rol

- [ ] B) Definir quién puede asumir un rol

- [ ] C) Definir recursos accesibles

- [ ] D) Definir horarios de acceso

  

**21. Una empresa quiere permitir acceso temporal a consultores externos. ¿Qué mecanismo es más apropiado?**

- [ ] A) Crear usuarios permanentes

- [ ] B) Usar roles con AssumeRole

- [ ] C) Compartir credenciales de usuario root

- [ ] D) Usar Access Keys permanentes

  

**22. ¿Qué es AWS STS (Security Token Service)?**

- [ ] A) Un servicio de almacenamiento

- [ ] B) Un servicio que emite credenciales temporales

- [ ] C) Un servicio de base de datos

- [ ] D) Un servicio de redes

  

**23. ¿Cuál es la duración máxima predeterminada para credenciales temporales de STS?**

- [ ] A) 15 minutos

- [ ] B) 1 hora

- [ ] C) 12 horas

- [ ] D) 24 horas

  

**24. ¿Qué condición IAM verificaría la dirección IP del solicitante?**

- [ ] A) aws:SourceIp

- [ ] B) aws:UserAgent

- [ ] C) aws:RequestedRegion

- [ ] D) aws:CurrentTime

  

**25. Una empresa quiere restringir el acceso a recursos solo durante horarios laborales. ¿Qué condición usaría?**

- [ ] A) aws:SourceIp

- [ ] B) aws:CurrentTime

- [ ] C) aws:RequestedRegion

- [ ] D) aws:UserAgent

  

**26. ¿Qué es AWS Organizations y cómo se relaciona con IAM?**

- [ ] A) Un servicio de base de datos

- [ ] B) Un servicio para gestionar múltiples cuentas AWS y aplicar políticas centralizadas

- [ ] C) Un servicio de almacenamiento

- [ ] D) Un servicio de redes

  

**27. ¿Qué es una Service Control Policy (SCP)?**

- [ ] A) Una política que define permisos para servicios

- [ ] B) Una política que define límites máximos de permisos en Organizations

- [ ] C) Una política que define acceso a recursos

- [ ] D) Una política que define horarios de acceso

  

**28. ¿Cuál es la diferencia entre Authorization y Authentication?**

- [ ] A) Son lo mismo

- [ ] B) Authentication verifica identidad, Authorization verifica permisos

- [ ] C) Authorization verifica identidad, Authentication verifica permisos

- [ ] D) No hay diferencia práctica

  

**29. ¿Qué es Cross-Account Access?**

- [ ] A) Acceso dentro de la misma cuenta

- [ ] B) Acceso entre diferentes cuentas AWS

- [ ] C) Acceso a recursos públicos

- [ ] D) Acceso temporal

  

**30. ¿Cuál es el propósito del External ID en cross-account access?**

- [ ] A) Identificar la cuenta de origen

- [ ] B) Adicionar una capa de seguridad para prevenir confused deputy attacks

- [ ] C) Definir permisos

- [ ] D) Establecer duración de acceso

  

**31. ¿Qué es AWS IAM Access Analyzer?**

- [ ] A) Una herramienta para analizar costos

- [ ] B) Una herramienta para analizar políticas y accesos externos

- [ ] C) Una herramienta para analizar performance

- [ ] D) Una herramienta para analizar redes

  

**32. ¿Cuál es la diferencia entre Allow y Deny en la evaluación de políticas?**

- [ ] A) Allow siempre gana

- [ ] B) Deny siempre gana

- [ ] C) No hay diferencia

- [ ] D) Depende del orden

  

**33. ¿Qué es AWS CloudTrail en relación con IAM?**

- [ ] A) Un servicio de backup

- [ ] B) Un servicio que registra llamadas a APIs de AWS

- [ ] C) Un servicio de almacenamiento

- [ ] D) Un servicio de redes

  

**34. ¿Qué información captura CloudTrail sobre eventos de IAM?**

- [ ] A) Solo errores

- [ ] B) Solo accesos exitosos

- [ ] C) Todas las llamadas a APIs, incluyendo quién, qué, cuándo y desde dónde

- [ ] D) Solo cambios en políticas

  

**35. ¿Cuál es la práctica recomendada para rotar Access Keys?**

- [ ] A) Nunca rotarlas

- [ ] B) Rotarlas cada 5 años

- [ ] C) Rotarlas regularmente (90 días recomendados)

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