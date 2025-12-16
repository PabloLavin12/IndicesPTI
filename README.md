# Cálculo de Índices Agroclimáticos para la PTI

## Descripción del Proyecto

Este repositorio contiene los flujos de trabajo y scripts desarrollados para el cálculo y análisis de índices agroclimáticos en el marco de la **Plataforma Temática Interdisciplinar (PTI)**.

El objetivo principal es la generación de indicadores climáticos de impacto para el sector agrícola, utilizando sistemas de predicción estacional y técnicas de corrección de sesgo para garantizar la fiabilidad de los datos.

## Metodología y Datos

El flujo de trabajo se basa en el uso de datos de predicción estacional del **Centro Europeo de Previsiones Meteorológicas a Plazo Medio (ECMWF)**, específicamente el modelo **System 5 (SEAS5)**.

### Fuentes de Datos

* **Modelo (Predicción):** ECMWF SEAS5.
  * **Hindcast:** Periodo 1981 - 2016.
  * **Forecast:** Periodo 2017 - 2022.
  * **Resolución Temporal:** Diaria.
  * **Resolución Espacial:** 1º (aproximadamente 100 km).
* **Observaciones (Referencia):** Reanálisis ERA5.
  * **Resolución Original:** 0.25º.
  * **Preprocesamiento:** Interpolación a la resolución del modelo (1º) para permitir la comparativa y corrección.

### Procesamiento

1. **Corrección de Sesgo (Bias Correction):** Se aplica el método **EQM (Empirical Quantile Mapping)** para corregir las variables de temperatura y precipitación del modelo SEAS5, utilizando ERA5 interpolado como referencia observacional.
2. **Cálculo de Índices:** Se utiliza el framework de `climate4R` en R. Específicamente, se emplea la función `agroindexGrid` del paquete `climate4R.agro`.

## Índices Agroclimáticos

A continuación se detallan los índices calculados, sus definiciones y los periodos de análisis considerados.

| Código | Índice | Descripción y Definición Técnica | Periodo / Umbrales |
| :--- | :--- | :--- | :--- |
| **ATD** | Amplitud Térmica Diaria | Diferencia entre la temperatura máxima y mínima diaria. Es un indicador clave para cultivos como la vid y los cítricos. | **01 Jul - 31 Oct** |
| **CGDD_S** | Grados Día (Verano) | *Cumulative Growing Degree Days*. Suma de grados día diarios. Se define como la diferencia entre la Tª media diaria y la Tª base (10ºC) siempre que la media sea superior a esta. | **01 Abr - 31 Oct**<br>Base: > 10ºC |
| **CGDD_W** | Grados Día (Invierno) | *Cumulative Growing Degree Days*. Suma de grados día diarios. Se define como la diferencia entre la Tª media diaria y la Tª base (5ºC) siempre que la media sea superior a esta. *Calculado mensualmente*. | **01 Nov - 31 Jul**<br>Base: > 5ºC |
| **NTS** | Estrés Térmico | *Number of Thermal Stress days*. Número de días con temperatura máxima por encima del umbral de estrés (28ºC). Periodo indicado por AEMET. | **01 Ene - 15 Jun**<br>Tmax ≥ 28ºC |
| **NFD** | Heladas | *Number of Frost Days*. Número de días con temperatura mínima por debajo de 0ºC. | **01 Ene - 15 Jun**<br>Tmin < 0ºC |
| **NPD_S** | Precipitación (Verano) | *Number of Precipitating Days*. Número de días con precipitación diaria superior a 0 mm. | **01 Abr - 31 Oct**<br>Precip > 0 mm |
| **NPD_W** | Precipitación (Invierno) | *Number of Precipitating Days*. Número de días con precipitación diaria superior a 0 mm. *Calculado mensualmente*. | **01 Nov - 31 Jul**<br>Precip > 0 mm |

## Tecnologías y Herramientas

El análisis se ha llevado a cabo utilizando el ecosistema de **R** y las herramientas del **Santander Meteorology Group**:

* [climate4R](https://github.com/SantanderMetGroup/climate4R): Framework para acceso y post-procesamiento de datos climáticos.
* `climate4R.agro`: Paquete específico para el cálculo de índices sectoriales.
* `downscaleR`: Utilizado para las técnicas de corrección de sesgo (EQM).

## Autoría

Este proyecto ha sido desarrollado por *Pablo Lavín Pellón*.

## Licencia

Este repositorio se distribuye bajo la licencia MIT. Consulta el archivo LICENSE para más detalles.