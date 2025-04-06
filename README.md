# Análisis ETL de Datos de la Fuerza Laboral en EE. UU. (1995-2011)

Este script de Python implementa un proceso de Extracción, Transformación y Carga (ETL) para analizar datos de la fuerza laboral en Estados Unidos durante el período de 1995 a 2011. El objetivo principal es limpiar, integrar y explorar un conjunto de datos principal con información sobre la fuerza laboral y el programa Wagner Peyser, complementándolo con datos económicos externos como ingresos, PIB e índices de desempleo.

## Requisitos Previos

Este código está diseñado para ejecutarse en el entorno de **Google Colaboratory (Colab)** debido a su dependencia del montaje de Google Drive para acceder a los archivos. Asegúrate de tener las siguientes bibliotecas de Python instaladas o disponibles en tu entorno de Colab:

* **pandas:** Para la manipulación y análisis de datos tabulares.
* **matplotlib:** Para la creación de gráficos y visualizaciones.
* **numpy:** Para operaciones numéricas y matriciales.
* **seaborn:** Para la creación de visualizaciones estadísticas atractivas.
* **scipy:** Para realizar pruebas estadísticas y operaciones científicas.
* **ydata-profiling:** Para generar informes de perfilamiento de datos (se instala durante la ejecución).

## Fuentes de Datos

El script utiliza los siguientes archivos CSV, que deben estar ubicados en la raíz de tu Google Drive dentro de la carpeta "My Drive/":

1.  **CSV Datos.csv:** Contiene el conjunto de datos principal con información trimestral a nivel estatal sobre la fuerza laboral, el empleo, el desempleo y la participación en el programa Wagner Peyser.
2.  **Complementario IMPH.csv:** Proporciona datos anuales sobre el ingreso medio por habitante en EE. UU.
3.  **Complementario PIB.csv:** Ofrece datos anuales sobre el Producto Interno Bruto (PIB) per cápita en EE. UU.
4.  **Complementario indice desempleo.csv:** Contiene datos mensuales sobre el índice de desempleo general en EE. UU.
5.  **Complementario indice desempleo latinos.csv:** Contiene datos mensuales sobre el índice de desempleo para la población latina en EE. UU.

## Proceso ETL Detallado

1.  **Extracción:**
    * Montaje de Google Drive para acceder a los archivos.
    * Importación de las bibliotecas necesarias.
    * Lectura del archivo "CSV Datos.csv" al DataFrame `df_dataset`.
    * Lectura de los archivos complementarios al inicio del script.

2.  **Transformación:**
    * **Limpieza del DataFrame principal (`df_dataset`):**
        * Eliminación y reemplazo de encabezados de columna para una mejor manipulación.
        * Creación de la columna calculada "Mujeres candidatas al programa Wagner Peyser".
        * Obtención de un resumen de la información del DataFrame y guardado en un archivo Excel.
        * Conversión de tipos de datos de columnas numéricas a enteros, llenando previamente los valores nulos con cero.
        * Verificación de la coherencia de los datos numéricos (por ejemplo, la relación entre la fuerza laboral total, empleados y desempleados).
        * Detección de valores nulos y de registros con estados o años inválidos según listas predefinidas.
        * Identificación y exportación de datos anómalos a un archivo CSV.
    * **Transformación de los DataFrames complementarios:**
        * Asignación de nombres de columna descriptivos.
        * Conversión de la columna "Fecha" al tipo datetime.
        * Extracción del año de la columna "Fecha" para facilitar la integración.
    * **Generación de un perfil de datos exploratorio** utilizando la biblioteca `ydata-profiling` para obtener una visión general de la calidad y las características de los datos.
    * **Imputación de valores faltantes** en la columna "GDP Trimestre" del DataFrame principal utilizando la media.
    * **Agrupación y agregación de datos** del DataFrame principal por año (considerando el último trimestre para algunas métricas) para obtener resúmenes anuales de la fuerza laboral y la participación en el programa Wagner Peyser.

3.  **Carga e Integración:**
    * **Fusión de los DataFrames agregados** del conjunto de datos principal para crear un resumen nacional por año.
    * **Integración de los datos complementarios** (ingresos, PIB, desempleo) al DataFrame resumen utilizando la columna "Año" como clave de unión.
    * **Imputación de los valores nulos restantes** en el DataFrame final integrado utilizando la media de cada columna numérica.

4.  **Análisis y Visualización:**
    * Generación de diversas visualizaciones utilizando Matplotlib y Seaborn para explorar las tendencias de la fuerza laboral, el empleo y su relación con el programa Wagner Peyser y los indicadores económicos.
    * Realización de una prueba de Shapiro-Wilk para evaluar la normalidad de las variables numéricas.
    * Cálculo y visualización de la matriz de correlación para identificar las relaciones entre las diferentes variables del conjunto de datos integrado.

## Estructura de archivos y carpetas

    ETL - PROJECT/
    ├── 1995-2011PWSD.xlsx
    ├── Codigo.ipynb
    ├── Complementario IMPH.csv
    ├── Complementario indice desempleo latinos.csv
    ├── Complementario indice desempleo.csv
    ├── Complementario PIB.csv
    ├── ETL - PROCCESS.jpg
    └── README.md

## Librerías Utilizadas

* pandas
* matplotlib.pyplot
* numpy
* seaborn
* sys
* io
* re
* scipy.stats
* ydata_profiling

## Salida del Script

El script genera las siguientes salidas principales:

* **Impresiones en consola:** Vistas previas de los DataFrames, resúmenes estadísticos, información de los datos, detección de anomalías y resultados de las agregaciones.
* **Archivos CSV:** `dataset_sin_encabezado.csv` (dataset sin encabezados), `datos_anomalos_detectados.csv` (registros con anomalías).
* **Archivo Excel:** `df_info.xlsx` (información detallada sobre las columnas del DataFrame principal).
* **Gráficos:** Varias visualizaciones generadas con Matplotlib y Seaborn que muestran tendencias, distribuciones y correlaciones.
* **Informe de Perfilamiento de Datos:** Un informe interactivo generado por `ydata-profiling` que proporciona un análisis detallado del DataFrame principal.
