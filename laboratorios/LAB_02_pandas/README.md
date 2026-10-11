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
| 02–13 | Pandas: transformaciones y agregaciones | Pendientes |

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
