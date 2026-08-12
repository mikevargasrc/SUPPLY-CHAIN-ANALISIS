# 📦 Supply Chain & Procurement Analytics Dashboard (Power BI)

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

## Esquema de Base de Datos

```
+-----------------------+
|    DIM_PROVEEDORES    |
+-----------------------+
| PK: cod_prov          |
|     nom_prov          |
|     tmp_entrega       |
|     org_pais          |
+-----------+-----------+
            |
            | 1
            |
            | *
+-----------------------+     +-----------------------+
|     DIM_PRODUCTOS     |     |      FACT_ORDENES     |
+-----------------------+     +-----------------------+
| PK: cod_prod          | 1 * | FK: fecha_odc         |
|     descrip_prod      +-----+ FK: nro_odc           |
|     Categoria         |     | FK: cod_prod          |
|     Subcategoria      |     | FK: cod_prov          |
|     costo_prod        |     |     cant_prod_odc     |
+-----------------------+     |     prec_unt          |
                              |     monto_odc         |
                              |     fecha_entrega     |
                              |     fecha_recibido    |
                              |     cant_recibida     |
                              |     monto_recibido    |
                              |     estado_odc        |
                              +-----------------------+
```
## 💡 Diccionario de KPIs e Indicadores Clave

| Indicador | Valor en Reporte | Fórmula / Concepto | Justificación de Negocio |
| :--- | :---: | :--- | :--- |
| **Monto Comprometido** | **$5,831,145** | `SUM(ORDENES[monto_odc])` | Presupuesto total emitido en órdenes de compra. |
| **Monto Recibido** | **$5,535,945** | `SUM(ORDENES[monto_recibido])` | Capital efectivamente ingresado a almacén en mercancía. |
| **OTIF** | **87.6%** | `OnTime % × InFull %` | **On-Time In-Full:** Mide si el pedido llegó completo y a tiempo. |
| **OnTime** | **87.3%** | `% ODC con fecha_recibido <= fecha_entrega` | Puntualidad de entrega respecto a la fecha pactada. |
| **InFull** | **100.4%** | `(Cant. Recibida / Cant. Solicitada) × 100` | Precisión del volumen entregado (identifica sobreentregas). |
| **Lead Time Cumplimiento** | **90.9%** | `% ODC dentro del tiempo de entrega pactado` | Mide la adherencia al acuerdo de nivel de servicio (SLA). |
| **Cantidad Solicitada** | **11,436** | `SUM(ORDENES[cant_prod_odc])` | Total de unidades pedidas en el periodo. |
| **Cantidad Recibida** | **11,478** | `SUM(ORDENES[cant_recibida])` | Total de unidades físicas que ingresaron al almacén. |
| **Proveedores Activos** | **22 de 29** | `DISTINCTCOUNT(ORDENES[cod_prov])` | Mide la utilización efectiva de la base de proveedores (76%). |

---

## 📈 Hallazgos y Análisis Estratégico

1. **Picos de Compra Temporales:**
   * **Mayo ($922K)**, **Julio ($882K)** y **Octubre ($901K)** representan el **46.3%** del gasto anual. Requieren planificación anticipada de flujo de caja.
2. **Productos de Mayor Impacto financiero:**
   * La línea de muebles lidera el gasto: **LIVING M ($687,680)** y **LIVING S ($558,800)** suman más de **$1.2M**.
3. **Calidad de Proveedores:**
   * Aunque el **InFull es del 100.4%**, el **OnTime es del 87.3%**, lo que indica que las demoras en entregas son el cuello de botella principal (12.7% de órdenes tardías).

---

## 🛠️ Tecnologías Utilizadas

* **Microsoft Power BI Desktop:** Modelado de datos, DAX y creación del dashboard.
* **Power Query (ETL):** Limpieza, transformación y estandarización de campos.
* **Excel / CSV:** Fuente de datos relacional inicial (`ORDENES`, `PROVEEDORES`, `PRODUCTOS`).
* **DAX (Data Analysis Expressions):** Creación de medidas dinámicas y cálculo de KPIs logísticos.

---

## 🚀 Cómo Replicar este Proyecto

1. **Clonar este repositorio:**
   ```bash
   git clone [https://github.com/mikevargasrc/SUPPLY-CHAIN-ANALISIS.git](https://github.com/mikevargasrc/SUPPLY-CHAIN-ANALISIS.git)

2.  **Abrir la Base de Datos:**

* **Revisa la carpeta /data para explorar el archivo 001 Compras.xlsx.**

3. **Ejecutar en Power BI:**

* **Abre el archivo .pbix con Power BI Desktop.**

* Si es necesario, actualiza la ruta del origen de datos desde Transformar Datos > Configuración del origen de datos.

## 👤 Autor & Contacto

Desarrollado como proyecto de analítica para la optimización de procesos de Supply Chain y Procurement.

* **GitHub:** @mikevargasrc

* **LinkedIn:** Maykol Anthony Vargas Bringas

* **Email:** maykolvargas98@hotmail.com
