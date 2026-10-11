# LAB_02_pandas — Bitácora de estudio

Fuente académica (solo lectura): https://github.com/2026-2-descriptiva/std-milena-gomez-jaramillo/tree/main/LAB_02_pandas

## Objetivo
Resolver transformaciones, agregaciones y combinaciones tabulares con **Pandas**; funciones retornan datos, sin imprimir dentro de ellas ni escribir archivos.

## Estructura verificada
- Datos: `data/tbl0.tsv`, `data/tbl1.tsv`, `data/tbl2.tsv` (tabuladores y encabezados).
- Soluciones: `src/pregunta_01.py` a `pregunta_13.py`.
- Pruebas: `tests/test_activity.py`. La configuración cambia el directorio a la raíz del laboratorio.

## Progreso
| Pregunta | Tema | Estado |
|---|---|---|
| 01 | Número de registros en tbl0.tsv | Explicada; pendiente de ejecución |
| 02 | Número de columnas en tbl0.tsv | Explicada; pendiente de ejecución |
| 03 | Frecuencias de c1 con value_counts | Explicada; pendiente de ejecución |
| 04 | Promedio de c2 por categoría c1 | Explicada; pendiente de ejecución |
| 05–13 | Pandas: transformaciones y agregaciones | Pendientes |

## Pregunta 01 — Número de registros
Enunciado: ¿Cuántos registros tiene `data/tbl0.tsv`? Retornar un entero.

Solución propuesta:
```python
import pandas as pd

def pregunta_01():
    ruta = r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_02_pandas\data\tbl0.tsv"
    df = pd.read_csv(ruta, sep="\t")
    cantidad = len(df)
    return int(cantidad)
```

Resultado esperado de las pruebas: **40**.

Explicación Feynman: `read_csv` carga TSV al especificar `sep="\t"`; `DataFrame` es una tabla; `len(df)` cuenta filas sin el encabezado. Pregunta de repaso: ¿por qué usamos `sep="\t"` y qué devuelve `len(df)`?

**Estado:** el código fue presentado, aún no hay ejecución confirmada del estudiante.


## Pregunta 02 — Número de columnas
Enunciado: ¿Cuántas columnas tiene `data/tbl0.tsv`? Retornar entero.

```python
import pandas as pd

def pregunta_02():
    ruta = r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_02_pandas\data\tbl0.tsv"
    df = pd.read_csv(ruta, sep="\t")
    cantidad = len(df.columns)
    return int(cantidad)
```

Resultado esperado: **4**. Feynman: `len(df)` cuenta filas; `len(df.columns)` cuenta columnas; `df.shape` devuelve (filas, columnas). **Pendiente:** ejecución por estudiante. Pregunta de comprobación: si un DataFrame tiene 10 filas y 3 columnas, ¿qué devuelven `len(df)` y `len(df.columns)`?


## Pregunta 03 — Frecuencias por categoría de c1
Enunciado: contar registros por categoría de `c1` en `data/tbl0.tsv`, devolver una **Serie Pandas** con índice alfabético.

```python
import pandas as pd

def pregunta_03():
    ruta = r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_02_pandas\data\tbl0.tsv"
    df = pd.read_csv(ruta, sep="\t")
    frecuencias = df["c1"].value_counts()
    return frecuencias.sort_index()
```

Resultado esperado: A=8, B=7, C=5, D=6, E=14 (total 40).

**Feynman:** `df["c1"]` selecciona una Serie; `value_counts()` cuenta ocurrencias y por defecto ordena por frecuencia; `sort_index()` ordena las etiquetas alfabéticamente. Distinguir contar registros de sumar valores de `c2`.

**Pregunta de repaso:** ¿por qué usamos `sort_index()` en lugar de `sort_values()`?

**Estado:** solución explicada, ejecución pendiente de confirmar.


## Pregunta 04 — Promedios por categoría
Enunciado: calcular media de `c2` agrupando por `c1` en `data/tbl0.tsv`, retornar Serie de Pandas ordenada alfabéticamente.

```python
import pandas as pd

def pregunta_04():
    ruta = r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_02_pandas\data\tbl0.tsv"
    df = pd.read_csv(ruta, sep="\t")
    promedios = df.groupby("c1")["c2"].mean()
    return promedios.sort_index()
```

Resultados esperados: A=4.6250, B=5.1429, C=5.4000, D=3.8333, E=4.7857 (aproximaciones a cuatro decimales; sin redondeo necesario).

**Feynman:** `groupby("c1")` forma grupos por categoría; `["c2"]` elige la variable cuantitativa; `mean()` calcula la media dentro de cada grupo; `sort_index()` ordena etiquetas. Diferencia con pregunta 03: frecuencia frente a media.

**Pregunta de repaso:** si A tiene valores 2, 6 y 7, ¿cuál es su media? ¿Qué cambiaría si usáramos `sum()` en vez de `mean()`?

**Estado:** explicación entregada, ejecución pendiente de confirmar.
