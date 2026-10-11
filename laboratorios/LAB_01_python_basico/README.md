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
| 05 | Mínimo y máximo por letter | En estudio | Propuesta de extremos por categoría, pendiente de ejecución |
| 06 | Mínimo y máximo por clave de metrics | En estudio | Propuesta de ciclos anidados y extremos; pendiente de ejecución |
| 07 | Letras por valor, con repeticiones | En estudio | Propuesta de diccionario de listas; pendiente de ejecución |
| 08 | Letras únicas por valor | En estudio | Propuesta con conjuntos y ordenación; pendiente de ejecución |
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


## Pregunta 05 — Máximo y mínimo por letra
El enunciado exige tuplas `(letra, máximo, mínimo)`, en ese orden. Resultado esperado: `[("A",9,2),("B",9,1),("C",9,0),("D",8,3),("E",9,1)]`.

### Código propuesto (sin ejecución confirmada)
```python
import gzip

def pregunta_05():
    extremos = {}
    with gzip.open(r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_01_python_basico\data\data.csv.gz", "rt", encoding="utf-8") as archivo:
        for linea in archivo:
            columnas = linea.strip().split("\t")
            letra = columnas[0]
            valor = int(columnas[1])
            if letra in extremos:
                extremos[letra][0] = max(extremos[letra][0], valor)
                extremos[letra][1] = min(extremos[letra][1], valor)
            else:
                extremos[letra] = [valor, valor]
    return [(letra, valores[0], valores[1]) for letra, valores in sorted(extremos.items())]
```

### Feynman
- **Conceptos:** diccionario de listas, índices, funciones `max` y `min`, comprensión de listas.
- **Explicación clave:** para la primera observación de cada letra, ese valor es tanto su máximo como su mínimo.
- **Pregunta:** si `extremos["A"] = [5,5]` y aparece una fila `A,9`, ¿cómo queda la lista? ¿Qué ocurre si después aparece `A,2`?
- **Estado:** código y explicación propuestos, pendientes de ejecución y respuesta de la estudiante.


## Pregunta 06 — Extremos de metrics (2026-10-11)
La quinta columna `metrics` contiene pares `clave:valor` separados por comas. Se deben obtener tuplas `(clave, mínimo, máximo)` ordenadas por clave; **a diferencia de la pregunta 05, el mínimo va primero**.

### Código propuesto (pendiente de ejecución)
```python
import gzip

def pregunta_06():
    extremos = {}
    with gzip.open(r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_01_python_basico\data\data.csv.gz", "rt", encoding="utf-8") as archivo:
        for linea in archivo:
            columnas = linea.strip().split("\t")
            metricas = columnas[4].split(",")
            for metrica in metricas:
                clave, valor = metrica.split(":")
                valor = int(valor)
                if clave in extremos:
                    extremos[clave][0] = min(extremos[clave][0], valor)
                    extremos[clave][1] = max(extremos[clave][1], valor)
                else:
                    extremos[clave] = [valor, valor]
    return [(clave, valores[0], valores[1]) for clave, valores in sorted(extremos.items())]
```

### Feynman
- **Conceptos:** dos ciclos `for` anidados, `split(",")`, desempaquetado `clave, valor = ...split(":")`, conversión `int`, actualización de extremos.
- **Ejemplo:** `aaa:5,bbb:3` y luego `aaa:2` producen para `aaa` mínimo 2 y máximo 5.
- **Pregunta diagnóstica:** ¿por qué necesitamos dos ciclos `for` y qué representan `clave` y `valor`?
- **Estado:** propuesta explicada, sin evidencia de ejecución ni dominio de la estudiante.


## Pregunta 07 — Agrupar letras por valor (2026-10-11)
Para cada valor entero de la segunda columna, reunir las letras de la primera en una lista **con repeticiones y en el orden original**. La respuesta es una lista de tuplas `(valor, letras)` ordenada numéricamente por valor.

### Código propuesto (pendiente de ejecución)
```python
import gzip

def pregunta_07():
    grupos = {}
    with gzip.open(r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_01_python_basico\data\data.csv.gz", "rt", encoding="utf-8") as archivo:
        for linea in archivo:
            columnas = linea.strip().split("\t")
            letra = columnas[0]
            valor = int(columnas[1])
            if valor in grupos:
                grupos[valor].append(letra)
            else:
                grupos[valor] = [letra]
    return sorted(grupos.items())
```

### Método Feynman
- **Estudiar:** diccionarios con listas como valores; método `.append()`; preservación de duplicados y orden; `sorted(...items())`.
- **Explicar:** por qué la clave del diccionario es `valor` y no `letra`.
- **Detectar vacíos:** diferenciar `grupos[valor] = [letra]` de `grupos[valor].append(letra)`.
- **Refinar:** con registros `(A,3),(B,1),(A,3)`, verificar `[(1,["B"]),(3,["A","A"])]`.
- **Estado:** propuesta explicada; no consta ejecución ni dominio.


## Pregunta 08 — Letras únicas por valor (2026-10-11)
Repetir la agrupación de la pregunta 07, pero eliminando letras duplicadas en cada valor y ordenando alfabéticamente las listas resultantes. Las tuplas se ordenan por el valor numérico.

### Código propuesto (pendiente de ejecución)
```python
import gzip

def pregunta_08():
    grupos = {}
    with gzip.open(r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_01_python_basico\data\data.csv.gz", "rt", encoding="utf-8") as archivo:
        for linea in archivo:
            columnas = linea.strip().split("\t")
            letra = columnas[0]
            valor = int(columnas[1])
            if valor in grupos:
                grupos[valor].add(letra)
            else:
                grupos[valor] = {letra}
    return [(valor, sorted(letras)) for valor, letras in sorted(grupos.items())]
```

### Feynman
- **Conceptos:** `set`, método `.add()`, diferencia con listas y `.append()`, ordenación `sorted()`.
- **Pregunta diagnóstica:** si un conjunto contiene `{"A", "E"}` y ejecutamos `.add("A")`, ¿cuántas letras contendrá y por qué?
- **Estado:** código propuesto, pendiente de ejecución y explicación propia.


## Pregunta 09 — Frecuencia de claves de metrics (2026-10-11)
Contar cuántas veces aparece cada clave de la quinta columna, ignorando los valores numéricos asociados. Retornar un **diccionario** de frecuencias, no una lista de tuplas.

### Código propuesto (pendiente de ejecución)
```python
import gzip

def pregunta_09():
    conteos = {}
    with gzip.open(r"C:\Analitica_descriptiva\std-milena-gomez-jaramillo\LAB_01_python_basico\data\data.csv.gz", "rt", encoding="utf-8") as archivo:
        for linea in archivo:
            columnas = linea.strip().split("\t")
            metricas = columnas[4].split(",")
            for metrica in metricas:
                clave = metrica.split(":")[0]
                if clave in conteos:
                    conteos[clave] += 1
                else:
                    conteos[clave] = 1
    return conteos
```

### Método Feynman
- **Conceptos:** ciclos anidados, separación de cadenas, diccionario de frecuencias.
- **Relación:** misma lógica de conteo que la pregunta 02 y mismo procesamiento de métricas que la pregunta 06.
- **Pregunta diagnóstica:** si las métricas son `aaa:5,bbb:3` y `aaa:9`, ¿cuántas apariciones tiene `aaa` y por qué sus valores 5 y 9 no afectan el conteo?
- **Estado:** propuesta explicada, pendiente de ejecución y explicación propia.
