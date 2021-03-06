---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.0'
      jupytext_version: 0.8.6
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

# Python para ciencias aplicadas



## Tema 1: Python 101

###### 																Tiempo estimado: una  sesión

+ Básicos
  + Asignación de variables.
  + Condicionales.
  + Ciclos.
  + `print`
+ Listas, diccionarios y comprensión.
+ Funciones.
  + Definir funciones
  + Funciones anónimas
  + Funciones de orden superior
  + Decoradores
  + `*args` y `**kwargs`
+ Excepciones
  + `try`/ `except`
  + `with`
+ Módulos y paquetes

## Tema 2: Python para cómputo científico

###### ​																Tiempo estimado: una  sesión

+ Vectorización para reducir tiempos de ejecución.
+ NumPy
  + Arreglos
  + Funciones básicas (`sort`, `unique`, `argmin`, `arange`)
  + Aritmética de arreglos
+ SciPy
  + `linalg`
    + Operaciones básicas.
    + Problemas espectrales.
    + Descomposiciones.
  + `integrate` y `optimize` (opcional)
    + Diferencias finitas
    + Integración
    + Encontrar raíces
+ Diferenciación (opcional)
  + SymPy
  + Numdifftools
+ Matplotlib
  + Gráficas básicas de la forma $f(x)$
  + Gráficas en tres dimensiones
  + subplots, `fig`, `ax`
+ Numba (opcional)

## Tema 3: Python para ciencia de datos

###### ​															Tiempo estimado: una sesión y media

+ Pandas
  + Dataframes
  + Índices y multiíndices
  + Series
  + `loc` y `query`
  + Gráficas desde pandas
  + Queries tipo SQL
    + `merge`
    + `groupby`
    + `agg`
+ Seaborn
  + Histogramas
  + Categorical plots
  + Pairplots
+ SciPy
  + `stats`
    + Distribuciones (explicar parametrización)
    + `fit`
    + `rvs`
+ StatsModels (opcional)
  + Series de tiempo
  + GLMs
+ PyMC3 (opcional) (mencionar su existencia y link al repo de BMH)
+ Scikit-Learn
  + La necesidad de una especificación consistente de ML
  + `fit`/`predict`/`transform`
  + Herramientas para selección de modelos
    + train/test split
    + Cross-Valdiation
    + GridSearch y BayesSearchCV
  + Ejemplo más o menos detallado (nivel aplicada 2/3).

## Tema 4: Ambientes de trabajo

###### ​																Tiempo estimado: media sesión

+ Introducción conceptual a conda, git y jupyter.
+ **Instalación.**
  + Python
  + Conda
+ Comandos básicos de Unix: `cp`, `mv`, `mkdir`, `rm`.
+ Conda
  + Crear ambientes
  + Instalar paquetería.
+ Jupyter
