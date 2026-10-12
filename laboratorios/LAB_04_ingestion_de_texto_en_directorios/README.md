# Laboratorio 4 — Ingestión de texto en directorios

Fuente académica (solo lectura): https://github.com/2026-2-descriptiva/std-milena-gomez-jaramillo/tree/main/LAB_04_ingestion_de_texto_en_directorios

## Objetivo
Recorrer `data/train` y `data/test`, cada una con carpetas `negative`, `neutral` y `positive`. Cada archivo .txt contiene una frase. Construir `submission/train_dataset.csv` y `submission/test_dataset.csv` con columnas `phrase` y `target`, recorriendo carpetas y archivos alfabéticamente, limpiando espacios exteriores y sin guardar índice.

## Cantidades esperadas según tests
- train: negative 236, neutral 1117, positive 458; total 1811.
- test: negative 67, neutral 274, positive 112; total 453.

## Script propuesto
```python
from pathlib import Path
import pandas as pd

def pregunta_01():
    laboratorio = Path(__file__).resolve().parents[1]
    carpeta_datos = laboratorio / "data"
    carpeta_salida = laboratorio / "submission"
    carpeta_salida.mkdir(parents=True, exist_ok=True)

    for division in ["train", "test"]:
        registros = []
        ruta_division = carpeta_datos / division
        for carpeta_categoria in sorted(ruta_division.iterdir()):
            if not carpeta_categoria.is_dir():
                continue
            categoria = carpeta_categoria.name
            for archivo in sorted(carpeta_categoria.glob("*.txt")):
                frase = archivo.read_text(encoding="utf-8").strip()
                registros.append({"phrase": frase, "target": categoria})
        df = pd.DataFrame(registros, columns=["phrase", "target"])
        ruta_csv = carpeta_salida / f"{division}_dataset.csv"
        df.to_csv(ruta_csv, index=False, encoding="utf-8")
```

## Conceptos
`Path(__file__).resolve().parents[1]`, `iterdir()`, `sorted()`, `glob("*.txt")`, `read_text()`, `strip()`, `pd.DataFrame()`, `to_csv(index=False)`.

## Validación
Desde la raíz del repositorio: `python -m pytest LAB_04_ingestion_de_texto_en_directorios/tests/test_activity.py -v`.

**Estado:** solución propuesta y explicada; ejecución local y test aún no confirmados.
