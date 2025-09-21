## ¿Qué es?

Amazon CloudFront es un servicio web de red de entrega de contenido (CDN) que acelera la distribución de contenido web estático y dinámico (archivos .html, .css, .js, imágenes, videos) a usuarios finales a nivel global. Entrega contenido a través de una red mundial de centros de datos llamados ubicaciones de borde (edge locations) con baja latencia y altas velocidades de transferencia.

**Diagrama:**

```
Usuario Final → [Edge Location más cercana] → [Edge Location Cache]
                        ↓ (si no está en cache)
                [CloudFront Distribution] → [Origin Server]
                                           (S3, EC2, ALB, Custom)
```

## Escenarios de uso

- **Aceleración de sitios web estáticos**: Distribuir contenido HTML, CSS, JS, imágenes desde S3 o servidores personalizados con baja latencia global
- **Streaming de video**: Entrega de contenido multimedia (VOD y live streaming) con protocolos HLS, DASH, Smooth Streaming
- **Distribución de APIs**: Cachear respuestas de APIs REST para reducir carga en backend y mejorar tiempo de respuesta
- **Protección DDoS y seguridad**: Integración con AWS Shield y WAF para proteger aplicaciones contra ataques y amenazas
- **Contenido privado**: Distribución segura usando URLs firmadas y cookies firmadas para controlar acceso
- **Edge computing**: Ejecutar funciones Lambda@Edge y CloudFront Functions para personalización en el borde

## Buenas prácticas

- **Usar Origin Access Control (OAC)** en lugar de Origin Access Identity (OAI) para S3, proporciona mejor seguridad y soporte para características modernas
- **Configurar TTL apropiados**: Establecer cache-control headers en origen para optimizar cacheo (largos para contenido estático, cortos para dinámico)
- **Implementar invalidaciones estratégicamente**: Usar invalidaciones solo cuando sea necesario ya que tienen costo, preferir versionado de archivos
- **Configurar origin failover**: Usar múltiples orígenes para alta disponibilidad cuando el origen primario falle
- **Optimizar clases de precio**: Usar Price Classes para limitar distribución a regiones específicas si usuarios están localizados geográficamente
- **Habilitar compresión**: Activar compresión automática para reducir ancho de banda y mejorar velocidad de carga

## Aspectos a configurar

- **Distribution Settings**: Tipo de distribución (web o RTMP), price class, certificados SSL/TLS personalizados
- **Origin Configuration**: Tipo de origen (S3, Custom HTTP/HTTPS), domain name, path patterns, custom headers
- **Cache Behaviors**: Path patterns, métodos HTTP permitidos, TTL mínimo/máximo/default, políticas de cache
- **Security Configuration**: WAF integration, SSL/TLS certificates, Origin Access Control, field-level encryption
- **Logging and Monitoring**: Standard logs, real-time logs, CloudWatch metrics adicionales
- **Edge Functions**: CloudFront Functions y Lambda@Edge para personalización de requests/responses

## Versiones/Variantes del servicio

|Versión/Tipo|Caso de uso|Características|
|---|---|---|
|Standard Distribution|Aplicaciones individuales, sitios web únicos|Configuración personalizada por distribución, full control|
|Multi-tenant Distribution|Proveedores SaaS, múltiples sitios web|Gestión centralizada, configuraciones compartidas|
|CloudFront Functions|Personalización ligera en el borde|JavaScript, sub-millisecond latency, costo muy bajo|
|Lambda@Edge|Personalización compleja en el borde|Node.js/Python, acceso completo a AWS APIs, mayor latencia|

## Modelo de precios y facturación

- **Método de cobro**: Pago por uso basado en transferencia de datos saliente y número de requests HTTP/HTTPS
- **Opciones de pricing**: Solo On-Demand, no hay opciones reservadas
- **Costos típicos**:
    - Data Transfer Out: $0.085-$0.12 per GB (varía por región)
    - HTTP/HTTPS Requests: $0.0075-$0.016 per 10,000 requests
    - Invalidations: $0.005 per path los primeros 1,000/mes, luego $0.005 cada path adicional
- **Free Tier**: 50 GB data transfer out, 2,000,000 requests HTTP/HTTPS por mes durante 12 meses

## Integración con otros servicios AWS

- **Servicios comunes**: S3 (origen), EC2 (custom origin), ELB, API Gateway, Route 53, Certificate Manager, WAF, Shield
- **Patrones arquitecturales**:
    - S3 + CloudFront + Route 53 (sitio web estático)
    - ALB + CloudFront + WAF (aplicaciones web dinámicas)
    - API Gateway + CloudFront (APIs cacheadas)
    - MediaPackage + CloudFront (streaming video)
- **Dependencias**: Requiere al menos un origen configurado (S3 bucket o HTTP server)

## Límites y cuotas

- **Límites por defecto**: 500 distribuciones por cuenta, 100 orígenes por distribución, 75 cache behaviors por distribución
- **Límites aumentables**: Distribuciones, orígenes, CNAMEs (100 por distribución), data transfer rate (150 Gbps por distribución)
- **Consideraciones de escalabilidad**:
    - 250,000 requests/second por distribución
    - Sin límite en número de archivos servidos
    - Máximo 50 GB por archivo individual para cacheo

## Seguridad y compliance

- **Modelo de responsabilidad**: AWS maneja infraestructura global, edge locations, y availability; cliente maneja configuración de distribución, origen, y políticas de acceso
- **Opciones de cifrado**: SSL/TLS en tránsito (certificados AWS o personalizados), field-level encryption para datos sensibles específicos
- **Certificaciones**: SOC, PCI DSS, HIPAA eligible, ISO certifications, compliance con múltiples estándares globales
- **Control de acceso**: IAM policies, Origin Access Control/Identity, signed URLs/cookies, integration con AWS WAF para filtering

## Monitoreo y troubleshooting

- **CloudWatch metrics**: Requests, BytesDownloaded/Uploaded, 4xxErrorRate, 5xxErrorRate, OriginLatency, CacheHitRate
- **Logs generados**:
    - Standard access logs (batch processing)
    - Real-time logs (streaming analysis)
    - Lambda@Edge logs en CloudWatch Logs
- **CloudTrail events**: Distribution configuration changes, invalidation requests, policy updates
- **Herramientas de diagnóstico**: CloudWatch dashboards, AWS X-Ray integration para tracing, Cache behavior testing tools

## Disponibilidad y durabilidad

- **SLA**: 99.9% availability guarantee con service credits si no se cumple
- **Durabilidad**: No aplica (es servicio de distribución de contenido, no almacenamiento)
- **Opciones de redundancia**:
    - Red global de 400+ edge locations en 90+ ciudades
    - Origin failover automático entre múltiples orígenes
    - Multiple origin groups para redundancia
- **Backup/Restore**: No aplica para el servicio CDN, pero origins pueden tener sus propias estrategias de backup

## Casos de uso: Correcto vs Incorrecto

### ✅ Cuándo SÍ usar CloudFront:

- **Aplicaciones web globales** que necesitan baja latencia para usuarios distribuidos mundialmente
- **Contenido estático frecuentemente accedido** (imágenes, CSS, JS) que se beneficia de cacheo en borde
- **Streaming de video/audio** que requiere distribución global optimizada con protocolos específicos
- **APIs con respuestas cacheables** donde puedes reducir carga en backend manteniendo freshness apropiado
- **Protección contra DDoS** cuando necesitas una capa adicional de seguridad con AWS Shield integration
- **Distribución de software/updates** para acelerar downloads de archivos grandes a nivel global

### ❌ Cuándo NO usar CloudFront:

- **Aplicaciones purely locales** con usuarios en una sola región → Alternativa: **Usar directamente ALB/NLB regional**
- **Contenido altamente dinámico y personalizado** que no puede ser cacheado → Alternativa: **Direct API Gateway o ALB**
- **Datos extremadamente sensibles** que no pueden salir de región específica → Alternativa: **Regional load balancers con endpoints privados**
- **Aplicaciones de tiempo real/websockets intensivas** donde latencia de CDN añade overhead → Alternativa: **Direct connection a ALB/NLB**
- **Costos muy ajustados** para proyectos pequeños donde el costo de CDN excede beneficios → Alternativa: **S3 website hosting o single-region deployment**
- **Contenido que cambia constantemente** (cada minuto) donde invalidations serían prohibitivamente costosas → Alternativa: **Direct origin access con short TTL**