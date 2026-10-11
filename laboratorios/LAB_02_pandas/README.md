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
| 05 | Máximo de c2 por categoría c1 | Explicada; pendiente de ejecución |
| 06 | Valores únicos de c4, mayúsculas y orden alfabético | Explicada; pendiente de ejecución |
| 07 | Suma de c2 por categoría c1 | Explicada; pendiente de ejecución |
| 08 | Nueva columna suma = c0 + c2 | Explicada; pendiente de ejecución |
| 09 | Extraer año textual de c3 | Explicada; pendiente de ejecución |
| 10 | Agrupar, ordenar y concatenar c2 | Explicada; pendiente de ejecución |
| 11 | Agrupar letras c4 por c0 | Explicada; pendiente de ejecución |
| 12–13 | Pandas: transformaciones y agregaciones | Pendientes |

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


## Pregunta 05 — Máximos por categoría
Enunciado: hallar máximo de `c2` agrupando por `c1` en `data/tbl0.tsv`; devolver Serie de Pandas con índice alfabético.

```python
import pandas as pd

def pregunta_05():
    ruta = r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_02_pandas\data\tbl0.tsv"
    df = pd.read_csv(ruta, sep="\t")
    maximos = df.groupby("c1")["c2"].max()
    return maximos.sort_index()
```

Resultados esperados: A=9, B=9, C=9, D=7, E=9.

**Feynman:** `groupby("c1")` forma grupos; `["c2"]` selecciona la variable; `max()` toma el valor mayor de cada grupo; `sort_index()` ordena alfabéticamente. A diferencia de `mean()`, no calcula un promedio.

**Estado:** explicada; ejecución no confirmada.


## Pregunta 06 — Valores únicos de c4
Enunciado: usar `data/tbl1.tsv` para obtener valores distintos de `c4`, pasarlos a mayúsculas y retornar lista ordenada alfabéticamente.

```python
import pandas as pd

def pregunta_06():
    ruta = r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_02_pandas\data\tbl1.tsv"
    df = pd.read_csv(ruta, sep="\t")
    valores_unicos = df["c4"].unique()
    valores_mayusculas = [valor.upper() for valor in valores_unicos]
    return sorted(valores_mayusculas)
```

Resultado esperado: `["A", "B", "C", "D", "E", "F", "G"]`.

**Feynman:** `unique()` quita duplicados; `upper()` convierte texto a mayúsculas; `sorted()` devuelve una lista ordenada. Alternativa: `sorted(df["c4"].str.upper().unique().tolist())`.

**Estado:** explicada, ejecución no confirmada.


## Pregunta 07 — Sumas por categoría
Enunciado: sumar `c2` para cada categoría de `c1` en `data/tbl0.tsv`; devolver Serie de Pandas ordenada alfabéticamente.

```python
import pandas as pd

def pregunta_07():
    ruta = r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_02_pandas\data\tbl0.tsv"
    df = pd.read_csv(ruta, sep="\t")
    sumas = df.groupby("c1")["c2"].sum()
    return sumas.sort_index()
```

Resultado esperado: A=37, B=36, C=27, D=23, E=67.

**Feynman:** `groupby("c1")` forma grupos; `["c2"]` selecciona la columna; `sum()` acumula los valores dentro de cada grupo; `sort_index()` ordena categorías. Contrastar con `mean()`, `max()` y `value_counts()`.

**Estado:** explicada, ejecución no confirmada.


## Pregunta 08 — Columna calculada por fila
Enunciado: retornar `data/tbl0.tsv` completa con una columna adicional al final, `suma`, igual a `c0 + c2` para cada fila. Se retorna un **DataFrame** (40 filas, 5 columnas), no una Serie.

```python
import pandas as pd

def pregunta_08():
    ruta = r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_02_pandas\data\tbl0.tsv"
    df = pd.read_csv(ruta, sep="\t")
    df["suma"] = df["c0"] + df["c2"]
    return df
```

Primeras filas de `suma`: 1, 3, 7, 6. **Feynman:** suma elemento a elemento (vectorizada), diferente de `df["c2"].sum()` y de `df.groupby("c1")["c2"].sum()`. La asignación a columna inexistente la crea al final.

**Estado:** explicada; ejecución pendiente de confirmar.


## Pregunta 09 — Año como texto
Enunciado: retornar `data/tbl0.tsv` completa con columna `year` al final, extrayendo los primeros cuatro caracteres de `c3` (formato AAAA-MM-DD). El año debe ser **texto**.

```python
import pandas as pd

def pregunta_09():
    ruta = r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_02_pandas\data\tbl0.tsv"
    df = pd.read_csv(ruta, sep="\t")
    df["year"] = df["c3"].str[:4]
    return df
```

Ejemplos: `1999-02-28` → `"1999"`; `1998-05-02` → `"1998"`. Resultado: DataFrame de 40 filas y 5 columnas. `.str[:4]` conserva texto, mientras que `pd.to_datetime(...).dt.year` produce años numéricos.

**Estado:** explicada; ejecución no confirmada.


## Pregunta 10 — Concatenación de valores por categoría
Enunciado: por cada categoría de `c1` en `data/tbl0.tsv`, ordenar los valores de `c2` numéricamente, unirlos con `:` y retornar **DataFrame** con índice de categorías alfabéticas y una única columna `c2`.

```python
import pandas as pd

def pregunta_10():
    ruta = r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_02_pandas\data\tbl0.tsv"
    df = pd.read_csv(ruta, sep="\t")
    resultado = df.groupby("c1")["c2"].apply(
        lambda valores: ":".join(str(valor) for valor in sorted(valores))
    )
    return resultado.sort_index().to_frame(name="c2")
```

Ejemplos del enunciado: A=`1:1:2:3:6:7:8:9`, B=`1:3:4:5:6:8:9`, C=`0:5:6:7:9`.

**Feynman:** `apply()` transforma cada grupo con función propia; `sorted()` ordena números antes de convertirlos a texto; `str()` permite usar `join()`; `to_frame(name="c2")` garantiza DataFrame de una columna. Conservar valores repetidos.

**Estado:** explicada, ejecución no confirmada.


## Pregunta 11 — Concatenar letras por identificador
Enunciado: en `data/tbl1.tsv`, una fila por `c0` ascendente, columnas `c0` y `c4`; en `c4`, letras de cada identificador ordenadas y separadas por comas.

```python
import pandas as pd

def pregunta_11():
    ruta = r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_02_pandas\data\tbl1.tsv"
    df = pd.read_csv(ruta, sep="\t")
    resultado = df.groupby("c0")["c4"].apply(
        lambda letras: ",".join(sorted(letras))
    )
    return resultado.reset_index().sort_values("c0")
```

Ejemplos: `0 → b,f,g`, `1 → a,c,f`, `2 → a,c,e,f`. Resultado: DataFrame 40×2, columnas `c0` y `c4`.

**Feynman:** `groupby("c0")` crea grupos; `sorted()` ordena letras; `join()` concatena; `reset_index()` recupera `c0` como columna. Diferencia con pregunta 10: allí se exige categoría como índice.

**Estado:** explicada, ejecución no confirmada.
