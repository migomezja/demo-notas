# Laboratorio 3 — Ingestión de texto plano

Fuente académica (solo lectura): https://github.com/2026-2-descriptiva/std-milena-gomez-jaramillo/tree/main/LAB_03_ingestion_de_texto_plano

## Propósito
Convertir el reporte semiestructurado `data/clusters_report.txt` en un DataFrame de Pandas. Los encabezados abarcan varias líneas, hay espacios de alineación y las listas de palabras clave continúan en líneas siguientes.

## Actividad
Una función `src/pregunta_01.py::pregunta_01()`: devolver 13 filas (clústeres 1 a 13), 4 columnas: `cluster` (entero), `cantidad_de_palabras_clave` (entero), `porcentaje_de_palabras_clave` (decimal, coma convertida a punto, sin %), `principales_palabras_clave` (texto con palabras clave separadas por ', ').

## Enfoque de estudio
1. Leer líneas del reporte como texto.
2. Identificar inicios de registros por número de clúster, cantidad y porcentaje.
3. Acumular líneas de continuación en el registro vigente.
4. Normalizar espacios repetidos y espacio después de comas, preservando términos.
5. Construir DataFrame y verificar las pruebas.

## Restricciones
Usar Pandas, no modificar `data/` ni `tests/`, retornar DataFrame sin imprimir ni escribir archivos de salida desde la función.

## Estado
Revisado el enunciado, datos y pruebas; explicación introductoria iniciada. Script propuesto y explicado; ejecución y pruebas pendientes de confirmación.


## Script propuesto para pregunta_01

```python
import re
from pathlib import Path
import pandas as pd

def pregunta_01():
    ruta = Path(__file__).resolve().parents[1] / "data" / "clusters_report.txt"
    texto = ruta.read_text(encoding="utf-8")
    patron = re.compile(r"^\s*(\d+)\s+(\d+)\s+(\d+,\d+)\s*%\s*(.*)$")
    registros = []
    actual = None
    for linea in texto.splitlines():
        m = patron.match(linea)
        if m:
            if actual is not None:
                registros.append(actual)
            cluster, cantidad, porcentaje, palabras = m.groups()
            actual = {
                "cluster": int(cluster),
                "cantidad_de_palabras_clave": int(cantidad),
                "porcentaje_de_palabras_clave": float(porcentaje.replace(",", ".")),
                "fragmentos": [palabras],
            }
        elif actual is not None and linea.strip():
            actual["fragmentos"].append(linea.strip())
    if actual is not None:
        registros.append(actual)
    for registro in registros:
        texto_palabras = " ".join(" ".join(registro["fragmentos"]).split())
        palabras = [p.strip() for p in texto_palabras.split(",")]
        registro["principales_palabras_clave"] = ", ".join(palabras)
        del registro["fragmentos"]
    return pd.DataFrame(registros, columns=[
        "cluster", "cantidad_de_palabras_clave",
        "porcentaje_de_palabras_clave", "principales_palabras_clave",
    ])
```

**Prueba sugerida:** `python -m pytest LAB_03_ingestion_de_texto_plano/tests/test_activity.py -v` desde la raíz del repositorio académico. No se ha confirmado su ejecución.


## Depuración tras primera ejecución de pytest
El usuario ejecutó `test_01`: pasaron las verificaciones de clúster, cantidades y porcentajes, pero falló la primera comparación textual porque el reporte conserva un punto terminal (`partial shade.`) y la prueba exige `partial shade`. Corregir la construcción de `principales_palabras_clave` con `", ".join(palabras).rstrip(".")` para quitar el punto final del texto consolidado. Repetir pytest; resultado posterior aún no confirmado.
