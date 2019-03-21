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

Richard Stallman sobre [software libre](https://www.gnu.org/philosophy/free-software-even-more-important.en.html)

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


Las listas tienen índices muy convenientes:
+ `a[i:j]` toma los elementos $[i, j)$

```python
a = [i for i in range(10)]
a
```

```python
a[4:7]
```

+ `a[i:]` toma todos los elementos desde (e incluyendo) el $i$

```python
a[7:]
```

+ `a[:j]` toma todos hasta (y sin incluir) el del índice $j$. Es más fácil pensarlo como los primeros $j$.

```python
a[:7]
```

+ `a[-1]` toma el último elemento, y en general los números negativos cuentan hacia atrás.

```python
a[-1]
```

> **Pregunta:** ¿Qué debería regresar `a[-4]`?


+ `a[::k]` regresa cada $k$-ésimo elemento

```python
a[::4]
```

Como corolario, todas las cadenas funcionan como listas de caracteres, y pueden usar estas mismas técnicas de slicing.


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

Aunque en Python tengan la libertad de hacer cosas de ese estilo, no es un buen hábito en general mezclar tipos en diccionarios y en listas sin hacerlo de manera sistemática.


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

Para conjunción se usa `or` y para disjunción `and`.

```python
x = 8

if x < 0 or x > 100:
    print('caso uno')
elif x%2==0 and x%4==0:
    print('caso dos')
else:
    print('caso 3')
```

Aunque cuando son números, el and puede evitarse.

```python
if -2 < x < 2:
    print(':)')
else:
    print(':(')
```

Como en C, hay un operador ternario para escribir condicionales cortos.

```python
2 if 8%3==0 else 3
```

es equivalente a

```python
if 8%3==0:
    2
else:
    3
```

pero puede usarse en asignción de variables.

```python
z = 2 if 8%3==0 else 3
z
```

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
Claro que se puede hacer comprensión de conjuntos, como en matemáticas. Después veremos que la idea general detrás de esta sintaxis son los *generadores*, otro concepto de Python.

```python
{i/3 for i in range(10) if i%2==0}
```

Igual que en C, puede salirse de un loop con `break` y proceder a la siguiente iteración con `continue`.

```python
for i in range(10):
    if i%3 == 0:
        continue
    print(i)
```

```python
for i in range(1000000):
    if i>2:
        break
    print(i)
```

Además, es posible cambiar los aumentos en un ciclo `for`. Por ejemplo, para ir de dos en dos:

```python
for i in range(0, 10, 2):
    print(i)
```

O avanzar hacia atrás.

```python
for i in range(10, 1, -3):
    print(i)
```

### Ciclos en estructuras de datos


Hay funciones de mucha ayuda en Python para recorrer secuencias. Para recorrer una lista y saber el índice, se usa `enumerate`.

```python
A = [2*i for i in range(10)]
for i, a in enumerate(A):
    print(f'i={i} y a={a}')
```

La sintaxis de cadena usando `f''` es relativamente nueva en Python. Las expresiones que están entre llaves se evalúan antes de guardar la cadena.

Se puede recorrer una secuencia al revés con `reverse`.

```python
for i, a in enumerate(reversed((A))):
    print(f'i={i} y a={a}')
```

> **Pregunta:** ¿Qué pasa con los índices?


Para ordenar la secuencia antes, se usa `sorted`.

```python
A = [9, 7, 2, 3, 5, 6, 8]
for a in sorted(A):
    print(a)
```

Los diccionarios cuentan con un método `items` para iterarlo.

```python
d = {2:'dos', 8:'ocho', 111:'ciento once'}
for k, v in d.items():
    print(f'key = {k} ...... value = {v}')
```

En todas las estructuras mutables puede revisarse pertenencia. La más rápida es `set`, que lo revisa en tiempo constante porque está implementado sobre una hash table.

```python
3 in [1, 2, 3]
```

```python
5 in {1, 2, 3, 5, 6}
```

```python
2 in d
```

```python
'dos' in d
```

> **Pregunta:** ¿Por qué una da `TRUE` y otra `FALSE`?


Una función de utilidad más es `zip`, que permite iterar dos listas a la vez. Por ejemplo, si tenemos llaves en una lista y valores en otra:

```python
keys = [1, 2, 3]

values = ['uno', 'dos', 'tres']

dict(zip(keys,values))
```

## Funciones


Para definir funciones, se usa la palabra clave `def`.

```python
def add(x, y):
    return x + y
```

Noten que en los argumentos de una función tampoco se necesita especificar el tipo.

```python
add(2,3)
```

En general, las funciones se documentan justo después de su `def` con cadenas en varias líneas. Yo uso las [convenciones de numpy](https://www.numpy.org/devdocs/docs/howto_document.html).

```python
def add(x, y):
    """ Suma dos números
    
    Parameters
    ----------
    x: float
        Un número
    y: float
        Otro número
        
    Returns
    -------
    float
        La suma x+y
    """
    
    return x+y
```

Sé que parece un poco exagerado, pero así será fácil generar documentación después usando [sphinx](http://www.sphinx-doc.org/en/master/).


En python, las funciones son objetos de primera clase. En términos prácticos, esto significa que puedes hacer asignaciones como

```python
f = add
```

```python
f(2, 3)
```

### Funciones de orden superior y aplicación parcial


Si las funciones pueden guardarse como cualquier otro objeto, en particular pueden regresarse de otra función. En matemáticas es muy normal trabajar con operadores y en genral funciones de funciones (por ejemplo, el operador $\nabla$ o el de Fourier). 

Para fijar ideas sin irnos a operadores, veamos un ejemplo de **aplicación parcial**. La idea de la aplicación parcial es tomar una función $f: X \times X \to Y$ que mapea $(x,x') \mapsto f(x, x')$ y fijar el primer argumento (digamos, en $x_0$) para tener una función $f_{x_0}: X \to Y$ que mapea $x \to f(x_0, x)$. Por supuesto que esto puede hacerse con cualquier número de elementos.

Recordemos en `add` es una función que recibe dos argumentos y los suma.

```python
add(2,4)
```

```python
def suma_x(x):
    """Regresa una función que suma x.
    """
    return lambda z: add(x, z)
```

```python
suma_2 = suma_x(2)
suma_2(3)
```

Pasaron muchas cosas en esas celdas que hay que analizar. La notación `lambda` define una **función anónima**, azucar sintáctica para evitar definiciones de funciones rápidas.
Básicamente, el código de arriba sería equivalente a 

```python
def suma_x_forma_larga(x):
    """ Regresa una función que suma x, pero está escrito feo.
    """
    def f(y):
        """ omg cuántas funciones
        """
        return add(x, y)
    return f
```

```python
g = suma_x_forma_larga(2)
g(3)
```

¿Qué hay en `g`? Una función de Python como cualquier otra.

```python
suma_2
```

```python
g
```

A veces es conveniente regresar más de un valor en una función. Por ejemplo,

```python
def x_2x(x):
    """Regresa x y 2x.
    """
    return x, 2*x
```

```python
results = x_2x(3)
results
```

Aunque Python formalmente sólo puede regresar un objeto, por lo que empaca ambos valores en una tupla. Para extraerlos, puede usarse.

```python
results[0]
```

```python
results[1]
```

Pero si desde antemano se sabe cuántos resultados arroja la función, hay azucar sintáctica:

```python
num, num_por_dos = x_2x(8)
```

```python
num
```

```python
num_por_dos
```

Además de argumentos por posición, python permite enviar **argumentos nombrados**. La única regla es que los argumentos nombrados deben ir al final. Por ejemplo,

```python
def bienvenida(nombre, num_veces=1):
    print(f"¡{'Hola'*num_veces} {nombre}!")
```

```python
bienvenida('Jorge')
```

Nota que tuvimos que dar un *valor por defecto* al argumento `num_veces` por si el usuario no lo especifica. Este es el caso de uso general de los argumentos nombrados: alguna especie de parámetro que puede ser modificable pero no es lo primordial de la función. Para cambiarlo, basta especificar

```python
bienvenida('Jorge', num_veces=3)
```

Otra vez, la regla es que los argumentos nombrados van al final. Hacerlo al revés regresa un error. 

```python
bienvenida(num_veces=3, 'Jorge')
```

Pero ignorar el nombre es posible.

```python
bienvenida('Jorge', 3)
```

En funciones con más de uno aún puede ignorarse, pero a menos que uno sepa el orden es preferible no hacerlo. Si se envían sin nombre, respeta el orden de la definción.

```python
def bienvenida(nombre, num_holas=1, num_signos=1):
    print(f"¡{'Hola'*num_holas} {nombre}{'!'*num_signos}")
```

```python
bienvenida('Jorge', 3, 9)
```

```python
bienvenida('Jorge', 9, 3)
```

Pero usar los nombres permite sólo modificar algunos y escribir en el orden conveniente.

```python
bienvenida('Jorge', num_signos=8)
```

```python
bienvenida('Jorge', num_signos=8, num_holas=2)
```

### `*args` y `**kwargs`


A veces es conveniente dejar libre el número de argumentos que puede recibir una función. Supongamos por ejemplo que se quiere devolver el producto de números que el usuario proporcione. Al menos se necesita un número pero no hay un número fijo más allá de esa restricción.

Para resolverlo, se usan los **argumentos variables**, convencionalmente llamados `*args`.

```python
def suma_arbitraria(x, *args):
    for i in args:
        x += i
    return x
```

```python
suma_arbitraria(1)
```

```python
suma_arbitraria(1, 2, 3, 4, 5, 6)
```

¿Cómo lo maneja python por dentro? Modifiquemos la función para imprimir los argumentos.

```python
def suma_arbitraria(x, *args):
    print(args)
    print(*args)
    for i in args:
        x += i
    return x
```

```python
suma_arbitraria(1, 2, 3, 4, 5, 6)
```

`args` es una tupla con todos los demás argumentos que fueron enviados y no correspondían a los de la definición. El asterisco desempaca los valores, como vemos en el segundo `print`. De hecho, podría usarse cualquier palabra después del asterisco (por ejemplo `*magia` o `*wow_que_maravilloso_es_python`) en vez de `*args`, pero es convencional usar `args`.

El equivalente para argumentos nombrados es `**kwargs`, que guarda un diccionario con argumentos nombrados arbitrarios.

```python
def f(**kwargs):
    print(kwargs)
```

```python
f(uno='string', dos=3, tres='dos')
```

El orden que debe usarse al llamar funciones es
1. Argumentos formales
2. `*args`
3. Argumentos nombrados
4. `**kwargs`

Otro buen caso de uso de los `**kwargs` es enviar argumentos a funciones internas. Si $g$ se ejecuta dentro de $f$ y sólo dentro de $f$, los parámetros de $g$ pueden ajustarse desde la llamada a $f$. 

> **Pregunta:** Implementa un ejemplo de esta idea.


## Módulos y paquetes


En la práctica, los programas son más complicados que un único archivo. Muchas veces querremos reutilizar funciones en diferentes contextos, o simplemente separar nuestro código en archivos para facilitar el mantenimiento y el trabajo en equipo.

Un archivo de python se llama un **módulo**. Podemos importar nuestros propios archivos de Python como módulos (y lo haremos más adelante) pero también podemos importar módulos instalados a través de un gestor de paquetes como `pip` o `conda`.

Para importar todo un módulo usamos `import`. Por ejemplo:


```python
import math
```

```python
dir(math)
```

```python
type(math)
```

`math` tiene sus métodos como `tanh` y sus atributos como `pi`.

```python
math.pi
```

```python
math.tanh(math.pi)
```

Si sólo queremos importar ciertos métodos o atributos, la sintaxis general es

# ```
from mod import f1, f2, f3, ..., fn
# ```

```python
from json import load
```

```python
json
```

```python
type(json)
```

```python
load
```

Python reconoce que `json` es un módulo y `load` una función. Notemos que con la sintaxis `from` no es necesario escribir `json.load`, a diferencia de lo que hicimos con math.


```python
pi
```

Una colección de módulos se llama **paquete**. Para referirsea un módulo dentro de un paquete se usa la notación de punto que ya han visto, como `package.module`. Más adelante usaremos esto mucho. 

Para crear paquetes con tus propios módulos, basta poner un archivo `__init__.py` en la carpeta que contiene los archivos. Si te interesa más, revisa la [documentación](https://docs.python.org/3.8/tutorial/modules.html).


## Más control de flujo


### Excepciones


¿Qué hace Python si intentamos dividir entre cero?

```python
3/0
```

Levanta una **excepción**. Una excepción ocure cuando el código es sintácticamente correcto pero algún tipo de problema no lo permite avanzar. A diferencia de los errores sintácticos, en los que Python simplemente no va a saber qué hacer, muchas veces es deseable que el código continúe su ejecución aunque se enfrente algún problema.

Para seguir con el ejemplo, supongamos que tenemos una función dividir.

```python
def divide(a, b):
    """ a/b
    """
    return a/b
```

```python
divide(5,3)
```

```python
divide(5,0)
```

Y otra vez recibimos una excepción: `ZeroDivisionError`. Claro que en este caso podríamos mejorar la función revisando el único valor crítico

```python
def divide(a, b):
    """a/b
    """
    if b == 0:
        print('No puedo dividir entre 0')
        return
    else:
        return a/b
```

```python
divide(5,0)
```

Pero no siempre sabemos los casos críticos, los errores que pueden ocurrir y un `if` no está pensado para esto. Por ejemplo, el usuario podría intentar

```python
divide(5, '0')
```

La manera correcta de evitar estos errores es usar `try` y `except`.

```python
def divide(a, b):
    """a/b
    """
    try:
        return a/b
    except (ZeroDivisionError, TypeError):
        print('Problema con los argumentos')
```

```python
divide(5,0)
```

Si no sabemos qué erorres pueden ocurrir, puede dejarse solamente `except`, y eso atrapa cualquier posible excepción. La forma general e`

# ```
try:
    do_something()
except SomeError1:
    action_for_error1()
except (SomeError2, SomeError3, ..., SomeErrorN):
    action_for_other_errors()
# Notación equivalente
except SomeError2 or SomeError3 or ... or SomeErrorN:
    action_for_other_errors()
# ```


### `with`


Al abrir archivos, el recolector de basura de Python no puede liberar la memoria automáticamente cuando el archivo deja de usarse. Para abrir y cerrar recursos sin llenar la memoria de basura, python usa `with`. 

```python
import json
try:
    with open('../data/moveis.json') as f:
        movies = json.load(f)
except FileNotFoundError as fnf:
    print(fnf)
```

```python
try:
    with open('../data/movies.json') as f:
        movies = json.load(f)
except FileNotFoundError as fnf:
    print(fnf)
```

## Ejercicios


1. Escribe una función que reciba dos listas y determine si tienen algún elemento en común.
2. Ahora extiéndela para que cuente el número total de elementos comunes.
3. Escribe una función que encuentre el k-ésimo elemento más grande de una lista de números.
4. Escribe una función que reciba una lista de diccionarios y los imprima como tabla.
5. Escribe una función cuyo argumento sea una serie de funciones que deben ejecutarse una por una e imprimir su nombre (antes de correrla) y su resultado (después de correrlas).


## Temas adicionales


+ [Decoradores](https://realpython.com/primer-on-python-decorators/)
+ [Tips de estilo](https://medium.com/the-andela-way/idiomatic-python-coding-the-smart-way-cc560fa5f1d6)
+ [Documentación](https://docs.python.org/3/)
