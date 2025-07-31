## 📋 Conceptos Fundamentales

### 🎯 Pay-as-You-Go

El modelo principal de AWS donde **pagas solo por lo que usas**, sin contratos a largo plazo ni tarifas iniciales. Este enfoque permite:

- **Flexibilidad total** en el uso de recursos
- **Escalamiento automático** según demanda
- **Sin compromisos mínimos** de tiempo o volumen
- **Facturación por segundo/hora** según el servicio

### 💰 Modelos de Precios Principales

#### 1. **On-Demand Pricing**
- **Pago por uso inmediato** sin compromisos
- **Facturación por segundo** (mínimo 60 segundos) para EC2 Linux
- **Facturación por hora** para Windows y otros OS
- **Ideal para:** Cargas de trabajo impredecibles, desarrollo, testing
- **Ventaja:** Máxima flexibilidad
- **Desventaja:** Costo más alto a largo plazo

#### 2. **Reserved Instances (RI)**
- **Descuentos hasta 75%** comparado con On-Demand
- **Compromisos de 1 ó 3 años**
- **Tres tipos de pago:**
    - **All Upfront:** Pago total adelantado (máximo descuento)
    - **Partial Upfront:** Pago parcial + mensualidades
    - **No Upfront:** Solo pagos mensuales
- **Tres tipos de flexibilidad:**
    - **Standard RI:** Máximo descuento, menos flexibilidad
    - **Convertible RI:** Puede cambiar tipo de instancia
    - **Scheduled RI:** Para patrones de uso predecibles

#### 3. **Savings Plans**
- **Descuentos hasta 72%** con compromisos de gasto por hora
- **Más flexible** que Reserved Instances
- **Dos tipos:**
    - **Compute Savings Plans:** EC2, Fargate, Lambda
    - **EC2 Instance Savings Plans:** Solo instancias EC2 específicas
- **Aplica automáticamente** a uso elegible

#### 4. **Spot Instances**
- **Descuentos hasta 90%** comparado con On-Demand
- **AWS puede interrumpir** con 2 minutos de aviso
- **Precio fluctúa** según oferta y demanda
- **Ideal para:** Trabajos tolerantes a fallos, big data, CI/CD

#### 5. **Dedicated Hosts**
- **Servidor físico completo** dedicado
- **Licencias de software** existentes (BYOL)
- **Compliance** y requisitos regulatorios
- **Facturación por host** por hora

#### 6. **Dedicated Instances**
- **Instancias en hardware dedicado**
- **Nivel de cuenta**, no por instancia específica
- **Más económico** que Dedicated Hosts
- **Sin acceso al hardware** subyacente

## 🔧 Factores que Afectan el Costo

### **Compute (EC2)**
- **Tipo de instancia** (t3.micro vs c5.xlarge)
- **Región geográfica** (us-east-1 vs eu-west-1)
- **Sistema operativo** (Linux vs Windows)
- **Tiempo de uso** (facturación por segundo/hora)

### **Storage (S3)**
- **Clase de almacenamiento** (Standard, IA, Glacier)
- **Cantidad de datos** almacenados
- **Número de requests** (GET, PUT, DELETE)
- **Transferencia de datos** (dentro/fuera de AWS)

### **Data Transfer**
- **Entrada de datos:** Generalmente GRATIS
- **Salida de datos:** Costo variable por GB
- **Entre regiones:** Costo por transferencia
- **Dentro de AZ:** Generalmente gratis

## 📊 Herramientas de Gestión de Costos

### **AWS Pricing Calculator**
- **Estimaciones precisas** antes del despliegue
- **Comparación de escenarios** diferentes
- **Exportación de estimaciones** en PDF/CSV

### **AWS Cost Explorer**
- **Análisis histórico** de gastos
- **Predicciones futuras** basadas en tendencias
- **Filtros y agrupaciones** por servicio, región, etc.

### **AWS Budgets**
- **Alertas proactivas** cuando se exceden límites
- **Presupuestos personalizados** por proyecto/departamento
- **Acciones automáticas** cuando se superan umbrales

### **AWS Cost and Usage Reports**
- **Informes detallados** de facturación
- **Datos granulares** por hora/día
- **Integración con herramientas** de BI

## 💡 Estrategias de Optimización

### **Right-Sizing**
- **Analizar métricas** de CPU, memoria, red
- **Downsizing** de instancias sobreutilizadas
- **Upsizing** para evitar cuellos de botella

### **Auto Scaling**
- **Escalamiento automático** según demanda
- **Scheduled scaling** para patrones predecibles
- **Reducción de costos** en horarios de baja demanda

### **Storage Optimization**
- **Lifecycle policies** en S3
- **Intelligent Tiering** automático
- **Compresión y deduplicación**

## 🎯 Casos de Uso por Modelo

|Modelo|Mejor Para|Ejemplo|
|---|---|---|
|**On-Demand**|Desarrollo, Testing, Picos impredecibles|Aplicación en desarrollo|
|**Reserved**|Producción estable, Bases de datos|Servidor web 24/7|
|**Savings Plans**|Workloads mixtos, Crecimiento previsto|Aplicación con múltiples servicios|
|**Spot**|Batch processing, Big Data|Análisis de datos nocturnos|
|**Dedicated**|Compliance, Licencias BYOL|Aplicaciones financieras|

## 🚨 Puntos Clave para Examen
1. **On-Demand es el más caro** pero más flexible
2. **Reserved Instances requieren compromiso** de 1-3 años
3. **Spot puede ser interrumpido** por AWS en cualquier momento
4. **Savings Plans son más flexibles** que RI
5. **Data transfer IN es gratis** generalmente
6. **Cada región tiene precios diferentes**
7. **AWS Free Tier** incluye servicios gratuitos por 12 meses

---

## 🧪 Cuestionario de Evaluación

### **Pregunta 1**
Una startup necesita ejecutar una aplicación web con tráfico muy variable e impredecible. ¿Qué modelo de precios recomendarías inicialmente?

- [ ] A) Reserved Instances por 3 años
- [ ] B) Spot Instances únicamente
- [ ] C) On-Demand Instances
- [ ] D) Dedicated Hosts

**Justificación:** _Para cargas impredecibles, On-Demand ofrece máxima flexibilidad sin compromisos._

---

### **Pregunta 2**
Tu empresa tiene una aplicación de producción que funciona 24/7 con uso constante y predecible. ¿Cuál es la mejor estrategia de costos?

- [ ] A) Mantener todo en On-Demand
- [ ] B) Usar Reserved Instances para la carga base
- [ ] C) Usar solo Spot Instances
- [ ] D) Migrar todo a Dedicated Hosts

**Justificación:** _Para uso constante y predecible, RI ofrece hasta 75% de descuento._

---

### **Pregunta 3**
¿Cuál de las siguientes afirmaciones sobre Spot Instances es CORRECTA?

- [ ] A) Garantizan disponibilidad 24/7
- [ ] B) Son más caras que On-Demand
- [ ] C) AWS puede interrumpirlas con 2 minutos de aviso
- [ ] D) Solo están disponibles en us-east-1

**Justificación:** _Spot Instances pueden ser interrumpidas cuando AWS necesita la capacidad._

---

### **Pregunta 4**
Una empresa quiere usar sus licencias de Windows Server existentes en AWS. ¿Qué opción deberían considerar?

- [ ] A) On-Demand Instances regulares
- [ ] B) Spot Instances
- [ ] C) Dedicated Hosts
- [ ] D) Reserved Instances estándar

**Justificación:** _Dedicated Hosts permite BYOL (Bring Your Own License)._

---

### **Pregunta 5**
¿Cuál es la principal diferencia entre Savings Plans y Reserved Instances?

- [ ] A) Savings Plans son más caros
- [ ] B) Savings Plans ofrecen mayor flexibilidad
- [ ] C) Reserved Instances no requieren compromiso
- [ ] D) No hay diferencias significativas

**Justificación:** _Savings Plans aplican automáticamente a diferentes servicios y tipos de instancia._

---

### **Pregunta 6**
Para un trabajo de procesamiento de datos que puede ejecutarse durante la noche y tolerar interrupciones, ¿qué modelo es más económico?

- [ ] A) On-Demand Instances
- [ ] B) Reserved Instances
- [ ] C) Spot Instances
- [ ] D) Dedicated Instances

**Justificación:** _Spot Instances ofrecen hasta 90% de descuento para workloads tolerantes a fallos._

---

### **Pregunta 7**
¿Qué herramienta de AWS te permite estimar costos ANTES de desplegar recursos?

- [ ] A) Cost Explorer
- [ ] B) AWS Budgets
- [ ] C) AWS Pricing Calculator
- [ ] D) Cost and Usage Reports

**Justificación:** _Pricing Calculator permite estimaciones antes del despliegue real._

---

### **Pregunta 8**
En el modelo de precios de AWS, ¿qué aspecto de la transferencia de datos es generalmente GRATUITO?

- [ ] A) Transferencia de datos saliente a Internet
- [ ] B) Transferencia de datos entrante desde Internet
- [ ] C) Transferencia entre regiones de AWS
- [ ] D) Todas las transferencias son gratuitas

**Justificación:** _Data transfer IN hacia AWS generalmente no tiene costo._

---

### **Pregunta 9**

Una empresa necesita cumplir con regulaciones estrictas que requieren aislamiento físico completo. ¿Qué opción de AWS es más apropiada?

- [ ] A) Instancias On-Demand regulares
- [ ] B) Reserved Instances
- [ ] C) Dedicated Hosts
- [ ] D) Spot Instances

**Justificación:** _Dedicated Hosts proporcionan aislamiento físico completo para compliance._

---

### **Pregunta 10**

Si quieres comprometerte a un gasto mínimo por hora durante 1-3 años pero mantener flexibilidad en los servicios utilizados, ¿qué opción eliges?

- [ ] A) Reserved Instances Standard
- [ ] B) Compute Savings Plans
- [ ] C) On-Demand Instances
- [ ] D) Spot Instances

**Justificación:** _Savings Plans permite compromiso de gasto con flexibilidad en servicios._

---

## ✅ Respuestas Correctas

1. **C** - On-Demand para máxima flexibilidad inicial
2. **B** - Reserved Instances para cargas predecibles 24/7
3. **C** - Spot puede ser interrumpido con 2 min de aviso
4. **C** - Dedicated Hosts para BYOL
5. **B** - Savings Plans más flexibles que RI
6. **C** - Spot para workloads tolerantes a fallos
7. **C** - Pricing Calculator para estimaciones
8. **B** - Data transfer IN generalmente gratis
9. **C** - Dedicated Hosts para compliance estricto
10. **B** - Compute Savings Plans para flexibilidad con compromiso