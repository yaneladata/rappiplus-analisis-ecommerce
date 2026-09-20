📊 Análisis de Suscripciones de RappiPlus
---

## 1. 🎯 Problema Analizado

El proyecto aborda la evaluación integral del desempeño operativo, financiero y de experiencia de usuario en la plataforma RappiPlus. Específicamente, se identificaron cuatro problemáticas clave:

* **Inconsistencias en los Datos**: Presencia de registros duplicados, valores nulos y errores de escala en las transacciones que distorsionaban las métricas de negocio.
* **Fuga de Margen de Ganancia**: Incertidumbre sobre la rentabilidad real por producto/categoría debido a posibles desajustes entre precios de venta y costos de adquisición.
* **Fricción en el Funnel y Churn**: Alta tasa de abandono en el proceso de compra y pérdida significativa de usuarios en las primeras etapas del ciclo de vida.
* **Efectividad del Rediseño UI**: Necesidad de evaluar con rigor estadístico si una nueva versión de Checkout (Tratamiento) incrementa la conversión respecto a la versión actual (Control).

---

## 2. 🛠️ Herramientas Utilizadas

* **Lenguaje de Programación**: Python
* **Procesamiento y Manipulación de Datos**: Pandas, NumPy
* **Análisis Estadístico e Inferencia**: SciPy (`scipy.stats` - Prueba Chi-cuadrado $\chi^2$)
* **Visualización de Datos &  Business Intelligence**:  Tableau Public (Dashboards ejecutivos e interactivos), Matplotlib, Seaborn
* **Entorno de Desarrollo**: Google Colab, Jupyter Notebooks 

---

## 3. 🔄 Proceso Que Se Siguió

1. **Ingesta y Limpieza de Datos (Data Quality)**:
   * Eliminación de registros duplicados en el conjunto de 25100 órdenes.
   * Corrección de errores de escala en la columna `cantidad` (factores de 10,000 y 20,000) y remoción de transacciones anómalas .
   * Imputación de precios unitarios faltantes mediante la mediana por producto y validación de integridad relacional con el catálogo.

2. **Auditoría Financiera y de Márgenes**:
   * Cálculo de ingresos totales, gastos de marketing y margen neto global.
   * Análisis comparativo de rentabilidad bruta real evaluando los 3 países de operación (México, Colombia, Argentina), las 3 categorías principales (Hogar, Electrónica, Moda) y los 3 canales de adquisición (Paid Search, Organic, Social).

3. **Análisis de Funnel y Cohortes de Retención**:
   * Mapeo de la conversión desde la visita inicial (`first_visit`) hasta la compra completada (`purchase`).
   * Medición de retención por cohortes semanales a lo largo de 22 semanas (8,000 usuarios).

4. **Evaluación de Experimento A/B**:
   * Formulación de hipótesis ($H_0$ vs. $H_1$) sobre la tasa de conversión en la pasarela de pago.
   * Aplicación de la prueba Chi-cuadrado para determinar significancia estadística.

5. **Diseño y Modelado del Dashboard BI (Tableau)**:
   * Construcción del modelo de datos en estrella (Star Schema) conectando las tablas procesadas en Tableau
   * Desarrollo de tableros interactivos(General y Detalle) con KPIs financieros, seguimiento de Revenue mensual, YTD acumulado, distribución de Revenue , Profit por producto, tabla de órdenes detallada, distribución de ingresos por categoría y desglose de Profit por País y Canal.
     
---
## 4.📂 Estructura del Repositorio
```text
├── data/
│   ├── raw/                       <- Datasets originales (Orders, Catalog, Marketing)
│   └── processed/                 <- Datasets limpios (orders_clean, catalog_clean, marketing_clean)
├── notebooks/
│   └── Proyecto_RappiPlus.ipynb   <- Notebook principal 
├── visualizaciones/
│   ├── Overview_Ejecutivo.png     <- Captura del Dashboard Vista General en Tableau
│   └── Vista_Detalle.png          <-  Captura del Dashboard Vista Detalle en Tableau
├── README.md                      <-  Documentación ejecutiva del proyecto

---
## 5. 📊 Principales Hallazgos

* **Rentabilidad General**: Se generaron **$3.83M USD en ventas totales** y un **Margen Neto del 30.3%** ($920,000 USD de ganancia neta).
* **Hallazgo Crítico (Ventas bajo costo)**: Se detectaron **4,378 pedidos** vendidos por debajo de su costo marginal. El producto *Laptop-Gaming-16GB* generó un **Margen Bruto de -8.6%**, acumulando **más de $300,000 USD en pérdidas directas**.
* **Top Productos en Profit**: *Vacuum-Pro-Black* ($1,496,715 USD) y *Sneakers-Urban-42* ($1,434,191 USD).
* **Distribución de Ingresos por Categoría**: La categoría **Hogar** lidera los ingresos con $3,193,018 USD, seguida de cerca por **Electrónica** ($3,172,549 USD) y **Moda** ($3,132,464 USD).
* **Punto de Abandono (Drop-off)**: El **60.39% de los usuarios que intentan pagar abandonan el checkout** (fase Intento de Pago ➔ Compra).
* **Patrón de Churn**: El **58.13% de la pérdida de usuarios ocurre en los primeros 6 días (Día 0 a W1)**. Quienes superan la primera semana mantienen una retención lineal cercana al 42%.
* **Resultado del Experimento A/B**: La prueba estadística arrojó un **$p\text{-valor} \ge 0.05$**, indicando que la nueva versión del Checkout (Tratamiento) no generó un incremento estadísticamente significativo en la conversión.

---
## 6. 💡 Conclusión del Análisis

* **Negocio y Pricing**: Se sugiere que la prioridad inmediata no es aumentar el volumen de ventas, sino **corregir la parametrización de precios y promociones** en la categoría Electrónica (*Laptop-Gaming-16GB*) para detener la fuga de margen.
* **Producto e Ingeniería**: Se debe **pausar el despliegue de la nueva UI de Checkout** ($H_0$ no rechazada) y redirigir los esfuerzos de ingeniería a resolver los problemas técnicos/fricciones en la pasarela de pago actual para mitigar el 60.39% de abandono.
* **Estrategia de Crecimiento**: Las campañas de retención y retargeting deben concentrarse de manera crítica en los **primeros 6 días post-registro** (onboarding), lugar donde se pierde a más de la mitad de la base de usuarios.



