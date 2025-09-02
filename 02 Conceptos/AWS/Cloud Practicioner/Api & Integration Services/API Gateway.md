# 💡 Amazon API Gateway

## 🧠 Descripción General

Amazon API Gateway es un servicio completamente administrado que actúa como puerta de entrada para aplicaciones que acceden a servicios backend. Maneja el tráfico API, autorización, monitoreo y control de versiones, permitiendo crear, publicar y mantener APIs seguras a cualquier escala. Es fundamental en arquitecturas serverless y microservicios, integrándose estrechamente con Lambda, VPC endpoints, CloudFront y servicios de autenticación.

---

## 🛠️ Configuraciones y Buenas Prácticas

### **1. Selección y Configuración de Tipo de API**

- **REST API:** Para funcionalidades completas (caching, API keys, WAF, request validation)
- **HTTP API:** Para casos simples con 70% menos costo, mejor performance para Lambda proxy
- **WebSocket API:** Para comunicación bidireccional en tiempo real

### **2. Configuración de Endpoints**

- **Edge-Optimized:** Para audiencias globales distribuidas (usa CloudFront automáticamente)
- **Regional:** Para audiencias concentradas en una región específica (menor latencia)
- **Private:** Para tráfico interno VPC únicamente (requiere VPC endpoints)

### **3. Configuración de Seguridad (Orden de Implementación)**

- **Resource Policies:** Control de acceso a nivel de API (IP whitelisting, VPC restrictions)
- **Authentication:** IAM, Cognito User Pools, Lambda Authorizers, o JWT (HTTP API)
- **Authorization:** Method-level permissions y resource-based access control
- **CORS:** Configurar origins, methods, headers permitidos para aplicaciones web
- **API Keys + Usage Plans:** Control de acceso y throttling por cliente
- **AWS WAF Integration:** Protección contra ataques web (solo REST API)
- **Mutual TLS:** Para autenticación bidireccional en conexiones sensibles

### **4. Configuración de Performance**

- **Throttling Settings:**
    - Account-level: 10,000 RPS con burst de 5,000 (ajustable)
    - Stage-level: Límites por ambiente
    - Method-level: Límites granulares por endpoint
    - Usage Plan-level: Límites por cliente/API key
- **Caching Configuration:** (Solo REST API)
    - Cache size: 0.5GB a 237GB
    - TTL: 0 segundos a 3600 segundos
    - Cache key parameters: Query strings, headers, path parameters
- **Request/Response Optimization:**
    - Request validation: Validar antes de llegar al backend
    - Response compression: Habilitar para payloads grandes
    - Request transformation: Mapping templates para modificar requests

### **5. Configuración de Integración**

- **Integration Types:**
    - Lambda Proxy: Para funciones Lambda (recomendado)
    - Lambda Integration: Para control granular de request/response
    - HTTP Proxy: Para servicios HTTP existentes
    - HTTP Integration: Con transformaciones personalizadas
    - AWS Service: Integración directa con servicios AWS
    - Mock Integration: Para testing y development
- **Connection Types:**
    - Internet: Para endpoints públicos
    - VPC Link: Para servicios privados en VPC
- **Timeout Configuration:**
    - Integration timeout: Máximo 29 segundos
    - Custom timeout: Basado en requirements del backend

### **6. Configuración de Logging y Monitoreo**

- **CloudWatch Logs:**
    - Access Logging: Log format personalizado con variables contextuales
    - Execution Logging: INFO/ERROR levels para debugging
- **CloudWatch Metrics:**
    - Default metrics: Count, Latency, IntegrationLatency, 4XXError, 5XXError
    - Custom metrics: Usando stage variables y mapping templates
- **AWS X-Ray:**
    - Tracing habilitado a nivel de stage
    - Sampling rules personalizadas
- **CloudWatch Alarms:**
    - Error rate thresholds
    - Latency thresholds
    - Traffic anomalies

### **7. Configuración de Deployment**

- **Stage Management:**
    - Stage variables para configuración por ambiente
    - Deployment history y rollback capability
    - Canary deployments para production (solo REST API)
- **Custom Domain Names:**
    - ACM certificate management
    - DNS configuration con Route 53
    - Base path mappings para múltiples APIs
- **API Documentation:**
    - OpenAPI/Swagger specification
    - Documentation parts para cada método
    - SDK generation configuration

### **8. Configuración de Data Transformation**

- **Request Mapping:**
    - Header mapping: Request headers a integration headers
    - Parameter mapping: Query/path parameters
    - Body transformation: JSON to XML, field mapping
- **Response Mapping:**
    - Status code mapping
    - Header transformation
    - Response body modification
- **Variables de Contexto Disponibles:**
    - $context.requestId, $context.stage, $context.httpMethod
    - $context.sourceIp, $context.userAgent
    - $context.authorizer.* para Lambda authorizers

---

## 📂 Casos de Uso

### **Caso de Uso 1: API Pública para Aplicación Móvil**

- **Configuración:** HTTP API con JWT authorizer, CORS habilitado, CloudFront distribution
- **Razón:** Menor costo, alta performance, autenticación estándar
- **Consideraciones:** Rate limiting por usuario, response caching con CloudFront

### **Caso de Uso 2: API de Microservicios Internos**

- **Configuración:** Private REST API con VPC endpoints, IAM authentication
- **Razón:** Seguridad interna, control granular de acceso, auditoría completa
- **Consideraciones:** Network Load Balancer para alta disponibilidad, service mesh integration

### **Caso de Uso 3: Legacy System Modernization**

- **Configuración:** REST API con HTTP integration, extensive mapping templates
- **Razón:** Transformación de protocolos, validación de requests, throttling control
- **Consideraciones:** Circuit breaker patterns, gradual migration strategy

### **Caso de Uso 4: Partner API con SLA**

- **Configuración:** REST API con API keys, usage plans, dedicated caching
- **Razón:** Revenue model, SLA enforcement, detailed analytics
- **Consideraciones:** Multi-tier pricing, overage policies, partner onboarding

### **Ejemplo Práctico: Checklist de Configuración Óptima**

```
□ Seleccionar tipo de API basado en requirements
□ Configurar endpoint type según audiencia geográfica
□ Implementar resource policy para control de acceso básico
□ Configurar authentication method apropiado
□ Establecer CORS para aplicaciones web
□ Configurar throttling a nivel account, stage y method
□ Habilitar caching si aplica (REST API)
□ Configurar integration type y timeout
□ Establecer logging detallado para troubleshooting
□ Configurar monitoring y alertas proactivas
□ Implementar custom domain con certificado válido
□ Documentar API con OpenAPI specification
□ Configurar deployment stages y variables
□ Realizar testing de performance y security
□ Configurar backup y disaster recovery
```

---

## 🔗 Relaciones con Otros Conceptos

- [[💡 AWS Lambda]] - Backend serverless principal para APIs
- [[💡 Amazon CloudFront]] - CDN para edge-optimized endpoints
- [[💡 AWS Certificate Manager]] - Gestión de certificados SSL/TLS
- [[💡 Amazon Cognito]] - User pools para autenticación OAuth/OIDC
- [[💡 AWS WAF]] - Web application firewall para REST APIs
- [[💡 AWS X-Ray]] - Distributed tracing para performance analysis
- [[💡 Amazon CloudWatch]] - Logging, metrics y monitoring
- [[💡 AWS IAM]] - Identity and access management
- [[💡 Amazon VPC]] - Virtual private cloud para private APIs
- [[💡 AWS Systems Manager]] - Parameter Store para configuraciones
- [[🧪 Lab - REST API con Múltiples Ambientes]]
- [[🧪 Lab - HTTP API con JWT Authentication]]
- [[🧪 Lab - Private API con VPC Integration]]

---

## ➕ Información Adicional

### **Límites y Quotas Críticas**

- **Request Rate:** 10,000 RPS por región (ajustable hasta 5,000,000)
- **Burst Capacity:** 5,000 requests (ajustable)
- **Payload Size:** 10MB REST API, 6MB HTTP API
- **Integration Timeout:** 29 segundos máximo
- **Mapping Template Size:** 1MB máximo
- **Stages per API:** 10 stages máximo
- **Methods per Resource:** 200 métodos máximo

### **Consideraciones de Costo**

- **REST API:** $3.50 por millón de requests + features adicionales
- **HTTP API:** $1.00 por millón de requests (70% ahorro)
- **WebSocket API:** $1.00 por millón de messages + $0.25 por millón de connection minutes
- **Caching:** $0.020 por hora por GB de cache
- **Data Transfer:** $0.09 per GB out después de 1GB free tier

### **Patrones de Configuración Avanzada**

- **Circuit Breaker:** Timeout cortos con retry logic en cliente
- **Rate Limiting Jerárquico:** Account > Stage > Method > Usage Plan
- **Cache Invalidation:** Invalidación selectiva por cache key patterns
- **Blue/Green Deployments:** Canary deployments con stage variables
- **Multi-Region:** Route 53 health checks con failover

### **Troubleshooting Común**

- **429 Too Many Requests:** Revisar throttling settings y usage plans
- **502 Bad Gateway:** Verificar integration timeout y backend health
- **403 Forbidden:** Validar resource policies, CORS, authentication
- **504 Gateway Timeout:** Aumentar integration timeout o optimizar backend
- **CORS Errors:** Verificar preflight OPTIONS method configuration

### **Security Hardening Checklist**

```
□ Resource policy restricts access por IP/VPC
□ Authentication habilitada en todos los métodos
□ HTTPS enforcement (redirect HTTP to HTTPS)
□ API keys rotadas regularmente
□ WAF rules configuradas para common attacks
□ CloudTrail logging habilitado
□ Sensitive data no expuesta en logs
□ Rate limiting apropiado para prevenir abuse
□ Input validation en todos los endpoints
□ Least privilege en IAM roles
```

### **Performance Optimization Checklist**

```
□ HTTP API usado para simple Lambda proxy
□ Regional endpoint para audiencia local
□ Caching habilitado con TTL apropiado
□ Request validation para rechazar requests inválidos temprano
□ Response compression habilitada
□ CloudFront distribution para contenido estático
□ Lambda function timeout < API Gateway timeout
□ Connection pooling en backend services
□ Async processing para operaciones long-running
□ Content-based routing para optimize backends
```

### **Recursos Externos**

- [Amazon API Gateway Documentation](https://docs.aws.amazon.com/apigateway/)
- [API Gateway REST API vs HTTP API Comparison](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html)
- [Security Best Practices](https://docs.aws.amazon.com/apigateway/latest/developerguide/security-best-practices.html)
- [Performance Best Practices](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html)
- [Cost Optimization Guide](https://aws.amazon.com/api-gateway/pricing/)

---

## 🎯 Exam Tips

### **Para Solutions Architect Associate:**

1. **REST vs HTTP API decision matrix:** HTTP para simple Lambda proxy (costo), REST para features avanzadas
2. **Endpoint types geographic considerations:** Edge para global, Regional para same-region clients
3. **Authentication methods comparison:** IAM para AWS services, Cognito para users, Lambda authorizer para custom logic

### **Para Developer Associate:**

1. **Integration timeout es 29 segundos máximo** - Diseñar para async patterns si necesitas más tiempo
2. **Caching solo disponible en REST APIs** - Factor clave en decisiones de arquitectura
3. **CORS debe configurarse explícitamente** - No está habilitado por defecto

### **Para Solutions Architect Professional:**

1. **Private APIs requieren VPC endpoints específicos** - Planificar networking apropiadamente
2. **Canary deployments solo en REST APIs** - Considerar alternativas para HTTP APIs
3. **Multi-region requires Route 53 health checks** - API Gateway no tiene automatic failover

---

## 📝 Preguntas de Práctica

**1.** Una empresa necesita una API que maneje 50,000 RPS con autenticación JWT, CORS, y el menor costo posible. ¿Cuál es la configuración óptima?

A) REST API con Lambda authorizer y edge-optimized endpoint B) HTTP API con JWT authorizer y regional endpoint C) WebSocket API con custom authorizer D) REST API con Cognito authorizer y private endpoint

**2.** Para una aplicación que requiere 45 segundos de processing time, ¿cuál es la mejor architectural approach con API Gateway?

A) Aumentar integration timeout a 45 segundos B) Usar async processing con SQS y polling endpoint C) Implementar WebSocket para long-running connections D) Usar Lambda con extended timeout

**3.** Una API privada debe ser accesible solo desde EC2 instances en subnets específicas. ¿Qué configuración de seguridad es necesaria?

A) Security groups en API Gateway B) Private endpoint con VPC endpoint y resource policy C) WAF rules con IP restrictions D) Lambda authorizer con subnet validation

**4.** Para minimizar latencia en una aplicación móvil global con backend en us-east-1, ¿cuál es la configuración óptima?

A) Regional API Gateway con CloudFront distribution B) Edge-optimized API Gateway únicamente C) Private API Gateway con global accelerator D) Multiple regional API Gateways con Route 53

**5.** Una API requiere diferentes rate limits: 100 RPS para free tier, 1000 RPS para paid tier. ¿Cómo configurar esto?

A) Multiple APIs con diferentes throttling settings B) Usage plans con API keys y different throttling limits C) Lambda authorizer con custom rate limiting logic D) CloudFront with rate limiting rules

---

**Respuestas:**

1. B) HTTP API con JWT authorizer y regional endpoint
2. B) Usar async processing con SQS y polling endpoint
3. B) Private endpoint con VPC endpoint y resource policy
4. A) Regional API Gateway con CloudFront distribution
5. B) Usage plans con API keys y different throttling limits