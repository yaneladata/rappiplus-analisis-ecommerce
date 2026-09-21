# 📦 Análisis de Rentabilidad, Conversión y Retención en RappiPlus

> 👤 **Rol:** Analista de Datos de Negocio y Producto (Proyecto Individual)  
> 🏢 **Contexto:** Evaluación de Servicio de Suscripción e-Commerce / Proyecto de Portafolio  
> 🎯 **Alcance:** Auditoría de calidad de datos, diagnóstico financiero ($9.61M USD Revenue acumulado / $3.83M en ventas evaluadas), optimización de margen, análisis de funnel, retención por cohortes y prueba A/B.  
> 🛠️ **Stack Técnico:** Python (`pandas`, `numpy`, `scipy.stats`), Tableau Public (Dashboards interactivos), Google Colab, Jupyter Notebooks.

---

## 🎯 Problema Analizado

El proyecto aborda la evaluación integral del desempeño operativo, financiero y de experiencia de usuario en la plataforma RappiPlus. Específicamente, se identificaron cuatro problemáticas clave:

* **Inconsistencias en los Datos:** Presencia de registros duplicados, valores nulos y errores de escala en las transacciones que distorsionaban las métricas reales de negocio.
* **Fuga de Margen de Ganancia:** Incertidumbre sobre la rentabilidad real por producto/categoría debido a desajustes críticos entre precios de venta y costos de adquisición.
* **Fricción en el Funnel y Churn:** Alta tasa de abandono en la pasarela de pago y pérdida masiva de usuarios en la primera semana del ciclo de vida.
* **Efectividad del Rediseño UI:** Necesidad de evaluar con rigor estadístico si la nueva versión de Checkout (Tratamiento) incrementa la conversión respecto a la versión actual (Control).

---

## 🛠️ Herramientas Utilizadas

* **Lenguaje de Programación:** Python
* **Procesamiento y Manipulación de Datos:** `pandas`, `numpy`
* **Análisis Estadístico e Inferencia:** `scipy.stats` (Prueba Chi-cuadrado $\chi^2$)
* **Visualización de Datos & Business Intelligence:** Tableau Public (Dashboards ejecutivos e interactivos), `matplotlib`, `seaborn`
* **Entorno de Desarrollo:** Google Colab, Jupyter Notebooks

---

## 🔄 Proceso Aplicado (Metodología)

1. **Ingesta y Limpieza de Datos (Data Quality):**
   * Eliminación de registros duplicados en el conjunto de 25,100 órdenes.
   * Corrección de errores de escala en la columna `cantidad` (factores de 10,000 y 20,000) y remoción de transacciones anómalas.
   * Imputación de precios unitarios faltantes mediante la mediana por producto y validación de integridad relacional con el catálogo.

2. **Auditoría Financiera y de Márgenes:**
   * Cálculo de ingresos totales, costos de ventas (COGS), gastos de marketing y margen neto global.
   * Análisis comparativo de rentabilidad bruta evaluando los 3 países de operación (México, Colombia, Argentina), las 3 categorías principales (Hogar, Electrónica, Moda) y los 3 canales de adquisición (Paid Search, Organic, Social).

3. **Análisis de Funnel y Cohortes de Retención:**
   * Mapeo de la conversión desde la visita inicial (`first_visit`) hasta la compra completada (`purchase`).
   * Medición de retención por cohortes semanales a lo largo de 22 semanas ($N = 8,000$ usuarios).

4. **Evaluación de Experimento A/B:**
   * Formulación de hipótesis ($H_0$ vs. $H_1$) sobre la tasa de conversión en la pasarela de pago.
   * Aplicación de la prueba Chi-cuadrado de independencia para determinar significancia estadística.

5. **Diseño y Modelado del Dashboard BI (Tableau):**
   * Construcción del modelo de datos en estrella (Star Schema) conectando las tablas procesadas en Tableau Public.
   * Desarrollo de tableros interactivos (Vista General y Vista Detalle) con KPIs financieros, seguimiento de Revenue mensual, YTD acumulado, distribución de Revenue, Profit por producto, tabla de órdenes detallada y desglose de Profit por País y Canal.

---

## 📊 Principales Hallazgos

* **Rentabilidad General:** Se generaron **$3.83M USD en ventas netas evaluadas** (de un acumulado de $9.61M USD) con un **Margen Neto Global del 30.3%** ($920,000 USD de ganancia neta).
* **Hallazgo Crítico (Ventas bajo costo) 🚨:** Se detectaron **4,378 pedidos** vendidos por debajo de su costo marginal de adquisición. El producto *Laptop-Gaming-16GB* generó un **Margen Bruto de -8.6%**, acumulando **más de $300,000 USD en pérdidas directas**.
* **Top Productos en Profit:** *Vacuum-Pro-Black* ($1,496,715 USD) y *Sneakers-Urban-42* ($1,434,191 USD).
* **Distribución de Ingresos por Categoría:** La categoría **Hogar** lidera los ingresos con $3,193,018 USD, seguida de **Electrónica** ($3,172,549 USD) y **Moda** ($3,132,464 USD). Argentina y Colombia destacan con los márgenes más altos en Hogar (>62%).
* **Punto de Abandono Crítico (Drop-off):** El **60.39% de los usuarios que intentan pagar abandonan el checkout** en el paso final (Intento de Pago ➔ Compra).
* **Patrón de Churn:** El **58.13% de la pérdida de usuarios ocurre en los primeros 6 días (Día 0 a W1)**. Quienes superan la primera semana mantienen una retención lineal sólida cercana al 42%.
* **Resultado del Experimento A/B:** La prueba estadística arrojó un **$p\text{-valor} = 0.4319 \ge 0.05$**, confirmando que la nueva versión del Checkout (Tratamiento) **no generó un incremento estadísticamente significativo** en la conversión respecto a la versión actual (Control).

---

## 💡 Conclusiones y Recomendaciones Estratégicas

* **Negocio y Pricing**: Se sugiere que la prioridad inmediata no es aumentar el volumen de ventas, sino **corregir la parametrización de precios y promociones** en la categoría Electrónica (*Laptop-Gaming-16GB*) para detener la fuga de margen.
* **Producto e Ingeniería**: Se debe **pausar el despliegue de la nueva UI de Checkout** ($H_0$ no rechazada) y redirigir los esfuerzos de ingeniería a resolver los problemas técnicos/fricciones en la pasarela de pago actual para mitigar el 60.39% de abandono.
* **Estrategia de Crecimiento**: Las campañas de retención y retargeting deben concentrarse de manera crítica en los **primeros 6 días post-registro** (onboarding), lugar donde se pierde a más de la mitad de la base de usuarios.
---

## 📁 Estructura del Repositorio

```text
├── data/
│   ├── raw/                        <- Datasets originales (Orders, Catalog, Marketing)
│   └── processed/                  <- Datasets limpios (orders_clean, catalog_clean, marketing_clean)
├── notebooks/
│   └── Proyecto_RappiPlus.ipynb    <- Notebook principal con ETL, análisis financiero y A/B Test
├── visualizaciones/
│   ├── Overview_Ejecutivo.png      <- Captura del Dashboard Vista General en Tableau
│   └── Vista_Detalle.png           <- Captura del Dashboard Vista Detalle en Tableau
└── README.md                       <- Documentación ejecutiva del proyecto





