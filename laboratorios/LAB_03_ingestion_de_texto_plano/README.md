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
Revisado el enunciado, datos y pruebas; explicación introductoria iniciada. Solución y ejecución pendientes de estudio y comprobación.
