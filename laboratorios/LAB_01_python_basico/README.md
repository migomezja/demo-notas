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
| 01 | Suma de value | Resuelta; pendiente pytest | La estudiante confirmó salida 214, explicó conversión numérica y resolvió ejercicio de rutas |
| 02 | Conteos por letter | En estudio | Propuesta de diccionario de frecuencias, pendiente de ejecución y explicación propia |
| 03 | Sumas por letter | Pendiente | — |
| 04 | Registros por mes | En estudio | Propuesta de conteo por mes; pendiente de ejecución y explicación propia |
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

### 2026-10-11 — Comprobación de rutas relativas
- La estudiante identificó correctamente que, al ejecutar desde `LAB_01_python_basico`, la ruta relativa `LAB_01_python_basico/data/data.csv.gz` se resuelve duplicando ese segmento.
- **Concepto comprobado:** resolución de rutas relativas desde el directorio de trabajo.
- **Pendiente:** confirmar ejecución y explicar `int(columnas[1])`.

### 2026-10-11 — Conversión numérica (Feynman)
- **Respuesta de la estudiante:** «porque para sumar se debe tener formato de numero, sea float o int».
- **Evaluación:** identifica correctamente que se requiere un tipo numérico para sumar aritméticamente. Se reforzó que la lectura en modo texto devuelve cadenas (`str`), que `+` concatena cadenas, y que `int` corresponde a la columna de enteros.
- **Estado:** comprensión conceptual inicial comprobada; todavía falta confirmar ejecución y resultado de prueba de `pregunta_01()`.

### 2026-10-11 — Resultado de pregunta 01 confirmado
- La estudiante confirmó que su ejecución local produjo **214**.
- Se completó la explicación básica de conversión a `int` y rutas relativas.
- **Pendiente:** no se ha comunicado resultado de `pytest`; no registrar la prueba como aprobada.

## Pregunta 02 — Frecuencia por letra
Se requiere una lista de tuplas `(letra, cantidad)` ordenada alfabéticamente. La prueba del profesor espera `[("A", 8), ("B", 7), ("C", 5), ("D", 6), ("E", 14)]`.

### Propuesta para estudiar (sin ejecución confirmada)
```python
import gzip

def pregunta_02():
    conteos = {}
    with gzip.open("data/data.csv.gz", "rt", encoding="utf-8") as archivo:
        for linea in archivo:
            columnas = linea.strip().split("\t")
            letra = columnas[0]
            if letra in conteos:
                conteos[letra] += 1
            else:
                conteos[letra] = 1
    return sorted(conteos.items())

if __name__ == "__main__":
    print(pregunta_02())
```

### Conceptos Feynman por verificar
- Diccionarios como tablas de frecuencias.
- Diferencia entre clave existente y nueva.
- `+= 1` como incremento de conteo.
- `.items()` y `sorted()`.
- **Pregunta diagnóstica:** ¿Por qué se usa `conteos[letra] = 1` cuando la letra aparece por primera vez y `+= 1` cuando ya existe?

### Plantilla para siguientes sesiones
- **Fecha y pregunta:**
- **Explicación propia:**
- **Errores y dudas:**
- **Resultado de pruebas:**
- **Ejemplo de transferencia:**
- **Próximo paso:**


## Pregunta 04 — Conteo por mes (2026-10-11)
El enunciado pide contar filas por mes de la columna `date` (tercera columna, índice 2), devolviendo lista de tuplas `(mes, cantidad)` ordenadas por mes. La fecha tiene formato `YYYY-MM-DD`.

### Solución propuesta (pendiente de ejecución por la estudiante)
```python
import gzip

def pregunta_04():
    conteos = {}
    with gzip.open(r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_01_python_basico\data\data.csv.gz", "rt", encoding="utf-8") as archivo:
        for linea in archivo:
            columnas = linea.strip().split("\t")
            fecha = columnas[2]
            mes = fecha.split("-")[1]
            if mes in conteos:
                conteos[mes] += 1
            else:
                conteos[mes] = 1
    return sorted(conteos.items())
```

### Conceptos Feynman
- `columnas[2]` es la tercera columna, pues los índices comienzan en 0.
- `fecha.split("-")` separa año, mes y día; `[1]` selecciona el mes.
- Los meses se conservan como texto de dos dígitos para respetar el formato solicitado.
- Se reutiliza el diccionario de frecuencias de la pregunta 02.
- **Pregunta diagnóstica:** ¿qué devuelve `"2024-07-15".split("-")[1]` y por qué no es necesario `int()`?
- **Estado:** solución ofrecida, todavía sin evidencia de ejecución ni dominio.
