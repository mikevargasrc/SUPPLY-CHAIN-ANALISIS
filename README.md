readme_content = """# 📦 Supply Chain & Procurement Analytics Dashboard (Power BI)

[![Power BI](https://img.shields.io/badge/Power_BI-F2C94C?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Data Model](https://img.shields.io/badge/Model-Star_Schema-blue?style=for-the-badge)](https://en.wikipedia.org/wiki/Star_schema)
[![DAX Enabled](https://img.shields.io/badge/DAX-Advanced-orange?style=for-the-badge)](https://learn.microsoft.com/en-us/dax/)
[![Excel Data Source](https://img.shields.io/badge/Source-Excel-1D6F42?style=for-the-badge&logo=microsoft-excel&logoColor=white)](https://office.com)

> **Un panel interactivo e integral de Inteligencia de Negocios diseñado para transformar datos transaccionales de abastecimiento en insights estratégicos de Supply Chain, optimizando el rendimiento de proveedores, el control presupuestario y el cumplimiento logístico (OTIF).**

---

## 📋 Tabla de Contenidos
- [🎯 Visión General del Proyecto](#-visión-general-del-proyecto)
- [📊 Dashboard Interactivo & Vistas Principales](#-dashboard-interactivo--vistas-principales)
- [🏗️ Arquitectura y Modelado de Datos](#️-arquitectura-y-modelado-de-datos)
- [💡 Diccionario de KPIs e Indicadores Clave](#-diccionario-de-kpis-e-indicadores-clave)
- [📈 Hallazgos y Análisis Estratégico](#-hallazgos-y-análisis-estratégico)
- [🛠️ Tecnologías Utilizadas](#️-tecnologías-utilizadas)
- [🚀 Cómo Replicar este Proyecto](#-cómo-replicar-este-proyecto)
- [👤 Autor & Contacto](#-autor--contacto)

---

## 🎯 Visión General del Proyecto

En entornos altamente competitivos, la eficiencia de la cadena de suministro y la gestión de compras (*Procurement*) impactan directamente en el margen operativo de las empresas. 

Este proyecto resuelve el desafío de unificar transacciones dispersas mediante la implementación de un **Dashboard en Power BI** capaz de monitorear en tiempo real:
* **Gasto y Presupuesto:** Compara el **Monto Comprometido** vs. el **Monto Recibido**.
* **Desempeño Logístico:** Evalúa la puntualidad y completitud mediante los estándares internacionales **OTIF**, **OnTime** e **InFull**.
* **Gestión de Proveedores:** Clasifica el nivel de servicio y volumen de compras por proveedor y región.
* **Control de Inventarios:** Monitorea la demanda y recepción por categoría de producto.

---

## 📊 Dashboard Interactivo & Vistas Principales

El reporte consta de 3 secciones principales diseñadas con una navegación fluida e intuitiva:

### 1️⃣ Resumen de Gestión de Compras (*Executive Overview*)
* **Propósito:** Ofrecer a los directores una vista macro del volumen monetario y rendimiento general.
* **Visuales Clave:** 
  * Tarjetas KPI de Montos, Cantidades y OTIF.
  * Mapa de calor global de proveedores.
  * Histórico mensual de órdenes y presupuesto.

### 2️⃣ Resumen por Proveedores (*Vendor Scorecard*)
* **Propósito:** Evaluar la eficiencia operativa de cada uno de los 29 proveedores registrados.
* **Visuales Clave:**
  * Ranking de cumplimiento OnTime e InFull por proveedor.
  * Distribución de órdenes: Concluidas, En Proceso y Anuladas.

### 3️⃣ Resumen por Producto (*Category Analytics*)
* **Propósito:** Analizar la rotación y recepción de bienes agrupados por categorías (Electrónica, Muebles, etc.).
* **Visuales Clave:**
  * Tendencia temporal de recepción física.
  * Top productos por volumen de compra y unidades canceladas.

---

## 🏗️ Arquitectura y Modelado de Datos

El modelo sigue un diseño en **Esquema en Estrella (*Star Schema*)** para garantizar un rendimiento óptimo en las consultas DAX y facilitar el filtrado cruzado.
