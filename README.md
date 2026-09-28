# Data Science Project: Análisis y Predicción de Ausentismo en la Administración Pública

[![Python 3.14+](https://img.shields.io/badge/python-3.14+-blue.svg)](https://www.python.org/downloads/)
[![Pandas](https://img.shields.io/badge/pandas-1.5+-150458.svg)](https://pandas.pydata.org/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-1.0+-F7931E.svg)](https://scikit-learn.org/)

Este repositorio contiene un proyecto end-to-end de Ciencia de Datos orientado al **Análisis Exploratorio (EDA)** y la **Modelación Predictiva del Ausentismo Laboral** en el ámbito de la administración pública. 

A través del procesamiento y la ingeniería de características (*Feature Engineering*) sobre registros masivos de licencias, el proyecto busca identificar patrones clave de ausentismo y entrenar modelos capaces de estimar el volumen, riesgo y duración de las inasistencias.

---

## <span style="font-size: 26px; font-weight: bold; color: #0d3c6c;">Equipo de trabajo Nro 15</span>
<ul>
  <li style="color: #81c6d2;"><b>Fabiana Winterstetter</b></li>
  <li style="color: #81c6d2;"><b>Nicolás Germán Diaz</b></li>
  <li style="color: #81c6d2;"><b>Nadir Nahuel Quiroga</b></li>
   
</ul>

---

## 📋 Tabla de Contenidos

- [Descripción del Dataset](#-descripción-del-dataset)
- [Objetivos del Proyecto](#-objetivos-del-proyecto)
- [Ingeniería de Variables (Feature Engineering)](#-ingeniería-de-variables-feature-engineering)
- [Modelos Predictivos Propuestos](#-modelos-predictivos-propuestos)

---

## 📊 Descripción del Dataset

El conjunto de datos (`prueba2025_b.csv`) contiene **949,038 registros históricos** de licencias y ausencias de agentes públicos con 16 variables originales sin valores nulos:

| Variable | Descripción |
| :--- | :--- |
| `Nro legajo` | Identificador único del agente/empleado. |
| `Escalafon` | Agrupamiento o carrera dentro de la administración pública. |
| `Categoría` | Categoría o clase dentro del escalafón de la administración pública. |
| `Cod Art ausencia` | Código del artículo de la licencia según la normativa laboral. |
| `Descripcion articulo ausencia` | Detalle o motivo de la ausencia (ej. *Enfermedad Común*, *Razones Particulares*). |
| `Es de Salud?` | Flag categórico (`yes` / `no`) para licencias de índole médica. |
| `Fecha Desde` / `Fecha Hasta` | Periodo de inicio y fin de la licencia tomada. |
| `Cantidad dias` | Días corridos de duración de la ausencia. |
| `Cant Dias Permitido Mes/Año` | Límites normativos de días permitidos por periodo. |
| `Dependencia` | Oficina o área de trabajo del agente. |
| `Año Nacimiento` / `Genero` | Datos demográficos del agente. |
| `Género (Sexo)` |  |
| `Antigüedad` | Años de servicio prestados por el agente. |
| `Remuneración Mensual` | Sueldo que percibe el agente mensualmente. |

---

## 🎯 Objetivos del Proyecto

1. **Análisis Exploratorio de Datos (EDA):** Identificar la estacionalidad, los artículos de licencia más solicitados y las métricas de ausentismo según rango etario, género, antigüedad y dependencia.
2. **Feature Engineering Temporal y Acumulado:** Derivar variables continuas y categóricas a partir de los datos históricos de cada legajo.
3. **Predicción de Riesgo de Alto Ausentismo (Clasificación):** Identificar agentes con alta probabilidad de superar el umbral crítico de inasistencias en el año.
4. **Estimación de Duración de Licencias (Regresión):** Predecir la cantidad de días que abarcará una licencia médica o personal para mejorar la planificación operativa y cobertura de servicios.

---

## 💡 Ingeniería de Variables (Feature Engineering)

El pipeline de preparación transforma el dataset original agregando las siguientes dimensiones de análisis:

* **Variables Temporales y Estacionales:**
  * `Edad_Agente`: Edad calculada al momento del evento.
  * `Mes_Inicio` y `Trimestre`: Estacionalidad anual (picos invernales / fin de año).
  * `Es_Fin_De_Semana_Adyacente`: Indicador de inicio en día Lunes/Viernes ("efecto puente").
* **Variables Históricas Acumuladas por Agente:**
  * `Dias_Desde_Ultima_Ausencia`: Intervalo de días desde la última inasistencia registrada.
  * `Num_Licencias_Previas_Agente`: Recuento de licencias acumuladas en el histórico.
  * `Dias_Ausencia_Acumulados_Año`: Acumulado de días ausentes consumidos a la fecha.
  * `Tasa_Uso_Cupo_Anual`: Porcentaje del cupo normativo anual consumido.
* **Agregaciones Organizacionales:**
  * `Promedio_Dias_Dependencia`: Promedio de inasistencias por área de trabajo.
  * `Promedio_Dias_Escalafon`: Promedio de días ausentes según escalafón laboral.

---

## 🤖 Modelos Predictivos Propuestos

1. **Supervised Classification (Alto Riesgo de Ausentismo):**
   * *Algoritmos:* XGBoost, LightGBM, Random Forest.
   * *Métricas:* ROC-AUC, F1-Score, Precision-Recall Curve.
2. **Regression Models (Duración del Ausentismo):**
   * *Algoritmos:* LightGBM Regressor, CatBoost, Ridge Regression.
   * *Métricas:* RMSE, MAE, $R^2$.
3. **Análisis de Supervivencia / Reincidencia:**
   * *Algoritmos:* Cox Proportional Hazards Model.
   * *Métricas:* Concordance Index (C-index).

---

