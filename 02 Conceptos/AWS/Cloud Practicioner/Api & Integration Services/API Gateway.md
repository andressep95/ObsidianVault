# 💡 Amazon API Gateway

## 🧠 Descripción General

Amazon API Gateway es un servicio completamente administrado de AWS que permite a los desarrolladores crear, publicar, mantener, monitorear y asegurar APIs REST, HTTP y WebSocket a cualquier escala. Actúa como una "puerta frontal" para que las aplicaciones accedan a datos, lógica de negocio o funcionalidad desde servicios backend como workloads en EC2, código en AWS Lambda, aplicaciones web o aplicaciones de comunicación en tiempo real.

API Gateway forma parte integral de la infraestructura serverless de AWS y maneja todas las tareas involucradas en aceptar y procesar hasta cientos de miles de llamadas API concurrentes, incluyendo gestión de tráfico, autorización y control de acceso, monitoreo y gestión de versiones de API.

---

## 🛠️ Configuraciones y Buenas Prácticas

### **Tipos de API**

- **REST APIs:** Soporte completo de funciones con claves API, throttling por cliente, validación de requests, integración con AWS WAF
- **HTTP APIs:** Diseñadas con funciones mínimas para ofrecer menor precio, ideales para proxies simples de Lambda
- **WebSocket APIs:** Para comunicación bidireccional y en tiempo real entre cliente y servidor

### **Tipos de Endpoints**

- **Edge-Optimized:** Enruta requests al CloudFront POP más cercano (por defecto para REST APIs)
- **Regional:** Para clientes en la misma región, reduce overhead de conexión
- **Private:** Accesible solo desde VPC usando VPC endpoints

### **Configuraciones de Seguridad**

- **Implementar Principio de Menor Privilegio:** Usar políticas IAM para controlar acceso granular
- **Autenticación Mutua TLS:** Disponible para REST y HTTP APIs
- **Integración con AWS WAF:** Solo para REST APIs, protege contra exploits web comunes
- **Lambda Authorizers:** Funciones personalizadas de autorización para validación compleja
- **Amazon Cognito:** Integración con pools de usuarios para autenticación

### **Mejores Prácticas de Logging y Monitoreo**

- **Habilitar CloudWatch Logs:** Para requests de API con niveles INFO y ERROR
- **Configurar CloudTrail:** Registro de acciones realizadas por usuarios, roles o servicios
- **Implementar CloudWatch Alarms:** Monitoreo de métricas como latencia, errores 4XX/5XX
- **Usar AWS X-Ray:** Para análisis de rendimiento y triaging de latencias
- **AWS Config:** Monitoreo de configuraciones de recursos API Gateway

### **Configuraciones de Rendimiento**

- **Caching:** Solo disponible en REST APIs, mejora rendimiento reduciendo llamadas backend
- **Throttling:** Control de rate limiting a nivel de stage, método y usage plan
- **Request Validation:** Validación de payloads antes de enviar al backend (REST APIs)
- **Data Transformation:** Transformación de request/response usando mapping templates

### **Gestión de Deployments**

- **Stages:** Ambientes lógicos como dev, test, prod con configuraciones independientes
- **Canary Deployments:** Deployments graduales para rollout seguro de cambios (REST APIs)
- **Stage Variables:** Variables de entorno para diferentes stages
- **Custom Domain Names:** Dominios personalizados con certificados SSL/TLS

---

## 📂 Casos de Uso

### **Caso de Uso 1: API Serverless con Lambda**

Crear una API completamente serverless integrando API Gateway con Lambda functions. Ideal para microservicios, procesamiento de datos y backends de aplicaciones móviles.

- **Escenario:** E-commerce con funciones para gestión de productos, pedidos y usuarios
- **Configuración:** HTTP API con integración Lambda proxy para menor latencia y costo

### **Caso de Uso 2: API Gateway como Proxy para Servicios Legacy**

Modernizar aplicaciones legacy exponiendo servicios existentes a través de API Gateway, agregando seguridad, throttling y monitoreo.

- **Escenario:** Sistema bancario con servicios SOAP legacy expuestos como REST APIs
- **Configuración:** REST API con HTTP proxy integration y transformación de datos

### **Caso de Uso 3: APIs en Tiempo Real con WebSocket**

Implementar funcionalidades de chat, notificaciones push, actualizaciones en vivo y gaming.

- **Escenario:** Aplicación de trading con precios en tiempo real
- **Configuración:** WebSocket API con routes para connect, disconnect y sendmessage

### **Caso de Uso 4: APIs Privadas para Arquitecturas Internas**

APIs accesibles solo desde VPC para comunicación segura entre servicios internos.

- **Escenario:** Microservicios en contenedores que se comunican internamente
- **Configuración:** Private REST API con VPC endpoints y resource policies

### **Ejemplo Práctico: Configuración REST API con Lambda**

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Example API",
    "version": "1.0.0"
  },
  "paths": {
    "/users": {
      "get": {
        "x-amazon-apigateway-integration": {
          "type": "aws_proxy",
          "httpMethod": "POST",
          "uri": "arn:aws:lambda:us-east-1:123456789012:function:GetUsers"
        }
      }
    }
  }
}
```

---

## 🔗 Relaciones con Otros Conceptos

- [[💡 AWS Lambda]] - Integración principal para APIs serverless
- [[💡 Amazon CloudFront]] - CDN para edge-optimized endpoints
- [[💡 AWS WAF]] - Protección de aplicaciones web para REST APIs
- [[💡 Amazon Cognito]] - Servicios de autenticación y autorización
- [[💡 AWS X-Ray]] - Distributed tracing y análisis de performance
- [[💡 Amazon CloudWatch]] - Monitoreo y logging de APIs
- [[💡 AWS Certificate Manager]] - Gestión de certificados SSL/TLS
- [[💡 Amazon VPC]] - Redes virtuales para private APIs
- [[💡 AWS IAM]] - Gestión de identidades y permisos
- [[🧪 Lab - Crear REST API con Lambda Integration]]
- [[🧪 Lab - Implementar WebSocket API para Chat]]
- [[🧪 Lab - Configurar API Gateway con Custom Authorizer]]

---

## ➕ Información Adicional

### **Límites y Quotas Importantes**

- **Throttle por defecto:** 10,000 requests por segundo con burst de 5,000
- **Payload máximo:** 10MB para REST APIs, 6MB para HTTP APIs
- **Timeout integration:** 29 segundos máximo
- **Stages por API:** 10 stages por REST API

### **Diferencias Clave REST vs HTTP APIs**

- **REST APIs:** Funciones completas, mayor costo, soporte para caching, API keys, WAF
- **HTTP APIs:** Funciones básicas, menor costo (hasta 70% menos), mejor performance
- **WebSocket APIs:** Comunicación bidireccional, stateful connections

### **Integración Types disponibles**

- **AWS Proxy Integration:** Para Lambda con formato de evento estándar
- **HTTP Proxy Integration:** Pass-through a HTTP endpoints
- **AWS Integration:** Integración directa con servicios AWS (DynamoDB, S3, etc.)
- **Mock Integration:** Respuestas estáticas para testing

### **Consideraciones de Pricing**

- **REST APIs:** Por millón de requests + costos adicionales por features
- **HTTP APIs:** Hasta 70% menos costoso que REST APIs
- **WebSocket APIs:** Por millón de mensajes + minutes conectados
- **Data Transfer:** Cobros por data out adicionales

### **Notas Importantes para Certificaciones**

- **Architect Associate:** Enfocarse en tipos de endpoint, integración con Lambda, seguridad básica
- **Developer Associate:** Profundizar en integration types, data transformation, deployment strategies
- **Solutions Architect Professional:** Arquitecturas complejas, multi-región, disaster recovery, cost optimization

### **Recursos Externos**

- [Amazon API Gateway Documentation](https://docs.aws.amazon.com/apigateway/)
- [API Gateway REST API vs HTTP API](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html)
- [Security Best Practices](https://docs.aws.amazon.com/apigateway/latest/developerguide/security-best-practices.html)
- [AWS Well-Architected Framework - API Gateway](https://docs.aws.amazon.com/wellarchitected/latest/serverless-applications-lens/api-gateway.html)

---

## 🎯 Exam Tips

### **Para Solutions Architect Associate:**

1. **Recuerda las diferencias clave entre REST y HTTP APIs** - HTTP APIs son más económicas pero con menos funciones
2. **Edge-optimized es el default para REST APIs** - Usa Regional para clientes en la misma región
3. **Private APIs requieren VPC endpoints** - Solo accesibles desde within VPC

### **Para Developer Associate:**

1. **Lambda Proxy Integration pasa todo el request context** - Incluye headers, query params, body en el evento
2. **Stage variables actúan como environment variables** - Útiles para diferentes ambientes (dev/prod)
3. **Request validation ocurre antes del backend call** - Reduce costos validando en API Gateway

### **Para Solutions Architect Professional:**

1. **Custom domain names requieren certificados en ACM** - Edge-optimized usa us-east-1, Regional usa región local
2. **Canary deployments permiten rollouts graduales** - Divide tráfico entre versiones base y canary
3. **Resource policies controlan acceso a nivel de API** - Combinan con IAM policies para control granular

---

## 📝 Preguntas de Práctica

**1.** Una empresa necesita exponer una REST API que debe ser accesible solo desde su VPC corporativa y rechazar todo el tráfico de internet. ¿Cuál es la configuración más apropiada?

A) Edge-optimized endpoint con AWS WAF rules B) Regional endpoint con security groups restrictivos  
C) Private endpoint con VPC endpoint y resource policy D) Regional endpoint con Lambda authorizer

**2.** Un desarrollador necesita crear una API que maneje hasta 50,000 requests por segundo con el menor costo posible, integrándose únicamente con Lambda functions. ¿Qué tipo de API debería usar?

A) REST API con Lambda integration B) HTTP API con Lambda proxy integration C) WebSocket API con Lambda integration D) REST API con AWS proxy integration

**3.** Una aplicación requiere autenticación JWT, transformación de requests, caching de respuestas y throttling por cliente. ¿Cuál es la mejor opción?

A) HTTP API con JWT authorizer y CloudFront B) REST API con Lambda authorizer y caching habilitado C) WebSocket API con custom authorizer D) REST API con Cognito authorizer y usage plans

**4.** Para un deployment de API Gateway que requiere rollback inmediato en caso de issues, ¿cuál es la estrategia más apropiada?

A) Blue/Green deployment con Route 53 weighted routing B) Canary deployment con 10% de tráfico inicialmente C) Rolling deployment con CloudFormation D) All-at-once deployment con stage variables

**5.** Una empresa necesita integrar API Gateway con un servicio interno que requiere certificados client-side SSL. ¿Qué configuración es necesaria?

A) Mutual TLS en REST API con custom domain B) Client-side SSL certificates en REST API integration C) VPC endpoint con security groups D) Lambda authorizer con certificate validation

---

**Respuestas:**

1. C) Private endpoint con VPC endpoint y resource policy
2. B) HTTP API con Lambda proxy integration
3. B) REST API con Lambda authorizer y caching habilitado
4. B) Canary deployment con 10% de tráfico inicialmente
5. B) Client-side SSL certificates en REST API integration