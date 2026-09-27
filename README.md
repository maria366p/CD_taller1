# Taller 1 – Ciencia de Datos Aplicada

Análisis exploratorio de contratos públicos de bienes registrados en el SECOP, orientado a identificar características asociadas con desviaciones en la ejecución contractual que puedan apoyar la focalización de la supervisión.

**Autores:** María Paula Ospina (202123208), Andrés Camilo Beltrán (202511522)

## Datos

- **Fuente:** `secop_bienes.parquet` — 196.391 contratos de bienes, 36 atributos.
- **Periodo:** 2019–2025 (cobertura temporal validada como completa).
- **Variables clave:** `valor_del_contrato`, `dias_adicionados`, `valor_pendiente_de_pago`, `modalidad_de_contratacion`, `liquidacion`, `sector`, `destino_gasto`.

## Contenido del notebook

1. **Entendimiento inicial de datos**: inspección de la estructura, cobertura temporal, diagnóstico de calidad (nulos, "No Definido", duplicados, consistencia de fechas y montos) y tratamiento conservador de inconsistencias (se documentan y se excluyen solo de los análisis específicos donde afectan el resultado, sin imputar ni eliminar registros). Análisis univariado de los 5 atributos seleccionados.
2. **Estrategia de análisis**: definición de tres señales de desviación (adición de plazo, porcentaje pendiente de pago en contratos finalizados, contratos finalizados sin liquidar) y del enfoque estadístico (medianas/cuantiles, tablas cruzadas, correlación de Spearman, pruebas de hipótesis con α = 0,05).
3. **Desarrollo de la estrategia**: construcción de las variables de desviación, análisis bivariado (modalidad, sector y destino del gasto vs. cada señal) y multivariado (matriz de correlación de Spearman), con contraste de hipótesis para las relaciones cuantitativas.

## Hallazgos principales

- Las variables monetarias (`valor_del_contrato`, `valor_pendiente_de_pago`) son extremadamente asimétricas; la mediana y el IQR describen mejor su comportamiento que la media.
- Solo el 9,51% de los contratos presenta adición de plazo, pero cuando ocurre puede ser considerable.
- La **modalidad de contratación** es el criterio más discriminante: Licitación pública concentra la mayor proporción de adiciones de plazo, mientras que Contratación directa y Contratación régimen especial concentran las mayores medianas de saldo pendiente y las mayores proporciones de contratos finalizados sin liquidar.
- El **sector** (destaca Trabajo) aporta señal adicional en adiciones de plazo; **destino del gasto** aporta información complementaria pero más débil.
- Las asociaciones entre variables cuantitativas (valor del contrato, días adicionados, % pendiente) son estadísticamente significativas pero de magnitud muy baja (Spearman < 0,2), por lo que no son criterios fuertes de manera aislada.
- Conclusión: la focalización de la supervisión debería combinar variables categóricas (modalidad, sector) con el valor del contrato, en lugar de depender de un único indicador.

> Todas las relaciones encontradas se interpretan como asociaciones descriptivas, no como evidencia de causalidad ni de irregularidad.

## Requisitos

```
pandas
numpy
matplotlib
seaborn
scipy
```

## Uso

```bash
jupyter notebook taller1.ipynb
```

El notebook espera el archivo `secop_bienes.parquet` en el mismo directorio.
