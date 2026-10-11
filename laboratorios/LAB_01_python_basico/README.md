# Laboratorio 01 — Python básico

## Propósito
Construir resúmenes descriptivos reproducibles a partir de un archivo tabulado y comprimido con gzip, **usando solo Python estándar**.

## Referencias
- [Enunciado del laboratorio](https://github.com/2026-2-descriptiva/std-milena-gomez-jaramillo/blob/main/LAB_01_python_basico/README.md)
- [Scripts de preguntas](https://github.com/2026-2-descriptiva/std-milena-gomez-jaramillo/tree/main/LAB_01_python_basico/src)
- [Pruebas automáticas](https://github.com/2026-2-descriptiva/std-milena-gomez-jaramillo/blob/main/LAB_01_python_basico/tests/test_activity.py)

## Datos y restricciones
El archivo `data/data.csv.gz` contiene registros tabulados sin encabezado, con cinco campos: `letter`, `value`, `date`, `codes` y `metrics`. Las fechas tienen formato `YYYY-MM-DD`; los códigos se separan por comas; las métricas son pares `clave:valor`. No usar pandas, numpy, scipy ni bibliotecas externas.

## Ruta de aprendizaje
| Pregunta | Objetivo | Estado | Evidencia |
| --- | --- | --- | --- |
| 01 | Suma de value | En estudio | Propuesta de código, pendiente de ejecución y explicación propia |
| 02 | Conteos por letter | Pendiente | — |
| 03 | Sumas por letter | Pendiente | — |
| 04 | Registros por mes | Pendiente | — |
| 05 | Mínimo y máximo por letter | Pendiente | — |
| 06 | Mínimo y máximo por clave de metrics | Pendiente | — |
| 07 | Letras por valor, con repeticiones | Pendiente | — |
| 08 | Letras únicas por valor | Pendiente | — |
| 09 | Conteo de claves metrics | Pendiente | — |
| 10 | Cantidad de codes y metrics por fila | Pendiente | — |
| 11 | Suma de value por code | Pendiente | — |
| 12 | Suma de metrics por letter | Pendiente | — |

## Método Feynman
1. Estudiar un concepto de Python presente en el ejercicio.
2. Explicarlo sin consultar apuntes.
3. Detectar vacíos mediante una pregunta o la ejecución de una prueba.
4. Refinar la explicación y transferir el concepto a otro ejemplo.

**Criterio de dominio:** código probado, explicación propia correcta y capacidad de aplicar el concepto sin copiar. No atribuir dominio sin evidencia.

## Pregunta 01 — Suma de la segunda columna
El script de partida imprime algunas líneas y también importa pandas, pero la actividad exige una función `pregunta_01()`, sin dependencias externas, que retorne un entero. El resultado esperado por `tests/test_activity.py` es `214`.

### Propuesta de solución (todavía no validada por la estudiante)
```python
import gzip

def pregunta_01():
    total = 0
    with gzip.open("data/data.csv.gz", "rt", encoding="utf-8") as archivo:
        for linea in archivo:
            columnas = linea.strip().split("\t")
            valor = int(columnas[1])
            total += valor
    return total

if __name__ == "__main__":
    print(pregunta_01())
```

### Conceptos por explicar
- `gzip.open`: abrir un archivo comprimido como texto.
- `with`: cerrar el archivo automáticamente al salir del bloque.
- `split("\t")`: separar columnas tabuladas.
- `columnas[1]`: segunda columna, pues los índices inician en cero.
- `int`: convertir a entero.
- `+=`: actualizar un acumulador.
- `return` frente a `print`: retornar no es imprimir.

### Primera pregunta Feynman
**¿Por qué usamos `int(columnas[1])` antes de sumar y qué pasaría si no lo hiciéramos?**

## Bitácora
### 2026-10-11 — Inicio del laboratorio
- Se revisaron el README, los 12 enunciados y las pruebas.
- Se propuso una solución de la pregunta 01 para trabajar localmente.
- **No hay evidencia de ejecución ni dominio de la estudiante.**
- **Siguiente paso:** explicar la conversión a entero y ejecutar la primera función.

### Plantilla para siguientes sesiones
- **Fecha y pregunta:**
- **Explicación propia:**
- **Errores y dudas:**
- **Resultado de pruebas:**
- **Ejemplo de transferencia:**
- **Próximo paso:**
