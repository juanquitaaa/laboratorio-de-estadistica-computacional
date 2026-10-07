# Tiempo en pantalla y salud mental

Análisis estadístico de cómo el tiempo frente a pantallas y la calidad del sueño se relacionan con el nivel de estrés, según la ocupación de las personas.

Proyecto del ramo **Estadística Computacional** de la Universidad Técnica Federico Santa María (2026-1), desarrollado en tres entregas.

## Pregunta de investigación

> ¿En qué medida la cantidad de horas en pantalla y la calidad del sueño se relacionan con los niveles de estrés, según la ocupación de las personas?

## Datos

Se usó el dataset [Screen Time vs Mental Wellness Survey - 2025](https://www.kaggle.com/datasets/adharshinikumar/screentime-vs-mentalwellness-survey-2025) (Adharshini Kumar, Kaggle), una encuesta a **400 personas** con 15 variables: edad, género, ocupación, modalidad de trabajo, horas en pantalla (total, trabajo y ocio), horas y calidad del sueño, estrés, productividad, ejercicio, vida social e índice de bienestar mental.

El archivo no está incluido en este repositorio: se descarga desde el link de Kaggle (ver [Cómo ejecutarlo](#cómo-ejecutarlo)).

> **Nota:** el estrés, la productividad y el bienestar mental son autorreportados, no medidos con evaluaciones clínicas, por lo que pueden tener sesgo subjetivo.

## Contenido

| Notebook | Qué incluye |
|---|---|
| [`01_analisis_exploratorio.ipynb`](01_analisis_exploratorio.ipynb) | Limpieza de datos, análisis univariado y multivariado, y formulación de la pregunta de investigación. |
| [`02_estimacion_bootstrap_montecarlo.ipynb`](02_estimacion_bootstrap_montecarlo.ipynb) | Teoría de estimadores puntuales, correlaciones de Spearman por ocupación, intervalos de confianza con bootstrap y dos simulaciones Monte Carlo. |
| [`03_inferencia_regresion_modelo.ipynb`](03_inferencia_regresion_modelo.ipynb) | Retoma la estimación y el bootstrap con intervalos al 95,4%, y agrega ajuste de bondad (Kolmogorov-Smirnov), test t, test de proporciones, regresión lineal y un modelo Random Forest. |

## Métodos

- **Análisis exploratorio:** histogramas, boxplots, matriz de correlación y comparaciones entre variables.
- **Bootstrap:** remuestreo con reemplazo implementado desde cero con NumPy (10.000 iteraciones) para estimar intervalos de confianza de medias, proporciones y correlaciones.
- **Monte Carlo:** simulación del estrés por ocupación con una distribución beta (parámetros por método de los momentos) y simulación de correlaciones con una normal bivariada.
- **Pruebas de hipótesis:** test t de comparación de medias y test Z de diferencia de proporciones.
- **Regresión lineal:** implementada con la ecuación normal, θ = (XᵀX)⁻¹Xᵀy, incluyendo R², p-values y análisis de residuos.
- **Machine learning:** Random Forest con scikit-learn para predecir estrés alto (≥ 8) a partir de la ocupación, la calidad del sueño y las horas en pantalla.

## Principales resultados

- El **62%** de la muestra reporta estrés crítico (≥ 8 de 10). Por ocupación: **75%** de los estudiantes, **63%** de los empleados y **27%** de los desempleados o retirados.
- Los estudiantes tienen en promedio más estrés que los no estudiantes (test t, p ≈ 0,0004). En la simulación Monte Carlo, resultan ser el grupo con más estrés crítico en el **98%** de las simulaciones.
- Quienes usan pantallas más de 6 horas al día presentan estrés crítico en un **69%** de los casos, frente a un **7%** de quienes las usan 6 horas o menos (test de proporciones, p < 0,001).
- La correlación de Spearman entre estrés y horas en pantalla va de **0,60 a 0,71** según la ocupación.
- En la regresión lineal, cada hora adicional de pantalla se asocia a **0,59 puntos más de estrés** (R² = 0,49).
- El modelo Random Forest acierta en el **80%** de los casos del conjunto de prueba (AUC = 0,85). Las horas en pantalla concentran cerca del 80% de la importancia del modelo.

<p align="center">
  <img src="imagenes/regresion_pantalla_estres.png" alt="Regresión entre horas en pantalla y estrés" width="48%">
  <img src="imagenes/importancia_variables.png" alt="Importancia de variables en el modelo Random Forest" width="48%">
</p>

Estos resultados muestran **asociaciones**, no relaciones causales: con datos de una encuesta no es posible afirmar que el tiempo en pantalla cause el estrés.

## Tecnologías

Python · pandas · NumPy · SciPy · scikit-learn · Matplotlib · seaborn · Jupyter

## Cómo ejecutarlo

1. Clona el repositorio e instala las dependencias:

   ```bash
   git clone https://github.com/juanquitaaa/laboratorio-de-estadistica-computacional.git
   cd laboratorio-de-estadistica-computacional
   pip install -r requirements.txt
   ```

2. Descarga el dataset desde [Kaggle](https://www.kaggle.com/datasets/adharshinikumar/screentime-vs-mentalwellness-survey-2025) y deja el archivo `ScreenTime vs MentalWellness.csv` en la misma carpeta que los notebooks, sin cambiarle el nombre.

3. Abre los notebooks con `jupyter notebook` y ejecútalos en orden.

También se pueden abrir en Google Colab, subiendo el notebook junto con el CSV.

## Autores

- Juan Carlos San Martín García
- Alonso Utreras
- Cristóbal Silva

Algunos fragmentos de código para gráficos se generaron con asistentes de IA (ChatGPT y Claude). Cada caso está indicado en el notebook junto con el prompt utilizado.
