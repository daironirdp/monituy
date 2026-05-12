# 🛒 Monitor de Precios de Supermercados (Uruguay)

Sistema de monitoreo de precios de supermercados en Uruguay que implementa un pipeline de datos completo para la recolección, procesamiento, almacenamiento y análisis de información histórica de productos.

El sistema permite detectar variaciones de precios, analizar tendencias y ofrecer información útil a usuarios finales a través de una API y una interfaz web.

---

# 🎯 Objetivos

- Comparar precios entre supermercados  
- Detectar ofertas y cambios de precios  
- Analizar tendencias históricas  
- Proveer datos accesibles vía API  
- Permitir a usuarios suscribirse a alertas  

---

# 🏗️ Arquitectura


---

# 📥 Ingesta de Datos

La ingesta de datos se realiza mediante un sistema de scraping web con las siguientes características:

- Scraper genérico basado en configuración (selectores, URLs, etc.)
- Soporte para scrapers específicos en casos particulares
- Extracción de datos desde sitios de supermercados en Uruguay
- Ejecución periódica (ej: semanal)

## 📌 Datos extraídos

- Nombre del producto  
- Categoría (original del supermercado)  
- Precio  
- Descuentos  
- Stock (si está disponible)  
- Supermercado de origen  
- Fecha de extracción  

---

# 📦 Almacenamiento de Datos

## 🔹 Datos crudos (Raw)

- Formato: JSON  
- Nomenclatura: `supermercado-fecha.json`  
- Estructura semi-estructurada  
- Uso: auditoría y reprocesamiento  

---

## 🔹 Datos procesados

Base de datos relacional (PostgreSQL):

### Tablas principales

- `products`
- `prices_current`
- `prices_history`

---

# 📊 Histórico de precios

El sistema mantiene un historial completo de precios:

- Separación entre datos actuales e históricos  
- Inserción automática en histórico ante cambios  
- Timestamps:
  - fecha de creación original  
  - fecha de actualización  

Esto permite análisis temporal sin afectar el rendimiento de consultas actuales.

---

# 🔄 Pipeline de Datos (ETL)

El flujo de datos sigue un proceso ETL:

## 1. Extracción
- Scraping desde múltiples fuentes

## 2. Transformación
- Limpieza de datos con pandas  
- Normalización de precios (UYU)  
- Estandarización de datos  

## 3. Carga
- Inserción en base de datos relacional  
- Actualización incremental (solo cambios)

---

# 🧠 Normalización de Categorías

Dado que cada supermercado puede manejar distintas categorías:

- Se almacena:
  - `categoria_original`
  - `categoria_normalizada`

Esto permite:
- análisis transversal  
- mantener fidelidad de los datos originales  

---

# 🌐 API

API desarrollada con FastAPI  

## Endpoints principales

- `GET /products`  
- `GET /products/{id}`  
- `GET /prices`  
- `GET /deals`  

---

# 👤 Usuarios y Autenticación

El sistema permite:

- Acceso público a datos sin autenticación  
- Registro de usuarios para funcionalidades avanzadas  

## Funcionalidades autenticadas

- Suscripción a alertas de precios  
- Notificaciones por correo electrónico  

## Métodos de autenticación

- Email y contraseña  
- OAuth (Google) *(futuro)*  

---

# 🔔 Sistema de Alertas

Los usuarios pueden recibir notificaciones cuando:

- Un producto baja de precio  
- Hay cambios de stock  

---

# 📈 Visualización y Reportes

El sistema incluye:

- Dashboard interactivo (ej: Streamlit)  
- Análisis de tendencias históricas  
- Comparación de precios  

---

# 📋 Logging y Trazabilidad

El sistema implementa un esquema de observabilidad completo:

## 🔹 Logging

- Logs de scraping  
- Logs de procesamiento  
- Logs de API  

## 🔹 Trazabilidad

- Uso de `trace_id` para seguimiento de procesos  
- Correlación de eventos en el pipeline  

## 🔹 Eventos registrados

- Cambios de precios  
- Errores  
- Interacciones de usuarios  

---

# ⚙️ Tecnologías

- FastAPI  
- pandas  
- Scrapy  
- PostgreSQL  
- Docker *(opcional)*  

---

# 🔁 Ejecución del Sistema

- Scraping programado (ej: semanal)  
- Actualización incremental de datos  
- Persistencia de histórico  

---

# 🚀 Roadmap

- [ ] Implementar autenticación OAuth  
- [ ] Sistema de alertas completo  
- [ ] Mejora de scrapers por sitio  
- [ ] Dashboard avanzado  
- [ ] Deploy en cloud  

---

# 🧠 Consideraciones Técnicas

- Scraping puede variar según estructura de cada sitio  
- Se permite extensión mediante scrapers específicos  
- Diseño orientado a escalabilidad y mantenimiento  

---

# 📌 Estado del Proyecto

🚧 En desarrollo  