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


> Schools (and this includes all educational activities) influence the future of society through what they teach. They should teach exclusively free software, so as to use their influence for the good. To teach a proprietary program is to implant dependence, which goes against the mission of education. By training in use of free software, schools will direct society's future towards freedom, and help talented programmers master the craft.

Richard Stallman sobre [https://www.gnu.org/philosophy/free-software-even-more-important.en.html](software libre)

```python
import this
```

Dependiendo de su carrera y elección de materias, en su estancia en el ITAM habrán usado MATLAB (sobre todo en cosas numéricas) o R (en cosas estadísticas). El objetivo de este curso es introducir Python como una mejor alternativa para sus clases y como lenguaje de programación general. Aunque R tenga sus casos de uso y MATLAB funcione, la [Popularidad de Python](http://pypl.github.io/PYPL.html) ha aumentado durante los últimos años.

![](./img/pl_popularity.png)


Algo debe tener, ¿no?

+ **Python es entendible.** A diferencia de otros lenguajes de programación, Python favorece la legibilidad casi ante todo: el código debe ser fácil de leer y las soluciones deben ser fáciles incluso para alguien que no la sepa. Esto se traduce en menos tiempo gastado peleando con puntuación y llaves (sorpresa: no hay tales) y más tiempo disponible para atacar el problema. Así la computadora es una verdadera herramienta y se reduce el obstáculo de la sintaxis complicada.

+ **Python es multiparadigma.** Permite hacer programación orientada a objetos, funcional, e imperativa.

+ **Python es *open source*.** A diferencia de MATLAB, Python es de código abierto. Esto no sólo significa que es gratis, sino que tiene una *comunidad activa de desarrollo*, tanto científico como tecnológico. ¡Casi siempre existe una librería para lo que intentas resolver!

+ **Python es produccionalizable.** Tu código en Python puede hacer *scraping* de un sitio web, procesarlo, ajustar algún modelo estadístico y arrojar predicciones a un FTP. Por supuesto que esto no es ideal, pero es definitivamente más de lo que se puede hacer en MATLAB o R y suficientemente bueno para proyectos a escala pequeña. En el mismo lenguaje puedes hacer software y cómputo científico.

+ **Python es flexible.** Gran parte del retraso de Python en entrar al cómputo numérico es que es un lenguaje de programación *interpretado* y de *tipado dinámico*. No importa demasiado ahondar en detalles, pero más o menos significa que (1) el código que nosotros escribimos se traduce a lenguaje de máquina directamente al momento de la ejecución y que (2), también en la ejecución se revisa el tipo de las variables. Este sistema da libertad al programador y junto con un esfuerzo explícito para diseñar una buena sintaxis, se presta para un código muy limpio.


Vale la pena detenerse un poco en esta última observación. Parte de la filosofía de Python desde su concepción era tener un lenguaje minimal pero fácilmente extensible. En la siguiente sesión veremos que el ecosistema de cómputo científico y estadístico de Python, que utiliza librerías eficientes de Fortran y C consigue velocidades comparables con MATLAB (igual que MATLAB, numpu corre sobre [LAPACK](https://en.wikipedia.org/wiki/LAPACK) y [BLAS](https://en.wikipedia.org/wiki/Basic_Linear_Algebra_Subprograms) *sin perder todas las demás ventajas*. 

Claro que hay casos de uso para software propietario, incluso en el cómputo científico, y que Python no va a alcanzar la velocidad de MATLAB todo el tiempo. Pero en la mayoría de los casos relevantes, la diferencia en tiempo no pesa más que las ventajas.


## Básicos

Las variables en python se asignan usando `=`. Por ejemplo

```python
x = 3
```

```python
x
```

Noten que no hubo necesidad de declarar la variable antes de utilizarla, y que puede por tanto cambiar de tipo libremente.

```python
x = 'Ahora soy una cadena'
```

```python
x
```

### [Estructuras de datos](https://docs.python.org/3.7/tutorial/datastructures.html)


Python tiene entre sus tipos base, además de números y cadenas, **listas**, conjuntos y diccionarios.
Las listas de Python *no* son equivalentes a los arreglos de R y MATLAB ni a las listas de Java, pues pueden tener más de un tipo de dato.

```python
['una', 2.59, 'lista', 'de', 8, 'cosas', sum, [i for i in range(3)]]
```

Las listas tienen métodos para usarse como pila.

```python
l = [1, 2, 3, 4, 5]
l
```

```python
l.append(6)
l
```

```python
print(l.pop())
l
```

Y hay colas y otras cosas en librerías que veremos después.


Los **diccionarios** son listas nombradas. Se guardan en pares llave-valor. Por ejemplo, podemos tener un diccionario que mapee claves únicas en nombres.

```python
d = {158391:'Jorge Rotter', 158612:'Eduardo Gil'}
d
```

Añadir nuevas observaciones es muy sencillo:

```python
d[159189] = 'Sergio Arnaud'
d
```

¿Y si quisieran mezclar llaves de distintos tipos?

```python
d['cadena'] = 1
d
```

> **NOTA:** Aunque en Python tengan la libertad de hacer cosas de ese estilo, no es un buen hábito en general mezclar tipos en diccionarios y en listas sin hacerlo de manera sistemática.


A diferencia de las listas, los conjuntos no mantienen orden y no guardan elementos repetidos. En ese sentido son como conjuntos matemáticos.

```python
s = {2, 1, 3, 2, 1}
s
```

```python
s.add(0)
s
```

La estructura de datos inmutable (con un valor fijo) más común en Python es la **tupla**. Una tupla se declara entre paréntesis y separando con comas.

```python
t = (1, 2, 3)
t
```

Para declarar una tupla de un solo elemento, la sintaxis cambia.

```python
(2)
```

```python
2,
```

### Condicionales

Una vez más Python se mostrará mucho más limpio que otros lenguajes.

```python
x = 3
```

```python
if x < 0:
    print('x es negativo')
elif x==0:
    print('x es cero')
else:
    print('x es positivo')
```

No hay llaves ni paréntesis, pero la identación importa. Es un buen hábito de python usar cuatro espacios (y no tabulador) para identar código.


### Ciclos
La estructura de un `for` en python es

```python
for i in range(10):
    print(i)
```
Noten que python indexa desde cero. ¿Y si hubiéramos querido ir del 1 al 10?

```python
for i in range(1,11):
    print(i)

```

Noten que el intervalo es de la forma $[l, u)$. 

Hay maneras más apropiadas de hacerlo. Por ejemplo, para un arreglo de los primeros 5 números pares (sin contar al cero):

```python
[2*i for i in range(1,6)]
```

Esta manera explícita de escribir una lista se llama una **lista comprensiva**. La forma general de una lista comprensiva es

# ```
[f(x) for x in X if p(x)]
# ```

donde `f` y `g` son funciones y `X` es un generador (que veremos después). 
Otro ejemplo, ¿cuáles son los elementos de esta lista?

```python
[i/3 for i in range(10) if i%2==0]
```
> **Nota:** Claro que se pueden hacer comprensión de conjuntos, como en matemáticas. Después veremos que la idea general detrás de esta sintaxis son los *generadores*, otro concepto de Python.

```python

```
