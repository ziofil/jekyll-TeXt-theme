---
layout: lecture
code: INFPHY201
title: Overview of Python and and the Jupyter environment
menu_title: 1. Python and Jupyter
author: Filippo Miatto

prerequisites:
  - a working installation of the latest Anaconda (python 3.7)
  - an essential knowledge of Python (basic types, control flow and loops, functions)
  - an essential knowledge of NumPy (arrays, operations between arrays)

# use verbs!
learning_objectives:
  - write clean and idiomatic python code
  - use control flow, loops, common types, functions and libraries
  - utilize the jupyter environment effectively
---


# INFPHY201 - Lecture 1

In the first part of this lecture we will review the Jupyter notebook environment and python. I am assuming that you have at least some familiarity with programming in general and that you have experience in finding programming resources online (e.g. stackoverflow.com). If you are unaware of this particular website, I highly recommend it: https://awesome-python.com/

## 1. Jupyter Notebooks

Jupyter notebooks run in your browser. You just need to start the server by issuing the command `jupyter notebook` in the terminal and your browser will connect to it automatically. If this does not happen you will see a link that you can copy and paste in your browser directly. You can install everything that you need with the Anaconda installer from https://www.anaconda.com/download

The interface is made of cells that you can edit and evaluate individually. Cells can be mainly of two types: those that run code, and those that display markdown text. You can switch the type of cell from the menu Cell > Cell type or with the keyboard shortcuts `Y` and `M` (there is also the raw mode `R`, but that's only to leave the cells unevaluated).

Markdown text supports several cool features like _italic_, __bold__, etc... as well as $\LaTeX$ formulas, both inline (wrap code between the dollar symbol \$): $\sum_{i=1}^\infty x^{-2}=\frac{\pi^2}{6}$ and in display mode (wrap code between the double dollar symbol \$\$) $$\sum_{i=1}^\infty\frac{1}{x^4}=\frac{\pi^4}{90}.$$

When you evaluate a cell with code, the code in the cell will be parsed by the Python interpreter and run. When you evaluate a cell with text, the text will be typeset according to the Markdown and $\LaTeX$ syntax.

Each notebook is a single standalone file, which means that (for example) you can easily send it as an email attachment.

I recommend you to get accustomed to using keyboard shortcuts, because they make many operations much faster, such as creating new cells with `A` and `B`, or deleting them with `DD`, copying a cell with `C` and pasting it with `D`. You can check out all of the shortcuts at any time with `H`.

## 2. Python

Python is one of the most well-known programming languages, as it combines simplicity and beauty. It is also one of the easiest languages to learn. I would be surprised if you didn't know about it, but just in case, here's a quick refresher.

### 2.1 syntax
Python does not have line termination characters and blocks are defined by indentation (four spaces or a tab). This leads to a much cleaner and organized code.
Statements that expect a new block (e.g. a `for` loop) end with a colon (:)


```python
if 4 in [1,2,3,4]:
    print("it's there")
```

    it's there


Comments start with a pound symbol (#) and values are assigned with the equal symbol (=)


```python
x = 5 # now x is assigned value 5
print(x)
```

    5


Some symbols are overloaded, so that you can use them with many data types (this is an example of polymorphism). For example you can increment an `int` with `+=`, but you can also append to a string or to a list with `+=`


```python
x = 5
x += 2
print(x)
```

    7



```python
y = "I'm a"
print(y)
y += " string"
print(y)
```

    I'm a
    I'm a string



```python
z = [1,2,3]
print(z)
z += [4,5,'other stuff']
print(z)
```

    [1, 2, 3]
    [1, 2, 3, 4, 5, 'other stuff']


Python is object-oriented, which means that everything is an object. Yes, even `int`:


```python
x = 10
x.bit_length()
```




    4



as you might have noticed, we access an object's methods with the dot notation `obj.method()`

### 2.2 common types
The most basic types (aside from ints, floats, strings, etc...) are `set`, `tuple`, `list` and `dict`

`set` is an unordered list, that you can really use as a set (also useful to remove duplicates from a list, for example). It implements union, intersection and the other common set operations.


```python
x = {1,2,3,3}
y = {3,4,5}
```


```python
x
```




    {1, 2, 3}




```python
x # notice that 3 is not repeated anymore
```




    {1, 2, 3}




```python
x.intersection(y)
```




    {3}




```python
x.union(y)
```




    {1, 2, 3, 4, 5}




```python
list_with_duplicates = [1,1,1,3,2,1,3]
list(set(list_with_duplicates)) # no duplicates now
```




    [1, 2, 3]



tuples are immutable lists and because of immutability they can be faster than lists. Also, they can be used as dictionary keys because by being immutable they are hashable.


```python
tup = (0,1,2,'hello world') # I'm a tuple
lst = [0,1,2,3,4] # I'm a list
```

lists and tuples (and strings) can be accessed with the following notation, but be careful that python is zero-indexed: the index starts from zero!


```python
tup[3]
```


```python
lst[2:4] # the indices are inclusive-exclusive, so here the element of lst at position 4 is not returned
```

dictionaries are unordered key,value pairs:


```python
dic = {1:'uno', 2:'due', 3:'tre'}
```


```python
dic[2]
```




    'due'




```python
dic = {'carrots':1, 'potatoes':2, 'onions':3}
```


```python
dic['onions']
```




    3




```python
dic['carrots'] = 2
dic['carrots']
```




    2




```python
dic['bananas'] = 'yellow' # here we create a new dictionary entry
```


```python
dic
```




    {'bananas': 'yellow', 'carrots': 2, 'onions': 3, 'potatoes': 2}




```python
dic['bananas']
```




    'yellow'




```python
lst = [1,2]
```


```python
example=(lst, 3 ,4)
```


```python
example
```




    ([1, 2], 3, 4)




```python
lst.append(9)
```


```python
example
```




    ([1, 2, 9], 3, 4)




```python
list((1,2,3))
```




    [1, 2, 3]




```python
tuple
set
dict
```


```python
help(dict)
```

    Help on class dict in module builtins:
    
    class dict(object)
     |  dict() -> new empty dictionary
     |  dict(mapping) -> new dictionary initialized from a mapping object's
     |      (key, value) pairs
     |  dict(iterable) -> new dictionary initialized as if via:
     |      d = {}
     |      for k, v in iterable:
     |          d[k] = v
     |  dict(**kwargs) -> new dictionary initialized with the name=value pairs
     |      in the keyword argument list.  For example:  dict(one=1, two=2)
     |  
     |  Methods defined here:
     |  
     |  __contains__(self, key, /)
     |      True if D has a key k, else False.
     |  
     |  __delitem__(self, key, /)
     |      Delete self[key].
     |  
     |  __eq__(self, value, /)
     |      Return self==value.
     |  
     |  __ge__(self, value, /)
     |      Return self>=value.
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __getitem__(...)
     |      x.__getitem__(y) <==> x[y]
     |  
     |  __gt__(self, value, /)
     |      Return self>value.
     |  
     |  __init__(self, /, *args, **kwargs)
     |      Initialize self.  See help(type(self)) for accurate signature.
     |  
     |  __iter__(self, /)
     |      Implement iter(self).
     |  
     |  __le__(self, value, /)
     |      Return self<=value.
     |  
     |  __len__(self, /)
     |      Return len(self).
     |  
     |  __lt__(self, value, /)
     |      Return self<value.
     |  
     |  __ne__(self, value, /)
     |      Return self!=value.
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  __repr__(self, /)
     |      Return repr(self).
     |  
     |  __setitem__(self, key, value, /)
     |      Set self[key] to value.
     |  
     |  __sizeof__(...)
     |      D.__sizeof__() -> size of D in memory, in bytes
     |  
     |  clear(...)
     |      D.clear() -> None.  Remove all items from D.
     |  
     |  copy(...)
     |      D.copy() -> a shallow copy of D
     |  
     |  fromkeys(iterable, value=None, /) from builtins.type
     |      Returns a new dict with keys from iterable and values equal to value.
     |  
     |  get(...)
     |      D.get(k[,d]) -> D[k] if k in D, else d.  d defaults to None.
     |  
     |  items(...)
     |      D.items() -> a set-like object providing a view on D's items
     |  
     |  keys(...)
     |      D.keys() -> a set-like object providing a view on D's keys
     |  
     |  pop(...)
     |      D.pop(k[,d]) -> v, remove specified key and return the corresponding value.
     |      If key is not found, d is returned if given, otherwise KeyError is raised
     |  
     |  popitem(...)
     |      D.popitem() -> (k, v), remove and return some (key, value) pair as a
     |      2-tuple; but raise KeyError if D is empty.
     |  
     |  setdefault(...)
     |      D.setdefault(k[,d]) -> D.get(k,d), also set D[k]=d if k not in D
     |  
     |  update(...)
     |      D.update([E, ]**F) -> None.  Update D from dict/iterable E and F.
     |      If E is present and has a .keys() method, then does:  for k in E: D[k] = E[k]
     |      If E is present and lacks a .keys() method, then does:  for k, v in E: D[k] = v
     |      In either case, this is followed by: for k in F:  D[k] = F[k]
     |  
     |  values(...)
     |      D.values() -> an object providing a view on D's values
     |  
     |  ----------------------------------------------------------------------
     |  Data and other attributes defined here:
     |  
     |  __hash__ = None
    


### 2.3 control flow
The control flow statements in python are `if`, `for` and `while`. There is no `switch`. Remember the colon and the indentation


```python
r = range(10)
```


```python
r.__next__()
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-37-3a998f5f1be5> in <module>()
    ----> 1 r.__next__()
    

    AttributeError: 'range' object has no attribute '__next__'



```python
list(range(10))
```




    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]




```python
for k in range(10):
    if k%2 == 0: # comparison is indicated with two equal signs
        print(k)
```

    0
    2
    4
    6
    8



```python
y = 10
x = 'y is small' if y < 3 else 'y is big' # simple if-else statements can work in a single line
print(x)
```

    y is big


list/dictionary comprehension is awesome, use it:


```python
[x**2 for x in range(10)] # single for
```




    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]




```python
lst = []
for x in range(10):
    lst.append(x**2)
```


```python
lst
```




    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]




```python
[[x for x in range(y)] for y in range(5)] # nested for
```




    [[], [0], [0, 1], [0, 1, 2], [0, 1, 2, 3]]




```python
[x for y in range(5) for x in range(y)] # double for
```




    [0, 0, 1, 0, 1, 2, 0, 1, 2, 3]




```python
[x for y in range(5) for x in range(y) if x%2 == 1] # double for with if 
```




    [1, 1, 1, 3]




```python
[x if x%2 == 1 else 'even' for y in range(5) for x in range(y)] # double for with if-else
```




    ['even', 'even', 1, 'even', 1, 'even', 'even', 1, 'even', 3]




```python
squares = {k:str(k**2) for k in range(10)}
```


```python
squares
```




    {0: '0',
     1: '1',
     2: '4',
     3: '9',
     4: '16',
     5: '25',
     6: '36',
     7: '49',
     8: '64',
     9: '81'}




```python
squares[4]
```




    '16'



If you try to write a "tuple comprehension" you get a generator instead (see [this awesome explanation](https://jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/) about generators):


```python
generator = (x**2 for x in range(20) if x%3 == 0)
```


```python
generator
```




    <generator object <genexpr> at 0x10dc62048>




```python
for item in generator:
    print(item)
```

    0
    9
    36
    81
    144
    225
    324



```python
generator.__next__()
```


    ---------------------------------------------------------------------------

    StopIteration                             Traceback (most recent call last)

    <ipython-input-68-4e10fd096f6b> in <module>()
    ----> 1 generator.__next__()
    

    StopIteration: 


### 2.4 booleans
You can use `True` and `False` in conjunction with `and` and `or` to make more complex control flows


```python
1 is 1
```




    True




```python
a = 1
b = 1
```


```python
a is b
```




    True




```python
1==2 or 1!=2
```




    True




```python
True and False
```




    False




```python
0 and 1 # 0 and 1 are overloaded and can be used as False and True
```




    0




```python
number = -2
if number in [1,2,3,4,5] or [-1,-2]: # notice that we don't need to write "if number in [...] or number in [...]"
    print('ok')
    
string = "many many words"
if 'ny wo' in string:      # notice the usage of `in`
    print("it's there")
```

    ok
    it's there


### 2.5 functions
Functions are defined with the `def` statement


```python
def int_add(first_arg, second_arg, optional_arg = 9):
    assert(type(first_arg) == type(second_arg) == int) # optional typecheck
    
    return first_arg + second_arg + optional_arg
```


```python
help(int_add)
```

    Help on function int_add in module __main__:
    
    int_add(first_arg, second_arg, optional_arg=9)
    



```python
int_add(1,1,2)
```




    4



but if you want an arbitrary number of arguments use this syntax


```python
def my_function(*arguments):
    for arg in arguments:
        print(arg)
```


```python
my_function(2,'apple','blabla')
```

    2
    apple
    blabla



```python
help(my_function)
```

    Help on function my_function in module __main__:
    
    my_function(*arguments)
    



```python
def func(x):
    """
    Here goes the documentation for the function.
    There are several standards that you can find,
    you should pick one that you like and stick to it.
    E.g.
    
    Parameters
    ----------
    x : float
        x is the input that we want to square
        
        
    Returns
    -------
    squared : float
        the input squared
        
    Raises
    ------
    ValueError
        if the input x is not a float
        
        
    Examples
    --------
    These are written in doctest format, and should illustrate how to
    use the function.

    >>> func(1.0)
    1.0
    >>> func(-2.0)
    4.0
    
    """
    
    if type(x) != float:
        raise ValueError('input must be a float')
    squared = x**2
    
    return squared
```


```python
func(1)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-104-9ed089a72395> in <module>()
    ----> 1 func(1)
    

    <ipython-input-102-29d6df6d653f> in func(x)
         36 
         37     if type(x) != float:
    ---> 38         raise ValueError('input must be a float')
         39     squared = x**2
         40 


    ValueError: input must be a float



```python
help(func) # the docstring appears when you call for help()
```

    Help on function func in module __main__:
    
    func(x)
        Here goes the documentation for the function.
        There are several standards that you can find,
        you should pick one that you like and stick to it.
        E.g.
        
        Parameters
        ----------
        x : float
            x is the input that we want to square
            
            
        Returns
        -------
        squared : float
            the input squared
            
        Raises
        ------
        ValueError
            if the input x is not a float
            
            
        Examples
        --------
        These are written in doctest format, and should illustrate how to
        use the function.
        
        >>> func(1.0)
        1.0
        >>> func(-2.0)
        4.0
    


### 2.6 classes (blueprints for objects)
a class is a blueprint for creating an object. It specifies what properties and methods an instance of that object will have.


```python
class Vehicle():
    def __init__(self, color = "red"):
        # this is the default class initializer method that is called when you instantiate the class
        
        self.color = color
        self.sound = None
        self.engine_noise = None
        
    def move(self, start_str, finish_str):
        print("going from {start} to {finish}, {noise}".format(start=start_str, finish=finish_str, noise=self.engine_noise))

    def honk(self):
        print(self.sound)
```


```python
v = Vehicle('blue')
```


```python
v.move('here','there')
```

    going from here to there, None


Classes can inherit from other classes:


```python
class Car(Vehicle):
    def __init__(self):
        super().__init__() # when we inherit from another class we need to call that class' initializer
        self.sound = "beep!"
        self.engine_noise = "vroom"
        self.tank_level = 1.0
        
    def move(self, start_str, finish_str):
        super().move(start_str, finish_str)
        self.tank_level -= 0.2

```


```python
class Bicycle(Vehicle):
    def __init__(self, color = None):
        super().__init__()
        self.color = color or self.color # if color is None, fall back on the defalut color of the superclass.
        self.sound = "drinn!"
        self.engine_noise = "..."
```


```python
car = Car()
car.color
```




    'red'




```python
car.move("A", "B")
car.tank_level # we used up some fuel
```

    going from A to B, vroom





    0.8




```python
bike = Bicycle()
bike.color
```




    'red'




```python
bike.color = 'green' # of course, properties can be modified
bike.color
```




    'green'




```python
bike.move("A","B") # bike uses its superclass method
```

    going from A to B, ...



```python
for vehicle in [bike, car]: # this is the power of polymorphism!
    vehicle.honk()
```

    drinn!
    beep!


### 2.7 exceptions
Exceptions are your friend. Use `try`/`except` statements to catch the exceptions and act upon them:


```python
lst = ['first','second','third']
try:
    for k in range(10):
        print(lst[k])
except Exception as e:
    print('oops: {exception}'.format(exception=e))
```

    first
    second
    third
    oops: list index out of range



```python
print(lst[3]) # this is what you'd get without catching the exception
```


    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-135-e61731f0ce41> in <module>()
    ----> 1 print(lst[3]) # this is what you'd get without catching the exception
    

    IndexError: list index out of range


You can also raise your own errors. This can be extremely useful in debugging your code.


```python
def func(a,b):
    if type(a) != str:
        raise TypeError('the first argument of func should be a string')
```


```python
func(1,2) # this raises our exception
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-137-b482dc8e2976> in <module>()
    ----> 1 func(1,2) # this raises our exception
    

    <ipython-input-136-6bbda1d561e6> in func(a, b)
          1 def func(a,b):
          2     if type(a) != str:
    ----> 3         raise TypeError('the first argument of func should be a string')
    

    TypeError: the first argument of func should be a string


**In-class activity**: *you have 20-30 minutes to develop the `Vehicle`, `Car` and `Bicycle` classes (or make others). What can you do? (suggestions: weight, owner, current speed, number of wheels, headlights on/off, current gear, accelerate, brake, parked/in motion, total km, tire pressure, wash, break/fix something, trip diary, front basket full or empty...)*

### 2.8 modules and libraries
python can be augmented with external libraries. There are TONS of libraries. The most relevant for us are `numpy`, `scipy`, `qutip` and `matplotlib`. Today we will check out `qutip`, the Quantum Toolbox in Python


```python
import qutip as qt # this shortens the library name (not necessary but useful)
import numpy as np # we'll need this too
```

## 3. Quantum mechanics and QuTiP

Now we begin talking about quantum mechanics. First the good news: quantum mechanics is a lot about linear algebra, so be prepared to use a lot of matrices and vectors. The bad news is that we have two lectures to cover enough material for you to begin the first project, so if at any point there is something that is not perfectly clear just give me a shout and I'll help you. There is no benefit in not asking questions, you are expected not to know things! I've been in your place, I remember how it was like and I know these topics can be confusing.

### 3.0 notation
There is a funny notation that has been adopted by the large scientific community, and it's known as Dirac's bra-ket notation. It comes from the notation $\langle v|w\rangle$ for an inner product of the two vectors $\mathbf{v}$ and $\mathbf{w}$. If you look at it as two objects coming together, you can separate them out into $\langle v|$ and $|w\rangle$ and use them as row and column vectors. As the space is complex, remember that to turn row and column vectors into each other you also take the complex conjugate of the elements: $\langle\psi| = |\psi\rangle^\dagger$ where the dagger symbol $\dagger$ computes the "hermitian conjugate" (which is just the conjugate transpose).

So, things that look like this: $|\psi\rangle$ are vectors, and matrices are usually indicated with latin capital letters or with greek letters. Sometimes we put a hat on them (like so $\hat \sigma$), but I'm not a fan. I will use hats only if I want to stress that an object is an operator. Matrices act on vectors by left-multiplication, so $U|\psi\rangle$ is a new vector, obtained by multiplying the vector $|\psi\rangle$ by the matrix U. there's not really much more to it!

### 3.1 states
So, let's begin: we describe quantum systems by specifying their "state". The state is an object that allows us to make predictions about them, such as "what will the result of this measurement be?", or "how will the state change if I apply this transformation?", or "how similar are these states?" and so on.
A quantum state is just a vector of length 1 (also called "state vector") in a complex vector space of some dimension, say $N$ (the dimension depends on the number of degrees of freedom of the system). This means that the entries $a_n$ can be complex numbers, but they satisfy this normalization condition: $$\sum_{n=1}^N|a_n|^2=1.$$ In QuTiP, we can write vectors using the canonical basis, which we can create with the `basis` function:


```python
s0 = qt.basis(N=5, n=0)
s0
```




Quantum object: dims = [[5], [1]], shape = (5, 1), type = ket\begin{equation*}\left(\begin{array}{*{11}c}1.0\\0.0\\0.0\\0.0\\0.0\\\end{array}\right)\end{equation*}




```python
s0.dag()
```




Quantum object: dims = [[1], [5]], shape = (1, 5), type = bra\begin{equation*}\left(\begin{array}{*{11}c}1.0 & 0.0 & 0.0 & 0.0 & 0.0\\\end{array}\right)\end{equation*}




```python
s1 = qt.basis(5,1) # and so on for other values of n.
s1
```




Quantum object: dims = [[5], [1]], shape = (5, 1), type = ket\begin{equation*}\left(\begin{array}{*{11}c}0.0\\1.0\\0.0\\0.0\\0.0\\\end{array}\right)\end{equation*}




```python
3*s0+8*s1 # using the canonical basis elements to write an arbitrary vector
```




Quantum object: dims = [[5], [1]], shape = (5, 1), type = ket\begin{equation*}\left(\begin{array}{*{11}c}3.0\\8.0\\0.0\\0.0\\0.0\\\end{array}\right)\end{equation*}




```python
# with .dag() we take the hermitian conjugate (dag is short for dagger), which is the conjugate transpose
s0.dag()
```




Quantum object: dims = [[1], [5]], shape = (1, 5), type = bra\begin{equation*}\left(\begin{array}{*{11}c}1.0 & 0.0 & 0.0 & 0.0 & 0.0\\\end{array}\right)\end{equation*}




```python
# notice that the hermitian conjugate changes the sign of i (the "conjugate" in conjugate transpose):
((2+1j)*s0).dag()
```




Quantum object: dims = [[1], [5]], shape = (1, 5), type = bra\begin{equation*}\left(\begin{array}{*{11}c}(2.0-1.0j) & 0.0 & 0.0 & 0.0 & 0.0\\\end{array}\right)\end{equation*}



### 3.2 superpositions
You may have already heard that quantum systems can exist in a superposition of states. This is true, and it is a consequence of the fact that the state space is a vector space, and we are perfectly allowed to have superpositions of vectors: 


```python
# make three basis vectors
basis0 = qt.basis(3,0)
basis1 = qt.basis(3,1)
basis2 = qt.basis(3,2)

state = (0.1*basis0 + 0.5*basis1 - 0.2j*basis2).unit() # unit() is to normalize the vector
state
```




Quantum object: dims = [[3], [1]], shape = (3, 1), type = ket\begin{equation*}\left(\begin{array}{*{11}c}0.183\\0.913\\-0.365j\\\end{array}\right)\end{equation*}



And we can verify the normalization condition:


```python
state.norm()
```




    0.9999999999999999




```python
# also by taking the inner product:
state.dag()*state
```




Quantum object: dims = [[1], [1]], shape = (1, 1), type = bra\begin{equation*}\left(\begin{array}{*{11}c}1.000\\\end{array}\right)\end{equation*}




```python
state*state.dag()
```




Quantum object: dims = [[3], [3]], shape = (3, 3), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}0.033 & 0.167 & 0.067j\\0.167 & 0.833 & 0.333j\\-0.067j & -0.333j & 0.133\\\end{array}\right)\end{equation*}



Obviously, whether a state is in a "superposition" or not, depends on the basis of the vector space. There is always a basis in which a state is not (strictly speaking) in a superposition. Of course you may object that it is the basis elements then that are in a superposition, but this means that you are regarding some particular bases as more "fundamental" than others. Example: take the state $|\psi_+\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$, in any basis that contains $|\psi_+\rangle$ as an element, this state is just $|\psi_+\rangle$, it is not a superposition of elements of that basis. So, if one insists that the basis elements are in a superposition, they are putting the basis $\{|0\rangle, |1\rangle\}$ on a different footing than the basis $\{|\psi_+\rangle, |\psi_-\rangle\}$. There might be a good reason to do this (e.g. for pointer states), or no reason at all.

From now on, I'll be using the following fuction to write states:


```python
def state(*amplitudes):
    """ Returns the normalized state containing the amplitudes specified as arguments"""
    
    dimension = len(amplitudes)
    state = 0*qt.basis(dimension) # the zero vector of dimension N
    
    for n,amplitude in enumerate(amplitudes):
        state += amplitude*qt.basis(dimension,n)
    
    return state.unit()
```


```python
for n,number in enumerate(['one','two','three']):
    print(n,number)
```

    0 one
    1 two
    2 three


Also, QuTiP comes equipped with a convenience method to compute the inner product of two states:


```python
psi = state(0.4,1)
phi = state(2,1j)
```


```python
phi
```




Quantum object: dims = [[2], [1]], shape = (2, 1), type = ket\begin{equation*}\left(\begin{array}{*{11}c}0.894\\0.447j\\\end{array}\right)\end{equation*}




```python
psi.overlap(phi)
```




    (0.33218191941495984+0.4152273992686998j)




```python
phi.overlap(psi)
```




    (0.33218191941495984-0.4152273992686998j)



We will use this from now on, unless we have a particular reason not to.

### 3.3 Operators
In quantum mechanics there are state vectors and operators that act on them. What acts on vectors? Matrices. (Remember I told you it's just linear algebra?) Another word that is very much used is "operator", which comes from the case of infinite-dimensional Hilbert spaces, but this is for the next lecture. For now just think of them as matrices. Operators can be used for all sorts of things: to evolve state vectors in time, to represent measurements, to represent observable properties and so on. The spectrum of an operator (i.e. the eigenvalues of the matrix) can tell us a lot about that object, as well as the properties of the matrix itself (is it unitary, hermitian, what is its rank, etc...). We will see them one by one, as we describe the main aspects of quantum theory.

### 3.4 Probabilities
Quantum mechanics is a probabilistic theory, in the sense that it is not always possible to predict future events with certainty. This inability is not due to lack of knowledge (as in predicting the weather): you may know a state vector perfectly well, but you may still be unable to predict, say, the result of a measurement. Why? We need first to look at how we compute the probability of an event.

This is the Born rule: *If a system is in the state $|\psi\rangle$, the probability of finding it in the state $|\phi\rangle$ is $p=|\langle\phi|\psi\rangle|^2$*. 

Do you recognize that the number $\langle\phi|\psi\rangle$ is the inner product of those two state vectors? Here we are linking the *orthogonality* of those two states (a geometrical property) to a physical effect: the probability that after you have prepared the state $|\psi\rangle$, you find it in the state $|\phi\rangle$. When this happens it does not mean that you \*thought\* you had prepared it in $|\psi\rangle$, but made a mistake and accidentally prepared it in $|\phi\rangle$: but rather that there exists a certain degree of *overlap*, or *compatibility*, between states that is captured by the inner product.

So now we can look at the state vector itself and interpret the complex numbers that we find: for example in the basis $|0\rangle,|1\rangle,|2\rangle$, the state $|\psi\rangle = a_0|0\rangle+a_1|1\rangle+a_2|2\rangle$ is the column vector $(a_0, a_1, a_2)^T$. Then the overlap between $|\psi\rangle$ and $|k\rangle$ is $a_k$:


```python
psi = state(np.sqrt(.2),np.sqrt(.5),np.sqrt(.3)) # I'm using sqrt of probabilities, so it's already normalized
abs(state(0,0,1).overlap(psi))**2 # this is <1|psi> = 1/sqrt(2)
```




    0.29999999999999993



So the normalization rule was not random: it makes all of the probabilities sum up to 1 (they don't here because we didn't normalize the state vector `psi`. The complex coefficients are called probability amplitudes, and the squared absolute value of an amplitude is a probability. The probability of what? Of finding the system in the state represented by the relative basis element.

Notice that $\langle\phi|\psi\rangle = \langle\psi|\phi\rangle^*$, so $p=|\langle\phi|\psi\rangle|^2 = \langle\psi|\phi\rangle\langle\phi|\psi\rangle$, which makes it possible to express the probability with a "sandwich" (I'll highlight it with big parentheses): $p=\langle\psi|\biggl(|\phi\rangle\langle\phi|\biggr)|\psi\rangle$. The object in parenteses is an operator (a projector, see below), because when the ket comes before the bra, we are doing a column-by-row multiplication, which gives a matrix:


```python
psi*psi.dag() # here we are using psi, but the idea is the same
```




Quantum object: dims = [[3], [3]], shape = (3, 3), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}0.200 & 0.316 & 0.245\\0.316 & 0.500 & 0.387\\0.245 & 0.387 & 0.300\\\end{array}\right)\end{equation*}



Now we can see that the "global phase" of a state does not matter: the state $|\psi\rangle$ and the state $e^{i\theta}|\psi\rangle$ represent the same physical state. In fact, you will never notice the global phase because it cannot change any measurement probability: $|\langle\phi|e^{i\theta}|\psi\rangle|^2 = |e^{i\theta}\langle\phi|\psi\rangle|^2 = |e^{i\theta}|^2|\langle\phi|\psi\rangle|^2=|\langle\phi|\psi\rangle|^2$.

### 3.5 Measurements

Quantum mechanics provides several ways to describe measurements, the simplest of which is by using *projectors*. An operator $P$ is a projector if $P^2=P$, which implies that its eigenvalues can only be zeros and ones.
If we have a quantum system with a Hilbert space of dimension $N$, we can have at most $N$ independent projectors. A set of projectors is complete if $\sum_i P_i=\mathbb{1}$ and any two of them are orthogonal, i.e. $P_iP_j=\delta_{ij}$. A rank-1 projector (the rank is the number of non-zero eigenvalues) can always be written as the outer product of two normalized kets: $P=|\phi\rangle\langle\phi|$.
For example, in a Hilbert space of dimension 2, we can make two independent rank-1 projectors using for example the states that define the canonical basis:


```python
P0 = state(1,0)*state(1,0).dag()
P1 = state(0,1)*state(0,1).dag()
```


```python
P0
```




Quantum object: dims = [[2], [2]], shape = (2, 2), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}1.0 & 0.0\\0.0 & 0.0\\\end{array}\right)\end{equation*}




```python
P1
```




Quantum object: dims = [[2], [2]], shape = (2, 2), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}0.0 & 0.0\\0.0 & 1.0\\\end{array}\right)\end{equation*}




```python
P0*P0 # this is the same as P0
```




Quantum object: dims = [[2], [2]], shape = (2, 2), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}1.0 & 0.0\\0.0 & 0.0\\\end{array}\right)\end{equation*}




```python
P1*P1 # this is the same as P1
```




Quantum object: dims = [[2], [2]], shape = (2, 2), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}0.0 & 0.0\\0.0 & 1.0\\\end{array}\right)\end{equation*}




```python
P0+P1
```




Quantum object: dims = [[2], [2]], shape = (2, 2), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}1.0 & 0.0\\0.0 & 1.0\\\end{array}\right)\end{equation*}



It's possible to fill a space of dimension, e.g. 3, with two projectors, but one has to be rank-2:


```python
Q0 = state(1,0,0)*state(1,0,0).dag()+state(0,1,0)*state(0,1,0).dag() # this is rank-2
Q1 = state(0,0,1)*state(0,0,1).dag()
```


```python
Q0
```




Quantum object: dims = [[3], [3]], shape = (3, 3), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}1.0 & 0.0 & 0.0\\0.0 & 1.0 & 0.0\\0.0 & 0.0 & 0.0\\\end{array}\right)\end{equation*}




```python
Q1
```




Quantum object: dims = [[3], [3]], shape = (3, 3), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}0.0 & 0.0 & 0.0\\0.0 & 0.0 & 0.0\\0.0 & 0.0 & 1.0\\\end{array}\right)\end{equation*}




```python
Q0+Q1 # identity? yes
```




Quantum object: dims = [[3], [3]], shape = (3, 3), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}1.0 & 0.0 & 0.0\\0.0 & 1.0 & 0.0\\0.0 & 0.0 & 1.0\\\end{array}\right)\end{equation*}



Where are the measurements? Each outcome of a measurement is associated to a projector in a complete set. In particular, if $P_i=|\phi_i\rangle\langle\phi_i|$, the meaning of $P_i$ is that it represents the outcome of finding the system in the state $|\phi_i\rangle$.

What is the probability of the outcome? This depends on the state of the system before the measurement: we can apply the Born rule to find out! Suppose that the system is in the state $|\psi\rangle$, we have $p_i = |\langle\psi|\phi_i\rangle|^2=\langle\psi|\phi_i\rangle\langle\phi_i|\psi\rangle=\langle\psi|P_i|\psi\rangle$. So by sandwiching the projector we find the probability of an outcome! (this also holds for projectors of any rank). That is why projectors are a type of "probability operators".

### 3.6 Quantum jumps
Measurements affect quantum systems. This is a pecuilar property of quantum physics that is not true in classical physics. We say that as a consquence of a measurement, systems "jump" to the state that the measurement found them in: (using the same notation of the previous section) if the measurement outcome corresponds to the rank-1 projector $P_i=|\phi_i\rangle\langle\phi_i|$, regardless of what the state was before the measurement, it is now $|\phi_i\rangle$ up to global phase. This is also known as the "collapse of the wave function".

If a measurement outcome corresponds to a projector of higher rank, we can find the new state using this relation (which also holds for rank-1): $|\psi_\mathrm{after}\rangle = P_i|\psi_\mathrm{before}\rangle/\sqrt{p_i}$. Notice that we have to renormalize the state using the square root of the measurement probability:

$\langle\psi_\mathrm{after}|\psi_\mathrm{after}\rangle=\langle\psi_\mathrm{before}|P_iP_i|\psi_\mathrm{before}\rangle/p_i=\langle\psi_\mathrm{before}|P_i|\psi_\mathrm{before}\rangle/p_i = p_i/p_i = 1$


```python
# a pair of random states
psi = state(1.2,3,3j)
phi = state(-2+1j,7,0.1)

projector = psi*psi.dag()
```


```python
# probability of measuring psi in the state phi
abs(psi.overlap(phi))**2
```




    0.3302714860759667




```python
# using the sandwich
phi.dag()*projector*phi
```




Quantum object: dims = [[1], [1]], shape = (1, 1), type = bra\begin{equation*}\left(\begin{array}{*{11}c}0.330\\\end{array}\right)\end{equation*}




```python
psi
```




Quantum object: dims = [[3], [1]], shape = (3, 1), type = ket\begin{equation*}\left(\begin{array}{*{11}c}0.272\\0.680\\0.680j\\\end{array}\right)\end{equation*}




```python
# state after the measurement
state_after = (projector*phi).unit()
state_after
```




Quantum object: dims = [[3], [1]], shape = (3, 1), type = ket\begin{equation*}\left(\begin{array}{*{11}c}(0.272+0.013j)\\(0.680+0.033j)\\(-0.033+0.680j)\\\end{array}\right)\end{equation*}



*"How is it possible? You said the new state should have been $|\psi\rangle$!"*
Almost! I said "up to global phase", which means that it can be $e^{i\theta}|\psi\rangle$ (and physically it wouldn't matter). To see that this is true, let's compute the inner product and verify that it is equal to a phase factor $e^{i\theta}$:


```python
# the overlap is 1, which means
maybe_phase = psi.overlap((projector*phi).unit())
```


```python
maybe_phase
```




    (0.9988313960820001+0.0483305514233226j)




```python
abs(maybe_phase) # yep!
```




    0.9999999999999999



### 3.7 Qubits and the Bloch sphere

Qubits are the simplest non-trivial quantum systems. Their state space is just 2-dimensional, which means that we only need two amplitudes to specify the state of a qubit. For example, here's a qubit state:


```python
qubit = state(0.5,0.5j) # this is a possible qubit state
qubit
```




Quantum object: dims = [[2], [1]], shape = (2, 1), type = ket\begin{equation*}\left(\begin{array}{*{11}c}0.707\\0.707j\\\end{array}\right)\end{equation*}



it's possible to represent the state of a qubit on the surface of a sphere:


```python
sphere = qt.Bloch()
sphere.add_states(qubit)
```


```python
sphere.render()
```


![png](output_170_0.png)


We can also add specific points by specifying their coordinates (the sphere is centered in the origin and has radius 1)


```python
sphere.clear()

xp = [np.cos(th) for th in np.linspace(0, 2*np.pi, 20)]
yp = [np.sin(th) for th in np.linspace(0, 2*np.pi, 20)]
zp = np.zeros(20)

sphere.add_points([xp,zp,yp])
```


```python
sphere.render()
```


![png](output_173_0.png)


The correspondence between $(x,y,z)$ (real) coordinates and $(\alpha,\beta)$ (complex) quantum amplitudes is not immediatley obvious, but here's how you can transform between them: you need three canonical operators called the "*Pauli operators*". They are usually indicated by $\sigma_X$, $\sigma_Y$ and $\sigma_Z$ or (more commonly in quantum computing) $X$, $Y$ and $Z$.

They are defined as follows:


```python
X = qt.operators.sigmax() # Pauli X
X
```




Quantum object: dims = [[2], [2]], shape = (2, 2), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}0.0 & 1.0\\1.0 & 0.0\\\end{array}\right)\end{equation*}




```python
Y = qt.operators.sigmay() # Pauli Y
Y
```




Quantum object: dims = [[2], [2]], shape = (2, 2), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}0.0 & -1.0j\\1.0j & 0.0\\\end{array}\right)\end{equation*}




```python
Z = qt.operators.sigmaz() # Pauli Z
Z
```




Quantum object: dims = [[2], [2]], shape = (2, 2), type = oper, isherm = True\begin{equation*}\left(\begin{array}{*{11}c}1.0 & 0.0\\0.0 & -1.0\\\end{array}\right)\end{equation*}



and then the 3D coordinates of the state vector in/on the Bloch sphere are found by sandwiching the Pauli operators:


```python
def vec3d_from_qubits(*qubits):
    """
    Returns the x,y,z coordinates of the Bloch vector of the input qubits.
    """
    # Pauli operators
    X,Y,Z = [qt.operators.sigmax(), qt.operators.sigmay(), qt.operators.sigmaz()]
    
    x_coord, y_coord, z_coord = [],[],[]
    
    for q in qubits:
        x_coord.append(np.real((q.dag()*X*q)[0,0])) # np.real is just to remove the unnecessary 0j
        y_coord.append(np.real((q.dag()*Y*q)[0,0]))
        z_coord.append(np.real((q.dag()*Z*q)[0,0]))
        
    return [x_coord, y_coord, z_coord]
```

`ATTENTION`: even though geometrically speaking these two vectors are at 90 degrees:


```python
sphere.clear()
sphere.add_states([state(1,0),state(1,1)])
sphere.render()
```


![png](output_181_0.png)


They are not "orthogonal" in the quantum sense:


```python
state(1,0).overlap(state(1,1))
```




    (0.7071067811865475+0j)



Orthogonal state vectors (in the sense that their inner product $\langle\phi|\psi\rangle$ is zero) are at **opposite points** of the Bloch sphere 


```python
sphere.clear()
sphere.add_states([state(1,0),state(0,1)])
sphere.render()
```


![png](output_185_0.png)



```python
state(1,0).overlap(state(0,1))
```




    0j



### 3.8 Transformations

The last topic of this lecture is about another type of operator: the unitary operator. Unitary operators have eigenvalues that fall on the unit circle on the complex plane (so projectors are not unitary because they can have zero as an eigenvalue). The cool thing about unitary operators is that they don't change the norm of vectors, which means that if you start with a state $|\psi\rangle$ and you apply a unitary to it: $|\psi'\rangle = U|\psi\rangle$ you still obtain a valid state, no need to renormalize. So unitary operators are perfect for describing state transformations!

As unitary transformations don't change the length of vectors, you can think them of "rotations" in a complex vector space.

A perhaps curious, but extremely useful fact is that every unitary operator can be written using the exponential function: $U=\exp(itA)$ where $t\in\mathbb{R}$ and $A$ is a "*hermitian*" operator. Hermitian operators are self-adjoint: $A=A^\dagger$, and as a consequence they have real eigenvalues (so yes, projectors are hermitian).

In QuTiP, we compute the exponential of an operator with the method `.expm()`

often times, the meaning of the hermitian operator that generates a unitary operator is very clear. This is the case of the rotations of vectors on the Bloch sphere, where the Pauli operators define the axis of rotation:


```python
def X_rotation(angle):
    X = qt.operators.sigmax()
    return (0.5*angle*1.0j*X).expm() # notice the factor of 1/2
```


```python
X_rotation(0.4)
```




Quantum object: dims = [[2], [2]], shape = (2, 2), type = oper, isherm = False\begin{equation*}\left(\begin{array}{*{11}c}0.980 & 0.199j\\0.199j & 0.980\\\end{array}\right)\end{equation*}




```python
sphere.clear()
statesX = [X_rotation(angle)*qubit for angle in np.linspace(0,2*np.pi,30)]
sphere.add_states(statesX)
sphere.render()
```


![png](output_192_0.png)



```python
sphere.clear()
sphere.add_points(vec3d_from_qubits(*statesX))
sphere.render()
```


![png](output_193_0.png)



```python
def Z_rotation(angle):
    Z = qt.operators.sigmaz()
    return (0.5*angle*1.0j*Z).expm() # notice the factor of 1/2
```


```python
sphere.clear()
sphere.add_points(vec3d_from_qubits(*[X_rotation(angle)*qubit for angle in np.linspace(0,2*np.pi,30)]))
sphere.add_points(vec3d_from_qubits(*[Z_rotation(angle)*qubit for angle in np.linspace(0,2*np.pi,30)]))
sphere.render()
```


![png](output_195_0.png)


## 4. Homework

Starting from the next lecture I will begin *my* notebooks with the following statement:


```python
import filippo as ip201 # short for INFPHY201
```

I will use `ip201` to call the following two functions: `ip201.state(*amplitudes)`, `ip201.rotate_qubit(state,axis,angle)` (in future lectures we will include more functions).

But you don't have the module named `filippo`, because you don't have the file `filippo.py`. You are supposed to make one of your own. To do so, create a file named `whateveryouwant.py` and place it in the same folder of the jupyter notebook and at the beginning of our next notebooks run `>>>import whateveryouwant as ip201`. Inside this file, import QuTiP and numpy (and whatever else you need), and develop those two functions.

We have already defined the `state` function, I want you to make it better: add some type checking, make it faster, document it properly. Don't worry about the code getting long, because it will be in the `.py` file. For the unitary rotation function, read this: http://www.vcpc.univie.ac.at/~ian/hotlist/qc/talks/bloch-sphere-rotations.pdf and define a function that takes a Qobj representing the state of a qubit and it returns the rotated state. Again, make it good, make it fast.

Sometime next week I will send you a file with unit tests that your functions have to pass. If they don't, then you will have problems running our future notebooks.

