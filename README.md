# Análisis de Rendimiento y Negocio de RappiPlus

## Descripción del Proyecto

Este proyecto evalúa el desempeño del servicio de suscripción RappiPlus mediante el procesamiento de datos de extremo a extremo y modelado analítico. Al integrar datos transaccionales, métricas de marketing, costos de catálogo y resultados de pruebas A/B, este análisis busca identificar los principales factores de ingresos, optimizar la inversión en marketing y proporcionar recomendaciones estratégicas de negocio para el próximo año fiscal.

## Conjuntos de Datos Utilizados

* **`rappiplus_orders_raw.csv`**: Datos transaccionales que incluyen detalles de pedidos, ingresos brutos, precios base y descuentos aplicados.

* **`rappiplus_catalog.csv`**: Detalles del catálogo de productos, costos unitarios, categorías de productos e información de proveedores.

* **`rappiplus_marketing_spend.csv`**: Inversión en adquisición y retención desglosada por canal de marketing y país.

* **Registros de Usuarios y Eventos en SQL (`events`, `users`, `user_activity`)**: Eventos de navegación, perfiles demográficos de usuarios y registros de interacción.

* **`experiment_checkout_ui.csv`**: Datos experimentales de una prueba A/B aleatorizada para evaluar tasas de conversión en variaciones de la interfaz de usuario del proceso de pago.

## Metodología y Flujo de Trabajo

### 1. Limpieza de Datos y Control de Calidad

* Exploración de conjuntos de datos mediante `pandas` y `numpy`.

* Conversión de campos de fecha y hora a formatos ISO estandarizados.

* Gestión de valores nulos mediante referencias cruzadas con catálogos y estrategias de imputación.

* Cálculo de métricas operativas derivadas (precio unitario, cantidad de artículos, descuentos netos).

### 2. Análisis Exploratorio de Datos (EDA) y Detección de Outliers

* Aplicación del método del Rango Intercuartílico (IQR) para identificar de manera sistemática anomalías extremas en las variables de cantidad y descuentos.

* Visualización de distribuciones mediante diagramas de caja (*boxplots*) e histogramas con `seaborn` para garantizar la integridad estadística.

```python
# Detección de outliers mediante el método IQR
Q1 = df['discount'].quantile(0.25)
Q3 = df['discount'].quantile(0.75)
IQR = Q3 - Q1
filtered_df = df[~((df['discount'] < (Q1 - 1.5 * IQR)) | (df['discount'] > (Q3 + 1.5 * IQR)))]
```

### 3. Pruebas A/B y Analítica con SQL

* Análisis de embudos de conversión y patrones de retención mediante consultas complejas en SQL (`JOIN`, `GROUP BY`, Funciones de Ventana).

* Evaluación de la significancia estadística para el experimento de interfaz de usuario en la pantalla de pago (`experiment_checkout_ui.csv`) para validar el incremento en conversión.

## Hallazgos Clave de Negocio

* **Impacto de Descuentos**: Identificación de límites en los umbrales de descuento para evitar la erosión del margen sin afectar la tasa de conversión.

* **Eficiencia del Marketing**: Determinación de los canales de marketing de alto rendimiento con base en el ROI por región operativa.

* **Resultados de Pruebas A/B**: Validación de la variante ganadora en la interfaz de pago para mejorar la conversión general del embudo.

## Tecnologías Utilizadas

* **Lenguaje:** Python

* **Librerías:** Pandas, NumPy, Matplotlib, Seaborn, SciPy

* **Consultas de Base de Datos:** SQL

* **Herramientas:** Jupyter Notebook / VS Code, Git/GitHub